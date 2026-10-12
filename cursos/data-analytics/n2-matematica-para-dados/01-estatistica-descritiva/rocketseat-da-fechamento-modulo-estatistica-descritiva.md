# 🏆 Fechamento de Módulo — Estatística Descritiva
**Trilha:** Rocketseat — Formação Data Analytics
**Nível:** 2 — Matemática para Dados
**Módulo:** Estatística Descritiva
**Data do fechamento:** 09/10/2026
**Origem:** módulo resgatado do "buraco de contexto" — aulas assistidas antes do uso do notetaker, processadas a partir da transcrição original recuperada (não é reconstrução por memória; ver Core → "Decisões estruturais").
**Quiz oficial da plataforma:** confirmado em 09/10/2026 com **100% (5/5)**.

### 1. Resumo Executivo
O módulo estabelece a porta de entrada de toda a análise de dados: antes de prever qualquer coisa ou tirar qualquer insight, o analista precisa ser capaz de organizar e resumir um conjunto de dados bruto de forma que um valor só já conte a história principal daquele conjunto. É essa a definição e o propósito da Estatística Descritiva — e o módulo constrói esse raciocínio em camadas, da base conceitual até o cálculo prático.

A primeira camada é conceitual: antes de calcular qualquer coisa, é preciso saber **o que** está sendo analisado — se é o todo (população) ou uma parte dele (amostra), e se essa amostra é representativa o suficiente para não distorcer a conclusão. Em seguida, cada coluna de uma tabela precisa ser classificada como variável **qualitativa** (categoria) ou **quantitativa** (permite soma/média) — e o módulo deixa claro que essa classificação depende do **uso** que se faz do dado, não só da sua natureza (o caso da data de nascimento, quantitativa por natureza mas usada como qualitativa ao categorizar por signo, é o exemplo-chave disso).

Só depois dessa base é que entram as três **medidas de tendência central**: a **média** (soma dividida pela quantidade), a **moda** (valor mais frequente) e a **mediana** (valor central de um conjunto **ordenado** — com a regra extra de que, em quantidade par de valores, a mediana é a média dos dois valores centrais). O exercício final do módulo amarra tudo isso na prática: aplicar as três medidas a um mesmo conjunto de dados (acessos diários a um site) e, a partir delas, **interpretar o gráfico** — identificar dias acima/abaixo da média e classificar o comportamento geral dos dados (uniforme, concentrado, ou com picos e vales).

A grande lição para um Analista Júnior: a Estatística Descritiva não é "fazer conta" — é o processo que transforma uma tabela de milhares de linhas em um punhado de números que já permitem decisão rápida. E a média, apesar de ser a medida mais usada, não é 100% confiável sozinha — ela sinaliza sem denunciar instabilidade, o que já antecipa o porquê do próximo módulo do curso (Medidas de Dispersão) existir.

### 2. Glossário Técnico
*Estatística Descritiva:* etapa inicial da análise de dados que resume e organiza um conjunto de dados de forma simples, permitindo visualizar informação e embasar decisão sem interpretar o dado bruto linha a linha.

*População:* o conjunto total que está sendo analisado (ex: todas as pessoas do Brasil). Cada elemento desse conjunto é um indivíduo.

*Amostra:* uma parcela da população, usada quando não é possível ou necessário analisar o todo. Precisa ser representativa — uma amostra pequena ou enviesada compromete a validade da conclusão.

*Variável:* cada coluna de uma tabela de dados, representando uma característica de cada indivíduo (ex: idade, cidade, valor da compra).

*Variável Qualitativa:* representa categorias ou características (ex: nome, sexo). Não permite soma ou média.

*Variável Quantitativa:* representa valores numéricos que indicam quantidade ou medida (ex: idade, matrícula). Permite soma e média — mas o mesmo dado pode virar qualitativo dependendo do uso (ex: categorizar datas de nascimento por signo).

*Média (Aritmética):* soma de todos os valores de um conjunto dividida pela quantidade de valores somados.

*Moda:* o valor que mais se repete em um conjunto de dados. Um conjunto pode ser unimodal, bimodal ou sem moda.

*Mediana:* o valor central de um conjunto de dados **ordenado** (rol). Em quantidade ímpar, é o valor que sobra no meio; em quantidade par, é a média dos dois valores centrais.

*Rol:* a organização de um conjunto de dados em ordem crescente, pré-requisito obrigatório para calcular a mediana (e, mais adiante no curso, quartis).

### 3. Desafio de Fixação (Quiz Interativo)

