# CLI Commands Reference

## Global Options

```bash
codrsync [OPTIONS] COMMAND [ARGS]
```

| Option | Description |
|--------|-------------|
| `--version`, `-v` | Show version and exit |
| `--help` | Show help message |
| `--help-ai` | Start AI-assisted onboarding chat |
| `--lang [en\|pt-br]` | Set language |

---

## Local Commands (No AI needed)

### status

Show project status dashboard.

```bash
codrsync status [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--path PATH` | Project directory |

---

### roadmap

Show project roadmap and timeline.

```bash
codrsync roadmap
```

---

### export

Export project to different formats.

```bash
codrsync export [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--format FORMAT` | Output format: `json`, `markdown`, `excel`, `jira`, `trello`, `notion` |
| `--output PATH` | Output file path |

**Examples:**
```bash
codrsync export --format excel --output sprint-report.xlsx
codrsync export --format jira
codrsync export --format notion
```

---

### scan

Scan current project to detect stack, docs, and integrations.

```bash
codrsync scan [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--path PATH` | Project directory (default: current) |
| `--github` | Import GitHub issues and PRs |
| `--docs` | Scan documentation files |
| `--deep` | Generate AI context summary |

**Example:**
```bash
codrsync scan --github --docs
```

**Detects:**
- Languages: Python, JavaScript/TypeScript, Go, Rust, etc.
- Frameworks: Next.js, FastAPI, Django, Express, etc.
- Databases: Prisma, Supabase, PostgreSQL, MongoDB
- Infrastructure: Docker, Kubernetes, Vercel, GitHub Actions
- Tools: Tailwind CSS, ESLint, Prettier, etc.

---

### connect

Check and display integration status for external services.

```bash
codrsync connect [SERVICE] [OPTIONS]
```

| Service | Description |
|---------|-------------|
| `supabase` | Connect Supabase project |
| `vercel` | Connect Vercel deployment |
| `github` | Connect GitHub repository |
| `tailwind` | Detect Tailwind configuration |
| `mcp` | Detect MCP servers |
| `digitalocean` | Connect DigitalOcean |

**Example:**
```bash
codrsync connect           # All services
codrsync connect supabase  # Specific service
```

---

### sprint

Manage development sprints.

