# Correcao SSH ao vivo - Hostinger

Data: 2026-05-08

## Quando usar

Use este procedimento somente no Terminal interno da Hostinger, conectado ao
sistema normal da VPS como `root`.

Nao use este procedimento no Windows. Nao use para repetir o ciclo de recovery
offline, porque as ultimas tentativas feitas no disco montado pelo recovery nao
persistiram apos o boot normal.

## O que este procedimento faz

- Cria backup logico antes de alterar SSH.
- Preserva arquivos existentes de `authorized_keys`.
- Garante o usuario operacional `givrs`.
- Instala a chave publica SSH correta para `root` e `givrs`.
- Corrige permissoes exigidas pelo OpenSSH.
- Garante `Port 22`, `PubkeyAuthentication yes`,
  `AuthorizedKeysFile .ssh/authorized_keys`, `PasswordAuthentication yes` e
  `PermitRootLogin yes` temporariamente para recuperacao.
- Garante que `AllowUsers`, se existir, permita `root` e `givrs`.
- Neutraliza `DenyUsers` somente se estiver bloqueando usuarios.
- Valida com `sshd -t` antes de reiniciar SSH.

## Comando para colar no Terminal interno da Hostinger

```bash
bash <<'EOF'
set -Eeuo pipefail

if [ "$(id -u)" -ne 0 ]; then
  echo "ERRO: execute este procedimento como root no Terminal interno da Hostinger."
  exit 1
fi

PUBKEY='ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIG/ceOk8fykSWDEpGqxIJDsjP/9jKE/haBKEOjbRDtMZ esperancita-openclaw-hostinger-2026-05-08'
TS="$(date +%F_%H%M%S)"
BKP="/root/esperancita-ssh-live-fix-backup-$TS"

mkdir -p "$BKP"
cp -a /etc/ssh "$BKP/etc-ssh" 2>/dev/null || true
cp -a /root/.ssh "$BKP/root-ssh" 2>/dev/null || true
cp -a /home/givrs/.ssh "$BKP/givrs-ssh" 2>/dev/null || true

if ! id givrs >/dev/null 2>&1; then
  useradd -m -s /bin/bash -G sudo givrs
else
  usermod -aG sudo givrs
fi

install -d -m 700 /root/.ssh
install -d -m 700 /home/givrs/.ssh
touch /root/.ssh/authorized_keys /home/givrs/.ssh/authorized_keys

grep -qxF "$PUBKEY" /root/.ssh/authorized_keys || printf '%s\n' "$PUBKEY" >> /root/.ssh/authorized_keys
grep -qxF "$PUBKEY" /home/givrs/.ssh/authorized_keys || printf '%s\n' "$PUBKEY" >> /home/givrs/.ssh/authorized_keys

chown -R root:root /root/.ssh
chmod 700 /root/.ssh
chmod 600 /root/.ssh/authorized_keys

chown -R givrs:givrs /home/givrs/.ssh
chmod go-w /home/givrs 2>/dev/null || true
chmod 700 /home/givrs/.ssh
chmod 600 /home/givrs/.ssh/authorized_keys

mkdir -p /etc/ssh/sshd_config.d
cat > /etc/ssh/sshd_config.d/99-esperancita-auth.conf <<'CONF'
Port 22
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
PasswordAuthentication yes
PermitRootLogin yes
CONF

for f in /etc/ssh/sshd_config /etc/ssh/sshd_config.d/*.conf; do
  [ -f "$f" ] || continue
  sed -i -E 's/^[[:space:]]*AllowUsers[[:space:]].*/AllowUsers root givrs/' "$f"
  sed -i -E 's/^[[:space:]]*DenyUsers[[:space:]].*/# DenyUsers disabled by esperancita ssh live fix: &/' "$f"
done

if ! grep -RqsE '^[[:space:]]*AllowUsers[[:space:]]' /etc/ssh/sshd_config /etc/ssh/sshd_config.d; then
  printf '\nAllowUsers root givrs\n' >> /etc/ssh/sshd_config.d/99-esperancita-auth.conf
fi

SSHD="$(command -v sshd || true)"
if [ -z "$SSHD" ]; then
  SSHD="/usr/sbin/sshd"
fi

"$SSHD" -t
systemctl restart ssh || systemctl restart sshd

echo "=== SSH ativo ==="
ss -tlnp | grep ':22' || true

echo "=== Chaves instaladas ==="
ssh-keygen -lf /root/.ssh/authorized_keys || true
ssh-keygen -lf /home/givrs/.ssh/authorized_keys || true

echo "Backup criado em: $BKP"
EOF
```

## Teste externo apos executar o comando

No Windows:

```powershell
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519 root@2.24.30.151
ssh -i $env:USERPROFILE\.ssh\esperancita_hostinger_ed25519 givrs@2.24.30.151
```

Quando os dois testes por chave funcionarem, o deploy OpenClaw/Esperancita pode
continuar na VPS.
