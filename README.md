# Esperancita OpenClaw

Repositorio oficial de versionamento da estrutura OpenClaw da Esperancita.

## Estado atual

- Runtime local: `C:\Users\aliss\.openclaw`
- Workspace versionavel: `openclaw/workspace`
- Agente atual: `main` / Esperancita
- Modelo de conversa: `openai-codex/gpt-5.5` via OAuth ChatGPT/OpenAI Codex
- API OpenAI: reservada para Whisper/transcricoes e recursos que exigem API direta
- Canal: Telegram via `TELEGRAM_BOT_TOKEN`
- Hostinger API: `HAPI_API_TOKEN` validado, sem deploy automatico ainda

## Politica de seguranca

Nunca commitar:

- tokens, PATs, chaves API, OAuth, secrets ou `.env`
- `openclaw.json` real
- `auth-profiles.json`
- sessoes privadas, logs, arquivos `.jsonl`
- backups locais em `_BACKUP_INSTALACAO_OPENCLAW`

Veja [docs/SEGURANCA_E_SECRETS.md](docs/SEGURANCA_E_SECRETS.md).

## Verificacoes rapidas

```powershell
openclaw config validate
openclaw models status
openclaw channels status --probe
```

Resultado esperado para conversas:

```text
defaultModel=openai-codex/gpt-5.5
allowed=openai-codex/gpt-5.5
provider=openai-codex
fallbackUsed=false
```

