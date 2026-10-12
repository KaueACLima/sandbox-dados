# 📌 Exercício de Recapitulação: Média, Mediana, Moda e Leitura de Gráfico

### 1. Conceito Central
Aula de exercício prático que recapitula média, mediana e moda aplicando-as a um conjunto real de dados: o número de acessos diários a um site ao longo de 10 dias, representado em um gráfico. Além de calcular as três medidas, a aula também trabalha a **leitura analítica do gráfico** — identificar o dia de maior acesso, os dias abaixo da média, e classificar o comportamento geral dos dados (uniforme, concentrado, ou com picos e vales) — encerrando o bloco inicial de Estatística Descritiva.

### 2. Pontos-chave e Sintaxe

#### Dados do exercício
- Gráfico com acessos diários ao longo de 10 dias. Valores citados explicitamente: dia 1 = 150 acessos, dia 2 = 200 acessos, dia 8 = 400 acessos (o maior valor do conjunto).
- Conjunto completo de valores usado nos cálculos (10 valores, já em ordem crescente): 150, 150, 200, 200, 200, 200, 250, 300, 350, 400.

#### Cálculo da média
```
# Soma de todos os 10 valores:
150 + 150 + 200 + 200 + 200 + 200 + 250 + 300 + 350 + 400 = 2400

# Divisão pela quantidade de valores (10):
2400 / 10 = 240

# Média de acessos diários = 240
```

#### Cálculo da mediana
- Dados já estavam em ordem crescente (rol já feito).
- Quantidade par (10 valores) → não há um único valor central; pega-se a média dos dois valores centrais (5º e 6º da lista ordenada).
```
# Os dois valores centrais (posições 5 e 6): 200 e 200
(200 + 200) / 2 = 400 / 2 = 200

# Mediana = 200
```

#### Moda
- Olhando a frequência dos valores: o número 200 aparece 4 vezes — mais que qualquer outro.
- **Moda = 200**.

#### Leitura analítica do gráfico
- **Dia de maior acesso:** dia 8, com 400 acessos.
- **Dias abaixo da média (240):** 6 dos 10 dias ficaram abaixo da média (dias 1, 2, 3, 6, 7 e 10) — ⚠️ **ponto de atenção:** isso sinaliza que o desempenho de acesso do e-commerce está, na maior parte dos dias, abaixo do próprio valor típico, exigindo investigação (ex: o que tornou o dia 8 um pico — campanha, promoção — e o que pode ser feito para elevar os dias mais fracos).
- **Comportamento do conjunto de dados:** pode ser classificado como uniforme (dados praticamente constantes, sem variação), concentrado (todos os valores próximos de um mesmo número) ou com picos e vales (valores muito acima e muito abaixo da média). Neste exercício, o gráfico apresenta **picos e vales** — um vale em 150 e um pico em 400 — e não os outros dois padrões.

### 3. 🧠 Raciocínio Lógico
- Para a **média**: soma-se todos os valores do conjunto e divide-se pela quantidade total de valores (10 dias → divide por 10).
- Para a **mediana**: primeiro confirma-se que os dados estão ordenados (rol); como a quantidade é par, calcula-se a média dos dois valores centrais em vez de pegar um único número do meio.
- Para a **moda**: observa-se qual valor se repete com mais frequência no conjunto.
- Para a leitura do gráfico: usa-se a média já calculada como linha de referência visual — valores acima da linha indicam dias de desempenho forte, valores abaixo indicam dias fracos — e observa-se a amplitude entre o menor e o maior valor para classificar o padrão geral (uniforme, concentrado, ou picos e vales).

---
**Salvar como:** `06-rocketseat-da-matematica-para-dados-exercicios-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.

Restam 0 aulas neste módulo (Estatística Descritiva) — este exercício encerra o módulo, conforme indicado na própria aula ("com isso a gente finaliza essa parte aqui de estatística descritiva... e agora vamos avançar pro próximo módulo").