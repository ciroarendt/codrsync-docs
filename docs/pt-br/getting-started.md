# Primeiros Passos

## Pré-requisitos

- Python 3.10 ou superior
- pip ou Homebrew (para instalação)
- Chave API da Anthropic (para recursos de IA)

## Instalação

### Opção 1: Homebrew (Recomendado para macOS)

```bash
# Adicionar o tap
brew tap ciroarendt/codrsync

# Instalar codrsync
brew install codrsync

# Verificar instalação
codrsync --version
```

### Opção 2: pip

```bash
pip install codrsync
codrsync --version
```

## Configuração

### Configurar Chave API

Para recursos com IA, você precisa de uma chave API da Anthropic:

```bash
export ANTHROPIC_API_KEY="sk-ant-..."
```

Adicione ao seu `~/.bashrc` ou `~/.zshrc` para persistência.

### Autenticação Cloud

Alternativamente, use o codrsync cloud:

```bash
codrsync auth --cloud
```

Isso abre o navegador para autenticação.

## Seu Primeiro Projeto

### Novo Projeto

```bash
# Criar e entrar no diretório do projeto
mkdir meu-projeto && cd meu-projeto

# Inicializar com codrsync
codrsync init
```

O wizard vai guiá-lo através de:
1. Nome e descrição do projeto
2. Seleção de linguagem/framework
3. Criação da estrutura inicial

### Projeto Existente

```bash
cd seu-projeto-existente

# Escanear para detectar stack
codrsync scan

# Conectar integrações
codrsync connect
```

## Próximos Passos

- [Referência de Comandos CLI](cli/commands.md)
- [Guia Rápido](guides/quickstart.md)
- [Configuração de Integrações](guides/integrations.md)
