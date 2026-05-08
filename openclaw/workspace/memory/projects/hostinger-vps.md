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

## Status em 2026-05-08

A execucao deve ficar na VPS, nao no Windows. O Windows esta sendo usado apenas
como estacao de bootstrap e backup ate o acesso SSH da VPS estar funcional.

### Acoes realizadas

- Chave SSH dedicada criada localmente:
  `C:\Users\aliss\.ssh\esperancita_hostinger_ed25519`.
- Chave operacional atual substituida para:
  `C:\Users\aliss\.ssh\esperancita_hostinger_ed25519_nova`.
- A chave antiga com passphrase nao deve mais ser usada para o deploy.
- Chave publica registrada na Hostinger e anexada a VPS `1577551`.
- API Hostinger validada por variavel de ambiente local, sem gravar token em arquivo.
- VPS `1577551` reiniciada pela API.
- Recovery mode usado para diagnosticar e tentar recuperar acesso SSH.
- Backups criados no disco da VPS antes de alteracoes, em caminhos do tipo:
  `/root/esperancita-recovery-backup-YYYYMMDDTHHMMSSZ`.

### Diagnostico encontrado

- VPS atual: `srv1577551.hstgr.cloud` / `2.24.30.151`.
- Ubuntu: 24.04.4 LTS.
- Existe usuario SSH permitido `givrs`; `sshd_config` tem `AllowUsers givrs`.
- O servidor usa `ssh.socket` no boot.
- `ufw` e `fail2ban` estao ativos no boot.
- Logs mostram bloqueio de conexoes pela UFW, incluindo tentativas na porta `2222`.
- A Hostinger possui opcoes de painel para `Reset firewall` e `Reset SSH`; essas
  opcoes nao aparecem como endpoint publico na API consultada.

### Status final do deploy VPS

OpenClaw/Esperancita esta rodando na VPS `srv1577551.hstgr.cloud`
(`2.24.30.151`) como `givrs`.

Evidencias:

- SSH por chave nova OK para `givrs` e `root`.
- Backup pre-deploy:
  `/root/esperancita-predeploy-backup-2026-05-08_231218`.
- Backup extra do stack Docker/GIVRS:
  `/root/esperancita-predeploy-backup-extra-givrs-2026-05-08_231330`.
- Node.js `v22.22.2`, npm `10.9.7`, OpenClaw `2026.5.7`.
- Runtime: `/home/givrs/.openclaw`.
- Workspace: `/home/givrs/.openclaw/workspace`.
- Repo clonado: `/home/givrs/Esperancita`.
- Servico systemd: `openclaw-esperancita.service`.
- Servico `active` e `enabled`.
- Reboot validado: SSH voltou e o servico subiu automaticamente.
- Modelo: `openai-codex/gpt-5.5`.
- OAuth OpenAI/Codex OK, sem fallback.
- Telegram `@esperancitamy_bot` OK via env privado.
- Teste de agente apos reboot: `VPS_REBOOT_OK`.

Pendencias:

- WhatsApp/Evolution nao configurado; stack Docker existente `givrs-*`
  preservado sem alteracao.
- Google Calendar/Gmail pendente de credenciais seguras.
- Push GitHub direto da VPS pendente de credencial segura.

Documento operacional: `docs/VPS_OPENCLAW_DEPLOY_FINAL.md`.

### Historico do bloqueio superado

SSH publico por chave foi corrigido para `root` e `givrs` usando a chave nova:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova givrs@2.24.30.151
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova root@2.24.30.151
```

Historico do diagnostico anterior:

- A chave publica correta foi gravada e validada via recovery em `root` e
  `givrs`.
- `sshd -T` no disco montado confirmou `PermitRootLogin yes`,
  `PubkeyAuthentication yes`, `PasswordAuthentication yes`,
  `AuthorizedKeysFile .ssh/authorized_keys` e `AllowUsers root/givrs`.
- Depois de sair do recovery e voltar ao boot normal, os arquivos gravados via
  recovery foram revertidos: `authorized_keys` do root voltou vazio,
  `authorized_keys` de `givrs` sumiu e o `sshd_config` voltou a restringir para
  `AllowUsers givrs`.
- Testes com marcadores em `/root`, `/etc` e `/usr/local/sbin` confirmaram que
  alteracoes feitas pelo recovery offline nao persistem de forma confiavel no
  boot normal.

Proxima acao correta: operar como `givrs`, usar `root` somente para tarefas
administrativas, criar backup logico e iniciar o deploy real do
OpenClaw/Esperancita na VPS.

Teste de acesso padrao:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova givrs@2.24.30.151 "hostname && whoami"
```

Teste administrativo:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova root@2.24.30.151 "hostname && whoami"
```

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
