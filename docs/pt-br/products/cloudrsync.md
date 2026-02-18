# cloudrsync — Armazenamento Cloud

Armazenamento cloud compatível com S3 em uma rede global distribuída. Até 70% mais barato que AWS S3 com criptografia AES-256-GCM por padrão.

## Visão Geral

cloudrsync oferece armazenamento cloud criptografado através de duas opções de backend:

| | Storj (Recomendado) | Filecoin (Verificável) |
|---|---|---|
| **Armazenamento** | $7/TB/mês | $30/TB/mês |
| **Egress** | $12/TB/mês | $30/TB/mês |
| **Melhor para** | Armazenamento geral | Compliance, arquivamento, resistência à censura |
| **Durabilidade** | 99.9999999% | Verificada criptograficamente |
| **Compatível S3** | Sim | Sim |
| **Criptografia** | AES-256-GCM | AES-256-GCM |
| **Plano necessário** | Grátis+ | Pro+ |

### Limites de Armazenamento por Plano

| Plano | Armazenamento | Egress/mês |
|-------|---------------|------------|
| Grátis | 1 GB | 5 GB |
| Pro ($29/mês) | 50 GB | 100 GB |
| Pro+ ($49/mês) | 200 GB | 500 GB |
| Teams | Personalizado | Personalizado |

---

## Começando

### 1. Inicializar Armazenamento

```bash
# Login primeiro
codrsync auth --cloud

# Inicializar armazenamento cloud
codrsync storage init
```

### 2. Criar um Bucket

```bash
# Criar com backend Storj (padrão, recomendado)
codrsync storage bucket create meu-bucket

# Criar com backend Filecoin (requer Pro+)
codrsync storage bucket create meu-arquivo --backend filecoin
```

### 3. Upload e Download

```bash
# Upload de arquivo
codrsync storage put ./meuarquivo.txt meu-bucket/meuarquivo.txt

# Download de arquivo
codrsync storage get meu-bucket/meuarquivo.txt ./baixado.txt

# Listar arquivos em um bucket
codrsync storage ls meu-bucket

# Remover um arquivo
codrsync storage rm meu-bucket/meuarquivo.txt
```

---

## Criptografia

Todos os buckets cloudrsync usam criptografia **AES-256-GCM** por padrão. É criptografia zero-knowledge — seus dados são criptografados antes de sair da sua máquina.

- Criptografia está sempre habilitada e não pode ser desabilitada
- Chaves são derivadas das suas credenciais de conta
- Nem o cloudrsync nem o backend de armazenamento podem ler seus dados
- Totalmente transparente — funciona com todos os clientes S3 sem configuração

---

## API Compatível com S3

cloudrsync expõe um endpoint padrão compatível com S3. Use qualquer cliente ou SDK S3.

**Endpoint:** `https://cloud.codrsync.dev`

### Gerar Chaves API

```bash
# Criar nova chave API
codrsync storage keys create --name "meu-app"

# Listar chaves existentes
codrsync storage keys list

# Revogar uma chave
codrsync storage keys revoke <key-id>
```

Você também pode gerenciar chaves API pelo [dashboard web](../guides/dashboard.md).

### AWS CLI

```bash
# Configurar AWS CLI para cloudrsync
aws configure --profile codrsync
# AWS Access Key ID: <sua-access-key-codrsync>
# AWS Secret Access Key: <sua-secret-key-codrsync>
# Default region name: us-east-1
# Default output format: json

# Usar
aws s3 ls --profile codrsync --endpoint-url https://cloud.codrsync.dev
aws s3 cp ./arquivo.txt s3://meu-bucket/arquivo.txt --profile codrsync --endpoint-url https://cloud.codrsync.dev
```

### Python (boto3)

```python
import boto3

s3 = boto3.client(
    "s3",
    endpoint_url="https://cloud.codrsync.dev",
    aws_access_key_id="sua-access-key-codrsync",
    aws_secret_access_key="sua-secret-key-codrsync",
)

# Listar buckets
response = s3.list_buckets()
for bucket in response["Buckets"]:
    print(bucket["Name"])

# Upload
s3.upload_file("arquivo-local.txt", "meu-bucket", "arquivo-remoto.txt")

# Download
s3.download_file("meu-bucket", "arquivo-remoto.txt", "arquivo-local.txt")
```

