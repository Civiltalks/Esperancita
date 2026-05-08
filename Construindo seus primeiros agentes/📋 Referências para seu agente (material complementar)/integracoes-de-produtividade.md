---
name: integracoes-de-produtividade
status: ATIVO
category: cheatsheet
referenced_by: [A12]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet de referência pra integrar qualquer ferramenta de produtividade no agente — Notion, GitHub, Calendar, Gmail, Drive, Stripe, Linear. Cobre 4 padrões de auth + 6 prompts prontos pra colar.
---

# Integrações de produtividade — referência rápida (A12)

## Os 4 padrões de auth

| # | Padrão | Como funciona | Exemplos |
|---|--------|---------------|----------|
| 1 | **Token simples** (API key) | Gera no painel · cola no `.env` · agente usa via Bearer | Notion · GitHub · Linear · Stripe · Buffer · Anthropic · Brave |
| 2 | **OAuth flow** | Fluxo de browser · agente recebe access_token | Slack · Twitter/X · Spotify · Hubspot · Salesforce |
| 3 | **CLI dedicada** | Instala CLI · autentica via browser · agente roda comandos | **Google: `gog`** · AWS: `aws` · Heroku: `heroku` |
| 4 | **IMAP/SMTP + skill** | Protocolo padrão · skill custom abstrai | Gmail · Outlook · Yahoo · email custom |

Princípio: *"Você decora 4 padrões. Não decora 50 APIs."*

## Tabela canônica — integrações comuns

### Padrão 1 — Token simples

