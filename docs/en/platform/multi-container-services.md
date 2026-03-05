---
title: Multi-Container Workspaces & Services
description: How to run sidecar services (Redis, Postgres, n8n, etc.) alongside your workspace, with automatic DNS and TLS.
order: 10
---

# Multi-Container Workspaces & Services

## What Are Sidecar Services?

A codrsync workspace is more than a code editor — it is a full Linux container with Docker networking, a public URL, and TLS. Sidecar services let you add additional containers (Redis, Postgres, n8n, RabbitMQ, Evolution API, and more) that run alongside your main workspace on the same network.

When Titan creates a sidecar, it runs as a Docker container on the same internal network as your workspace. Your code can reach it by hostname (e.g., `ws-yourslug-redis:6379`). If you expose a service, it gets an automatic HTTPS subdomain like `redis-yourslug.app.codrsync.dev`.

## Available Service Templates

| Service | Image | Port | Default RAM | Use Case |
|---------|-------|------|-------------|----------|
| **redis** | redis:7-alpine | 6379 | 128 MB | Cache, message broker, session store, queues |
| **postgres** | postgres:16-alpine | 5432 | 256 MB | Relational database for structured data |
| **n8n** | n8nio/n8n:latest | 5678 | 512 MB | Visual workflow automation (like Zapier) |
| **rabbitmq** | rabbitmq:3-management-alpine | 5672 | 256 MB | Advanced message queuing |
| **evolution-api** | atendai/evolution-api:latest | 8080 | 512 MB | WhatsApp Business API |
| **minio** | minio/minio:latest | 9000 | 256 MB | S3-compatible local object storage |
| **qdrant** | qdrant/qdrant:latest | 6333 | 256 MB | Vector database for AI/embeddings |

## How to Use Sidecar Services

Ask Titan naturally:

- "Add Redis to my workspace"
- "I need a Postgres database with password mypass123"
- "Set up n8n with a public URL so I can receive webhooks"
- "Create a full prospecting stack: Redis + Postgres + Evolution API"

Titan will use the `service_create` tool to provision the container, configure networking, and optionally expose it with a public HTTPS subdomain.

### Titan Tools for Service Management

- **service_templates** — List all available services and their specs
- **service_create** — Create a new sidecar (specify name, env vars, whether to expose publicly)
- **service_list** — Show all running sidecars with their URLs
- **service_remove** — Stop and remove a sidecar
- **service_logs** — View recent logs from a sidecar

## Tier Limits

| Tier | Max Sidecars | Max Sidecar RAM | Max Exposed (public URL) |
|------|-------------|-----------------|--------------------------|
| Basic (free/pro) | 0 | 0 | 0 |
| Pro (pro_plus/team) | 3 | 1 GB total | 2 |
| Power (enterprise) | 8 | 4 GB total | 5 |

Users on Basic tier cannot create sidecars. Upgrade to Pro or Power to unlock this feature.

## Networking Between Services

All sidecars share the same Docker network as your workspace. You can reach any sidecar from your code using its container hostname:

```python
# Python example — connecting to Redis sidecar
import redis
r = redis.Redis(host='ws-yourslug-redis', port=6379)
r.set('key', 'value')
```

```javascript
// Node.js example — connecting to Postgres sidecar
const { Pool } = require('pg');
const pool = new Pool({
  host: 'ws-yourslug-postgres',
  port: 5432,
  user: 'postgres',
  password: 'mypassword',
  database: 'postgres',
});
```

Titan knows the exact hostnames and will configure your code to use them correctly.

## Public URLs and DNS

When you expose a sidecar, it gets an automatic HTTPS subdomain:

```
{service}-{workspace-slug}.app.codrsync.dev
```

For example: `n8n-c0e0e0b7f.app.codrsync.dev`

