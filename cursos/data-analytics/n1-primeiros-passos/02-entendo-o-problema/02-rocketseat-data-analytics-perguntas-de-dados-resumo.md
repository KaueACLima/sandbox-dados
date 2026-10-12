# 📌 Perguntas de Negócio vs. Perguntas de Dados

### 1. Conceito Central
Uma demanda de negócio raramente chega pronta para virar análise — quem pede (o stakeholder) nem sempre conhece dados, então formula a pergunta de forma estratégica e aberta demais ("como podemos melhorar nossa retenção de clientes?"). Cabe ao analista traduzir essa pergunta de negócio em uma **pergunta de dados**: específica, mensurável, baseada em fato e que aponte para uma hipótese testável. Sem essa tradução, a demanda fica ampla demais para ser trabalhada — tem dezenas de caminhos possíveis e nenhum ponto de partida claro. A aula também alerta para um risco paralelo dessa tradução malfeita: confundir correlação com causalidade, o que pode levar a "resolver" um sintoma errado em vez da causa raiz do problema.

### 2. Pontos-chave e Sintaxe
- Pergunta de negócio = estratégica, focada no objetivo final da empresa, mas vaga demais para ser respondida diretamente (ex: "nossos anúncios estão funcionando?").
- Pergunta de dado = mensurável, específica, baseada em fato, aponta para uma hipótese (ex: "qual a taxa de conversão por canal de aquisição nos últimos três meses?").
- Passo a passo citado para refinar uma pergunta de negócio em pergunta de dados: especificar o objetivo (o que exatamente se quer descobrir), definir uma métrica/KPI mensurável, estabelecer um recorte temporal, e considerar segmentações relevantes (região, canal, tipo de cliente).
- **Método SMART**, aplicado à pergunta de dados: **E**specífica (clara e bem definida), **M**ensurável (dá para quantificar a resposta), **A**tingível (os dados necessários realmente existem e estão disponíveis), **R**elevante (a resposta de fato ajuda na tomada de decisão, sem atacar só um efeito colateral), **T**emporal (cobre um período de tempo adequado).
- ⚠️ **Ponto de atenção:** uma pergunta de negócio pode parecer resolvível mas falhar no critério "Atingível" — não adianta formular uma ótima pergunta de dados se o dado necessário simplesmente não existe ou não está acessível.
- 💡 **Dica prática:** antes de aceitar a primeira hipótese causal, verifique se não é só uma correlação — a aula usa o exemplo clássico de "mais sorvete vendido = mais ataques de tubarão": ambos aumentam no verão, mas um não causa o outro. **Correlação não implica causalidade.**
- Exemplo de armadilha real citado: identificar que clientes de um produto X têm mais churn e concluir que o produto X é o problema, quando na verdade esses clientes já vinham insatisfeitos de um produto anterior (Y) — descontinuar o produto X seria atacar o sintoma errado.
- Exemplos de pares pergunta de negócio → pergunta de dados refinada trabalhados na aula: "nosso app é popular?" → "qual a taxa de retenção de usuários do app nos últimos 3 meses e como ela se compara ao benchmark do setor?"; "nossos clientes gostam do nosso suporte?" → "qual o NPS por canal de atendimento nos últimos 6 meses e quais os principais motivos de reclamação?"; "nosso e-mail marketing está trazendo clientes?" → "qual a taxa de abertura, clique e conversão das campanhas de e-mail enviadas nos últimos 3 meses?".

### 3. 🧭 Implicações Práticas
- Antes de iniciar qualquer análise, sempre perguntar: "isso é uma pergunta de negócio ou já é uma pergunta de dados?" — se ainda for vaga, ela precisa passar pelo processo de refinamento (objetivo → métrica → recorte temporal → segmentação) antes de qualquer trabalho técnico começar.
- Rodar o checklist SMART mentalmente em qualquer pergunta de dados formulada, antes de considerar o escopo "fechado" para análise.
- Desconfiar de conclusões causais rápidas — vale o hábito de perguntar "isso é causa ou só coincide no tempo com outra coisa?" antes de recomendar uma ação baseada num padrão observado.
- Internalizar o vocabulário de negócio citado (churn, NPS, ROI, taxa de conversão, CAC) é parte do trabalho do analista júnior — a aula reforça que isso exige pesquisa/anotação contínua de quem vem sem bagagem corporativa prévia.

### 4. Links e Referências Oficiais
*(Aula de metodologia de negócio, sem termo técnico com documentação oficial correspondente — seção omitida.)*

---
**Salvar como:** `02-rocketseat-data-analytics-perguntas-de-dados-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Restam 2 aulas neste módulo ("Entendendo o Problema").