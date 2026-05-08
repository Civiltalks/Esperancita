# Material 3 — Cérebro da Diretoria

> **Fonte:** material da aula Pixel AI Hub (versão pós-review Cayo, 30/04)
> **Arquivo origem:** `material-3-cerebro-diretoria-v6-2026-04-30.html`

---

# Material 3 v4 — Cérebro da Diretoria | Pixel AI Hub


# Agora você separa o que é operação do que é diretoria.

O cérebro da diretoria é o repositório sensível da empresa. A aula precisa mostrar, na prática, que o diretor começa no cérebro pessoal, decide o que pode virar diretoria e nunca exige que o aluno pense em detalhe técnico de Git.


## Promessa da aula

Ao final, você entende como proteger assuntos sensíveis sem misturar diretoria com operação do time.

Resultado esperado: dinheiro nominal, pessoas específicas e jurídico deixam de cair no cérebro operacional.

Ideia central: o diretor pensa no pessoal, compartilha com a diretoria só quando fizer sentido e o agente prepara tudo para revisão humana.

Veja ao vivo: um item sensível fica fora do cérebro da empresa, aparece como proposta para sócios revisarem e nunca fica visível para o colaborador.


## Um cérebro só vira risco quando a empresa cresce.

No começo, tudo parece contexto. Depois aparecem salários, contratos, conflitos e decisões de sócio. A aula 3 ensina você a não misturar sensível com operacional.


### Permissão por repo

GitHub controla acesso bem por repositório, não por pasta. Por isso diretoria precisa de repo separado.


### Menos vazamento

O agente do time não tem acesso ao repo da diretoria. A barreira é estrutural, não só uma instrução no prompt.


### Mais revisão

Aqui nada vira memória oficial automaticamente. Tudo que sai do privado e vira registro de diretoria passa por revisão humana.


### Privado por padrão

Diferente do cérebro do time, o default aqui é: pense primeiro no pessoal. Só compartilhe com a diretoria quando fizer sentido para os sócios.


## Se disparou um gatilho, não vai pro cérebro do time.

Essa é a principal decisão da aula. Você não precisa decorar uma política enorme. Só precisa perguntar se o conteúdo cai em um desses três casos — e eu vou mostrar ao vivo um item sendo barrado antes de chegar no cérebro do time.


### Dinheiro com nome próprio

Salário, comissão, bônus individual, pró-labore, dívida nominal, negociação de remuneração.


### Pessoa específica

Avaliação, feedback direto, conflito, contratação, desligamento, performance individual.


### Peso jurídico ou contratual

Contrato, NDA, litígio, compliance, LGPD, obrigação societária, risco formal.


## O time vê operação. A diretoria vê o sensível.

O repo da diretoria não substitui o repo da empresa. Ele nasce como segunda camada. Os dois não compartilham contexto automaticamente.


### Arquitetura correta

Cérebro do time: marketing, vendas, atendimento, operações, produto.

Cérebro da diretoria: financeiro sensível, RH, jurídico, governança.

Sócio humano: é a ponte entre os dois cérebros.

Agente do time: não acessa o repo da diretoria.

Agente da diretoria: opera com tom prudente e revisão humana obrigatória.


## A diretoria usa a mesma arquitetura, com mais trava.

A estação de trabalho continua sendo onde o diretor pensa. O OpenClaw da diretoria ajuda a organizar propostas para revisão. O repo da diretoria guarda apenas o sensível que precisa ser compartilhado entre sócios. O colaborador não vê essa camada.


### Pensar e capturar

Claude Cowork ajuda o sócio a preparar conselho, contrato, decisão de gente ou discussão estratégica.


### Consolidar com prudência

Organiza inbox, sugere destino, prepara revisão para sócios e nunca transforma sensível em memória oficial sozinho.


### Guardar o sensível

Fonte de verdade restrita para dinheiro nominal, pessoas, jurídico, contratos e governança.


## Você começa como diretor: pessoal, empresa e diretoria conectados.

Essa é a mudança de clareza: o diretor não trabalha só em um cérebro. Ele pensa no pessoal, manda operação para a empresa e protege sensível na diretoria. O colaborador, por outro lado, usa apenas o cérebro da empresa.


### Diretor conecta 3

Você pede ao agente para usar pessoal, empresa e diretoria.


### Trabalhar

Você conversa, pensa, faz brainstorm, prepara conselho, contrato ou decisão.


