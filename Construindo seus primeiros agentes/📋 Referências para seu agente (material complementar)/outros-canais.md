---
name: outros-canais
status: ATIVO
category: cheatsheet
referenced_by: [A3, A11]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet de referência pra conectar qualquer canal nativo do OpenClaw (24 canais com URL canônica + Voice Call e WebChat como plugins separados).
---

# Outros canais — referência rápida (24 canais nativos)

## Como usar este cheatsheet

**Caminho default — meta-prompt natural:**

```
Conecta meu agente no [Slack / Discord / iMessage / Signal / Teams / outro].

Lê a doc oficial em https://docs.openclaw.ai/channels, segue o
passo-a-passo do canal escolhido, me pede o que precisar (token,
OAuth, QR, allowlist), valida que tá funcionando, e me avisa
quando tiver tudo pronto.
```

**Caminho de plano B — comando CLI direto** (se agente travar).

## Tabela canônica — 24 canais

### Trabalho async (PME comum)

| Canal | Setup CLI | Auth | Doc |
|-------|-----------|------|-----|
| **Slack** | `openclaw channels add --channel slack --token <bot-token>` | Bot OAuth | [docs.openclaw.ai/channels/slack](https://docs.openclaw.ai/channels/slack) |
| **Discord** | `openclaw channels add --channel discord --token <bot-token>` | Bot Token | [docs.openclaw.ai/channels/discord](https://docs.openclaw.ai/channels/discord) |
| **Microsoft Teams** | `openclaw channels add --channel msteams --token <bot-token>` | Bot Framework | [docs.openclaw.ai/channels/msteams](https://docs.openclaw.ai/channels/msteams) |
| **Mattermost** | `openclaw channels add --channel mattermost --token <bot-token>` | Bot API + WebSocket | [docs.openclaw.ai/channels/mattermost](https://docs.openclaw.ai/channels/mattermost) |

### Mensagem direta (pessoal/privacidade)

| Canal | Setup CLI | Auth | Doc |
|-------|-----------|------|-----|
| **Telegram** ⭐ | `openclaw channels add --channel telegram --token <bot-token>` | Bot Token (BotFather) | [docs.openclaw.ai/channels/telegram](https://docs.openclaw.ai/channels/telegram) |
| **WhatsApp** ⚠️ | `openclaw channels login --channel whatsapp --account dedicado` | QR pairing (Baileys) | [docs.openclaw.ai/channels/whatsapp](https://docs.openclaw.ai/channels/whatsapp) |
| **iMessage** ⚠️ | `openclaw channels add --channel imessage` | imsg CLI (deprecated) | [docs.openclaw.ai/channels/imessage](https://docs.openclaw.ai/channels/imessage) |
| **BlueBubbles** | `openclaw channels add --channel bluebubbles --token <api-token>` | REST API | [docs.openclaw.ai/channels/bluebubbles](https://docs.openclaw.ai/channels/bluebubbles) |
| **Signal** | `openclaw channels add --channel signal` | signal-cli (privacy-focused) | [docs.openclaw.ai/channels/signal](https://docs.openclaw.ai/channels/signal) |
| **LINE** | `openclaw channels login --channel line` | Bot API | [docs.openclaw.ai/channels/line](https://docs.openclaw.ai/channels/line) |

⭐ = canal padrão do curso (default da A1 Bloco 5 + A3)
⚠️ = ressalvas A3/A10 — banimento, manipulação social, deprecated

### Comunidade aberta / federado

| Canal | Setup CLI | Auth |
|-------|-----------|------|
| **Matrix** | `openclaw channels login --channel matrix` | Protocol login (federado) |
| **IRC** | `openclaw channels add --channel irc` | Allowlist |
| **Google Chat** | `openclaw channels login --channel googlechat` | HTTP webhook |
| **Twitch** | `openclaw channels add --channel twitch --token <oauth-token>` | IRC chat (apenas grupo) |
| **Nostr** | `openclaw channels add --channel nostr --token <nip04-key>` | NIP-04 (descentralizado) |
| **Tlon (Urbit)** | `openclaw channels add --channel tlon --token <ship-id>` | Urbit |

### Self-hosted (infra própria)

| Canal | Setup CLI |
|-------|-----------|
| **Nextcloud Talk** | `openclaw channels add --channel nextcloud-talk --token <token>` |
| **Synology Chat** | `openclaw channels add --channel synology-chat --token <webhook>` |

### Mercado Ásia

| Canal | Setup CLI |
|-------|-----------|
| **Feishu** | `openclaw channels add --channel feishu --token <bot-token>` |
| **WeChat** | `openclaw channels login --channel wechat` |
| **Zalo** | `openclaw channels add --channel zalo --token <bot-token>` |
| **Zalo Personal** | `openclaw channels login --channel zalouser` |
| **QQ Bot** | `openclaw channels add --channel qqbot --token <bot-token>` |
| **Yuanbao** | `openclaw channels login --channel yuanbao` |

## Plugins separados (não usam `channels add`)

| Plugin | Para que serve | Onde achar |
|--------|---------------|------------|
| **Voice Call** | Chamadas de voz via Plivo/Twilio | Bônus R4 (VPS) |
| **WebChat** | UI Gateway web embarcável | [docs.openclaw.ai/cli/channels](https://docs.openclaw.ai/cli/channels) |

## 3 informações que o agente sempre vai pedir

| Informação | Exemplo prático |
|------------|-----------------|
| **Identidade do agente naquele canal** (recap A5) | Slack: "bot dedicado da empresa" |
| **Credencial** (token, OAuth, QR, app password) | OAuth flow do canal |
| **Escopo** (DM só seu? canal específico?) | "Só DM comigo + canal #ai-help" |

## Princípios de segurança aplicados (recap A10)

1. **Conta dedicada do agente** (não conta pessoal)
2. **Prompt blindado** se o canal é público (anti-prompt-injection)
3. **Monitoramento diário** nos primeiros 30 dias
4. **Scope mínimo** no token/OAuth
5. **Revogação rápida** se vazar — `openclaw channels remove --channel <nome>`

## Troubleshooting comum

| Sintoma | Causa | Ação |
|---------|-------|------|
| `getUpdates 409` (Telegram) | Outro gateway/poller usando o mesmo bot | Verifica 2 OpenClaws com mesmo bot · desliga duplicado |
| OAuth expira (Slack/Discord) | Token rotacionado pela plataforma | Reinstala app + atualiza token |
| QR expira (WhatsApp/WeChat) | Pareamento expira em ~1h | Refazer login |
| 2FA bloqueia bot | Conta com 2FA em app que exige | Usar app password ou conta dedicada sem 2FA |
| Bot não posta em canal | Falta admin ou permissão | Adicionar bot como admin |
| Re-add bot necessário (Telegram) | Mudou privacy mode no @BotFather | Remove + Re-add no grupo |

## Quando NÃO usar o plano B

- **Aluno PME que não tem confiança em terminal**: stay com meta-prompt
- **Canal novo na sua vida**: deixa o agente conduzir
- **Token sensível (Stripe, banco, prod)**: nunca cola no terminal sem revisar 3x

## Referências

- A3 (Telegram aprofundado) · A11 (outros canais)
- Doc OpenClaw channels: [docs.openclaw.ai/cli/channels](https://docs.openclaw.ai/cli/channels)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
