# Seguranca e Secrets

Este repositorio deve conter documentacao, templates, skills e estrutura segura
do OpenClaw. Estado privado fica fora do Git.

## Secrets existentes no ambiente

Os nomes abaixo podem existir como variaveis de ambiente locais, mas os valores
nao devem ser gravados no repositorio:

- `OPENAI_API_KEY`: somente Whisper/transcricoes e recursos de API direta.
- `TELEGRAM_BOT_TOKEN`: canal Telegram.
- `HAPI_API_TOKEN`: API Hostinger.
- GitHub PAT: usado apenas no processo atual para push/pull seguro.

## Arquivos proibidos no Git

- `.env` e variantes reais
- `openclaw.json`
- `auth-profiles.json`
- `auth-state.json`
- `gateway.cmd`
- `sessions/`
- `*.jsonl`
- logs
- `_BACKUP_INSTALACAO_OPENCLAW/`

## Regra OpenAI da Esperancita

Conversas da Esperancita devem usar:

```text
openai-codex/gpt-5.5
```

O modelo direto por API:

```text
openai/gpt-5.5
```

nao deve ser usado como modelo principal de conversa.

## Antes de push

Rodar:

```powershell
git status --short
git diff --cached --stat
rg -n "github_pat_|ghp_|gho_|ghu_|ghs_|ghr_|sk-proj-|TELEGRAM_BOT_TOKEN=|HAPI_API_TOKEN=|OPENAI_API_KEY=" .
```

Se qualquer segredo real aparecer, interromper o push.