### Salvar

A skill save materializa a sessão no cérebro pessoal. Ainda não publicou em nenhum coletivo.


### Roteamento

A skill /sync-diretoria pergunta item por item: isso é operação do time ou assunto de diretoria?

Se cair nos 3 gatilhos, vai para o inbox restrito da diretoria. Se não, vai para empresa — que é o único cérebro do colaborador.


### Revisão aprovada

Na diretoria, nada vira memória oficial sem revisão de pelo menos um sócio.


## O cérebro da diretoria é pequeno, mas mais rígido.

A estrutura vem do template real. Não tem marketing, vendas ou produto aqui. Esse repo só guarda áreas que exigem confidencialidade e revisão.


### Anatomia do repo da diretoria

CLAUDE.md instrui a estação de trabalho com regras de segurança.

MAPA.md explica áreas, papéis e regra dos 3 gatilhos.

areas/ tem financeiro, RH, jurídico e governança.

empresa/contexto/ guarda princípios, arquitetura e segurança.

inbox/ é triagem de sócios. Não é memória oficial.


## O diretor tem três portas. O colaborador tem uma.

Essa é a explicação que torna o permissionamento óbvio sem virar aula técnica.


### Pessoal + Empresa + Diretoria

Pensa no pessoal, compartilha operação com a empresa e guarda sensível na diretoria. O diretor decide o que atravessa.


### Empresa apenas

Consulta e captura no cérebro da empresa. Não tem acesso ao pessoal do diretor nem ao repo da diretoria.


## Antes de salvar, pergunte: onde isso mora?

Essa seção precisa deixar você confiante em classificar conteúdo. O erro mais caro é jogar assunto sensível no cérebro do time.


### Fica no cérebro do time

- Receita agregada do mês
- Plano de campanha
- Roadmap de produto
- Script de atendimento
- Processo operacional sem pessoa nomeada

### Vai para diretoria

- Comissão da Ana em abril
- Feedback individual sobre Bruno
- Conflito entre duas pessoas
- Contrato com cláusula de exclusividade
- Discussão de equity, pró-labore ou desligamento

## Esse cérebro é para pensamento estratégico com proteção.

Sócio não usa a diretoria só para “guardar arquivo sensível”. Usa para pensar melhor: brainstorm, reunião de conselho, conversa estratégica, decisão de gente, contrato, investidor e governança.


### Uso normal do diretor

- Preparar reunião de conselho
- Simular cenários de caixa e contratação
- Debater conflito ou performance de pessoa
- Revisar proposta, contrato ou parceria
- Registrar decisão estratégica ainda não pública

### Como isso vira operação

- O raciocínio sensível fica aqui
- O que for seguro vira síntese operacional
- O sócio humano decide o que atravessa
- O agente da diretoria pode enviar captura diplomática ao cérebro do time
- Nada sensível atravessa automaticamente

## Uma regra, três aplicações. Privado nunca sobe pro repo.

Esse é o ponto que confunde mais gente, então vou tirar o mistério: a pasta privado/ é sempre privada, nos 3 cérebros. O que muda é só onde o Claude guarda os rabiscos do dia , dependendo de quem você é.


### "Privado por padrão na diretoria" é só comportamento, não versionamento.

Quando você roda /sync-diretoria , o default é guardar em privado/ — continua não saindo do seu computador. Só vira público pros sócios se você decidir item-por-item no quiz . Privacidade aqui é decisão sua, não do agente.


## Dúvida do diretor fica no pessoal. Decisão de sócios vai pra diretoria.

Para colaborador, dúvida sensível nunca vai pra diretoria — ele só usa empresa e sinaliza pra um diretor. Para diretor, se ainda é pensamento individual, fica no cérebro pessoal. Só quando precisa ser compartilhado com sócios entra no cérebro da diretoria.


### Não tem diretoria

Se aparecer algo sensível, não publica no cérebro da empresa. Sinaliza para um diretor.


### Fica no pessoal

Se ainda é reflexão, hipótese ou dúvida individual, salva no cérebro pessoal do diretor.


### Vai para inbox da diretoria

Se os sócios precisam revisar ou decidir juntos, entra no fluxo restrito da diretoria.


## Do pensamento privado à revisão de sócios.