This URL is publicly accessible with a valid TLS certificate (Let's Encrypt). It's perfect for:
- **Webhook endpoints** — receive callbacks from Stripe, WhatsApp, GitHub, etc.
- **API endpoints** — expose a FastAPI or Express app to the internet
- **Admin dashboards** — access n8n, RabbitMQ management UI, MinIO console

## Lifecycle: What Happens When Your Workspace Pauses?

When your workspace auto-pauses due to inactivity:

1. All sidecar containers are **stopped**
2. Sidecar data volumes are **archived to cloud storage** (Storj) — this frees local disk
3. Public URLs are **de-registered** (return 404 until resumed)

When you resume your workspace:

1. Data volumes are **restored from cloud storage** (takes ~10-30 seconds extra)
2. Sidecar containers are **recreated** with the same configuration
3. Public URLs are **re-registered** with TLS
4. **All your data is intact** — nothing is lost

This means you pay zero resources when not using your stack, but everything comes back exactly as you left it.

## Storage Architecture

codrsync uses three storage tiers, optimized for cost and performance:

| Tier | Where | Speed | Cost | Used For |
|------|-------|-------|------|----------|
| **Hot** | Local SSD | <1ms | Included | Active sidecar data (Postgres tables, Redis keys) |
| **Warm** | Storj (S3) | ~50-100ms | ~$7/TB/mo | App uploads, PDFs, images (via cloud-gateway) |
| **Cold** | Storj (S3) | ~5-30s | ~$4/TB/mo | Archived sidecar volumes (auto on pause) |

Your application code can use the cloud-gateway as an S3-compatible API for storing files:

```python
import requests

# Upload a file to cloud storage (from inside your workspace)
requests.put(
    'http://cloud-gateway:3003/s3/my-bucket/photo.jpg',
    headers={'Authorization': f'Bearer {INTERNAL_TOKEN}'},
    data=open('photo.jpg', 'rb'),
)
```

This is useful for user uploads, generated reports, backups, or any data that should persist independently of your workspace state.

## Common Use Cases

### Automated Prospecting Machine
A typical setup for lead generation automation:
- **n8n** (exposed): Workflow orchestration — scrape leads, enrich data, sequence outreach
- **Postgres**: Store lead data, track pipeline stages
- **Redis**: Cache enriched profiles, manage rate limits
- **Evolution API** (exposed): WhatsApp outreach via webhook

Ask Titan: "Set up a prospecting stack with n8n, Postgres, Redis, and Evolution API. Expose n8n and Evolution API publicly."

### SaaS Backend
Run your entire backend stack:
- **Postgres**: Main database
- **Redis**: Session store + cache
- **RabbitMQ**: Background job queue
- Your **FastAPI/Express** app running in the workspace

### AI/ML Pipeline
Process and search embeddings:
- **Qdrant**: Vector database for semantic search
- **Postgres**: Metadata and user data
- **Redis**: Caching layer for API responses
- **MinIO**: Store training data and model artifacts

### WhatsApp Bot
Automate WhatsApp conversations:
- **Evolution API** (exposed): Receive and send WhatsApp messages
- **n8n** (exposed): Visual workflow builder for conversation logic
- **Redis**: Session state for multi-turn conversations
- **Postgres**: Log messages and analytics

## Compared to Static Publishing (CDN)

codrsync offers two ways to "publish" from your workspace:

| Feature | Static CDN (existing) | Sidecar Services (new) |
|---------|----------------------|----------------------|
| What it serves | HTML, CSS, JS files | Running processes |
| Survives pause? | Yes (files on Storj) | Data yes, processes no (restart on resume) |
| Needs compute? | No (Storj serves files) | Yes (containers running) |
| URL format | cdn.codrsync.dev/s/slug/ | service-slug.app.codrsync.dev |
| Best for | Landing pages, docs, SPAs | APIs, bots, automation, databases |

Static publishing is great for front-end apps. Sidecar services are for anything that needs a running process — databases, APIs, bots, workflow engines.

## Security Notes

- Only pre-approved container images are allowed (no arbitrary Docker images)
- Sidecar env vars (passwords, API keys) are stored encrypted and never shown in chat output
- Services are blocked in review mode (Titan Review) and plan mode
- Resource limits are enforced per tier — you cannot exceed your RAM/service quota
- Each service runs with CPU and memory caps to prevent resource exhaustion
