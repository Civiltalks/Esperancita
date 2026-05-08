---
name: preparar-deploy-hostinger
status: ATIVO
category: esperancita
owner: aluno
version: 1.0
mode: guarded
estimated_time: 15-40min apos SSH
model_compatible: [gpt-5, gpt-5.5]
description: Use para preparar ou executar deploy da Esperancita em VPS Hostinger. Nao inventa acesso: exige SSH autorizado. Usa Ubuntu 24.04 bare metal, sem Docker por padrao do curso.
---

# Preparar Deploy Hostinger

## Estado conhecido

- VPS recomendada: `srv1577551.hstgr.cloud`
- IP: `2.24.30.151`
- Sistema: Ubuntu 24.04
- SSH 22 respondeu no teste local
- Pendente: chave SSH autorizada

## Pre-condicao obrigatoria

Nao executar deploy sem SSH funcional.

Validar:

```powershell
ssh root@2.24.30.151 "hostname && lsb_release -a"
```

Se falhar, registrar pendencia e parar.

## Plano de instalacao na VPS

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
openclaw onboard --install-daemon
openclaw config set tools.profile full
openclaw config validate
```

Configurar:

- OAuth OpenAI para conversa.
- `TELEGRAM_BOT_TOKEN` no ambiente da VPS.
- `OPENAI_API_KEY` somente para Whisper/transcricao.
- `HAPI_API_TOKEN` se a VPS precisar usar API Hostinger.
- `OPENCLAW_TZ=America/Sao_Paulo`.

## Cuidados

- Parar gateway local antes de ativar gateway remoto com o mesmo Telegram bot.
- Nao expor dashboard publico sem autenticacao.
- Fazer backup do estado local antes de copiar.
- Validar logs antes de declarar sucesso.

## Criterio de sucesso

- `openclaw gateway status` running na VPS.
- Telegram responde pela VPS.
- `openclaw models status` mostra `openai-codex/gpt-5.5`.
- Logs sem erro de polling duplicado.