| Ferramenta | Onde criar token | Scope mínimo | Doc oficial |
|------------|------------------|--------------|-------------|
| **Notion** | [notion.so/my-integrations](https://www.notion.so/my-integrations) | Read-only se só lê · Read+Write se cria/atualiza | [developers.notion.com](https://developers.notion.com/) |
| **GitHub** (PAT) | [github.com/settings/tokens](https://github.com/settings/tokens) | `repo:read` se só lê · `repo` se commit | [docs.github.com/rest](https://docs.github.com/en/rest) |
| **Linear** | [linear.app/settings/api](https://linear.app/settings/api) | Read-only se só consulta | [developers.linear.app](https://developers.linear.app/) |
| **Stripe** | [dashboard.stripe.com/apikeys](https://dashboard.stripe.com/apikeys) | Restricted Key (read MRR ≠ write charges) | [stripe.com/docs/api](https://stripe.com/docs/api) |
| **Buffer** | [publish.buffer.com/account/apps](https://publish.buffer.com/account/apps) | Token com escopo de canais específicos | [buffer.com/developers/api](https://buffer.com/developers/api) |
| **Brave Search** | [api.search.brave.com](https://api.search.brave.com/) | Free tier suficiente | [api.search.brave.com](https://api.search.brave.com/) |

### Padrão 3 — Google Workspace via gog CLI

```bash
# gog já vem instalado no OpenClaw 2026.4+. Setup:
gog auth credentials /path/to/client_secret.json
gog auth add seu@email.com --services gmail,calendar,drive,contacts,docs,sheets

# Uso típico:
gog calendar events <calendar-id> --from 2026-01-01 --to 2026-01-07
gog gmail search 'newer_than:7d'
gog gmail send --to "x@y.com" --subject "X" --body-file -
gog drive search "minha pasta"
gog sheets get <sheet-id>!A1:Z100
```

| Serviço Google | Comando gog |
|----------------|-------------|
| Gmail | `gog gmail search/send/reply/draft` |
| Calendar | `gog calendar events/create/update` |
| Drive | `gog drive search/get/upload` |
| Docs | `gog docs cat/export` |
| Sheets | `gog sheets get/update/append/clear` |

**Por que gog em vez de gcloud:** cobre Google Workspace inteiro num CLI unificado · sem precisar criar projeto manualmente no Google Cloud Console · skills oficiais OpenClaw já usam gog.

## 6 prompts prontos pra colar

### 1. Conectar Notion via API token

```
Quero conectar meu Notion. Vai na doc oficial em
https://docs.openclaw.ai/cli/secrets e em
https://developers.notion.com/, lê como conectar via API com
Bearer token, me explica:

1. Onde criar o token (notion.so/my-integrations)
2. Qual scope mínimo eu preciso
3. Como adicionar token no .env (qual nome canônico)
4. Como compartilhar pages/databases com a integração
5. Como testar que tá funcionando

Me pede a credencial quando estiver pronto, valida lendo uma
page de teste, me avisa quando estiver tudo certo.

Princípios A10: scope mínimo · token no cofre · rotação periódica.
```

### 2. Conectar GitHub via PAT

```
Quero conectar meu GitHub. Vai na doc oficial em
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens,
me explica:

1. Onde criar o PAT (fine-grained ou classic? me explica diferença)
2. Qual scope mínimo eu preciso pro meu caso de uso
3. Como adicionar token no .env como GITHUB_TOKEN
4. Quanto tempo o token dura e como rotacionar

Me pede a credencial, valida listando meus repos, me avisa quando
estiver pronto.
```

### 3. Conectar Google Workspace via gog CLI

```
Quero conectar Gmail + Calendar + Drive do meu Google Workspace
no agente. O caminho oficial é gog CLI.

Vai na doc oficial em https://github.com/steipete/gogcli, lê o setup,
me explica:

1. Se gog já tá instalado nesse OpenClaw
2. Como criar projeto no Google Cloud Console e baixar
   client_secret.json
3. Como autenticar via gog auth
4. Como testar (lista próximos 3 eventos)

Me pede o que precisar, conduz o fluxo OAuth, valida que tudo
funciona, me avisa quando estiver pronto.
```

### 4. Conectar Stripe via API key (modo seguro)

```
Quero conectar minha conta Stripe — só pra LER MRR, listar
customers, ler invoices. Sem write nessa primeira fase.

Vai na doc oficial, lê como conectar via Restricted Key, me explica:

1. Por que Restricted Key e não Secret Key
2. Como criar Restricted Key com permissões mínimas:
   - balance: read · customers: read · invoices: read
   - charges: read · subscriptions: read
3. Como adicionar token no .env
4. Como testar lendo meu balance atual

Aviso: NÃO me peça pra criar Secret Key full. Quero scope mínimo
desde o dia 1.
```

## 3 informações que o agente sempre vai pedir

| Informação | Exemplo prático |
|------------|-----------------|
| **Tipo de credencial** | Notion → Bearer token · Calendar → gog auth |
| **Scope** | Stripe → Restricted Key com `balance:read + customers:read` |
| **Onde guardar** | `.env` no Managed · futuro: 1Password |

## Princípios de segurança aplicados (recap A10)

1. **Scope de estagiário** — read-only quando der
2. **Token no cofre** — hábito do dia 1
3. **Rotação periódica** — cron mensal
4. **Banco produção: nunca direto** — agente sempre via API
5. **Defesa anti-prompt-injection** em toda leitura externa
6. **Monitoramento inicial** — primeiros 30 dias

## Troubleshooting comum

| Sintoma | Causa | Ação |
|---------|-------|------|
| `401 Unauthorized` | Token expirou | Gera novo + atualiza `.env` + `openclaw secrets reload` |
| `403 Forbidden` (Notion) | Page não compartilhado com integração | Compartilha page com integração explicitamente |
| `rate limit exceeded` | Cron muito frequente | Aumenta intervalo + retry com backoff |
| `gog: command not found` | gog não instalado | Roda via agente: `npm install -g gogcli` |

## Referências

- A12 · A10 (segurança) · A9 (cron de rotação)
- [docs.openclaw.ai/cli/secrets](https://docs.openclaw.ai/cli/secrets)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
