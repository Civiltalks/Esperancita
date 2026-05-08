# Deploy VPS OpenClaw/Esperancita

Data: 2026-05-08

## Resumo

OpenClaw/Esperancita esta rodando na VPS Hostinger `srv1577551.hstgr.cloud`
(`2.24.30.151`) como usuario `givrs`, com servico systemd persistente,
workspace migrado, OAuth OpenAI/Codex validado e Telegram configurado por
variavel de ambiente privada.

## Acesso SSH

Usar somente a chave nova:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova givrs@2.24.30.151
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova root@2.24.30.151
```

A chave antiga `esperancita_hostinger_ed25519` nao deve mais ser usada.

## Backups criados na VPS

- `/root/esperancita-predeploy-backup-2026-05-08_231218`
- `/root/esperancita-predeploy-backup-extra-givrs-2026-05-08_231330`

Esses backups preservam configuracoes SSH, estado OpenClaw se existisse,
estrutura Docker existente e manifestos de auditoria. Ficam em `/root` com
acesso administrativo.

## Estado preservado

- Nenhum agente `claudio` ou `david` foi encontrado na VPS antes do deploy.
- Nenhum estado remoto OpenClaw preexistente foi apagado.
- Stack Docker existente foi preservado e nao foi parado:
  - `givrs-api`
  - `givrs-postgres`
  - `givrs-redis`
- Portas existentes `5000`, `5432` e `6379` foram deixadas intactas.
- Gateway local do Windows foi parado para evitar polling duplicado do Telegram.

## Dependencias

- Ubuntu 24.04.4 LTS.
- Git ja presente.
- Python 3.12 ja presente.
- Docker ja presente e em uso pelo stack `givrs`.
- Node.js instalado via NodeSource: `v22.22.2`.
- npm: `10.9.7`.
- OpenClaw CLI: `2026.5.7`.

## Configuracao OpenClaw

- Runtime: `/home/givrs/.openclaw`
- Workspace ativo: `/home/givrs/.openclaw/workspace`
- Repositorio GitHub clonado: `/home/givrs/Esperancita`
- Config privada: `/home/givrs/.openclaw/openclaw.json`
- Ambiente privado: `/home/givrs/.openclaw/openclaw.env`
- Permissao do env: `600`, dono `givrs:givrs`
- Timezone: `America/Sao_Paulo`

O arquivo `openclaw.env` contem segredos operacionais e nao deve ser versionado.

## Modelo e OpenAI

- Modelo principal: `openai-codex/gpt-5.5`
- Autenticacao de conversa: OAuth OpenAI/Codex por auth-profile.
- Fallback de API para conversa: desabilitado pela configuracao de modelos
  permitidos.
- `OPENAI_API_KEY` fica disponivel somente no ambiente privado para Whisper,
  transcricoes e recursos que exigem API direta.

## Telegram

- Bot: `@esperancitamy_bot`
- Credencial: variavel de ambiente privada.
- Modo: `polling`
- Probe: OK
- Envio direto pela VPS: OK

## Servico 24/7

Unit:

```bash
/etc/systemd/system/openclaw-esperancita.service
```

Status:

```bash
systemctl status openclaw-esperancita.service --no-pager
systemctl is-active openclaw-esperancita.service
systemctl is-enabled openclaw-esperancita.service
```

Comandos:

```bash
sudo systemctl start openclaw-esperancita.service
sudo systemctl stop openclaw-esperancita.service
sudo systemctl restart openclaw-esperancita.service
sudo journalctl -u openclaw-esperancita.service -f
```

O gateway escuta apenas localmente:

```text
127.0.0.1:18789
[::1]:18789
```

## Validacoes realizadas

- SSH por chave para `givrs`: OK.
- SSH por chave para `root`: OK.
- Backup pre-deploy: OK.
- Node/npm/OpenClaw: OK.
- Onboarding OpenClaw sem reset: OK.
- Migração de workspace/memoria/sessoes/skills/OAuth: OK.
- Config `openai-codex/gpt-5.5`: OK.
- Telegram por env: OK.
- Systemd ativo: OK.
- Reboot da VPS: OK.
- Servico subiu automaticamente apos reboot: OK.
- Teste de agente apos reboot: resposta `VPS_REBOOT_OK`.

## Comandos de verificacao

Como `givrs`:

```bash
set -a
. /home/givrs/.openclaw/openclaw.env
set +a

openclaw health
openclaw models status
openclaw channels status --probe
openclaw agent --local --agent main -m "Responda exatamente: OK_OPENCLAW" --json --timeout 300
```

Como `root`:

```bash
systemctl status openclaw-esperancita.service --no-pager
ss -tlnp | grep ':18789'
journalctl -u openclaw-esperancita.service -n 120 --no-pager
```

## GitHub

Repositorio oficial:

```text
https://github.com/Civiltalks/Esperancita.git
```

Clone na VPS:

```bash
/home/givrs/Esperancita
```

Nenhum token GitHub foi gravado na VPS durante esta etapa. O clone esta pronto
para leitura/sincronizacao segura. Para push direto da VPS, configurar uma
credencial propria depois, sem salvar PAT em arquivos versionados.

## Pendencias

- WhatsApp/Evolution: nao configurado nesta etapa; o stack Docker existente
  `givrs-*` foi preservado e nao foi alterado.
- Google Calendar/Gmail: pendente de credenciais seguras.
- Push GitHub a partir da VPS: pendente de decisao sobre credencial segura.
- Hardening futuro: trocar `PermitRootLogin yes` para chave somente ou
  restringir root depois de validar toda a operacao 24/7 por alguns ciclos.

## Recuperacao

Para restaurar estado OpenClaw, parar o servico antes:

```bash
sudo systemctl stop openclaw-esperancita.service
```

Nunca apagar o estado atual diretamente. Renomear primeiro:

```bash
sudo mv /home/givrs/.openclaw /home/givrs/.openclaw_antes_restore_$(date +%F_%H%M%S)
```

Restaurar a partir de backup validado e corrigir dono:

```bash
sudo chown -R givrs:givrs /home/givrs/.openclaw
sudo systemctl start openclaw-esperancita.service
```
