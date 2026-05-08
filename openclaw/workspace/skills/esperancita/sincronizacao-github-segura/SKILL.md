---
name: sincronizacao-github-segura
status: ATIVO
category: esperancita
owner: aluno
version: 1.0
mode: guarded
estimated_time: 2-10min
model_compatible: [gpt-5, gpt-5.5]
description: Use quando houver mudancas versionaveis no workspace/repositorio da Esperancita. Faz status, diff, scan de segredos, commit Conventional Commit e push sem salvar token no remote.
---

# Sincronizacao GitHub Segura

## Promessa

Versionar mudancas da Esperancita sem vazar segredos e sem destruir historico.

## Antes de commit

Rodar:

```powershell
git status --short --branch
git diff --stat
git grep -n -I -E "github_pat_|ghp_|gho_|ghu_|ghs_|ghr_|sk-(proj-)?|TELEGRAM_BOT_TOKEN|HAPI_API_TOKEN|OPENAI_API_KEY" HEAD -- .
```

Se houver staged files:

```powershell
git grep --cached -n -I -E "github_pat_|ghp_|gho_|ghu_|ghs_|ghr_|sk-(proj-)?|TELEGRAM_BOT_TOKEN|HAPI_API_TOKEN|OPENAI_API_KEY"
```

## Regras

- Nunca usar token no remote URL.
- Nunca versionar `_BACKUP_INSTALACAO_OPENCLAW`.
- Nunca versionar `.env`, sessoes, logs ou `openclaw.json` real.
- Nunca usar force push.
- Se scan encontrar segredo real, abortar.

## Commit

Usar Conventional Commits:

- `docs: update Esperancita architecture`
- `feat: add Esperancita memory governance`
- `fix: harden OpenClaw configuration`

## Depois do push

Validar:

```powershell
git status --short --branch
git log --oneline -3
git ls-remote origin HEAD refs/heads/main
```
