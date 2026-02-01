# CLI Commands Reference

## Global Options

```bash
codrsync [OPTIONS] COMMAND [ARGS]
```

| Option | Description |
|--------|-------------|
| `--version`, `-v` | Show version and exit |
| `--help` | Show help message |
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
| `--format FORMAT` | Output format (json, markdown) |
| `--output PATH` | Output file path |

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
| `list` | List all sprints |
| `current` | Show current sprint |
| `create` | Create new sprint |

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

## Configuration Commands

### auth

Configure AI backend authentication.

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

### storage

Manage cloud storage.

```bash
codrsync storage [SUBCOMMAND]
```

| Subcommand | Description |
|------------|-------------|
| `list` | List stored files |
| `sync` | Sync local/cloud |
| `clear` | Clear cloud storage |

---

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 2 | Configuration error |
| 3 | Authentication required |
