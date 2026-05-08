# Plano Seguro de Instalacao do OpenClaw

Data/hora do plano: 2026-05-08 14:47:24 -03:00  
Base local: `C:\Users\aliss\OneDrive\Desktop\Open Claw`

## 1. Metodo correto identificado

O metodo correto para este Windows, considerando o estado atual, e:

1. Instalar a CLI OpenClaw pelo pacote npm oficial `openclaw@latest`.
2. Validar o binario `openclaw`.
3. Rodar diagnosticos da CLI.
4. Inicializar/onboardar o OpenClaw quando houver como preencher as escolhas humanas.
5. Criar/validar o workspace padrao `C:\Users\aliss\.openclaw\workspace`.
6. Migrar o `starter-kit-openclaw-v2.5.6.zip` para o workspace, preservando qualquer conteudo existente.
7. Validar que as skills do kit foram copiadas para `workspace\skills`.

Justificativa:

- A raiz auditada nao e um projeto Node/Python/Docker.
- O ZIP `starter-kit-openclaw-v2.5.6.zip` e um kit de workspace/skills, nao o binario OpenClaw.
- O README oficial atual do OpenClaw recomenda `npm install -g openclaw@latest` e depois `openclaw onboard --install-daemon`.
- O ambiente ja tem Node.js `v24.14.1`, que atende ao requisito `node >=22.14.0`.

## 2. Pre-requisitos

Obrigatorios:

- Windows 11.
- PowerShell 7+.
- Git.
- Node.js >= 22.14.0.
- npm.
- Acesso a internet para baixar `openclaw@latest`.

Ja atendidos:

- Windows 11 Pro.
- PowerShell 7.6.1.
- Git 2.53.0.
- Node.js 24.14.1.
- npm 11.11.0.

Nao obrigatorios para este metodo:

- Docker.
- WSL.
- Python/pip.
- GitHub CLI.

## 3. Backups necessarios antes de alteracoes

Criar:

```powershell
New-Item -ItemType Directory -Force -Path "C:\Users\aliss\OneDrive\Desktop\Open Claw\_BACKUP_INSTALACAO_OPENCLAW"
```

Registrar/copiar:

- `starter-kit-openclaw-v2.5.6.zip`
- Inventario de arquivos ZIP/template usados como base
- Estado "antes" de `C:\Users\aliss\.openclaw` (atualmente inexistente)
- Lista de pacotes npm globais antes da instalacao
- Se surgirem durante a instalacao, copiar antes de modificar:
  - `.env`
  - `openclaw.json`
  - `config`
  - `configs`
  - `database`
  - `db`
  - `storage`
  - `memory`
  - `memories`
  - `state`
  - `states`
  - `sessions`
  - `agents`
  - `logs`
  - qualquer arquivo de `claudio` ou `david`

## 4. Ordem de instalacao

### Fase A - Backup

```powershell
New-Item -ItemType Directory -Force -Path "C:\Users\aliss\OneDrive\Desktop\Open Claw\_BACKUP_INSTALACAO_OPENCLAW"
```

Copiar o ZIP principal para o backup:

```powershell
Copy-Item -LiteralPath "C:\Users\aliss\OneDrive\Desktop\Open Claw\Construindo seus primeiros agentes\🛠️ Starter kit (wizard openclaw)\starter-kit-openclaw-v2.5.6.zip" -Destination "C:\Users\aliss\OneDrive\Desktop\Open Claw\_BACKUP_INSTALACAO_OPENCLAW\" -Force
```

### Fase B - Instalar CLI OpenClaw

```powershell
npm install -g openclaw@latest
```

### Fase C - Validar CLI

```powershell
openclaw --version
openclaw doctor
openclaw --help
```

### Fase D - Inicializar workspace/onboarding

Comando oficial:

```powershell
openclaw onboard --install-daemon
```

Observacao: este comando pode abrir fluxo interativo de autenticacao/configuracao. Se pedir provider, login OAuth, bot token ou modelo, a execucao deve parar para entrada humana. Nao inventar valores.

