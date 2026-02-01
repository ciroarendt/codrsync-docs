# Referência de Comandos CLI

## Opções Globais

```bash
codrsync [OPÇÕES] COMANDO [ARGS]
```

| Opção | Descrição |
|-------|-----------|
| `--version`, `-v` | Mostrar versão e sair |
| `--help` | Mostrar mensagem de ajuda |
| `--lang [en\|pt-br]` | Definir idioma |

---

## Comandos Locais (Sem IA)

### status

Mostrar dashboard de status do projeto.

```bash
codrsync status [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto |

---

### roadmap

Mostrar roadmap e timeline do projeto.

```bash
codrsync roadmap
```

---

### export

Exportar projeto para diferentes formatos.

```bash
codrsync export [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--format FORMATO` | Formato de saída (json, markdown) |
| `--output CAMINHO` | Caminho do arquivo de saída |

---

### scan

Escanear projeto atual para detectar stack, docs e integrações.

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

**Detecta:**
- Linguagens: Python, JavaScript/TypeScript, Go, Rust, etc.
- Frameworks: Next.js, FastAPI, Django, Express, etc.
- Bancos de dados: Prisma, Supabase, PostgreSQL, MongoDB
- Infraestrutura: Docker, Kubernetes, Vercel, GitHub Actions
- Ferramentas: Tailwind CSS, ESLint, Prettier, etc.

---

### connect

Verificar e mostrar status de integrações com serviços externos.

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
| `digitalocean` | Conectar DigitalOcean |

**Exemplo:**
```bash
codrsync connect           # Todos os serviços
codrsync connect supabase  # Serviço específico
```

---

### sprint

Gerenciar sprints de desenvolvimento.

```bash
codrsync sprint [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `list` | Listar todas as sprints |
| `current` | Mostrar sprint atual |
| `create` | Criar nova sprint |

---

## Comandos com IA

### init

Inicializar novo projeto com kickstart guiado por IA.

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

Se executado em diretório com código existente, oferece importar o projeto.

---

### build

Executar desenvolvimento com guia de IA.

```bash
codrsync build [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--prp ARQUIVO` | Arquivo PRP para executar |
| `--step N` | Iniciar de passo específico |

---

### prp

Gerenciar PRPs (Product Requirement Prompts).

```bash
codrsync prp [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `list` | Listar todos os PRPs |
| `create` | Criar novo PRP |
| `show NOME` | Mostrar detalhes do PRP |

---

### start

Iniciar Claude Code com codrsync como superego.

```bash
codrsync start [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto |
| `--model MODELO` | Modelo de IA a usar |

Inicia o Claude Code com contexto completo do projeto e diretrizes do codrsync.

---

## Comandos de Configuração

### auth

Configurar autenticação do backend de IA.

```bash
codrsync auth [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--cloud` | Autenticar com codrsync cloud |
| `--logout` | Remover credenciais salvas |
| `--status` | Mostrar status de autenticação |

---

### doctor

Verificar instalação e configuração do codrsync.

```bash
codrsync doctor [OPÇÕES]
```

Verifica:
- Versão do Python
- Configuração da chave API
- Estrutura do projeto
- Status das integrações
- Dependências do CLI

---

### storage

Gerenciar armazenamento cloud.

```bash
codrsync storage [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `list` | Listar arquivos armazenados |
| `sync` | Sincronizar local/cloud |
| `clear` | Limpar armazenamento cloud |

---

## Códigos de Saída

| Código | Significado |
|--------|-------------|
| 0 | Sucesso |
| 1 | Erro geral |
| 2 | Erro de configuração |
| 3 | Autenticação necessária |
