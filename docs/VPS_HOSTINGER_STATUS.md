# Status VPS Hostinger - Esperancita

Data: 2026-05-08

## Decisao operacional

A Esperancita deve rodar na VPS Hostinger. O Windows nao sera ambiente de
execucao permanente; ele permanece somente como origem dos arquivos, backup e
estacao de bootstrap ate a VPS aceitar SSH.

## VPS alvo

- Hostname: `srv1577551.hstgr.cloud`
- IP: `2.24.30.151`
- Plano: KVM 2
- Sistema: Ubuntu 24.04.4 LTS
- Estado pela API: `running`
- Firewall gerenciado Hostinger: nenhum grupo ativo pela API

## O que foi feito

- Chave SSH dedicada criada em `C:\Users\aliss\.ssh\esperancita_hostinger_ed25519`.
- Chave publica cadastrada na Hostinger e anexada a VPS.
- Reinicio da VPS feito pela API.
- Recovery mode usado com senha temporaria gerada em memoria, sem gravar senha.
- Disco original localizado em recovery como `/mnt/sdb1`.
- Backups criados antes das tentativas de correcao, em:
  `/root/esperancita-recovery-backup-*`.
- Diagnostico de `sshd`, `ufw`, `fail2ban`, `journalctl` e usuarios coletado.

## Achados tecnicos

- `sshd_config` permite apenas `givrs` via `AllowUsers givrs`.
- `ssh.socket` inicia no boot.
- `ufw.service` e `fail2ban.service` iniciam no boot.
- Logs mostram UFW bloqueando tentativas externas, inclusive na porta `2222`.
- A API publica da Hostinger permite recovery, restart, root password, snapshots e
  public keys, mas nao expõe claramente o reset de firewall/SSH do hPanel.

## Bloqueio atual

O acesso SSH publico ainda nao esta funcional. Portanto, OpenClaw ainda nao foi
instalado nem migrado para a VPS.

Atualizacao em 2026-05-08, fase 2:

- A porta `22` voltou a responder externamente.
- O problema atual nao e firewall externo; o bloqueio atual e autenticacao SSH.
- Login externo por chave para `root` e `givrs` ainda falha com
  `Permission denied (publickey,password)`.
- Validacao externa feita por chave, sem senha:
  - `Test-NetConnection 2.24.30.151 -Port 22`: `TcpTestSucceeded=True`;
  - `ssh -i ... root@2.24.30.151`: `Permission denied`;
  - `ssh -i ... givrs@2.24.30.151`: `Permission denied`.
- O usuario `givrs` foi criado/preservado no sistema normal.
- Em recovery, a chave publica correta foi instalada e validada em:
  - `/root/.ssh/authorized_keys`;
  - `/home/givrs/.ssh/authorized_keys`.
- Em recovery, `sshd -T` confirmou:
  - `permitrootlogin yes`;
  - `pubkeyauthentication yes`;
  - `passwordauthentication yes`;
  - `authorizedkeysfile .ssh/authorized_keys`;
  - `allowusers root`;
  - `allowusers givrs`.
- Mesmo assim, apos sair do recovery e voltar ao boot normal, os arquivos
  escritos via disco montado foram revertidos:
  - `/root/.ssh/authorized_keys` voltou com tamanho `0`;
  - `/home/givrs/.ssh/authorized_keys` nao existia;
  - `sshd_config` voltou a conter `AllowUsers givrs`;
  - drop-ins e scripts de correcao criados em recovery nao existiam mais.
- Um teste de persistencia com marcadores em `/root`, `/etc` e
  `/usr/local/sbin` confirmou que alteracoes feitas no disco montado pelo
  recovery nao persistiram ao boot normal.

Conclusao operacional: repetir a correcao pelo recovery nao e confiavel neste
momento. A correcao precisa ser aplicada no sistema normal em execucao, pelo
Terminal interno da Hostinger, ou por uma funcao do painel/API que injete a
chave diretamente no sistema normal.

## Acao necessaria agora

No Terminal interno da Hostinger da VPS `srv1577551.hstgr.cloud`, conectado ao
sistema normal como `root`, executar o procedimento documentado em:

- `docs/HOSTINGER_SSH_LIVE_FIX.md`

Esse procedimento:

1. cria backup de `/etc/ssh`, `/root/.ssh` e `/home/givrs/.ssh`;
2. garante que `givrs` existe;
3. adiciona a chave publica correta a `root` e `givrs`;
4. corrige permissoes de `.ssh` e `authorized_keys`;
5. ajusta `sshd_config`/drop-ins para `Port 22`, chave publica e acesso
   temporario por senha;
6. valida com `sshd -t`;
7. reinicia o servico SSH;
8. confirma que a porta `22` esta escutando.

## Teste depois do reset

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519 givrs@2.24.30.151 "hostname && whoami && lsb_release -ds"
```

Fallback:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519 root@2.24.30.151 "hostname && whoami && lsb_release -ds"
```

## Proxima etapa apos SSH

1. Criar backup do estado atual da VPS.
2. Instalar OpenClaw bare metal com o instalador oficial.
3. Rodar onboarding com daemon.
4. Configurar OAuth OpenAI para conversa.
5. Configurar Telegram na VPS.
6. Copiar workspace/memoria/skills da Esperancita.
7. Validar Telegram respondendo pela VPS.
8. Parar gateway local no Windows para evitar polling duplicado.
