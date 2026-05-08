# Template Empresa — Como usar

> Cérebro coletivo da empresa. Compartilhado pelo time inteiro.

---

## O que vai aqui

- Operação (processos · workflows · SOPs)
- Marketing (calendário · campanhas · criativos · métricas)
- Vendas (pipeline · clientes · scripts · objeções comuns)
- Atendimento (FAQ · escalation · postmortems)
- Time (estrutura · papéis · cadência · cerimônias)
- Conhecimento técnico (estack · runbooks · arquitetura · skills compartilhadas)

## O que NÃO vai aqui

- Informação sensível dos sócios (cérebro diretoria)
- Reflexões individuais (cérebro pessoal)
- Salários · contratos · equity (cérebro diretoria)

---

## Como usar

### 1. Baixa o zip

`template-empresa-0.1.0.zip` (nesta mesma pasta · arrasta manualmente do Drive legado se ainda não tá aqui)

### 2. Anexa na IA do agente da empresa

Pode ser o agente principal da operação · ou um agente dedicado da empresa. Importante: cada membro do time clona o repo desse cérebro depois.

### 3. Cola este prompt

```
Te mandei `template-empresa-0.1.0.zip` — template do cérebro coletivo da
[SUA EMPRESA], parte da Imersão Segundo Cérebro do Pixel AI Hub.

Quero que você:

1. Extraia o zip
2. Leia a estrutura inteira
3. Me ajude a configurar pra MINHA empresa:
   - Nome · setor · tamanho · contexto
   - Áreas operacionais ativas (marketing? vendas? atendimento? produto?)
   - Estrutura do time (sócios · líderes · operação · DRIs)
   - Vocabulário interno (gírias · siglas · termos próprios)
   - Cerimônias (daily? weekly? quarterly?)

Auto-commit é OK pra dados não-sensíveis (operação, marketing, vendas).
Mas adicione gatilhos de roteamento pra cérebro DIRETORIA quando aparecer
informação sensível (salário · contrato · equity · etc.).

Mostra a configuração antes de salvar.
```

---

## Princípio crítico

Diferente do cérebro da diretoria (sempre revisão humana), o cérebro da empresa **PODE** ter auto-commit pra coisas não-sensíveis. Mas precisa ter **filtro de gatilhos** que detecta informação sensível e desvia pra diretoria automaticamente.

Exemplo: time discute estratégia de marketing → vai direto pra cérebro empresa. Time menciona salário do CMO → roteia pra diretoria com revisão.

---

## Permissionamento de time

Como o GitHub controla acesso por repo (não por pasta), cérebro empresa = repo separado.

Cada membro do time:
1. Tem GitHub conectado ao agente dele
2. Clona o repo da empresa
3. Tem permissão read-only ou read+write conforme papel

⚠️ Funcionário sai? Remove acesso ao repo. Histórico fica preservado.

---

📌 Pixel Educação · Pixel AI Hub
