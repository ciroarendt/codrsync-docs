# Product Suite Overview

codrsync is more than a CLI — it's a complete development platform. Here's everything in the suite.

## codrsync

**AI Development Orchestrator**

The core CLI that orchestrates your AI-powered development. Context engineering that makes any AI 10x smarter.

- **Universal AI support** — Claude, GPT-5, Gemini 3, Grok, or local models via Ollama
- **Persistent context** — Your project knowledge survives across sessions
- **Superego validation** — Use codrsync as a meta-orchestrator for Claude Code
- **MCP integrations** — Connect Supabase, Vercel, GitHub, and more
- **BYOK supported** — Bring your own API key on any plan

```bash
codrsync init        # Initialize project
codrsync scan        # Detect stack and integrations
codrsync start       # Launch superego mode
codrsync build       # AI-guided development
```

**Available on:** All plans (Free includes full CLI with BYOK).

---

## cloudrsync

**S3-Compatible Cloud Storage**

Cloud storage across a distributed global network — up to 70% cheaper than AWS S3 with AES-256-GCM encryption by default.

- **Two backends** — Storj (recommended, $7/TB) or Filecoin (verifiable, $30/TB)
- **S3-compatible API** — Works with AWS CLI, boto3, any S3 SDK
- **Zero-knowledge encryption** — AES-256-GCM enabled on all buckets
- **99.9999999% durability** — Enterprise-grade reliability
- **No vendor lock-in** — Standard S3 protocol

**Storage by plan:** Free 1 GB / Pro 50 GB / Pro+ 200 GB

[Full cloudrsync documentation →](cloudrsync.md)

---

## docrsync

**Auto Documentation**

Generate and maintain technical documentation automatically. README, API docs, guides — always up to date.

- **Auto-generated docs** — From codebase analysis
- **API documentation** — OpenAPI/Swagger compatible
- **Multi-language support** — English, Portuguese, and more
- **Ongoing updates** — Teams plan includes continuous auto-updates

### Credit Costs

| Mode | Output | Credits |
|------|--------|---------|
| README generation | Single README file | 5 |
| Technical docs | ~10 pages of documentation | 15 |
| Full documentation suite | Complete docs package | 30 |

```bash
codrsync docrsync --mode readme       # 5 credits
codrsync docrsync --mode technical    # 15 credits
codrsync docrsync --mode full         # 30 credits
```

**Available on:** Pro, Pro+, Teams. Not available on Free.

---

## pptrsync

**AI Presentations**

Create beautiful presentations from your codebase. Pitch decks, demos, reports with AI-generated visuals.

- **AI slide generation** — Analyze code and create slides automatically
- **Flux Pro images** — Premium AI-generated visuals (Pro+ only)
- **PPTX/PDF export** — Download in standard formats
- **Custom templates** — Match your brand

### Credit Costs

| Mode | Output | Credits |
|------|--------|---------|
| Quick deck | 5 slides | 10 |
| Standard deck | 10 slides | 20 |
| Full deck | 20 slides | 35 |
| Flux Pro images | AI-generated premium images | +10 |
| PPTX/PDF export | Downloadable file | +5 |

```bash
codrsync pptrsync --mode quick        # 10 credits
codrsync pptrsync --mode standard     # 20 credits
codrsync pptrsync --mode full         # 35 credits
codrsync pptrsync --mode full --flux  # 45 credits (full + Flux Pro)
codrsync export --format pptx         # +5 credits
```

**Available on:** Pro, Pro+, Teams. Not available on Free.

---

## envrsync

**Environment Scanner**

Analyze your project environment instantly. Detect stack, dependencies, security issues, and get AI recommendations.

- **Stack detection** — Languages, frameworks, databases, tools
- **Security analysis** — Vulnerability scanning and recommendations
- **Dependency audit** — Outdated packages, license issues
- **AI recommendations** — Actionable improvement suggestions

### Credit Costs

| Mode | Description | Credits |
|------|-------------|---------|
| Basic scan | Local analysis, no AI | 0 (free) |
| Deep AI analysis | Full AI-powered analysis | 5 |

```bash
codrsync envrsync                    # Basic scan (free)
codrsync envrsync --deep             # Deep AI analysis (5 credits)
```

**Available on:** All plans. Free includes basic scans; Pro+ includes deep AI analysis.

---

## gpursync

**Distributed GPU Cloud** *(Coming Soon)*

On-demand GPU compute for ML training, inference, and batch processing — powered by a distributed network of GPU providers.

- **On-demand GPUs** — No long-term commitments
- **Distributed network** — Access GPUs globally
- **ML-optimized** — Pre-configured for TensorFlow, PyTorch, JAX
- **Cost-efficient** — Pay only for what you use

> gpursync is currently in development. [Join the waitlist →](https://codrsync.dev/gpursync)

---

## Plan Comparison

| Feature | Free | Pro ($29/mo) | Pro+ ($49/mo) | Teams ($99/seat/mo) |
|---------|------|--------------|---------------|---------------------|
| codrsync CLI | Full | Full | Full | Full |
| Cloud Workspace | — | Included | Included | Included |
| cloudrsync storage | 1 GB | 50 GB | 200 GB | Custom |
| docrsync | — | 5-30 credits | 5-30 credits | Auto-updates |
| pptrsync | — | 10-35 credits | + Flux Pro | + Flux Pro |
| envrsync | Basic | + Deep AI | + Deep AI | + Deep AI |
| Credits/month | 0 | 500 | 1,500 | 2,000/seat |
| Credit rollover | — | — | Up to 500 | Up to 500 |

[Full pricing details →](../guides/pricing.md)
