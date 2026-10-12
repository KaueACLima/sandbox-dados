# 🏆 Fechamento de Módulo e Teste de Fixação — Medidas de Posição
**Trilha:** Rocketseat — Formação Data Analytics
**Nível:** 2 — Matemática para Dados
**Módulo:** Medidas de Posição
**Data do fechamento:** 10/10/2026
**Origem:**  módulo resgatado do "buraco de contexto" — aulas assistidas antes do uso do notetaker, processadas a partir da transcrição original recuperada (não é reconstrução por memória; ver Core → "Decisões estruturais").
**Quiz oficial da plataforma:** confirmado em 10/10/2026 com **100% (5/5)**.

### 1. Resumo Executivo
Medidas de posição generalizam uma ideia que você já conhecia pela mediana: dividir o conjunto de dados ordenado em partes iguais para localizar valores específicos dentro da distribuição. O módulo expandiu essa lógica em três direções — quartil (4 partes), decil (10 partes) e, com mais detalhe, percentil (100 partes) — e mostrou que o método de cálculo é sempre o mesmo em essência: primeiro achar a **posição** (via uma fração K multiplicada pelo total de dados), depois achar o **valor** nessa posição, seja direto numa lista simples, seja por interpolação numa tabela de intervalos (usando limite inferior, frequência acumulada anterior, frequência do intervalo e amplitude).

A aplicação prática mais importante dessa teoria apareceu em dois destinos convergentes: a **amplitude interquartil** (Q3 − Q1), uma medida de dispersão mais robusta que a amplitude total porque ignora os 25% mais extremos de cada lado; e o **gráfico boxplot**, que usa Q1/Q2/Q3 para desenhar a "caixa" central dos dados e usa 1,5× a amplitude interquartil para demarcar limites além dos quais um valor é considerado **outlier**. O ponto mais sutil do módulo — e o que mais vale a pena levar para o dia a dia como Analista Júnior — é que o limite do boxplot nunca é cego à fórmula: ele sempre é ajustado pelo valor real mínimo/máximo do conjunto, nunca ultrapassando os dados que de fato existem. Essa disciplina de "não confiar só na média, olhar a distribuição inteira" é exatamente o que sustenta a próxima etapa prática da trilha (Tratando os Dados, N4), onde outliers reais vão precisar ser identificados antes de qualquer limpeza ou modelagem.

### 2. Glossário Técnico
- **Medida de posição (separatriz):** estatística que divide o conjunto de dados ordenado em partes iguais, localizando um valor específico dentro da distribuição.
- **Quartil (Q1, Q2, Q3):** divide os dados em 4 partes de 25% cada; Q2 é a mediana.
- **Decil:** divide os dados em 10 partes de 10% cada.
- **Percentil (centil):** divide os dados em 100 partes de 1% cada; P25=Q1, P50=Q2, P75=Q3.
- **Rol:** os dados organizados em ordem crescente — passo obrigatório antes de calcular qualquer medida de posição.
- **Frequência acumulada (Fac) / frequência do intervalo (Fi):** usados na fórmula de interpolação de quartil/percentil para dados agrupados em intervalos de classe.
- **Amplitude interquartil (AIQ/IQR):** Q3 − Q1; mede a dispersão da metade central dos dados, ignorando os 25% mais extremos de cada lado.
- **Boxplot (diagrama de caixa):** gráfico que representa Q1, Q2 (mediana) e Q3 como uma caixa, com limites de "uma caixa e meia" (1,5×IQR) para cada lado.
- **Outlier:** valor que ultrapassa os limites do boxplot — discrepante do restante dos dados, geralmente investigado ou descartado na análise.
- **Limite superior/inferior do boxplot:** calculado por Q3 + 1,5×IQR (ou Q1 − 1,5×IQR), mas sempre **ajustado** para não ultrapassar o maior/menor valor real do conjunto.

### 3. Desafio de Fixação (Quiz Interativo)

**Questão 1 — Cálculo direto**
Uma pesquisa de preços (em reais) de 12 produtos de uma loja já está organizada em rol:
`12, 15, 15, 18, 20, 22, 25, 28, 30, 35, 40, 50`
Calcule Q1, Q2 (mediana) e Q3 desse conjunto.

**Questão 2 — Amplitude interquartil e boxplot**
Usando os valores de Q1 e Q3 que você encontrou na Questão 1, calcule a amplitude interquartil e o limite superior teórico (Q3 + 1,5 × amplitude). O maior valor do conjunto (R$ 50) ficaria dentro ou fora desse limite? O que isso significa para a construção do boxplot desse conjunto?

**Questão 3 — Posição em dados agrupados**
Numa pesquisa com 50 pessoas (dados agrupados em intervalos de idade, frequência acumulada final = 50), você quer encontrar o percentil 40 (P40). Qual é a posição (o "quantos-ésimo valor") que você precisaria localizar na tabela de frequência acumulada para montar essa conta?

### 4. Correção Comentada

**Questão 1 — ✅ Correto.**
Conjunto ordenado (N=12, par): `12, 15, 15, 18, 20, 22, 25, 28, 30, 35, 40, 50`.
- **Q2 (mediana):** N par → média dos termos centrais (6º e 7º): Q2 = (22 + 25) / 2 = **23,5**.
- **Q1:** mediana da 1ª metade (6 valores: `12, 15, 15, 18, 20, 22`) → média do 3º e 4º termo dessa metade: Q1 = (15 + 18) / 2 = **16,5**.
- **Q3:** mediana da 2ª metade (6 valores: `25, 28, 30, 35, 40, 50`) → média do 3º e 4º termo dessa metade: Q3 = (30 + 35) / 2 = **32,5**.
- *Por que está certo:* é o mesmo método ensinado na aula de amplitude interquartil — como N=12 é par, não há valor central a excluir; a lista se divide em duas metades de 6, cada uma tratada como seu próprio sub-problema de mediana.

**Questão 2 — ✅ Correto.**
- AIQ = Q3 − Q1 = 32,5 − 16,5 = **16**.
- Limite superior teórico = Q3 + 1,5 × AIQ = 32,5 + 24 = **56,5**.
- O maior valor real (50) é **menor** que 56,5 → fica **dentro** do limite.
- *Significado para o boxplot:* como nenhum valor ultrapassa o limite teórico, não há outlier superior — o bigode direito do boxplot se estende até o próprio valor máximo real (50), e não até o 56,5 calculado pela fórmula. É exatamente a regra de ajuste vista nas aulas de boxplot: o limite final nunca ultrapassa o dado real existente.

**Questão 3 — ✅ Correto.**
- Fórmula de posição: Posição = (k × N) / 100, com k=40 e N=50.
- Posição = (40 × 50) / 100 = **20ª posição**.
- *Por que está certo:* é a mesma lógica de K × ΣFi usada para quartil, só trocando a fração (1/4, 1/2, 3/4) pelo equivalente em percentil (k/100). O próximo passo, não pedido aqui, seria localizar em qual intervalo da tabela de frequência acumulada essa 20ª posição cai, e aplicar a fórmula de interpolação (Li + ((Posição − Fac_anterior)/Fi) × h) para achar o valor de P40.

**Resultado: 3/3 — módulo com domínio sólido da teoria e do cálculo prático de quartil, percentil, amplitude interquartil e boxplot.**
```