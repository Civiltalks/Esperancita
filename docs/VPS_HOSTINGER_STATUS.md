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
- A chave antiga com passphrase foi substituida operacionalmente pela nova
  chave local sem passphrase:
  `C:\Users\aliss\.ssh\esperancita_hostinger_ed25519_nova`.
- A partir de agora, os acessos SSH devem usar somente a chave nova.
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

## SSH atual

O acesso SSH publico por chave foi corrigido em 2026-05-08. A VPS aceita login
externo por chave para `givrs` e `root` usando a chave nova.

Comandos validos a partir de agora:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova givrs@2.24.30.151
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova root@2.24.30.151
```

OpenClaw foi instalado, configurado e validado na VPS em 2026-05-08.

Status final da etapa:

- Usuario operacional: `givrs`.
- Usuario administrativo: `root`.
- Chave SSH operacional: `C:\Users\aliss\.ssh\esperancita_hostinger_ed25519_nova`.
- Runtime OpenClaw: `/home/givrs/.openclaw`.
- Workspace ativo: `/home/givrs/.openclaw/workspace`.
- Repositorio GitHub clonado para leitura/sincronizacao:
  `/home/givrs/Esperancita`.
- Servico 24/7: `openclaw-esperancita.service`.
- Porta do gateway: `127.0.0.1:18789` e `[::1]:18789`.
- Modelo principal: `openai-codex/gpt-5.5`.
- Autenticacao principal: OAuth OpenAI/Codex por auth-profile.
- API OpenAI: disponivel via ambiente privado apenas para Whisper/transcricao
  e recursos que exigem API direta.
- Telegram: configurado por variavel de ambiente privada, modo `polling`,
  probe OK para `@esperancitamy_bot`.
- Timezone da VPS: `America/Sao_Paulo`.

Validacoes concluidas:

- SSH voltou apos reboot com a chave nova.
- `systemctl is-active openclaw-esperancita.service`: `active`.
- `systemctl is-enabled openclaw-esperancita.service`: `enabled`.
- `openclaw health`: OK.
- `openclaw models status`: `openai-codex/gpt-5.5`, OAuth OK, sem fallback.
- Teste de agente local na VPS: resposta `VPS_REBOOT_OK`.
- Envio direto Telegram pela VPS: `ok=true`.

Observacoes:

- O comando nativo `openclaw gateway status` informa `systemd user (disabled)`
  porque o deploy usa uma unit systemd de sistema customizada, nao a unit de
  usuario criada pelo instalador do OpenClaw. O status real deve ser verificado
  com `systemctl status openclaw-esperancita.service`.
- A identidade de dispositivo importada do Windows gerava pendencia de pairing.
  Ela foi preservada por renome em
  `/home/givrs/.openclaw/imported-device-state-*`, e a VPS gerou identidade
  propria.
- Caminhos de sessao herdados do Windows foram corrigidos em `sessions.json`.
  Artefatos com nome Windows foram preservados em
  `/home/givrs/.openclaw/agents/main/sessions/windows-path-artifacts-*`.

## Historico do bloqueio SSH

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

## Acao executada para corrigir SSH

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

## Teste depois da correcao

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova givrs@2.24.30.151 "hostname && whoami && lsb_release -ds"
```

Fallback:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519_nova root@2.24.30.151 "hostname && whoami && lsb_release -ds"
```

## Proxima etapa apos SSH

Concluida. Ver documento operacional:

- `docs/VPS_OPENCLAW_DEPLOY_FINAL.md`

## Atualizacao - memoria permanente Super Esperancita

Data: 2026-05-08

Foi concluida a sincronizacao segura da memoria permanente consolidada da
Super Esperancita para:

```text
/home/givrs/.openclaw/workspace
```

Backup remoto criado antes da alteracao:

```text
/home/givrs/.openclaw/backups/workspace-before-super-esperancita-2026-05-08_205602
```

Arquivos novos no workspace remoto:

- `ESPERANCITA_PERSONALIDADE.md`
- `ESPERANCITA_TOM_DE_VOZ.md`
- `ESPERANCITA_FUNCIONAMENTO.md`
- `ESPERANCITA_CRITERIOS_OPERACIONAIS.md`
- `ESPERANCITA_MEMORIA_PERMANENTE.md`
- `ESPERANCITA_LIMITES_E_SEGURANCA.md`

Validacoes reais executadas na VPS:

- `openclaw health`
- `openclaw models status`
- tres chamadas `openclaw agent --local --agent main ... --json --timeout 300`

Resultado: a agente respondeu como governanta digital/secretaria executiva do
lar, citando reducao de carga mental, seguranca, consentimento, memoria,
dignidade, microacoes e rotina possivel.

Pendencias tecnicas:

- `openclaw health` indicou `degraded` por `event_loop_utilization,cpu`.
- A memoria vetorial emitiu aviso `sqlite-vec unavailable`, com recall vetorial
  degradado. A memoria textual e os testes do agente funcionaram.