```bash
codrsync sprint [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `start` | Start a new sprint |
| `plan` | Plan sprint tasks and goals |
| `review` | Review sprint progress |
| `retro` | Run sprint retrospective |
| `close` | Close current sprint |
| `check` | Check sprint health |
| `time` | Show time tracking |
| `calibrate` | Calibrate velocity estimates |
| `list` | List all sprints |
| `current` | Show current sprint |
| `create` | Create new sprint |

**Examples:**
```bash
codrsync sprint start --name "Sprint 5"
codrsync sprint plan
codrsync sprint check
codrsync sprint review
codrsync sprint retro
codrsync sprint close
codrsync sprint calibrate
```

---

## AI-Powered Commands

### init

Initialize a new project with AI-guided kickstart.

```bash
codrsync init [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--path PATH` | Project directory (default: current) |
| `--template NAME` | Use a specific template |

**Example:**
```bash
codrsync init --path ./my-app
```

If run in a directory with existing code, offers to import the project.

---

### build

Execute development with AI guidance.

```bash
codrsync build [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--prp FILE` | PRP file to execute |
| `--step N` | Start from specific step |

---

### prp

Manage PRPs (Product Requirement Prompts).

```bash
codrsync prp [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `list` | List all PRPs |
| `create` | Create new PRP |
| `show NAME` | Show PRP details |

---

### start

Start Claude Code with codrsync as superego.

```bash
codrsync start [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--path PATH` | Project directory |
| `--model MODEL` | AI model to use |

Launches Claude Code with full project context and codrsync guidelines.

---

### docrsync

Generate technical documentation from your codebase.

```bash
codrsync docrsync [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--mode MODE` | Generation mode: `readme`, `technical`, `full` |
| `--output PATH` | Output directory |

**Credit costs:**

| Mode | Description | Credits |
|------|-------------|---------|
| `readme` | Generate README file | 5 |
| `technical` | ~10 pages of documentation | 15 |
| `full` | Complete documentation suite | 30 |

**Examples:**
```bash
codrsync docrsync --mode readme          # 5 credits
codrsync docrsync --mode technical       # 15 credits
codrsync docrsync --mode full            # 30 credits
```

**Available on:** Pro, Pro+, Teams.

---

### pptrsync

Create presentations from your codebase with AI.

```bash
codrsync pptrsync [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--mode MODE` | Generation mode: `quick`, `standard`, `full` |
| `--flux` | Use Flux Pro AI images (Pro+ only) |
| `--output PATH` | Output file path |

**Credit costs:**

| Mode | Slides | Credits |
|------|--------|---------|
| `quick` | 5 slides | 10 |
| `standard` | 10 slides | 20 |
| `full` | 20 slides | 35 |
| `--flux` | Flux Pro images | +10 |

**Examples:**
```bash
codrsync pptrsync --mode quick           # 10 credits
codrsync pptrsync --mode standard        # 20 credits
codrsync pptrsync --mode full --flux     # 45 credits
codrsync export --format pptx            # Export to PPTX (+5 credits)
```

**Available on:** Pro, Pro+, Teams.

---

### envrsync

Analyze your project environment.

```bash
codrsync envrsync [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--deep` | Run deep AI analysis (5 credits) |

**Credit costs:**

| Mode | Description | Credits |
|------|-------------|---------|
| Default | Basic local scan | 0 (free) |
| `--deep` | Full AI-powered analysis | 5 |

**Examples:**
```bash
codrsync envrsync                        # Basic scan (free)
codrsync envrsync --deep                 # Deep AI analysis (5 credits)
```

**Available on:** All plans. Deep analysis requires Pro+.

---

## Cloud Storage Commands

### storage

Manage cloudrsync cloud storage. [Full cloudrsync docs →](../products/cloudrsync.md)

```bash
codrsync storage [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `init` | Initialize cloud storage connection |
| `put <local> <remote>` | Upload file to cloud |
| `get <remote> <local>` | Download file from cloud |
| `ls [bucket]` | List buckets or files in a bucket |
| `rm <remote>` | Remove file from cloud |
| `config` | Show storage configuration |

**Examples:**
```bash
codrsync storage init
codrsync storage put ./data.csv my-bucket/data.csv
codrsync storage get my-bucket/data.csv ./local-data.csv
codrsync storage ls
codrsync storage ls my-bucket
codrsync storage rm my-bucket/old-file.txt
codrsync storage config
```

### storage bucket

Manage storage buckets.

```bash
codrsync storage bucket [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `create <name> [--backend storj\|filecoin]` | Create a new bucket |
| `list` | List all buckets |
| `delete <name>` | Delete a bucket |

**Examples:**
```bash
codrsync storage bucket create my-bucket                    # Storj (default)
codrsync storage bucket create my-archive --backend filecoin  # Filecoin
codrsync storage bucket list
codrsync storage bucket delete old-bucket
```

### storage keys

Manage S3-compatible API keys.

```bash
codrsync storage keys [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `create --name <name>` | Create a new API key |
| `list` | List all API keys |
| `revoke <key-id>` | Revoke an API key |

**Examples:**
```bash
codrsync storage keys create --name "production"
codrsync storage keys list
codrsync storage keys revoke abc123
```

---

## Cloud Session Commands

### cloud

Manage cloud workspace sessions.

```bash
codrsync cloud [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `status` | Show cloud workspace status |
| `download` | Download workspace files |
| `upload` | Upload files to workspace |
| `stop` | Stop cloud workspace |

---

## Billing Commands

### billing

Manage subscription and billing.

```bash
codrsync billing [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `status` | Show current plan and usage |
| `upgrade` | Open upgrade portal |
| `portal` | Open Stripe billing portal |
| `credits` | Show credit balance |

### credits

Manage credits.

```bash
codrsync credits [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `buy` | Purchase additional credits ($5/100) |
| `history` | View credit usage history |

---

## Configuration Commands

### auth

Configure authentication.

```bash
codrsync auth [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--cloud` | Authenticate with codrsync cloud |
| `--logout` | Remove saved credentials |
| `--status` | Show auth status |

---

### doctor

Check codrsync installation and configuration.

```bash
codrsync doctor [OPTIONS]
```

Checks:
- Python version
- API key configuration
- Project structure
- Integration status
- CLI dependencies

---

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 2 | Configuration error |
| 3 | Authentication required |
