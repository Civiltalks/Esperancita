# TOOLS.md - Ferramentas e ambiente da Esperancita

## Maquina local

- Windows user: `aliss`
- Projeto local: `C:\Users\aliss\OneDrive\Desktop\Open Claw`
- Estado OpenClaw: `C:\Users\aliss\.openclaw`
- Workspace OpenClaw: `C:\Users\aliss\.openclaw\workspace`
- OpenClaw CLI: `OpenClaw 2026.5.7`
- Git: instalado
- Node/npm: instalados
- pnpm: instalado
- Docker: nao instalado no diagnostico inicial

## GitHub

- Repo: `https://github.com/Civiltalks/Esperancita.git`
- Branch principal: `main`
- Remote local: `origin`
- Token GitHub: nunca salvar em arquivo ou remote URL.
- Fluxo: autenticar transitoriamente quando necessario.

## OpenAI

- Conversa principal: OAuth OpenAI/Codex.
- Perfil OAuth conhecido: `openai-codex:civiltalks.ai@gmail.com`
- Modelo principal: `openai-codex/gpt-5.5`
- `OPENAI_API_KEY`: usar apenas para Whisper/transcricao/API direta.

## Telegram

- Canal: `telegram/default`
- Bot: Esperancita
- Owner allowlist: `telegram:8413871765`
- Regra: evitar dois gateways usando o mesmo bot ao mesmo tempo.

## Hostinger

- `HAPI_API_TOKEN`: configurado no ambiente de usuario.
- API validada.
- VPS detectadas:
  - `srv1546212.hstgr.cloud` - `187.77.227.242` - Ubuntu 24.04 - SSH nao respondeu no teste local.
  - `srv1577551.hstgr.cloud` - `2.24.30.151` - Ubuntu 24.04 - SSH respondeu na porta 22.
- VPS recomendada para etapa de deploy: `srv1577551.hstgr.cloud`.
- Pendente: chave SSH autorizada ou acesso seguro.

## Comandos de verificacao

```powershell
openclaw --version
openclaw config validate
openclaw gateway status
openclaw models status
openclaw skills check --agent main
git status --short --branch
```

## Comandos de risco

Nao usar sem decisao humana explicita:

```powershell
git reset --hard
git clean
Remove-Item -Recurse
rmdir /s
del
```