Não peça para o aluno pensar em detalhe técnico de Git. A ideia didática é mais simples: primeiro salve no pessoal; depois escolha se algo deve ser compartilhado com a diretoria; por fim, o agente prepara uma revisão para outro sócio aprovar.

O diretor trabalha no cérebro pessoal: conselho, pessoa, contrato, caixa ou governança.

Se houver dúvida, fica só no cérebro pessoal do diretor. Não precisa ir para diretoria ainda.

Quando o assunto precisa ser visto por sócios, o /sync-diretoria envia para o inbox da diretoria.

Como na aula 2, a captura vem com metadata/sidecar para explicar autor, tipo, maturidade e destino.

O OpenClaw da diretoria organiza o item e prepara uma proposta clara para sócios revisarem.

Um sócio revisa. Só depois vira memória oficial da diretoria.


## As skills são o roteador entre os cérebros.

Você não precisa operar Git nem decorar arquitetura. O fluxo certo é: carregar contexto, salvar no cérebro pessoal e depois rotear item por item para o cérebro correto.


### /sync-pessoal

(do mini-curso) Mantém workspace sincronizado.


### "salva isso"

Linguagem natural no workspace pessoal.


### /sync-empresa

Para o operacional.


### /sync-diretoria

Para o sensível (3 gatilhos).

O /sync-diretoria não filtra automaticamente. O agente apresenta cada captura ("este menciona Marina e R$8k") e pergunta: "vai pra diretoria?" . Os 3 gatilhos servem como sanity check humano, não como trigger automático. Mecanismos de proteção (PR obrigatório, CODEOWNERS, allowlist sócios-only) impedem atalho — mas a decisão é sempre humana.


## Como uma conversa vira memória no cérebro certo.

Essa é a parte mais importante para você: as skills não são decoração. Elas são a esteira operacional que impede contexto sensível de cair no lugar errado.

O agente carrega os três cérebros disponíveis: pessoal, empresa e diretoria.

Você trabalha normalmente: brainstorm, conselho, RH, contrato, decisão.

A sessão vira arquivo no cérebro pessoal. Ainda não foi para nenhum repo coletivo.

O agente faz quiz item a item e aplica a regra dos 3 gatilhos.

Operação vai para empresa. Sensível vai para diretoria.

No cérebro da diretoria, tudo entra como proposta revisável; sócio aprova antes de virar memória oficial.


## O arquivo não anda sozinho. Ele anda com metadata.

Esse conceito já apareceu na aula 2: captura boa anda com metadata. Aqui ele volta porque, em contexto sensível, o agente precisa explicar por que aquilo existe, quem capturou, qual gatilho disparou e quem deve revisar.


### Arquivo capturado

Exemplo em inbox/bruno/comissao-ana-abril.md .


### Sidecar obrigatório

Exemplo em inbox/bruno/comissao-ana-abril.md.meta.yaml .


## O aluno não precisa falar Git. Precisa falar intenção.

Troque comandos técnicos por pedidos em linguagem natural. O agente conhece revisão e proposta por baixo; o aluno só precisa dizer o que quer proteger e quem deve revisar.


### Sempre peça assim


### Nunca aceite assim


## Registro oficial da diretoria sempre precisa de sócio aprovador.

O agente prepara. A diretoria decide. Esse é o limite que protege salário, contrato, pessoa e decisão estratégica de virarem memória oficial por acidente.


### Quem aprova?

Pelo menos um sócio-diretor com acesso ao repo da diretoria. O ideal é definir um responsável padrão por área: financeiro, RH, jurídico ou governança.


### O agent propõe

Ele consolida inbox, sugere destino, prepara a proposta de revisão e explica o que mudou. Ele não aprova sozinho.


### O sócio assume

O sócio revisa risco, nomes, valores e implicação. Se estiver certo, aprova a entrada na memória oficial.


## Mostre o sensível ficando fora do cérebro do time.

Aqui entra a demo ao vivo: diretor captura item sensível, /sync-diretoria pergunta o destino, OpenClaw prepara revisão de sócio e a visão do colaborador continua sem esse contexto.

Conversa no pessoal sobre comissão, contrato ou pessoa.

Team-sync aplica os 3 gatilhos.

Arquivo entra no inbox sensível da diretoria.

OpenClaw prepara revisão e pede aprovação de sócio.

Abre só o cérebro da empresa.

O sensível não aparece para o colaborador.


## A validação é ver a fronteira segura, não só ver o arquivo.

