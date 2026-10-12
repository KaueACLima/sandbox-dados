# 🏆 Fechamento de Módulo e Teste de Fixação
**Trilha:** Rocketseat — Formação Data Analytics
**Nível:** 1 — Primeiros Passos
**Módulo:** Entendendo o Problema
**Data do fechamento:** 08/10/26

### 1. Resumo Executivo
Este módulo cobre a primeira etapa prática do CRISP-DM — compreensão do negócio — e mostra por que ela é a etapa mais crítica e mais frequentemente subestimada da análise de dados: se a pergunta entendida está errada, nenhuma execução técnica posterior corrige isso. A primeira aula classifica as demandas que chegam ao analista em quatro tipos (exploratória, diagnóstica, preditiva, prescritiva), ensinando a reconhecer cada uma pelo momento temporal da pergunta — a exploratória olha a natureza do dado, a diagnóstica olha o passado, a preditiva estima o futuro, a prescritiva recomenda ação. A segunda aula ensina a traduzir uma pergunta de negócio vaga ("como melhorar a retenção?") em uma pergunta de dados mensurável, usando o método SMART como checklist e alertando para o erro clássico de confundir correlação com causalidade.

A terceira aula completa essa tradução com a identificação de stakeholders — as pessoas que precisam ser consultadas, informadas ou que aprovam a análise — usando a matriz RACI como ferramenta de mapeamento. A quarta e última aula adiciona uma camada de maturidade de carreira: saber priorizar demandas concorrentes, via duas lentes complementares (esforço × impacto, e must/should/could/won't have). A grande lição que conecta tudo: antes de qualquer linha de código ou consulta SQL, o trabalho real do analista é garantir que a pergunta certa foi feita, para a pessoa certa, da forma certa — e saber dizer não (ou "depois") para o que não merece prioridade agora.

### 2. Glossário Técnico
*Demanda exploratória:* análise sobre a natureza dos próprios dados (sem comparar passado/futuro) — ex: identificar outliers, valores nulos, ou a composição geral de uma base.

*Demanda diagnóstica:* pergunta que busca a causa de algo que já aconteceu no passado (ex: "por que a venda caiu?").

*Demanda preditiva:* estimativa de algo que ainda vai acontecer, geralmente via técnicas estatísticas como regressão.

*Demanda prescritiva:* recomendação de ação com base numa previsão — vai além de prever, orienta o que fazer.

*Pergunta de negócio vs. pergunta de dados:* a primeira é estratégica e aberta; a segunda é mensurável, específica e aponta para uma hipótese testável — o trabalho do analista é traduzir uma na outra.

*Método SMART (aplicado à pergunta de dados):* checklist de Específica, Mensurável, Atingível, Relevante e Temporal, usado para validar se uma pergunta de dados está bem formulada.

*Correlação ≠ causalidade:* dois eventos relacionados no tempo não implicam que um causa o outro — erro comum ao formular hipóteses de negócio.

*Stakeholder:* qualquer pessoa envolvida na análise, seja como responsável, aprovador, consultado ou apenas informado do resultado.

*Matriz RACI:* framework que classifica cada stakeholder como Responsável, Aprovador (Accountable), Consultado ou Informado.

*Quick win:* demanda de baixo esforço e alto impacto, ideal para gerar valor rápido no início de um projeto ou numa nova posição.

*Matriz esforço × impacto / MoSCoW (must/should/could/won't have):* duas ferramentas complementares para priorizar demandas concorrentes de dados.

### 3. Desafio de Fixação (Quiz Interativo)

**Cenário:** Você é analista júnior numa empresa de assinatura de streaming de música. Numa mesma semana, chegam para você três pedidos: (A) o CMO pergunta "por que nosso app perdeu assinantes no mês passado?"; (B) um colega de produto pede, "só por curiosidade", um gráfico de quantos usuários ouvem podcast às segundas-feiras; (C) a diretoria define, no planejamento anual, migrar toda a base de dados de usuários para uma nova arquitetura de data lake ao longo do ano.

1. Classifique cada um dos três pedidos (A, B, C) na matriz esforço × impacto (quick win / projeto estratégico / tarefa complexa / tarefa corriqueira) e justifique brevemente cada escolha.
2. O pedido (A) do CMO ainda é uma pergunta de negócio, não uma pergunta de dados. Reescreva-o como uma pergunta de dados, aplicando pelo menos três dos cinco critérios do SMART de forma explícita (diga quais critérios você está aplicando e como).
3. Para a análise do pedido (A), identifique pelo menos dois stakeholders diferentes (além do CMO) que você provavelmente precisaria envolver, e classifique cada um deles na matriz RACI (Responsável, Aprovador, Consultado ou Informado), justificando a escolha.

### 4. Correção Comentada

**Questão 1 — ⚠️ Duas corretas, uma com mistura de categoria.**
- **Pedido B** (colega, curiosidade) = ✅ Tarefa corriqueira, exatamente como a aula descreve: baixo esforço, baixo impacto, motivada por curiosidade pontual.
- **Pedido C** (diretoria, migração de data lake) = ✅ Projeto estratégico, correto — alto esforço, alto impacto, definido em planejamento anual. Único cuidado: o texto menciona "(Tarefa Complexa)" entre parênteses — tarefa complexa é a categoria de alto esforço + **baixo** impacto, categoria diferente; não se aplica aqui, já que o impacto é alto.
- **Pedido A** (CMO, queda de assinantes) = ⚠️ A matriz da aula é binária em cada eixo (baixo/alto esforço × baixo/alto impacto) — não existe categoria "quick win a médio esforço". Quick win, por definição, é baixo esforço. Dado o cenário (análise urgente, mas usando dados que já existem, sem pipeline novo), quick win é defensável — mas a classificação final precisa escolher um lado do eixo, sem meio-termo.

**Questão 2 — ✅ Correta.**
A pergunta reformulada aplica S, M e T de forma clara e explícita, exatamente como pedido (pelo menos 3 dos 5 critérios). Boa especificação de segmento (assinantes premium, Brasil) e recorte temporal (setembro de 2026) — é o tipo de pergunta de dados que já nasce acionável.

**Questão 3 — ✅ Correta.**
CMO como Aprovador, Engenheiro de Dados/DBA e Gerente de Atendimento como Consultados, e o próprio analista como Responsável — todos com justificativa coerente com os papéis descritos na aula.

**Resultado:** 2 de 3 completamente corretas (Q2, Q3), 1 com acerto parcial (Q1 — raciocínio certo, mas categorização final inconsistente). Vale fixar: a matriz esforço × impacto não tem meio-termo — force a escolha binária em cada eixo antes de nomear a categoria.

---
**Nota de origem:** este módulo faz parte do "buraco de contexto" registrado no Core (aulas assistidas via gem do Gemini, antes do uso do notetaker). As transcrições originais foram recuperadas e processadas normalmente — não houve reconstrução por memória.