**Cenário:** Uma analista está avaliando o número de pedidos recebidos por uma loja online ao longo de 9 dias. Os valores registrados foram: 40, 55, 70, 40, 85, 100, 40, 60, 110.

1. Classifique as seguintes colunas de uma tabela de pedidos como variável qualitativa ou quantitativa, justificando cada uma: (a) "Status do pedido" (ex: "Enviado", "Cancelado"); (b) "Valor total do pedido em R$".
2. Calcule a média, a moda e a mediana do número de pedidos recebidos nos 9 dias. Mostre os passos de cada cálculo (lembre-se do rol antes da mediana).
3. No dia seguinte (10º dia), a loja registra 200 pedidos — um valor muito acima de todos os outros. Sem recalcular nada, explique: esse novo dado deve impactar mais a **média** ou a **mediana** do conjunto? Por quê?

### 4. Correção Comentada — Gabarito

**Cenário:** número de pedidos recebidos por uma loja online ao longo de 9 dias — 40, 55, 70, 40, 85, 100, 40, 60, 110.

**Questão 1 — ✅ Correta nas duas alternativas.**
- **(a) Status do pedido → Variável Qualitativa.** Representa uma categoria/estado do pedido ("Enviado", "Cancelado") — não é um valor numérico resultante de contagem ou medição, logo não permite soma nem média.
- **(b) Valor total do pedido em R$ → Variável Quantitativa (Contínua).** Expressa uma quantidade numérica que permite soma e média. A subclassificação **Contínua** (o valor pode assumir qualquer ponto de uma escala, incluindo centavos, em oposição à Discreta, que só assume valores inteiros/contáveis) é um conceito real e corretamente aplicado — mas vale registrar que esse par contínua/discreta **não foi ensinado neste módulo específico** (o módulo cobriu só qualitativa vs. quantitativa). Não é erro: é conhecimento prévio correto, não uma exigência deste fechamento.

**Questão 2 — ✅ Todos os três cálculos corretos, com o método certo.**

*Rol (ordenação crescente — passo obrigatório antes da mediana):*
$$40,\ 40,\ 40,\ 55,\ 60,\ 70,\ 85,\ 100,\ 110$$

*Média (soma de todos os valores ÷ quantidade de valores):*
$$\text{Média} = \frac{40+40+40+55+60+70+85+100+110}{9} = \frac{600}{9} \approx \mathbf{66,67\ pedidos}$$

*Moda (valor que mais se repete):*
$$\text{40 aparece 3 vezes; os demais, 1 vez cada} \implies \text{Moda} = \mathbf{40\ pedidos}$$

*Mediana ($n=9$, ímpar → posição central $= \frac{n+1}{2}$):*
$$\frac{9+1}{2} = 5^{\underline{a}}\ \text{posição do rol}$$
$$40,\ 40,\ 40,\ 55,\ \boxed{60},\ 70,\ 85,\ 100,\ 110 \implies \text{Mediana} = \mathbf{60\ pedidos}$$

Usar a fórmula de posição ($\frac{n+1}{2}$) em vez de só "contar no olho" é exatamente o rigor que escala bem para conjuntos de dados maiores.

**Questão 3 — ✅ Correta e bem argumentada.**
A **média** é sensível a valores extremos porque entra na soma com seu valor exato — um outlier de 200 distorce a soma total e, portanto, puxa a média para cima de forma desproporcional. A **mediana** é robusta a outliers porque depende só da **posição** do dado no rol, não do seu valor absoluto — por isso o enunciado pedia para responder sem recalcular nada.

Como extra (não era exigido, mas correto), a resposta demonstrou o efeito: com o 10º valor (200) inserido no rol, $n$ passa a ser par, e a mediana passa a ser a média entre a 5ª e a 6ª posição (60 e 70):
$$\text{Nova Mediana} = \frac{60+70}{2} = \mathbf{65\ pedidos}$$
Uma variação pequena (60 → 65), bem diferente do salto que a média sofreria com a entrada de 200 — o que reforça exatamente o ponto pedido: o *tamanho* do outlier não importa para a mediana, só a sua *posição* no rol.

**Resultado final: 3 de 3 corretas**, com domínio completo do método (rol → mediana, soma/quantidade → média, frequência → moda) e do raciocínio sobre sensibilidade a outliers. Único ponto a anotar — não um erro, apenas um registro: a distinção **contínua/discreta** é conhecimento correto trazido de fora do módulo, útil para guardar, mas não cobrada por ele.
