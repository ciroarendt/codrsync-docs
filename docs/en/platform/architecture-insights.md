---
title: Platform Architecture Insights
description: Strategic insights about codrsync's evolution from code workspace to mini-PaaS, storage tiers, and scaling strategy.
order: 11
---

# Platform Architecture Insights

## codrsync Is Already a VPS

A codrsync workspace is not just an IDE in the browser. It is a full Linux container running on a Hetzner ARM server with:
- Docker networking (shared bridge network with all platform services)
- Public URL with TLS (via Traefik reverse proxy)
- Persistent volumes (survive pause/resume)
- Direct access to cloud storage (Storj via cloud-gateway)
- AI-powered development assistant (Titan)

This means codrsync already provides the infrastructure that users typically need a VPS for. The key evolution is enabling users to run multi-container stacks — not just a single workspace container.

## From Static Files to Running Processes

codrsync has two publishing models:

**Static Publishing (CDN):** Workspace files are exported, uploaded to Storj, and served via `cdn.codrsync.dev`. The workspace can pause — files persist on Storj. Best for landing pages, documentation sites, SPAs, and portfolios.

**Service Publishing (Sidecars):** Additional containers run alongside the workspace with public HTTPS URLs. These are running processes — databases, APIs, bots, workflow engines. They need compute (CPU/RAM) and their data is archived to Storj when the workspace pauses.

The gap between these two is the gap between "hosting a website" and "running infrastructure." Sidecar services bridge this gap.

## Storage Tier Strategy

The platform uses three storage tiers to balance performance and cost:

**Hot tier (SSD, <1ms):** Docker volumes for active sidecar containers. Postgres data, Redis AOF, n8n databases. Limited by server SSD capacity (320 GB on current server). Used only when containers are actively running.

**Warm tier (Storj, ~50-100ms):** Application blobs accessed via the cloud-gateway S3 API. User uploads, generated PDFs, images, exports. Unlimited capacity at ~$7/TB/month. Apps inside the workspace use `http://cloud-gateway:3003/s3/` as an S3 endpoint — no credentials needed.

**Cold tier (Storj archive, ~5-30s):** Archived sidecar volumes. When a workspace pauses, sidecar data volumes are compressed (tar.gz) and uploaded to Storj, freeing local SSD. On resume, they are downloaded and restored. This makes paused workspaces cost essentially $0 in server resources.

Future: Filecoin via Storacha (PRP-22) will add an ultra-cold tier at ~$3/TB/month for long-term archives (volumes paused >30 days).

## No MinIO in the Architecture

The cloud-gateway connects directly to Storj's S3-compatible endpoint using the AWS SDK v3. There is no MinIO intermediary. The cloud-gateway itself acts as an authenticated S3 proxy — workspace containers call it with INTERNAL_TOKEN and it forwards to Storj.

For users who need a local S3 API (e.g., for an app that expects an S3 endpoint), MinIO can be added as an optional sidecar service. But for most use cases, the cloud-gateway is sufficient and simpler.

## DNS and Routing Architecture

All routing goes through Traefik v3.3 using the file provider (not the Docker provider, which is broken on Docker Engine 29.x).

**Workspace routes:** `{slug}.ws.codrsync.dev` → `ws-{slug}:8080` via per-workspace YAML files in `/etc/traefik/dynamic/`.

**Service routes:** `{name}-{slug}.app.codrsync.dev` → `ws-{slug}-{name}:{port}` via per-service YAML files.

**Static routes:** `cdn.codrsync.dev`, `n8n.codrsync.dev` → fixed backend containers.

TLS certificates are issued per-hostname via Let's Encrypt HTTP-01 challenge. Wildcard DNS records (`*.ws.codrsync.dev`, `*.app.codrsync.dev`) resolve all subdomains to the server IP, and Traefik routes based on the Host header.

## Scaling Path

**Current server (Hetzner CAX41):** 16 ARM vCPU, 32 GB RAM, 320 GB SSD (~$27/month). Supports ~25 concurrent workspace stacks with sidecars.

**First scale-up:** Add a worker node (CAX31, ~$14/month). Manager runs on the primary node, workspace containers run on the worker. The manager already uses dockerode — switching from local socket to remote Docker host is minimal code change.

**Multi-node:** Docker Swarm or k3s with 2+ worker nodes. Traefik stays on the primary node as the ingress controller.

The cold storage strategy (archive to Storj on pause) means disk capacity is only needed for actively running stacks, making the server much more efficient.

## n8n Integration (PRP-81)

There is a shared n8n instance at `n8n.codrsync.dev` that all workspaces can use via MCP tools (n8n_ping, n8n_execute, etc.). This is for platform-wide automations and actions (create GitHub issues, send Telegram messages, etc.).

With PRP-82 sidecar services, users can also run their OWN n8n instance as a sidecar, fully under their control. The shared n8n is for codrsync platform actions; per-user n8n is for user-specific automations.

## Key Insight: Automation Users Need Stacks, Not Just Code

The traditional "coding workspace" user wants to write and run code. But automation-focused users (agencies, growth teams, solopreneurs) need a different value proposition:

- **They need running infrastructure**, not just a development environment
- **They need webhook endpoints** to receive callbacks from external services
- **They need databases** to persist state across workflow executions
- **They need message queues** for reliable async processing
- **They need always-on processes** (bots, scrapers, API servers)

Sidecar services turn codrsync from "a place to write code" into "a place to run your entire automation stack." The AI assistant (Titan) makes this accessible to non-DevOps users — they describe what they want, and Titan provisions the infrastructure.
