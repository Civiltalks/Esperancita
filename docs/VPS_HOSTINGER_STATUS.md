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

## Acao necessaria no hPanel

No painel da Hostinger da VPS `srv1577551.hstgr.cloud`:

1. Abrir `VPS` > `Manage`.
2. Usar `Reset firewall`.
3. Se SSH ainda falhar, usar `Reset SSH`.
4. Reiniciar a VPS.
5. Avisar para continuar o deploy.

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
