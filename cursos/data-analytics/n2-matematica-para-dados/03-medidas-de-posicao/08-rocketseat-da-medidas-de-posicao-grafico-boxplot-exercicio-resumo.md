# 📌 Gráfico Boxplot — Exercício Prático (Notas de 40 Alunos)

### 1. Conceito Central
Esta aula aplica, passo a passo, toda a construção de um boxplot a um exercício concreto: as notas de 40 alunos. O fluxo reforça a sequência já vista — organizar os dados (rol), achar a mediana (Q2), dividir cada metade para achar Q1 e Q3, calcular a amplitude interquartil (Q3 − Q1), calcular os limites teóricos ("uma caixa e meia" para cada lado) e, por fim, **ajustar** esses limites pelos valores reais do conjunto de dados — sempre usando o menor entre o limite teórico e o maior/menor dado real, conforme o lado. O exercício reforça concretamente a regra vista na aula anterior: o limite final de um boxplot nem sempre é o valor calculado pela fórmula.

### 2. Pontos-chave e Sintaxe
- **Passo a passo aplicado ao exercício:**
  1. Organizar as notas em ordem crescente (rol) — 40 valores, de 0 (menor) a 100 (maior).
  2. Achar a **mediana (Q2)**: como a quantidade é par (40), é a média entre o 20º e o 21º valor.
  3. Achar **Q1**: média entre o 10º e o 11º valor (mediana da primeira metade de 20 valores).
  4. Achar **Q3**: média entre o 20º e o 21º valor **da segunda metade** (equivalente às posições 30ª e 31ª do conjunto total).
  5. Calcular a **amplitude interquartil**: Q3 − Q1.
  6. Calcular os **limites teóricos**: LS_teórico = Q3 + 1,5 × amplitude; LI_teórico = Q1 − 1,5 × amplitude.
  7. **Ajustar pelos dados reais:** comparar cada limite teórico com o maior/menor valor real do conjunto, usando o mais restritivo dos dois (ver regra da aula anterior).
  8. Qualquer valor além do limite final ajustado é marcado como **outlier**.

### 3. 🧠 Raciocínio Lógico (exercício resolvido)
- Conjunto: 40 notas organizadas em ordem crescente, menor nota = 0, maior nota = 100.
- **Q2 (mediana):** média entre o 20º e o 21º valor, ambos = 70 → Q2 = (70 + 70) / 2 = **70**.
- **Q1:** média entre o 10º e o 11º valor, ambos = 50 → Q1 = (50 + 50) / 2 = **50**.
- **Q3:** média entre o 20º e o 21º valor da segunda metade, ambos = 80 → Q3 = (80 + 80) / 2 = **80**.
- **Amplitude interquartil:** Q3 − Q1 = 80 − 50 = **30**.
- **Limite superior teórico:** Q3 + 1,5 × 30 = 80 + 45 = **125**.
  - Comparando com o maior valor real (100): como 100 < 125, o **limite superior final é 100** (o próprio maior valor do conjunto).
  - Como não há nenhum valor acima de 100, não há outlier no lado superior.
- **Limite inferior teórico:** Q1 − 1,5 × 30 = 50 − 45 = **5**.
  - Comparando com o menor valor real (0): como 0 está **abaixo** de 5, o **limite inferior final é 5**, e o valor **0 é classificado como outlier**.
- **Resultado final:** caixa entre Q1 = 50 e Q3 = 80, mediana em Q2 = 70, limite superior = 100 (sem outliers acima), limite inferior = 5 (com um outlier: a nota 0).

---
**Salvar como:** `08-rocketseat-da-medidas-de-posicao-grafico-boxplot-exercicio-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Esta foi a última aula do módulo (8/8) — nota informativa, não uma ação.