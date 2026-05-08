# Template Diretoria — Como usar

> Cérebro confidencial dos sócios. Informação sensível. **Sempre revisado por humano.**

---

## O que vai aqui

- Contratos com clientes (valores · prazos · cláusulas sensíveis)
- Salários · comissões · pro-labore · bônus
- Negociações em andamento (M&A · parcerias · investimento)
- Decisões de RH sensíveis (desligamentos · contratações sêniores)
- Compliance · litígio · LGPD · obrigações fiscais
- Equity · cap table · acordo de sócios

## O que NÃO vai aqui

- Operação do dia-a-dia (cérebro empresa)
- Reflexões individuais (cérebro pessoal)
- Conteúdo de marketing/vendas (cérebro empresa)
- Discussões abertas com o time (cérebro empresa)

---

## ⚠️ Princípio CRÍTICO

**Cérebro da diretoria NÃO tem auto-commit.** Toda informação passa por revisão humana antes de virar memória oficial.

Por que: agente de madrugada pode classificar errado e expor informação que não devia. Diretoria = sempre revisão consciente.

Workflow típico:
1. Você (sócio) registra info
2. Vai pro `staging/` ou `inbox/`
3. Diretor revisa · ajusta · aprova
4. Aí vira commit oficial no `main`

---

## Como usar

### 1. Baixa o zip

`template-diretoria-0.1.0.zip` (nesta mesma pasta · arrasta manualmente do Drive legado se ainda não tá aqui)

### 2. Anexa na sua IA

⚠️ **IA do agente de DIRETORIA**, não da operação. Tem que ser conta separada · escopo restrito.

### 3. Cola este prompt

```
Te mandei `template-diretoria-0.1.0.zip` — template do cérebro confidencial
dos sócios da [SUA EMPRESA], parte da Imersão Segundo Cérebro do Pixel AI Hub.

Quero que você:

1. Extraia o zip
2. Leia a estrutura inteira (note que diretoria tem regras DIFERENTES da empresa)
3. Me ajude a configurar pra MINHA realidade:
   - Quem são os sócios (nomes · papéis · permissões)
   - Estrutura societária (CNPJ · cap table simplificado · comitês internos)
   - Tipos de informação que entram aqui (contratos? salários? equity?)
   - Workflow de revisão (quem aprova o quê antes de virar memória oficial)

CRÍTICO: NÃO faça auto-commit de nada. Tudo passa por revisão. Default é
staging → human review → main. Confirma esse comportamento antes de eu
começar a popular.
```

---

## Gatilhos automáticos (palavras que disparam roteamento pra diretoria)

Esses termos, quando aparecem em mensagem do agente de outro cérebro, fazem roteamento automático pra cérebro da diretoria (com revisão humana):

- Salário · pro-labore · comissão · bônus · remuneração
- Nome próprio + valor monetário (ex: "Bruno · R$ 25k")
- Contratação · desligamento · feedback de pessoa específica
- Contrato · cláusula · NDA · litígio · LGPD
- Equity · acordo de sócios · cap table · investimento
- M&A · venda · aquisição · valuation

Configure esses gatilhos no AGENTS.md do template.

---

📌 Pixel Educação · Pixel AI Hub
