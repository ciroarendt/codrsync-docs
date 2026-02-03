# codrsync

[English](#english) | [Português](#português)

---

## English

**Your AI's AI — Context engineering made simple**

codrsync is an AI-powered development orchestrator that helps you ship faster with confidence through guided implementation, interactive validation, and persistent context.

### Features

- **Context Engineering**: Optimize AI interactions with structured context
- **AI-Guided Development**: Intelligent assistance for complex implementations
- **AI-Assisted Onboarding**: Get help during installation with `codrsync --help-ai`
- **Stack Detection**: Automatic detection of languages, frameworks, and tools
- **Integration Support**: Connect with Supabase, Vercel, GitHub, Tailwind, and more
- **Superego Mode**: Use codrsync as a meta-orchestrator for Claude Code
- **Multi-provider**: Works with Claude, GPT, Gemini, and local models via Ollama

### Installation

Choose your preferred method:

```bash
# Recommended: Install script
curl -fsSL https://codrsync.dev/install.sh | bash

# Homebrew (macOS/Linux)
brew tap ciroarendt/codrsync
brew install codrsync

# pip
pip install codrsync

# pipx (isolated environment)
pipx install codrsync

# npm (installs Python package automatically)
npm install -g codrsync
```

### Quick Start

```bash
# Initialize a new project
codrsync init

# Scan existing project
codrsync scan

# Check project status
codrsync status

# Connect integrations
codrsync connect

# Start superego mode with Claude Code
codrsync start
```

### Commands

| Command | Description |
|---------|-------------|
| `init` | Initialize project with AI-guided kickstart |
| `scan` | Detect stack, docs, and integrations |
| `connect` | Check integration status |
| `status` | Show project dashboard |
| `build` | Execute development with AI guidance |
| `prp` | Manage PRPs (Product Requirement Prompts) |
| `start` | Start Claude Code with codrsync as superego |
| `sprint` | Manage development sprints |
| `doctor` | Check installation and configuration |

### Documentation

- [Getting Started](docs/en/getting-started.md)
- [CLI Commands](docs/en/cli/commands.md)
- [Quickstart Guide](docs/en/guides/quickstart.md)

### Configuration

Set your API key for AI features:

```bash
# Anthropic (Claude)
export ANTHROPIC_API_KEY="your-key"

# OpenAI (GPT)
export OPENAI_API_KEY="your-key"

# Or login to codrsync cloud
codrsync auth --cloud
```

---

## Português

**A IA da sua IA — Engenharia de contexto simplificada**

codrsync é um orquestrador de desenvolvimento com IA que ajuda você a entregar mais rápido e com confiança através de implementação guiada, validação interativa e contexto persistente.

### Recursos

- **Context Engineering**: Otimize interações com IA usando contexto estruturado
- **Desenvolvimento Guiado por IA**: Assistência inteligente para implementações complexas
- **Onboarding com IA**: Receba ajuda durante a instalação com `codrsync --help-ai`
- **Detecção de Stack**: Detecção automática de linguagens, frameworks e ferramentas
- **Suporte a Integrações**: Conecte com Supabase, Vercel, GitHub, Tailwind e mais
- **Modo Superego**: Use codrsync como meta-orquestrador para Claude Code
- **Multi-provider**: Funciona com Claude, GPT, Gemini e modelos locais via Ollama

### Instalação

Escolha seu método preferido:

```bash
# Recomendado: Script de instalação
curl -fsSL https://codrsync.dev/install.sh | bash

# Homebrew (macOS/Linux)
brew tap ciroarendt/codrsync
brew install codrsync

# pip
pip install codrsync

# pipx (ambiente isolado)
pipx install codrsync

# npm (instala o pacote Python automaticamente)
npm install -g codrsync
```

### Início Rápido

```bash
# Inicializar novo projeto
codrsync init

# Escanear projeto existente
codrsync scan

# Verificar status do projeto
codrsync status

# Conectar integrações
codrsync connect

# Iniciar modo superego com Claude Code
codrsync start
```

### Comandos

| Comando | Descrição |
|---------|-----------|
| `init` | Inicializar projeto com kickstart guiado por IA |
| `scan` | Detectar stack, docs e integrações |
| `connect` | Verificar status de integrações |
| `status` | Mostrar dashboard do projeto |
| `build` | Executar desenvolvimento com guia IA |
| `prp` | Gerenciar PRPs (Product Requirement Prompts) |
| `start` | Iniciar Claude Code com codrsync como superego |
| `sprint` | Gerenciar sprints de desenvolvimento |
| `doctor` | Verificar instalação e configuração |

### Documentação

- [Primeiros Passos](docs/pt-br/getting-started.md)
- [Comandos CLI](docs/pt-br/cli/commands.md)
- [Guia Rápido](docs/pt-br/guides/quickstart.md)

### Configuração

Configure sua chave API para recursos de IA:

```bash
# Anthropic (Claude)
export ANTHROPIC_API_KEY="sua-chave"

# OpenAI (GPT)
export OPENAI_API_KEY="sua-chave"

# Ou faça login no codrsync cloud
codrsync auth --cloud
```

---

## Links

- [Website](https://codrsync.dev)
- [PyPI](https://pypi.org/project/codrsync/)
- [npm](https://www.npmjs.com/package/codrsync)
- [Homebrew Tap](https://github.com/ciroarendt/homebrew-codrsync)

## License / Licença

MIT
