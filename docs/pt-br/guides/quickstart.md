# Guia Rápido

Comece a usar o codrsync em 5 minutos.

## 1. Instalar

```bash
# macOS
brew tap ciroarendt/codrsync && brew install codrsync

# ou via pip
pip install codrsync
```

## 2. Configurar Chave API

```bash
export ANTHROPIC_API_KEY="sua-chave"
```

## 3. Criar Seu Primeiro Projeto

```bash
mkdir meu-app && cd meu-app
codrsync init
```

Siga os prompts interativos para:
- Nomear seu projeto
- Escolher linguagem/framework
- Configurar estrutura inicial

## 4. Explorar Comandos

```bash
# Verificar status do projeto
codrsync status

# Executar diagnósticos
codrsync doctor

# Iniciar sessão com IA
codrsync kickstart
```

## 5. Para Projetos Existentes

```bash
cd seu-projeto

# Detectar stack
codrsync scan

# Conectar serviços
codrsync connect
```

## Próximos Passos

- [Referência Completa CLI](../cli/commands.md)
- [Configuração de Integrações](integrations.md)
- [Boas Práticas](best-practices.md)

## Precisa de Ajuda?

- [Website](https://codrsync.dev)
- [Documentação](https://codrsync.dev/docs)
