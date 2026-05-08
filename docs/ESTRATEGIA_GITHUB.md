# Estrategia GitHub

Repositorio remoto:

```text
https://github.com/Civiltalks/Esperancita.git
```

## Estrategia inicial

1. Validar API do GitHub.
2. Confirmar que o repositorio remoto esta vazio.
3. Criar `.gitignore` antes de `git add`.
4. Inicializar branch `main`.
5. Conectar `origin` sem token na URL.
6. Versionar apenas estrutura segura.
7. Usar token GitHub apenas em autenticacao transitoria do Git.

## Branches recomendadas

- `main`: estado estavel e restauravel.
- `backup/YYYY-MM-DD`: snapshots auditaveis quando necessario.
- `feature/<tema>`: mudancas de skills, docs, workflows ou integracoes.
- `fix/<tema>`: correcao pontual.

## Padrao de commits

Usar Conventional Commits:

```text
chore: bootstrap Esperancita OpenClaw repository
docs: update installation report
fix: harden gitignore for OpenClaw secrets
feat: add workflow documentation
```

## Regras de sincronizacao

- Nunca usar `git push --force` sem decisao humana explicita.
- Nunca colocar token no remote URL.
- Nunca versionar sessoes, OAuth, logs, backups ou `openclaw.json` real.
- Fazer backup local antes de mudancas estruturais.

## Status em 2026-05-08

- Git local inicializado em `main`.
- Remoto `origin` conectado em `https://github.com/Civiltalks/Esperancita.git`.
- Repositorio remoto estava vazio, sem branches.
- Commit local inicial criado: `bde0ee8 chore: bootstrap Esperancita OpenClaw repository`.
- Tentativa de `git push -u origin main` retornou `403 Permission denied`.
- O token nao foi salvo em arquivo, commit ou remote URL.
- Proximo passo: ajustar token/permissao GitHub para escrita de conteudo e repetir o push.
