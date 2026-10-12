# 📌 Recap do Módulo: Princípios Gerais da Análise de Dados

### 1. Conceito Central
Esta aula fecha o módulo "O Trabalho de um Analista de Dados" consolidando os conceitos vistos e trazendo alguns princípios que devem guiar qualquer trabalho com dados, independente da metodologia ou ferramenta usada. O fio condutor de todos os pontos é o mesmo: dado isolado não tem valor — ele só serve quando conectado a um contexto de negócio e usado para apoiar uma decisão real. Isso vale tanto para a entrega final de uma análise quanto para a interpretação de estatísticas básicas, que podem enganar se olhadas sem entender o comportamento completo dos dados.

### 2. Pontos-chave e Sintaxe

#### Dado é meio, não fim
- 💡 **Dica central da aula:** entregar um KPI ou indicador não é, por si só, o objetivo do trabalho do analista — o dado precisa servir como meio para uma tomada de decisão real. É comum cair na armadilha de achar que "entreguei o número, acabou"; o trabalho só está completo se aquele número for útil para alguém decidir algo.

#### Os quatro tipos de análise de dados
- **Descritiva** → o que aconteceu (mais simples de realizar).
- **Diagnóstica** → por que aconteceu.
- **Preditiva** → o que tende a acontecer.
- **Prescritiva** → o que fazer diante disso (a mais complexa).
- A complexidade e o tempo de execução crescem nessa ordem — o tipo de análise pedido por um executivo depende diretamente da pergunta de negócio feita.

#### Níveis de estruturação do dado
- **Estruturado:** formato tabular (linhas/colunas) — o mais fácil de trabalhar.
- **Semi-estruturado:** formatos como JSON, logs de sistema — meio-termo entre tabular e livre.
- **Não estruturado:** textos, vídeos, áudios — quanto mais desorganizado, mais difícil a análise.

#### Estatística: cuidado com média, mediana e moda
- ⚠️ **Ponto de atenção:** média, mediana e moda não são intercambiáveis — a métrica escolhida pode distorcer completamente a leitura dos dados. A aula usa um exemplo: numa sala com 10 jovens (18–25 anos) e uma pessoa bem mais velha (outlier), a média de idade do grupo pode subir a ponto de sugerir, para quem só vê o número, que a sala tem bastante gente mais velha — quando isso não reflete a realidade da maioria.
- 🔎 **Observação:** por isso é preciso "se tornar amigo dos dados" — olhar para outliers, valor mínimo, valor máximo e o comportamento geral da distribuição, não só para um único número resumo.

### 3. 🏗️ Arquitetura / Diagrama Lógico
Ciclo de vida do dado, desde a origem até a decisão final:

```
[Dado gerado] -> [Coletado] -> [Transformado/estruturado] -> [Carregado]
      -> chega "na mão" do analista para análise e modelagem
      -> [Geração de visualização] -> [Tomada de decisão]
```

A metodologia usada para tratar o dado (CRISP-DM, Lean, A/B Test etc.) acontece dentro dessa etapa de "análise e modelagem", mas nunca pode se afastar da área de negócio — dado sem contexto de negócio é um dado que não pode ser usado em todo o seu potencial.

### 4. Links e Referências Oficiais
*(Aula de recap conceitual/carreira, sem termo técnico novo que demande documentação oficial própria — seção omitida.)*

---
**Salvar como:** `04-rocketseat-data-analytics-base-conceitual-de-dados-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Módulo "O Trabalho de um Analista de Dados" completo (4/4 aulas). Falta só o outro módulo do Nível 1, "Entendendo o Problema" (4 aulas), para fechar o Nível inteiro.