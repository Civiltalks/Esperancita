# Politica de seguranca

## Segredos

Nunca gravar valores reais de:

- GitHub PAT;
- Telegram bot token;
- Hostinger API token;
- OpenAI API key;
- OAuth tokens;
- senhas;
- chaves SSH privadas;
- cookies ou sessoes.

## Git

Antes de commit:

```powershell
git status --short
git diff --cached --name-only
git grep --cached -n -I -E "github_pat_|ghp_|gho_|ghu_|ghs_|ghr_|sk-(proj-)?|TELEGRAM_BOT_TOKEN|HAPI_API_TOKEN|OPENAI_API_KEY"
```

Se encontrar segredo real, abortar commit.

## Backups

Antes de alterar configuracao, memoria, agente ou workspace:

- criar backup em `_BACKUP_INSTALACAO_OPENCLAW`;
- registrar no `INDICE_BACKUP.md`;
- nao copiar segredo para relatorio.

## Exposicao de rede

- Local: manter gateway em `loopback` por padrao.
- VPS: usar servico systemd, firewall e allowlist.
- Publico: nao expor dashboard/gateway sem autenticao e decisao humana.
