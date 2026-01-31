# CLI Commands Reference

## Global Options

```bash
codrsync [OPTIONS] COMMAND [ARGS]
```

| Option | Description |
|--------|-------------|
| `--version` | Show version and exit |
| `--help` | Show help message |
| `--lang [en\|pt-br]` | Set language |

---

## Commands

### init

Initialize a new project with guided setup.

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

---

### scan

Scan existing project to detect stack and context.

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

---

### connect

Connect project integrations.

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

**Example:**
```bash
codrsync connect           # All services
codrsync connect supabase  # Specific service
```

---

### status

Show project status and configuration.

```bash
codrsync status [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--path PATH` | Project directory |

---

### doctor

Diagnose project configuration and dependencies.

```bash
codrsync doctor [OPTIONS]
```

Checks:
- Python version
- API key configuration
- Project structure
- Integration status

---

### auth

Manage authentication.

```bash
codrsync auth [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--cloud` | Authenticate with codrsync cloud |
| `--logout` | Remove saved credentials |
| `--status` | Show auth status |

---

### kickstart

Start AI-guided development session.

```bash
codrsync kickstart [OPTIONS]
```

| Option | Description |
|--------|-------------|
| `--path PATH` | Project directory |

Launches an interactive AI session for guided development.

---

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | General error |
| 2 | Configuration error |
| 3 | Authentication required |
