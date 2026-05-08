# 📝 Notas para Próximas Gravações — Março 2026

> Mudanças do changelog (2026.3.13 → 2026.3.24) que merecem menção em vídeo.
> Gerado em 30/03/2026.

---

## 1. Security: exec config protegida
**Onde mencionar:** Aula de Segurança (02) ou gravação nova
**O que mudou:** O agente não pode mais alterar a própria configuração de `exec` via `config.patch`. Isso impede que uma skill maliciosa ou um prompt injection eleve as permissões do agente silenciosamente.
**Por que importa pro aluno:** Se ele está preocupado com segurança, agora tem uma camada a mais de proteção out-of-the-box.

---

## 2. ACP bind direto no chat (Discord)
**Onde mencionar:** Aula de Multi-agentes (08) ou gravação nova
**O que mudou:** Agora é possível spawnar um agente ACP (Claude Code, Codex) diretamente dentro de uma thread de Discord, sem precisar de CLI separada.
**Por que importa pro aluno:** Quem usa Discord como interface pode delegar tarefas de coding direto no chat.

---

## 3. Flag `--container` pra Docker
**Onde mencionar:** Aula de Setup VPS (01/03)
**O que mudou:** `openclaw gateway start --container` é o modo recomendado pra rodar dentro de Docker. Ajusta paths, signals e logs automaticamente.
**Por que importa pro aluno:** Quem faz deploy via Docker não precisa mais de workarounds manuais no entrypoint.

---

## 4. /status mostra até 1M tokens corretamente
**Onde mencionar:** Aula de Memória (04) — pode ser só uma nota rápida
**O que mudou:** Modelos 4.6+ reportam contexto de 1M tokens e o `/status` agora exibe corretamente.
**Por que importa pro aluno:** O contexto disponível é muito maior do que parecia — afeta a estratégia de compactação.

---

## 5. Gateway expõe /v1/models e /v1/embeddings (OpenAI-compatible)
**Onde mencionar:** Aula de Mission Control (10) ou Integrações (05/06)
**O que mudou:** O gateway agora serve endpoints compatíveis com a API OpenAI. Isso permite conectar ferramentas externas (LangChain, LiteLLM, custom apps) direto no gateway do OpenClaw.
**Por que importa pro aluno:** Quem está construindo Mission Control customizado pode usar o gateway como backend de API.

---

## 6. requireApproval pra skills sensíveis
**Onde mencionar:** Aula de Skills Avançado (12) ou Segurança (02)
**O que mudou:** Skills agora podem ter um hook `requireApproval` — antes de executar uma ação sensível (enviar email, deletar arquivo, fazer deploy), o agente pede confirmação do humano.
**Por que importa pro aluno:** É o "guardrail" que faltava pra dar mais autonomia sem medo. Permite escalar automações com safety net.

---

## Prioridade de gravação sugerida

| # | Nota | Urgência | Pode ser update rápido? |
|---|---|---|---|
| 1 | exec config protegida | 🔴 Alta | ✅ Sim — 2min na aula de segurança |
| 6 | requireApproval | 🔴 Alta | ❌ Merece demo ao vivo |
| 2 | ACP bind Discord | 🟡 Média | ✅ Sim — nota rápida |
| 3 | --container Docker | 🟡 Média | ✅ Sim — nota na aula VPS |
| 4 | /status 1M tokens | 🟢 Baixa | ✅ 30 segundos |
| 5 | /v1/models endpoint | 🟢 Baixa | ✅ Nota pra quem é dev |

---

*Amora · 30/03/2026*
