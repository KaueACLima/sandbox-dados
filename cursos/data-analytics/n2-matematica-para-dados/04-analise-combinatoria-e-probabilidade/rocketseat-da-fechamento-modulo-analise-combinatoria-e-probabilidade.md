# 🏆 Fechamento de Módulo e Teste de Fixação — Análise Combinatória e Probabilidade

> Rocketseat · Data Analytics · Nível 2 (Matemática para Dados) · 13 aulas · fechado em 20/10/2026 · quiz oficial do módulo 100% (5/5) · revisão de 30 dias a partir de 19/11/2026.

### 1. Resumo Executivo
O módulo tem duas metades que se encaixam. A primeira ensina a **contar possibilidades sem listá-las uma a uma**. O ponto de partida é o **Princípio Fundamental da Contagem (PFC)**: o conectivo **E** vira multiplicação e o conectivo **OU** vira soma. Dele nasce o **fatorial** (n × (n−1) × ... × 1) e, em cima dele, três técnicas que dependem de uma única pergunta: **a ordem importa?** Se importa e os elementos são todos escolhidos, é **permutação simples** (n!). Se importa e só uma parte é escolhida, é **arranjo simples** (n! / (n−p)!). Se a ordem não importa, é **combinação simples**, que é o arranjo dividido por p! para eliminar as ordens repetidas (n! / [p! × (n−p)!]). O professor insistiu que as fórmulas são atalho: tudo se resolve só com o PFC, e o essencial é interpretar o problema para "não trabalhar com achismo".

A segunda metade usa essa base para lidar com **incerteza**. **Probabilidade** é a chance de um evento acontecer, sempre positiva e entre 0 e 1 (ou 0% e 100%). Para calculá-la, define-se o **espaço amostral** (tudo o que pode acontecer) e o **evento** (o que se quer), e divide-se: `P(E) = n(E) / n(S)`. A aula também separa os **tipos de probabilidade** pela origem do número (clássica = lógica matemática, empírica = dados reais, subjetiva = intuição) e classifica os eventos em certo, impossível e complementares. A aula do funil de e-mail mostrou que CTR, conversão e retenção são probabilidades. A última aula fechou com a **probabilidade condicional**, em que a condição ("entre os que clicaram", "sabendo que colocou no carrinho") **reduz o espaço amostral** e muda o denominador.

A grande lição para o dia a dia do Analista Júnior é fazer três perguntas antes de qualquer conta: o problema liga as escolhas por **E** ou por **OU**? A **ordem importa**? **Qual é o meu espaço amostral**, o total ou só o grupo da condição? Acertar essas perguntas importa mais do que decorar fórmula, já que o cálculo em si pode ser delegado a um programa.

> ⚠️ **Lacuna registrada:** o quiz oficial do módulo cobrou dois assuntos que **não apareceram nas 13 aulas resumidas**: permutação de uma palavra com letra repetida (a aula de permutação simples só tratou elementos distintos) e frequência absoluta em tabela de agrupamento de dados. O quiz foi acertado, mas esses pontos não têm base nos resumos deste módulo.

### 2. Glossário Técnico
- **Princípio Fundamental da Contagem (PFC):** método para contar possibilidades sem listá-las. Divide-se em **multiplicativo** (escolhas juntas, conectivo **E** → multiplica) e **aditivo** (escolhas alternativas, conectivo **OU** → soma).
- **Fatorial (n!):** produto de n por todos os seus antecessores até 1 (4! = 4 × 3 × 2 × 1 = 24). Convenção da aula: 0! = 1. Em divisões, corta-se o fatorial igual em cima e embaixo.
- **Permutação simples:** mudar a ordem de n elementos **distintos**; resultado n!.
- **Arranjo simples:** escolher p entre n elementos **com a ordem importando**, sem repetição. Fórmula: n! / (n−p)!.
- **Combinação simples:** escolher p entre n elementos **com a ordem sem importância**. Fórmula: n! / [p! × (n−p)!]. É o arranjo dividido por p! para eliminar os casos repetidos.
- **Espaço amostral (S ou Ω):** conjunto de todos os resultados possíveis; é o denominador da probabilidade (ex.: dado → {1, 2, 3, 4, 5, 6}).
- **Evento (E):** subconjunto do espaço amostral, o que se quer que ocorra; são os casos favoráveis (numerador). Pode ser **certo** (E = S), **impossível** (E = ∅) ou **complementar** (união = S e interseção vazia).
- **Probabilidade P(E):** chance de um evento ocorrer, `n(E) / n(S)`. Fica entre 0 e 1, nunca é negativa e deve ser apresentada na fração mais simples ou em porcentagem. Escala: 0 = impossível, 0,25 = improvável, 0,5 = chance igual, 0,75 = provável, 1 = certeza.
- **Tipos de probabilidade:** **clássica** (lógica matemática, ex.: sorteio), **empírica** (dados reais já observados) e **subjetiva** (intuição/experiência, sem levantamento).
- **Probabilidade condicional, P(A | B):** probabilidade de A acontecer dado que B já aconteceu. A condição reduz o espaço amostral ao grupo de B.

### 3. Desafio de Fixação (Quiz Interativo)

**Questão 1 — Escolher entre somar e multiplicar**
Uma loja vai disparar uma campanha por **um único canal**: **ou** e-mail (3 modelos de mensagem), **ou** SMS (2 modelos), **ou** WhatsApp (4 modelos). Além disso, cada disparo vai para **um** de 2 públicos (clientes novos ou recorrentes). Quantas ações diferentes de campanha (canal + modelo + público) a loja consegue montar? Explique em qual parte você somou e em qual multiplicou, e por quê.

**Questão 2 — A ordem importa?**
Você testou 7 assuntos de e-mail diferentes.
- (a) Você quer indicar o **1º e o 2º melhores** assuntos, nessa ordem. De quantas formas isso pode acontecer?
- (b) Agora você quer apenas **escolher 3 assuntos** para um novo teste, sem ordem entre eles. De quantas formas isso pode acontecer?
Para cada item, diga qual técnica usou (permutação, arranjo ou combinação) e por que a ordem importa ou não.

**Questão 3 — Probabilidade condicional**
Um time de atendimento acompanhou **800 clientes**. **200** abriram chamado de suporte e, desses, **50** cancelaram o contrato. Entre os **600** que não abriram chamado, **30** cancelaram.
- (a) Qual a probabilidade de cancelar **entre os que abriram chamado**?
- (b) Qual a probabilidade de cancelar **entre os que não abriram chamado**?
- (c) Qual grupo tem maior chance de cancelar, e qual é o espaço amostral usado em cada item?
- (d) Esse número é uma probabilidade clássica, empírica ou subjetiva? Por quê?