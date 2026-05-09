# Super Esperancita - memoria permanente

Data: 2026-05-08

## Origem analisada

Pasta local:

```text
C:\Users\aliss\OneDrive\Desktop\Super Esperancita
```

A pasta solicitada como `esperancita-leia primeiro` foi encontrada no disco com o nome real:

```text
Esperancita-LEIA PRIMERO
```

Ela foi tratada como a pasta obrigatoria de primeira leitura.

## Manifesto local

Foi criado:

```text
C:\Users\aliss\OneDrive\Desktop\Super Esperancita\SUPER_ESPERANCITA_MANIFESTO.md
```

O manifesto registra estrutura, ordem de leitura, arquivos criticos, arquivos de personalidade, memoria, comportamento, operacao, estrategia, riscos e materiais que nao devem entrar diretamente na memoria ativa.

## Ordem de leitura aplicada

1. `Esperancita-LEIA PRIMERO`
2. Manual mestre de personalidade, voz, comportamento, memoria e humanizacao.
3. Criterios de construcao agentica.
4. Criterio de input de novos conhecimentos na memoria.
5. Documento Final da Plataforma Esperancita.
6. Mapeamento profundo de dores.
7. Arquitetura e fluxos n8n em `.docx`.
8. Workflows, modelo WhatsApp, memoria/RAG, catalogo de skills, criterios funcionais e nao funcionais.
9. Guia visual da Esperancita.
10. Inventarios e cursos reconstruidos como conhecimento complementar.
11. `Complementar-2do Leitura` apenas como biblioteca complementar a curar, nao como memoria ativa bruta.

## Consolidacao aplicada

A memoria permanente foi organizada em camadas:

- nucleo da identidade;
- personalidade e alma;
- operacao;
- seguranca e limites;
- conhecimento complementar.

O conteudo bruto de cursos, PDFs, transcricoes, evidencias de publico e documentos privados nao foi copiado para a memoria ativa. Foi consolidado apenas o que e essencial para identidade, comportamento, criterio e funcionamento.

## Arquivos de workspace alterados/criados

Arquivos atualizados:

- `openclaw/workspace/IDENTITY.md`
- `openclaw/workspace/SOUL.md`
- `openclaw/workspace/MEMORY.md`
- `openclaw/workspace/BOOTSTRAP.md`
- `openclaw/workspace/AGENTS.md`
- `openclaw/workspace/TOOLS.md`
- `openclaw/workspace/HEARTBEAT.md`
- `openclaw/workspace/MAPA.md`

Arquivos criados:

- `openclaw/workspace/ESPERANCITA_PERSONALIDADE.md`
- `openclaw/workspace/ESPERANCITA_TOM_DE_VOZ.md`
- `openclaw/workspace/ESPERANCITA_FUNCIONAMENTO.md`
- `openclaw/workspace/ESPERANCITA_CRITERIOS_OPERACIONAIS.md`
- `openclaw/workspace/ESPERANCITA_MEMORIA_PERMANENTE.md`
- `openclaw/workspace/ESPERANCITA_LIMITES_E_SEGURANCA.md`

## Backups criados

Backup local:

```text
C:\Users\aliss\OneDrive\Desktop\Super Esperancita\_BACKUP_SUPER_ESPERANCITA_MEMORIA\2026-05-08_205053
```

Backup remoto na VPS:

```text
/home/givrs/.openclaw/backups/workspace-before-super-esperancita-2026-05-08_205602
```

O backup remoto foi criado antes da sincronizacao e preserva o workspace anterior completo.

## Sincronizacao com a VPS

Destino:

```text
/home/givrs/.openclaw/workspace
```

Foram copiados apenas os Markdown consolidados e arquivos de boot alterados. A pasta bruta `Super Esperancita` nao foi enviada para a VPS.

Permissoes finais verificadas:

- dono: `givrs`
- grupo: `givrs`
- arquivos Markdown: `644`

## Validacoes executadas

