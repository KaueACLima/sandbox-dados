# 📌 Gráfico Boxplot (Diagrama de Caixa)

### 1. Conceito Central
O **boxplot** (ou diagrama de caixa) é uma representação gráfica de um conjunto de dados que permite avaliar rapidamente sua dispersão e destacar valores discrepantes — os chamados **outliers**. Ele é construído inteiramente a partir dos conceitos de mediana e quartil já estudados: a "caixa" do gráfico vai do **Q1** ao **Q3**, com uma linha no meio marcando o **Q2 (mediana)**. Como Q1 e Q3 delimitam 50% centrais dos dados, a caixa representa justamente essa metade central da distribuição. Para além da caixa, o gráfico traça **limites** (bigodes) para cima e para baixo, calculados a partir do tamanho da caixa (a amplitude interquartil); qualquer valor que ultrapasse esses limites é marcado separadamente como **outlier**. A utilidade principal do boxplot é visual: ele evidencia rapidamente se há valores "fora da curva", algo que a média sozinha pode mascarar, já que valores muito altos ou muito baixos distorcem a média para um lado ou outro.

### 2. Pontos-chave e Sintaxe
- **Boxplot / diagrama de caixa / block spot:** representação gráfica (horizontal ou vertical) que mostra a dispersão dos dados e evidencia outliers.
- **Outlier:** valor discrepante, fora do padrão do restante dos dados — costuma ser representado por um asterisco ou ponto isolado no gráfico. Geralmente é descartado na análise, ou investigado para checar se houve erro na coleta.
- **Construção da caixa:**
  - Organizar os dados (rol).
  - Achar a mediana → **Q2** (linha central da caixa).
  - Achar o valor mediano da primeira metade dos dados → **Q1** (uma extremidade da caixa).
  - Achar o valor mediano da segunda metade dos dados → **Q3** (outra extremidade da caixa).
  - Entre Q1 e Q3 está **50%** dos dados (cada quartil representa 25%).
- **Tamanho da caixa = amplitude interquartil = Q3 − Q1.**
- **Limites (bigodes), em termos de "uma caixa e meia":**
  - Limite superior teórico = Q3 + 1,5 × (Q3 − Q1)
  - Limite inferior teórico = Q1 − 1,5 × (Q3 − Q1)
- **Regra de ajuste do limite pelos dados reais** (ponto crítico da aula): o limite teórico calculado pela fórmula **não é necessariamente** o limite final.
  - Se o **maior valor real** dos dados for **menor** que o limite superior teórico, é esse maior valor real que assume o papel de limite superior (o bigode só vai até onde existe dado de fato).
  - Se o **maior valor real** for **maior** que o limite superior teórico, o limite superior fica no valor teórico, e esse valor real que o ultrapassa vira um **outlier**.
  - O mesmo raciocínio se aplica espelhado ao limite inferior (comparando com o **menor valor real** dos dados).
- 💡 **Dica:** o professor enfatiza não decorar a fórmula, e sim entender o conceito — "pegar o tamanho de uma caixa e meia e jogar pra frente (limite superior) e pra trás (limite inferior)" a partir das bordas da caixa (Q3 e Q1, respectivamente).

### 3. 🧠 Raciocínio Lógico
- Organize os dados (rol) → ache Q2 (mediana) → ache Q1 (mediana da primeira metade) → ache Q3 (mediana da segunda metade).
- Calcule o tamanho da caixa: amplitude interquartil = Q3 − Q1.
- Calcule os limites teóricos: LS_teórico = Q3 + 1,5 × amplitude; LI_teórico = Q1 − 1,5 × amplitude.
- Compare o LS_teórico com o maior valor real dos dados:
  - Maior valor real ≤ LS_teórico? → o limite superior final é o maior valor real.
  - Maior valor real > LS_teórico? → o limite superior final é o LS_teórico, e o maior valor real é um outlier.
- Repita o mesmo raciocínio (espelhado) para o limite inferior, comparando com o menor valor real dos dados.
- Qualquer valor além dos limites finais (para cima ou para baixo) é marcado no gráfico como outlier.
- **Exemplo numérico usado na aula** (valores ilustrativos, não de um dataset real): maior valor = 100, Q3 = 70, amplitude = 30 → LS_teórico = 70 + 1,5×30 = 115. Como 100 < 115, o limite superior final vira 100 (o próprio maior valor). Se o maior valor real fosse 135 (> 115), o limite superior final ficaria em 115, e o 135 seria classificado como outlier.

---
**Salvar como:** `07-rocketseat-da-medidas-de-posicao-grafico-boxplot-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Resta 1 aula neste módulo.