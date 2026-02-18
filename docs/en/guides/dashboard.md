# Web Dashboard Guide

The codrsync web dashboard at [codrsync.dev/dashboard](https://codrsync.dev/dashboard) provides a visual interface for managing your cloud storage, API keys, billing, and integrations.

## Cloud Storage

### Creating a Bucket

1. Navigate to **Cloud Storage** in the sidebar
2. Click **Create Bucket**
3. Choose your backend:
   - **Storj** (Recommended) — Best price-performance, $7/TB
   - **Filecoin** (Verifiable) — Cryptographic proof of storage, $30/TB (requires Pro+)
4. Enter a bucket name
5. Confirm — encryption (AES-256-GCM) is enabled automatically

### Managing Buckets

From the Cloud Storage page you can:

- **View bucket details** — Name, backend, object count, encryption status
- **Browse files** — Navigate bucket contents
- **Delete buckets** — With confirmation dialog (bucket must be empty)

### Usage Monitoring

The dashboard shows real-time usage stats:

- **Storage used** — Current usage vs. plan limit (e.g., 2.4 GB / 50 GB)
- **Egress this month** — Bandwidth consumed vs. plan limit
- **Requests this month** — Total API requests
- **S3 endpoint** — `https://cloud.codrsync.dev`

---

## API Keys

Manage S3-compatible API keys for programmatic access to your cloud storage.

### Creating a Key

1. Go to **Cloud Storage** → **API Keys**
2. Click **Create Key**
3. Name your key (e.g., "production-app", "ci-cd")
4. Copy the Access Key ID and Secret Key — the secret is only shown once

### Using API Keys

API keys work with any S3-compatible client:

```bash
# AWS CLI
aws configure --profile codrsync
# Enter your Access Key ID and Secret Key

aws s3 ls --profile codrsync --endpoint-url https://cloud.codrsync.dev
```

```python
# boto3
import boto3
s3 = boto3.client("s3",
    endpoint_url="https://cloud.codrsync.dev",
    aws_access_key_id="your-access-key",
    aws_secret_access_key="your-secret-key",
)
```

### Revoking Keys

Click the revoke button next to any key. Revoked keys stop working immediately.

---

## Billing & Subscription

### Viewing Your Plan

The billing page shows:

- Current plan (Free / Pro / Pro+ / Teams)
- Credits remaining this month
- Credit usage history
- Storage usage

### Upgrading

1. Go to **Billing** in the sidebar
2. Click **Upgrade**
3. Choose your plan
4. Complete payment through Stripe

### Managing Subscription

```bash
# Or from the CLI:
codrsync billing status     # View current plan
codrsync billing upgrade    # Open upgrade portal
codrsync billing portal     # Open Stripe billing portal
```

### Buying Extra Credits

```bash
codrsync credits buy        # Purchase additional credits ($5/100)
codrsync credits history    # View credit usage history
```

---

## Integrations

Connect external services to enhance your workflow.

### Active Integrations

- **Notion** — Sync project documentation to Notion pages

### Coming Soon

- **Jira** — Sync sprints and tasks
- **Trello** — Board synchronization
- **ClickUp** — Task management integration

---

## See Also

- [cloudrsync Documentation](../products/cloudrsync.md) — Full cloud storage reference
- [CLI Commands](../cli/commands.md) — Manage everything from the terminal
- [Pricing & Plans](pricing.md) — Plan comparison and credit costs