### Saude e modelos

Comandos:

```bash
openclaw health
openclaw models status
```

Resultado:

- Telegram configurado.
- Agente `main` disponivel.
- Servico 24/7 ativo.
- Modelo principal: `openai-codex/gpt-5.5`.
- Autenticacao: OAuth por auth-profile.
- Nenhum token/API key usado como conversa principal.

Observacao tecnica: `openclaw health` retornou `degraded` por `event_loop_utilization,cpu`. O servico respondeu e os testes funcionaram, mas isso deve ser monitorado.

### Teste 1 - identidade

Prompt:

```text
Explique em 5 linhas quem e a Esperancita, qual sua missao e como voce deve agir.
```

Resultado resumido:

- Respondeu que Esperancita e governanta digital e secretaria executiva do lar.
- Citou reducao da carga mental.
- Citou casa, familia, pendencias e operacao.
- Citou seguranca, memoria, continuidade, evidencia e autorizacao para decisoes sensiveis.

### Teste 2 - criterios inegociaveis

Prompt:

```text
Quais sao seus criterios inegociaveis de funcionamento?
```

Resultado resumido:

- Seguranca antes de velocidade.
- Acao com prova.
- Memoria e continuidade.
- Consentimento em acoes sensiveis.
- Reducao de carga mental.
- Dignidade de casa, familia e colaboradores.
- Pessoas antes de perfeicao domestica.

### Teste 3 - mae sobrecarregada

Prompt:

```text
Como voce deve ajudar uma mae sobrecarregada a organizar a rotina da casa?
```

Resultado resumido:

- Acolher sem culpar.
- Reduzir ao essencial.
- Transformar caos em microacoes.
- Priorizar seguranca, criancas, alimentacao, roupa essencial, prazos e transporte.
- Distribuir responsabilidade com dono, prazo, criterio de pronto e plano B.
- Evitar perfeccionismo.
- Preservar vinculo familiar e dignidade.

## Observacoes tecnicas

O relatorio `systemPromptReport` do OpenClaw mostrou que o bootstrap automatico injeta os arquivos padrao do workspace, como `AGENTS.md`, `SOUL.md`, `TOOLS.md`, `IDENTITY.md`, `USER.md`, `HEARTBEAT.md`, `BOOTSTRAP.md` e `MEMORY.md`.

Os novos arquivos `ESPERANCITA_*.md` foram copiados e referenciados, mas nao apareceram na lista de injecao automatica padrao. Por isso, os pontos essenciais foram tambem espelhados nos arquivos padrao (`IDENTITY.md`, `SOUL.md`, `MEMORY.md`, `AGENTS.md`) para garantir comportamento imediato.

Pendencia tecnica futura: se o OpenClaw permitir configurar lista explicita de arquivos de bootstrap, adicionar os `ESPERANCITA_*.md` ao carregamento automatico.

Outro aviso observado:

```text
[memory] chunks_vec not updated - sqlite-vec unavailable. Vector recall degraded.
```

A memoria textual e os testes do agente funcionaram, mas a memoria vetorial/RAG esta degradada e deve ser tratada em etapa propria.

## Seguranca

Nao foram gravados tokens, senhas, chaves privadas ou PATs nesta documentacao.

Antes do commit, rodar scan de segredos e adicionar apenas arquivos especificos.

## Proximos passos

1. Investigar `sqlite-vec unavailable` para restaurar recall vetorial completo.
2. Investigar alerta de `event_loop_utilization,cpu` no `openclaw health`.
3. Definir se os arquivos `ESPERANCITA_*.md` devem ser injetados automaticamente pelo bootstrap do OpenClaw ou se permanecem como documentos de referencia lidos sob demanda.
4. Curar a biblioteca complementar por tema antes de transformar cursos/PDFs em memoria ativa.
5. Validar juridicamente/LGPD qualquer ingestao futura de documentos privados, dados de criancas, colaboradores, saude, financas, escola ou conteudos de terceiros.
