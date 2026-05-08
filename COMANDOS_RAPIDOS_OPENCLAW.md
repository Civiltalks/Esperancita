# Comandos Rapidos OpenClaw

## Iniciar

```powershell
$env:TELEGRAM_BOT_TOKEN = [Environment]::GetEnvironmentVariable('TELEGRAM_BOT_TOKEN', 'User')
Start-Process -FilePath 'cmd.exe' -ArgumentList @('/c', "$env:USERPROFILE\.openclaw\gateway.cmd") -WindowStyle Hidden
Start-Sleep -Seconds 8
openclaw gateway status
```

## Parar

```powershell
$pidOpenClaw = (Get-NetTCPConnection -LocalPort 18789 -State Listen).OwningProcess
Stop-Process -Id $pidOpenClaw
```

## Reiniciar

```powershell
$conn = Get-NetTCPConnection -LocalPort 18789 -State Listen -ErrorAction SilentlyContinue
if ($conn) { Stop-Process -Id $conn.OwningProcess }
$env:TELEGRAM_BOT_TOKEN = [Environment]::GetEnvironmentVariable('TELEGRAM_BOT_TOKEN', 'User')
Start-Process -FilePath 'cmd.exe' -ArgumentList @('/c', "$env:USERPROFILE\.openclaw\gateway.cmd") -WindowStyle Hidden
Start-Sleep -Seconds 8
openclaw gateway status
```

## Status

```powershell
openclaw --version
openclaw config validate
openclaw gateway status
openclaw status --deep
openclaw channels status --probe
```

## Dashboard

```powershell
Start-Process 'http://127.0.0.1:18789/'
```

## Logs

```powershell
openclaw logs --follow
```

```powershell
Get-Content -Tail 120 "$env:LOCALAPPDATA\Temp\openclaw\openclaw-$(Get-Date -Format yyyy-MM-dd).log"
```

## Teste do agente

```powershell
openclaw agent --local --agent main -m "Responda exatamente: OK_OPENCLAW" --json --timeout 180
```

## Verificar OpenAI

```powershell
openclaw models status
openclaw agent --local --agent main -m "Responda exatamente: OAUTH_CHATGPT_OK" --json --timeout 240
```

Resultado esperado para conversas do agente:

```text
defaultModel=openai-codex/gpt-5.5
provider=openai-codex
authMode=auth-profile
fallbackUsed=false
```

## Renovar Login ChatGPT/OAuth

Use quando `openclaw models status` indicar OAuth expirado ou ausente:

```powershell
openclaw models auth login --provider openai-codex --method oauth --set-default
openclaw config unset 'agents.defaults.models["openai/gpt-5.5"]'
openclaw config validate
openclaw models status
```

Regra local: a Esperancita deve usar `openai-codex/gpt-5.5` para conversas. `OPENAI_API_KEY` fica apenas para Whisper/transcricoes e recursos que exigem API direta.

## Verificar Telegram

```powershell
openclaw channels list --json
openclaw channels status --probe
openclaw status --deep
```

Bot configurado: `@esperancitamy_bot`.

## Configurar ou trocar token Telegram

Use este bloco somente se precisar trocar o token. Nao cole o token em relatorios.

```powershell
[Environment]::SetEnvironmentVariable('TELEGRAM_BOT_TOKEN', 'COLOQUE_SEU_TOKEN_AQUI', 'User')
$env:TELEGRAM_BOT_TOKEN = [Environment]::GetEnvironmentVariable('TELEGRAM_BOT_TOKEN', 'User')
openclaw channels add --channel telegram --use-env
openclaw channels status --probe
```

## Autorizar Telegram depois do /start

Depois de enviar `/start` para `@esperancitamy_bot`, verifique se surgiu pedido de pareamento:

```powershell
openclaw pairing list --channel telegram --json
```

Quando souber o seu ID:

```powershell
openclaw config set commands.ownerAllowFrom '["telegram:SEU_ID_AQUI"]'
openclaw config validate
```

