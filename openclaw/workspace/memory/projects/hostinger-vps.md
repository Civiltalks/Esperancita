# Projeto - Hostinger/VPS

## Objetivo

Rodar OpenClaw/Esperancita 24/7 em VPS Ubuntu 24.04, sem depender do Windows local.

## VPS detectadas

| Hostname | IP | Status | Observacao |
|---|---|---|---|
| `srv1546212.hstgr.cloud` | `187.77.227.242` | running | SSH 22 nao respondeu no teste local |
| `srv1577551.hstgr.cloud` | `2.24.30.151` | running | SSH 22 respondeu |

## VPS recomendada

`srv1577551.hstgr.cloud` (`2.24.30.151`)

## Pendencia bloqueante

Autorizar chave SSH ou fornecer acesso seguro. A API Hostinger nao entrega senha root.

## Plano de deploy

1. Acessar VPS por SSH.
2. Atualizar pacotes Ubuntu.
3. Instalar OpenClaw via instalador oficial.
4. Rodar `openclaw onboard --install-daemon`.
5. Configurar OAuth OpenAI.
6. Configurar `TELEGRAM_BOT_TOKEN`.
7. Configurar `OPENAI_API_KEY` somente para Whisper.
8. Configurar timezone `America/Sao_Paulo`.
9. Restaurar/copiar workspace da Esperancita.
10. Validar gateway, Telegram e modelo.
11. Parar gateway local para evitar conflito de polling.

## Criterios de sucesso

- `openclaw gateway status` na VPS mostra running.
- Telegram responde pela VPS.
- Modelo principal e `openai-codex/gpt-5.5`.
- Workspace e memoria estao presentes.
- Logs sem erro de polling duplicado.