O “aha moment” da aula 3 é diferente das aulas anteriores. Aqui você prova que o sistema protege o sensível: pessoal → decisão de compartilhar → inbox da diretoria → revisão de sócio → memória oficial.


### O “aha moment” é a fronteira segura.

Você percebe que o agente não está só lembrando. Ele está respeitando o limite entre operação e diretoria, e não promove conteúdo sensível sem aprovação de um sócio.

Métrica de validação: na tela, o item sensível nunca aparece no cérebro do time e só vira memória oficial depois de revisão de sócio.


## Checklist de maturidade antes de abrir esse repo.

Não abra o cérebro da diretoria cedo demais. Você precisa ter o cérebro do time rodando, estações pessoais funcionando e pelo menos um caso real dos 3 gatilhos. Sem isso, a diretoria vira teatro de arquitetura.

Idealmente 60+ dias de uso real.

Todo mundo sabe capturar no próprio inbox.

Rotina já funciona no repo operacional.

Dinheiro nominal, pessoa específica ou contrato/jurídico.


## Como você trabalha no dia a dia com os três cérebros.

A aula fecha amarrando o sistema completo. Você não troca de cérebro por estética; você troca de cérebro conforme permissão, risco e destino do contexto.


### Pessoal

Uso diário: pensar, rascunhar, decidir, registrar preferências, preparar reuniões e salvar contexto seu.

Exemplo: “me ajuda a preparar uma conversa difícil com o Head de Marketing”.


### Empresa

Uso diário: distribuir o que o time pode usar: processos, decisões operacionais, vendas, marketing, produto e atendimento.

Exemplo: “essa nova regra de qualificação de lead pode ir para vendas”.


### Diretoria

Uso diário: proteger o que envolve dinheiro nominal, pessoa específica, jurídico, contrato, conselho ou governança.

Exemplo: “vamos discutir comissão da Ana, cláusula do contrato ou cenário de desligamento”.


## O fluxo diário é simples: pensar, salvar, rotear, aprovar.

Essa é a rotina que você deve levar para a vida real depois da aula. Não começa pelo GitHub. Começa pelo trabalho.

Peça ao agente para usar os cérebros disponíveis antes de trabalhar.

Use o agent para brainstorm, conselho, contrato, pessoa, estratégia.

Materialize a conversa no seu cérebro pessoal.

Escolha o que pode sair do pessoal e para onde vai.

Na diretoria, um sócio precisa aprovar antes de virar memória oficial.


## Você precisa reconhecer situações reais.

Esses exemplos evitam que a aula fique abstrata. A pergunta sempre é: isso é meu, é operacional do time ou é sensível da diretoria?


### Vai para empresa

- Nova regra de qualificação de leads
- Processo de onboarding de cliente
- Aprendizado de uma campanha
- Resumo operacional de reunião semanal
- Playbook de atendimento ou suporte
- Comissão ou salário de alguém
- Feedback individual sobre uma pessoa
- Conversa de conselho ou investidor
- Contrato com cláusula sensível
- Decisão de contratação, desligamento ou equity

## O que tá rodando debaixo do capô do cérebro da diretoria.

Aqui é onde mais importa: dinheiro, pessoas, contrato. Os 2 mecanismos abaixo são os mesmos dos outros cérebros — mas aqui eles existem por uma razão muito específica.


### /cerebro

Mesma lógica de antes — primeira coisa que você roda quando abre o Claude. Só que aqui ele é especialmente importante: o agente precisa saber que existe um cérebro de diretoria antes de sair distribuindo qualquer coisa. Sem /cerebro , ele pode confundir o que é da diretoria com o que é da empresa. E aí dá ruim.


### Agente não salva sozinho

Mesma trava dos outros cérebros, mas aqui ela vale ouro: nada vira público sem você decidir . Só skills oficiais destravam, e o quiz do /sync-diretoria é item-por-item. Aurora (a agente da diretoria) tem a chave no servidor dela pra rodar consolidação à noite — mas decisão de subir conteúdo sensível? Sempre humana, sempre item-a-item.


## O cérebro da diretoria não é mais inteligente. Ele é mais seguro.

Essa é a mensagem final: conforme a empresa cresce, memória sem fronteira vira risco. A diretoria precisa de uma camada separada, privada por padrão ( UX, não versionamento ), com decisão humana item-a-item no sync.