No estado atual, o pareamento ja foi aprovado e `commands.ownerAllowFrom` ja foi configurado para o remetente aprovado.

## Testar entrega do agente pelo Telegram

```powershell
openclaw agent --agent main --channel telegram --to SEU_ID --message "Responda exatamente: ESPERANCITA_OAUTH_OK" --deliver --json --timeout 300
```

Resultado esperado:

```text
deliverySucceeded=true
provider=openai-codex
model=gpt-5.5
fallbackUsed=false
```

## Skills

```powershell
openclaw skills list
Test-Path "$env:USERPROFILE\.openclaw\workspace\skills\starter\onboarding-checklist\SKILL.md"
```

## Backup

```powershell
$stamp = Get-Date -Format 'yyyy-MM-dd_HHmmss'
$dest = "C:\Users\aliss\OneDrive\Desktop\Open Claw\_BACKUP_INSTALACAO_OPENCLAW\backup_manual_$stamp"
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item -LiteralPath "$env:USERPROFILE\.openclaw" -Destination $dest -Recurse
```

## Restaurar backup

```powershell
$conn = Get-NetTCPConnection -LocalPort 18789 -State Listen -ErrorAction SilentlyContinue
if ($conn) { Stop-Process -Id $conn.OwningProcess }

$stamp = Get-Date -Format 'yyyy-MM-dd_HHmmss'
Rename-Item -LiteralPath "$env:USERPROFILE\.openclaw" -NewName ".openclaw_antes_restore_$stamp"
Copy-Item -LiteralPath "C:\Users\aliss\OneDrive\Desktop\Open Claw\_BACKUP_INSTALACAO_OPENCLAW\backup_2026-05-08_1500_openclaw_final_funcional\.openclaw" -Destination "$env:USERPROFILE" -Recurse
```

## Atualizar dependencias com seguranca

Antes:

```powershell
$stamp = Get-Date -Format 'yyyy-MM-dd_HHmmss'
$dest = "C:\Users\aliss\OneDrive\Desktop\Open Claw\_BACKUP_INSTALACAO_OPENCLAW\backup_pre_update_$stamp"
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item -LiteralPath "$env:USERPROFILE\.openclaw" -Destination $dest -Recurse
npm list -g --depth=0
```

Atualizar:

```powershell
npm install -g openclaw@latest
openclaw --version
openclaw config validate
openclaw gateway status
```

## Instalar gateway persistente

Se quiser persistencia apos reboot, abra PowerShell como administrador e rode:

```powershell
openclaw gateway install
openclaw gateway start
openclaw gateway status
```

## Hospedagem

Para teste local com Telegram em polling, nao precisa de dominio nem hospedagem externa: mantenha o gateway rodando neste Windows. Para 24/7, use VPS/Hostinger/WSL2 ou instale o gateway como Scheduled Task em PowerShell administrador.

GitHub e Hostinger nao foram configurados neste processo.

## Hostinger API

Token configurado como variavel de ambiente de usuario `HAPI_API_TOKEN`. O valor nao deve ser escrito em arquivos.

Em cada novo PowerShell, importe a variavel para o processo atual antes de usar:

```powershell
$env:HAPI_API_TOKEN = [Environment]::GetEnvironmentVariable('HAPI_API_TOKEN', 'User')
```

Verificar se a variavel existe:

```powershell
[bool][Environment]::GetEnvironmentVariable('HAPI_API_TOKEN', 'User')
```

Listar VPS Hostinger via API, somente leitura:

```powershell
$env:HAPI_API_TOKEN = [Environment]::GetEnvironmentVariable('HAPI_API_TOKEN', 'User')
Invoke-RestMethod -Method Get -Uri 'https://developers.hostinger.com/api/vps/v1/virtual-machines' -Headers @{
  Accept = 'application/json'
  Authorization = "Bearer $env:HAPI_API_TOKEN"
}
```

Observacao: isso valida acesso a Hostinger, mas nao hospeda o OpenClaw automaticamente. Para hospedar, ainda e necessario escolher uma VPS, definir metodo de acesso SSH/painel e migrar o estado com backup.
