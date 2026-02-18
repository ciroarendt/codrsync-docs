# cloudrsync — Cloud Storage

S3-compatible cloud storage across a distributed global network. Up to 70% cheaper than AWS S3 with AES-256-GCM encryption by default.

## Overview

cloudrsync provides encrypted cloud storage through two backend options:

| | Storj (Recommended) | Filecoin (Verifiable) |
|---|---|---|
| **Storage** | $7/TB/month | $30/TB/month |
| **Egress** | $12/TB/month | $30/TB/month |
| **Best for** | General-purpose storage | Compliance, archival, censorship resistance |
| **Durability** | 99.9999999% | Cryptographically verified |
| **S3 compatible** | Yes | Yes |
| **Encryption** | AES-256-GCM | AES-256-GCM |
| **Plan required** | Free+ | Pro+ |

### Storage Limits by Plan

| Plan | Storage | Egress/month |
|------|---------|--------------|
| Free | 1 GB | 5 GB |
| Pro ($29/mo) | 50 GB | 100 GB |
| Pro+ ($49/mo) | 200 GB | 500 GB |
| Teams | Custom | Custom |

---

## Getting Started

### 1. Initialize Storage

```bash
# Login first
codrsync auth --cloud

# Initialize cloud storage
codrsync storage init
```

### 2. Create a Bucket

```bash
# Create with Storj backend (default, recommended)
codrsync storage bucket create my-bucket

# Create with Filecoin backend (requires Pro+)
codrsync storage bucket create my-archive --backend filecoin
```

### 3. Upload and Download

```bash
# Upload a file
codrsync storage put ./myfile.txt my-bucket/myfile.txt

# Download a file
codrsync storage get my-bucket/myfile.txt ./downloaded.txt

# List files in a bucket
codrsync storage ls my-bucket

# Remove a file
codrsync storage rm my-bucket/myfile.txt
```

---

## Encryption

All cloudrsync buckets use **AES-256-GCM encryption** by default. This is zero-knowledge encryption — your data is encrypted before it leaves your machine.

- Encryption is always enabled and cannot be disabled
- Keys are derived from your account credentials
- Neither cloudrsync nor the storage backend can read your data
- Fully transparent — works with all S3 clients without configuration

---

## S3-Compatible API

cloudrsync exposes a standard S3-compatible endpoint. Use any S3 client or SDK.

**Endpoint:** `https://cloud.codrsync.dev`

### Generate API Keys

```bash
# Create a new API key
codrsync storage keys create --name "my-app"

# List existing keys
codrsync storage keys list

# Revoke a key
codrsync storage keys revoke <key-id>
```

You can also manage API keys from the [web dashboard](../guides/dashboard.md).

### AWS CLI

```bash
# Configure AWS CLI for cloudrsync
aws configure --profile codrsync
# AWS Access Key ID: <your-codrsync-access-key>
# AWS Secret Access Key: <your-codrsync-secret-key>
# Default region name: us-east-1
# Default output format: json

# Use it
aws s3 ls --profile codrsync --endpoint-url https://cloud.codrsync.dev
aws s3 cp ./file.txt s3://my-bucket/file.txt --profile codrsync --endpoint-url https://cloud.codrsync.dev
```

### Python (boto3)

```python
import boto3

s3 = boto3.client(
    "s3",
    endpoint_url="https://cloud.codrsync.dev",
    aws_access_key_id="your-codrsync-access-key",
    aws_secret_access_key="your-codrsync-secret-key",
)

# List buckets
response = s3.list_buckets()
for bucket in response["Buckets"]:
    print(bucket["Name"])

# Upload
s3.upload_file("local-file.txt", "my-bucket", "remote-file.txt")

# Download
s3.download_file("my-bucket", "remote-file.txt", "local-file.txt")
```

### JavaScript (@aws-sdk/client-s3)

```javascript
import { S3Client, ListBucketsCommand, PutObjectCommand } from "@aws-sdk/client-s3";
import { readFileSync } from "fs";

const client = new S3Client({
  endpoint: "https://cloud.codrsync.dev",
  region: "us-east-1",
  credentials: {
    accessKeyId: "your-codrsync-access-key",
    secretAccessKey: "your-codrsync-secret-key",
  },
});

// List buckets
const { Buckets } = await client.send(new ListBucketsCommand({}));
console.log(Buckets);

// Upload
await client.send(new PutObjectCommand({
  Bucket: "my-bucket",
  Key: "file.txt",
  Body: readFileSync("./file.txt"),
}));
```

---

## CLI Reference

### Storage Commands

```bash
codrsync storage init                          # Initialize cloud storage
codrsync storage put <local> <remote>          # Upload file
codrsync storage get <remote> <local>          # Download file
codrsync storage ls [bucket]                   # List files/buckets
codrsync storage rm <remote>                   # Remove file
codrsync storage config                        # Show storage configuration
```

### Bucket Management

```bash
codrsync storage bucket create <name> [--backend storj|filecoin]
codrsync storage bucket list
codrsync storage bucket delete <name>
```

### API Key Management

```bash
codrsync storage keys create --name <name>
codrsync storage keys list
codrsync storage keys revoke <key-id>
```

---

## Storj Backend

Storj is the **recommended** backend for most use cases. It uses erasure coding across a globally distributed network of storage nodes.

**Why Storj:**
- Best price-performance ratio ($7/TB storage, $12/TB egress)
- 99.9999999% durability (11 nines)
- Data split and distributed across 80+ countries
- No single point of failure
- S3-compatible with zero configuration

**Annual cost comparison (10 TB):**

| Provider | Annual Cost |
|----------|-------------|
| **cloudrsync (Storj)** | **$840** |
| AWS S3 | $3,730 |
| Google Cloud Storage | $3,714 |
| Azure Blob | $3,294 |

---

## Filecoin Backend

Filecoin provides **cryptographically verifiable** storage. Every piece of data stored on Filecoin is backed by mathematical proofs.

**Why Filecoin:**

- **Proof of Replication (PoRep)** — Cryptographic proof that your data is uniquely stored
- **Proof of Spacetime (PoST)** — Continuous verification that data persists over time
- **Censorship resistance** — No single entity can remove your data
- **Immutability** — Content-addressed by CID (Content Identifier)
- **Vendor independence** — Open protocol, not controlled by any company

**Best for:**
- Regulatory compliance requiring proof of storage
- Long-term archival with verifiable integrity
- Data that must be censorship-resistant
- Organizations requiring vendor independence

**Requirements:** Pro or Pro+ plan.

---

## Pricing

cloudrsync storage costs are included in your plan limits. No credits are consumed.

| | Free | Pro ($29/mo) | Pro+ ($49/mo) |
|---|---|---|---|
| Storage | 1 GB | 50 GB | 200 GB |
| Egress/month | 5 GB | 100 GB | 500 GB |
| Storj backend | Yes | Yes | Yes |
| Filecoin backend | — | Yes | Yes |

Need more storage? [Contact us for Teams/Enterprise pricing.](https://codrsync.dev/pricing)

---

## See Also

- [Dashboard Guide](../guides/dashboard.md) — Manage buckets and keys from the web
- [Pricing & Plans](../guides/pricing.md) — Full plan comparison
- [CLI Commands](../cli/commands.md) — Complete CLI reference
