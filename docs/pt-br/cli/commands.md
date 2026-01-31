# Referência de Comandos CLI

## Opções Globais

```bash
codrsync [OPÇÕES] COMANDO [ARGS]
```

| Opção | Descrição |
|-------|-----------|
| `--version` | Mostrar versão e sair |
| `--help` | Mostrar mensagem de ajuda |
| `--lang [en\|pt-br]` | Definir idioma |

---

## Comandos

### init

Inicializar um novo projeto com setup guiado.

```bash
codrsync init [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto (padrão: atual) |
| `--template NOME` | Usar um template específico |

**Exemplo:**
```bash
codrsync init --path ./meu-app
```

---

### scan

Escanear projeto existente para detectar stack e contexto.

```bash
codrsync scan [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto (padrão: atual) |
| `--github` | Importar issues e PRs do GitHub |
| `--docs` | Escanear arquivos de documentação |
| `--deep` | Gerar resumo de contexto com IA |

**Exemplo:**
```bash
codrsync scan --github --docs
```

---

### connect

Conectar integrações do projeto.

```bash
codrsync connect [SERVIÇO] [OPÇÕES]
```

| Serviço | Descrição |
|---------|-----------|
| `supabase` | Conectar projeto Supabase |
| `vercel` | Conectar deploy Vercel |
| `github` | Conectar repositório GitHub |
| `tailwind` | Detectar configuração Tailwind |
| `mcp` | Detectar servidores MCP |

**Exemplo:**
```bash
codrsync connect           # Todos os serviços
codrsync connect supabase  # Serviço específico
```

---

### status

Mostrar status e configuração do projeto.

```bash
codrsync status [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto |

---

### doctor

Diagnosticar configuração e dependências do projeto.

```bash
codrsync doctor [OPÇÕES]
```

Verifica:
- Versão do Python
- Configuração da chave API
- Estrutura do projeto
- Status das integrações

---

### auth

Gerenciar autenticação.

```bash
codrsync auth [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--cloud` | Autenticar com codrsync cloud |
| `--logout` | Remover credenciais salvas |
| `--status` | Mostrar status de autenticação |

---

### kickstart

Iniciar sessão de desenvolvimento guiada por IA.

```bash
codrsync kickstart [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto |

Inicia uma sessão interativa com IA para desenvolvimento guiado.

---

## Códigos de Saída

| Código | Significado |
|--------|-------------|
| 0 | Sucesso |
| 1 | Erro geral |
| 2 | Erro de configuração |
| 3 | Autenticação necessária |
