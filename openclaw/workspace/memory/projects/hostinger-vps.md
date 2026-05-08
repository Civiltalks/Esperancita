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

### Pendencia bloqueante

SSH publico esta com a porta `22` aberta, mas a autenticacao ainda falha para
`root` e `givrs` com `Permission denied (publickey,password)`.

Diagnostico novo:

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

Acao correta agora: aplicar a correcao no sistema normal pelo Terminal interno
da Hostinger, como `root`, usando `docs/HOSTINGER_SSH_LIVE_FIX.md`.

Depois disso, testar do Windows:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519 givrs@2.24.30.151 "hostname && whoami"
```

Se `givrs` falhar, testar `root` somente por chave:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519 root@2.24.30.151 "hostname && whoami"
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
