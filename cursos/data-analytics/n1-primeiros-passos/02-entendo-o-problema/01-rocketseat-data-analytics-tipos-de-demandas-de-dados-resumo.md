# 📌 Tipos de Demandas em Análise de Dados

### 1. Conceito Central
Este módulo inicia a etapa de "compreensão de negócio" do CRISP-DM — a camada mais importante e, ao mesmo tempo, mais negligenciada da análise de dados: entender exatamente qual pergunta está sendo respondida antes de sair tratando dado ou aplicando técnica. Um executivo nem sempre sabe especificar com clareza o que precisa; parte do papel do analista é lapidar esse pedido até chegar numa pergunta de dados real — errar essa tradução significa responder, com perfeição técnica, a pergunta errada. Para isso, a aula detalha os quatro tipos de demanda em análise de dados (exploratória, descritiva/diagnóstica, preditiva e prescritiva), mostrando como cada um se diferencia pelo momento temporal da pergunta — presente/natureza do dado, passado, futuro previsto, ou futuro recomendado.

### 2. Pontos-chave e Sintaxe
- **Demanda exploratória:** olha para a natureza dos próprios dados, sem comparar passado ou prever futuro — ex: "há outlier aqui?", "qual o mês de venda mínima no ano?". Está diretamente ligada à Análise Exploratória de Dados (EDA) e costuma anteceder as outras demandas, servindo de base para elas.
- **Demanda descritiva:** resume informações e apresenta métricas — é o que já costuma estar pronto em dashboards e relatórios mensais que o executivo já acessa.
- **Demanda diagnóstica:** pergunta "por que isso aconteceu?" — surge quando o dashboard descritivo revela algo (como uma queda de vendas) e o executivo quer a causa. Exige levantar hipóteses (ex: outlier pontual, sazonalidade, questão política, características de uma venda B2B).
- **Demanda preditiva:** estima o que pode acontecer no futuro, geralmente via técnicas como regressão — ex: estimar receita até o fim do ano, ou avaliar a chance de um cliente de banco se tornar inadimplente por similaridade comportamental com outros clientes.
- **Demanda prescritiva:** vai além de prever — recomenda o que fazer com base na previsão (conceito citado como "relatório aumentado", termo trazido pela Gartner). Ex: recomendação de ofertas para um vendedor ou de produtos para um cliente, roteamento em tempo real em apps como Uber/iFood.
- 💡 **Critério prático de distinção citado na aula:** a demanda exploratória não é sobre tempo (passado/futuro), é sobre a natureza do dado; a diagnóstica olha para o passado (o que já aconteceu), a preditiva olha para o futuro (o que pode acontecer), e a prescritiva já parte para a ação (o que fazer a respeito).
- ⚠️ **Ponto de atenção:** uma pergunta pode parecer estar no passado sem ser diagnóstica — o exemplo da aula ("quais produtos têm menor giro de estoque?") soa retrospectivo, mas é exploratória, porque está descrevendo a natureza dos dados, não investigando uma causa.

### 3. 🧠 Raciocínio Lógico
Sequência de reconhecimento do tipo de demanda, conforme ensinado na aula:
- A pergunta é sobre a natureza/composição dos próprios dados (sem comparar com um evento específico)? → **Exploratória**.
- A pergunta pede a causa de algo que já aconteceu (um resultado observado no passado)? → **Diagnóstica**.
- A pergunta pede uma estimativa de algo que ainda vai acontecer? → **Preditiva**.
- A pergunta pede uma recomendação de ação baseada nessa estimativa? → **Prescritiva**.
- A demanda exploratória tende a aparecer primeiro e de forma recorrente, servindo de insumo para as outras três — ela raramente é o pedido final do executivo, mas quase sempre está por trás da preparação do restante da análise.

### 4. Links e Referências Oficiais
*(Aula de conceito/metodologia de negócio, sem termo técnico com documentação oficial correspondente — seção omitida.)*

---
**Salvar como:** `01-rocketseat-data-analytics-tipos-de-demandas-de-dados-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Restam 3 aulas neste módulo ("Entendendo o Problema").