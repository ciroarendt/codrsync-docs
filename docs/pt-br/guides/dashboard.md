# Guia do Dashboard Web

O dashboard web do codrsync em [codrsync.dev/dashboard](https://codrsync.dev/dashboard) fornece uma interface visual para gerenciar seu armazenamento cloud, chaves API, faturamento e integrações.

## Armazenamento Cloud

### Criando um Bucket

1. Navegue até **Cloud Storage** na barra lateral
2. Clique em **Create Bucket**
3. Escolha seu backend:
   - **Storj** (Recomendado) — Melhor custo-benefício, $7/TB
   - **Filecoin** (Verificável) — Prova criptográfica de armazenamento, $30/TB (requer Pro+)
4. Digite o nome do bucket
5. Confirme — a criptografia (AES-256-GCM) é habilitada automaticamente

### Gerenciando Buckets

Na página Cloud Storage você pode:

- **Ver detalhes do bucket** — Nome, backend, contagem de objetos, status de criptografia
- **Navegar arquivos** — Explorar conteúdo do bucket
- **Excluir buckets** — Com diálogo de confirmação (bucket deve estar vazio)

### Monitoramento de Uso

O dashboard mostra estatísticas de uso em tempo real:

- **Armazenamento usado** — Uso atual vs. limite do plano (ex.: 2.4 GB / 50 GB)
- **Egress este mês** — Banda consumida vs. limite do plano
- **Requisições este mês** — Total de requisições API
- **Endpoint S3** — `https://cloud.codrsync.dev`

---

## Chaves API

Gerencie chaves API compatíveis com S3 para acesso programático ao seu armazenamento cloud.

### Criando uma Chave

1. Vá em **Cloud Storage** → **API Keys**
2. Clique em **Create Key**
3. Nomeie sua chave (ex.: "production-app", "ci-cd")
4. Copie o Access Key ID e a Secret Key — o segredo é mostrado apenas uma vez

### Usando Chaves API

Chaves API funcionam com qualquer cliente compatível com S3:

```bash
# AWS CLI
aws configure --profile codrsync
# Digite seu Access Key ID e Secret Key

aws s3 ls --profile codrsync --endpoint-url https://cloud.codrsync.dev
```

```python
# boto3
import boto3
s3 = boto3.client("s3",
    endpoint_url="https://cloud.codrsync.dev",
    aws_access_key_id="sua-access-key",
    aws_secret_access_key="sua-secret-key",
)
```

### Revogando Chaves

Clique no botão de revogar ao lado de qualquer chave. Chaves revogadas param de funcionar imediatamente.

---

## Faturamento & Assinatura

### Visualizando Seu Plano

A página de faturamento mostra:

- Plano atual (Grátis / Pro / Pro+ / Teams)
- Créditos restantes este mês
- Histórico de uso de créditos
- Uso de armazenamento

### Fazendo Upgrade

1. Vá em **Billing** na barra lateral
2. Clique em **Upgrade**
3. Escolha seu plano
4. Complete o pagamento pelo Stripe

### Gerenciando Assinatura

```bash
# Ou pelo CLI:
codrsync billing status     # Ver plano atual
codrsync billing upgrade    # Abrir portal de upgrade
codrsync billing portal     # Abrir portal de faturamento Stripe
```

### Comprando Créditos Extras

```bash
codrsync credits buy        # Comprar créditos adicionais ($5/100)
codrsync credits history    # Ver histórico de uso de créditos
```

---

## Integrações

Conecte serviços externos para melhorar seu fluxo de trabalho.

### Integrações Ativas

- **Notion** — Sincronize documentação do projeto com páginas do Notion

### Em Breve

- **Jira** — Sincronização de sprints e tarefas
- **Trello** — Sincronização de boards
- **ClickUp** — Integração de gerenciamento de tarefas

---

## Veja Também

- [Documentação cloudrsync](../products/cloudrsync.md) — Referência completa de armazenamento cloud
- [Comandos CLI](../cli/commands.md) — Gerencie tudo pelo terminal
- [Preços & Planos](pricing.md) — Comparação de planos e custos de créditos