### Fase E - Garantir workspace

Path esperado:

```powershell
$workspace = "$env:USERPROFILE\.openclaw\workspace"
```

Se o onboarding nao criar o workspace, criar somente a pasta vazia e registrar no relatorio:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.openclaw\workspace"
```

### Fase F - Migrar starter kit para o workspace

Extrair o ZIP para uma pasta temporaria controlada dentro do backup ou de `_OPENCLAW_EXTRACAO_TEMP`, sem sobrescrever estado.

Copiar:

- `starter-kit\skills\*` para `~\.openclaw\workspace\skills\`
- arquivos de leitura (`README.md`, `FAQ.md`, `manifesto.md`, `0-LEIA-PRIMEIRO-AGENTE.md`, `_curso`, `templates`, `exemplos`) para `~\.openclaw\workspace\`

Regra: se o destino existir e for divergente, fazer backup antes e nao sobrescrever sem registro.

### Fase G - Validar migracao

```powershell
Test-Path "$env:USERPROFILE\.openclaw\workspace\skills\starter\onboarding-checklist\SKILL.md"
Get-ChildItem "$env:USERPROFILE\.openclaw\workspace\skills" -Recurse -Filter SKILL.md | Measure-Object
```

### Fase H - Testar OpenClaw

```powershell
openclaw doctor
openclaw gateway status
```

Se o gateway nao estiver iniciado:

```powershell
openclaw gateway start
openclaw gateway status
```

Se o comando exigir configuracao interativa ou credenciais, registrar o bloqueio e as instrucoes exatas.

## 5. Arquivos que serao criados

Na pasta `Open Claw`:

- `RELATORIO_DIAGNOSTICO_INSTALACAO_OPENCLAW.md`
- `RELATORIO_AMBIENTE_WINDOWS.md`
- `PLANO_INSTALACAO_OPENCLAW.md`
- `_BACKUP_INSTALACAO_OPENCLAW\INDICE_BACKUP.md`
- `INSTALACAO_OPENCLAW_FINALIZADA.md`
- `COMANDOS_RAPIDOS_OPENCLAW.md`

No perfil do usuario, se a instalacao/onboarding prosseguir:

- `C:\Users\aliss\.openclaw\`
- `C:\Users\aliss\.openclaw\workspace\`
- `C:\Users\aliss\.openclaw\workspace\skills\`
- arquivos do starter kit dentro do workspace

No npm global:

- pacote `openclaw@latest`
- comando `openclaw` em `C:\Users\aliss\AppData\Roaming\npm`

## 6. Arquivos que poderao ser alterados

Nenhum arquivo critico existente da pasta auditada sera alterado.

Fora da pasta auditada, a instalacao npm global pode criar/alterar:

- `C:\Users\aliss\AppData\Roaming\npm\openclaw*`
- `C:\Users\aliss\AppData\Roaming\npm\node_modules\openclaw\`

O onboarding pode criar/alterar:

- `C:\Users\aliss\.openclaw\openclaw.json`
- `C:\Users\aliss\.openclaw\workspace\*`

Antes de qualquer alteracao em `~\.openclaw` apos sua criacao, o estado sera copiado para backup.

## 7. Testes de validacao

Minimos:

```powershell
openclaw --version
openclaw doctor
openclaw gateway status
Test-Path "$env:USERPROFILE\.openclaw\workspace"
Test-Path "$env:USERPROFILE\.openclaw\workspace\skills\starter\onboarding-checklist\SKILL.md"
```

Complementares:

```powershell
openclaw config validate
openclaw models list --all
openclaw channels status --probe
```

Esses complementares podem depender de configuracao inicial completa.

## 8. Como iniciar o OpenClaw

Depois de configurado:

```powershell
$env:TELEGRAM_BOT_TOKEN = [Environment]::GetEnvironmentVariable('TELEGRAM_BOT_TOKEN', 'User')
openclaw gateway start
openclaw gateway status
```

Ou, se o daemon/servico foi instalado pelo onboarding:

```powershell
openclaw gateway status
```

## 9. Como parar o OpenClaw

```powershell
openclaw gateway stop
openclaw gateway status
```

## 10. Como verificar se esta funcionando

```powershell
openclaw --version
openclaw doctor
openclaw gateway status
openclaw gateway logs
```

Sinais esperados:

- `openclaw --version` retorna a versao.
- `openclaw doctor` nao mostra erro bloqueante.
- `gateway status` indica gateway rodando ou informa exatamente o que falta configurar.

## 11. Politica de preservacao de agentes

Se surgirem agentes `claudio` ou `david` em qualquer path do OpenClaw:

- nao apagar
- nao recriar
- nao resetar
- nao sobrescrever memoria/sessoes/historico/config
- copiar para backup antes de qualquer alteracao relacionada
- registrar no relatorio final

No estado atual, nenhum desses agentes foi encontrado.

## 12. Atualizacao do plano apos execucao

Status atualizado em 2026-05-08 15:25 -03:00.

- Instalacao base concluida.
- Historico inicial: OpenAI foi validado por `OPENAI_API_KEY` com `openai/gpt-5.5`.
- Estado atual: conversas da Esperancita foram migradas para `openai-codex/gpt-5.5` via OAuth; `OPENAI_API_KEY` fica para transcricao/Whisper.
- Telegram configurado por `TELEGRAM_BOT_TOKEN` em modo `polling`.
- Para teste local, nao e necessario decidir hospedagem agora; o gateway precisa ficar rodando neste Windows.
- Para uso 24/7, escolher uma destas opcoes:
  - PowerShell administrador com `openclaw gateway install`.
  - VPS/Hostinger rodando OpenClaw continuamente.
  - WSL2, se preferir ambiente Linux local.
- Proxima etapa operacional: enviar `/start` para `@esperancitamy_bot` e configurar `commands.ownerAllowFrom` com o ID do usuario.

## 13. Atualizacao de pareamento Telegram

Status atualizado em 2026-05-08 15:37 -03:00.

- O usuario enviou mensagem ao bot e o OpenClaw gerou pedido de pareamento.
- Pareamento aprovado.
- `commands.ownerAllowFrom` configurado automaticamente.
- Fluxo validado: OpenAI gera resposta e OpenClaw entrega pelo Telegram.
- Nao foi necessario configurar Hostinger, GitHub, dominio publico ou webhook para o teste local, pois o Telegram esta em modo `polling`.

## 14. Atualizacao Hostinger API

Status atualizado em 2026-05-08 15:45 -03:00.

- Token Hostinger salvo como `HAPI_API_TOKEN`, conforme padrao do CLI oficial da Hostinger.
- API validada por chamada somente-leitura de VPS.
- Proximo passo para hospedagem real:
  1. escolher qual das 2 VPS `KVM 2` sera usada;
  2. definir acesso SSH/root ou painel Hostinger Managed;
  3. criar backup do estado local `C:\Users\aliss\.openclaw`;
  4. copiar estado/config para a VPS;
  5. configurar `OPENAI_API_KEY`, `TELEGRAM_BOT_TOKEN` e `HAPI_API_TOKEN` no ambiente da VPS;
  6. iniciar gateway na VPS;
  7. validar Telegram/OpenAI pela VPS antes de desligar o gateway local.

## 15. Politica OpenAI da Esperancita

Status atualizado em 2026-05-08 16:03 -03:00.

- Conversas do agente: `openai-codex/gpt-5.5` via OAuth ChatGPT/OpenAI Codex.
- Transcricao/Whisper: `OPENAI_API_KEY`.
- Nao usar `openai/gpt-5.5` como modelo principal da Esperancita.
- Verificacao principal:
  ```powershell
  openclaw models status
  openclaw agent --agent main --channel telegram --to SEU_ID --message "Responda exatamente: ESPERANCITA_OAUTH_OK" --deliver --json --timeout 300
  ```
- Resultado esperado: `provider=openai-codex`, `fallbackUsed=false`, `deliverySucceeded=true`.