### JavaScript (@aws-sdk/client-s3)

```javascript
import { S3Client, ListBucketsCommand, PutObjectCommand } from "@aws-sdk/client-s3";
import { readFileSync } from "fs";

const client = new S3Client({
  endpoint: "https://cloud.codrsync.dev",
  region: "us-east-1",
  credentials: {
    accessKeyId: "sua-access-key-codrsync",
    secretAccessKey: "sua-secret-key-codrsync",
  },
});

// Listar buckets
const { Buckets } = await client.send(new ListBucketsCommand({}));
console.log(Buckets);

// Upload
await client.send(new PutObjectCommand({
  Bucket: "meu-bucket",
  Key: "arquivo.txt",
  Body: readFileSync("./arquivo.txt"),
}));
```

---

## Referência CLI

### Comandos de Armazenamento

```bash
codrsync storage init                          # Inicializar armazenamento cloud
codrsync storage put <local> <remoto>          # Upload de arquivo
codrsync storage get <remoto> <local>          # Download de arquivo
codrsync storage ls [bucket]                   # Listar arquivos/buckets
codrsync storage rm <remoto>                   # Remover arquivo
codrsync storage config                        # Mostrar configuração de armazenamento
```

### Gerenciamento de Buckets

```bash
codrsync storage bucket create <nome> [--backend storj|filecoin]
codrsync storage bucket list
codrsync storage bucket delete <nome>
```

### Gerenciamento de Chaves API

```bash
codrsync storage keys create --name <nome>
codrsync storage keys list
codrsync storage keys revoke <key-id>
```

---

## Backend Storj

Storj é o backend **recomendado** para a maioria dos casos de uso. Usa erasure coding em uma rede globalmente distribuída de nós de armazenamento.

**Por que Storj:**
- Melhor relação custo-benefício ($7/TB armazenamento, $12/TB egress)
- 99.9999999% durabilidade (11 noves)
- Dados divididos e distribuídos em mais de 80 países
- Sem ponto único de falha
- Compatível com S3 sem configuração

**Comparação de custo anual (10 TB):**

| Provedor | Custo Anual |
|----------|-------------|
| **cloudrsync (Storj)** | **$840** |
| AWS S3 | $3.730 |
| Google Cloud Storage | $3.714 |
| Azure Blob | $3.294 |

---

## Backend Filecoin

Filecoin oferece armazenamento **criptograficamente verificável**. Cada dado armazenado no Filecoin é respaldado por provas matemáticas.

**Por que Filecoin:**

- **Proof of Replication (PoRep)** — Prova criptográfica de que seus dados são armazenados de forma única
- **Proof of Spacetime (PoST)** — Verificação contínua de que os dados persistem ao longo do tempo
- **Resistência à censura** — Nenhuma entidade única pode remover seus dados
- **Imutabilidade** — Endereçado por conteúdo via CID (Content Identifier)
- **Independência de vendor** — Protocolo aberto, não controlado por nenhuma empresa

**Melhor para:**
- Compliance regulatória que exige prova de armazenamento
- Arquivamento de longo prazo com integridade verificável
- Dados que precisam ser resistentes à censura
- Organizações que requerem independência de vendor

**Requisitos:** Plano Pro ou Pro+.

---

## Preços

Os custos de armazenamento cloudrsync estão incluídos nos limites do seu plano. Nenhum crédito é consumido.

| | Grátis | Pro ($29/mês) | Pro+ ($49/mês) |
|---|---|---|---|
| Armazenamento | 1 GB | 50 GB | 200 GB |
| Egress/mês | 5 GB | 100 GB | 500 GB |
| Backend Storj | Sim | Sim | Sim |
| Backend Filecoin | — | Sim | Sim |

Precisa de mais armazenamento? [Entre em contato para preços Teams/Enterprise.](https://codrsync.dev/pricing)

---

## Veja Também

- [Guia do Dashboard](../guides/dashboard.md) — Gerencie buckets e chaves pelo navegador
- [Preços & Planos](../guides/pricing.md) — Comparação completa de planos
- [Comandos CLI](../cli/commands.md) — Referência completa do CLI
