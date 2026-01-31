# codrsync

[English](#english) | [Português](#português)

---

## English

**Turn any dev into jedi ninja codr**

codrsync is an AI-powered development orchestrator that helps you ship faster with confidence through guided implementation, interactive validation, and persistent context.

### Features

- **AI-Guided Development**: Intelligent assistance for complex implementations
- **Project Scaffolding**: Quick project setup with best practices
- **Stack Detection**: Automatic detection of languages, frameworks, and tools
- **Integration Support**: Connect with Supabase, Vercel, GitHub, and more
- **Persistent Context**: Maintains project context across sessions

### Installation

#### Via Homebrew (macOS)

```bash
brew tap ciroarendt/codrsync
brew install codrsync
```

#### Via pip

```bash
pip install codrsync
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
```

### Documentation

- [Getting Started](docs/en/getting-started.md)
- [CLI Commands](docs/en/cli/commands.md)
- [Quickstart Guide](docs/en/guides/quickstart.md)

### Configuration

Set your Anthropic API key for AI features:

```bash
export ANTHROPIC_API_KEY="your-key"
```

Or login to codrsync cloud:

```bash
codrsync auth --cloud
```

---

## Português

**Transforme qualquer dev em jedi ninja codr**

codrsync é um orquestrador de desenvolvimento com IA que ajuda você a entregar mais rápido e com confiança através de implementação guiada, validação interativa e contexto persistente.

### Recursos

- **Desenvolvimento Guiado por IA**: Assistência inteligente para implementações complexas
- **Scaffolding de Projetos**: Setup rápido com boas práticas
- **Detecção de Stack**: Detecção automática de linguagens, frameworks e ferramentas
- **Suporte a Integrações**: Conecte com Supabase, Vercel, GitHub e mais
- **Contexto Persistente**: Mantém contexto do projeto entre sessões

### Instalação

#### Via Homebrew (macOS)

```bash
brew tap ciroarendt/codrsync
brew install codrsync
```

#### Via pip

```bash
pip install codrsync
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
```

### Documentação

- [Primeiros Passos](docs/pt-br/getting-started.md)
- [Comandos CLI](docs/pt-br/cli/commands.md)
- [Guia Rápido](docs/pt-br/guides/quickstart.md)

### Configuração

Configure sua chave API da Anthropic para recursos de IA:

```bash
export ANTHROPIC_API_KEY="sua-chave"
```

Ou faça login no codrsync cloud:

```bash
codrsync auth --cloud
```

---

## Links

- [Website](https://codrsync.dev)
- [PyPI](https://pypi.org/project/codrsync/)
- [Homebrew Tap](https://github.com/ciroarendt/homebrew-codrsync)

## License / Licença

MIT
