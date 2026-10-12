# 📌 Quartis — Cálculo e Interpretação

### 1. Conceito Central
Quartil é a generalização direta da mediana: em vez de dividir o conjunto de dados ordenado em 2 partes (50%/50%), ele divide em **4 partes iguais de 25% cada**. O ponto de partida é a própria mediana geral, que passa a se chamar **Q2** (porque é exatamente o mesmo valor — o corte em 50%). A partir daí, divide-se cada metade ao meio novamente: a metade **inferior** aos dados (abaixo de Q2) é cortada ao meio, gerando **Q1**; a metade **superior** (acima de Q2) é cortada ao meio, gerando **Q3**. Cada quartil tem uma leitura de posição relativa: Q1 indica que 25% dos dados são menores que ele (e 75% maiores); Q2 indica 50%/50%; Q3 indica que 75% dos dados são menores que ele (e 25% maiores). Em termos de fração, Q1 representa 1/4 do conjunto, Q2 representa 1/2, e Q3 representa 3/4.

### 2. Pontos-chave e Sintaxe
- **Quartil:** divide o conjunto ordenado (100% dos dados) em 4 partes iguais de 25%.
- **Q2 = mediana** — são o mesmo valor, só muda o nome.
- **Q1** = mediana da metade inferior dos dados (os valores abaixo de Q2).
- **Q3** = mediana da metade superior dos dados (os valores acima de Q2).
- **Leitura de posição:** Q1 → 25% menores / 75% maiores · Q2 → 50% / 50% · Q3 → 75% menores / 25% maiores.
- **Em frações:** Q1 = 1/4 dos dados · Q2 = 1/2 dos dados · Q3 = 3/4 dos dados.
- **Passo a passo do método (do exercício resolvido):**
  - Ordenar os valores do conjunto.
  - Se a quantidade total de valores for **ímpar**, o valor central já é o Q2 (mediana) diretamente.
  - Para achar Q1 e Q3, separa-se a metade inferior e a metade superior dos dados (sem incluir o próprio Q2 ímpar nessas metades) e repete-se a lógica da mediana em cada uma. Se a metade tiver quantidade **par** de valores, Q1 (ou Q3) é a **média dos dois valores centrais** dessa metade.
- ⚠️ **Nota de transcrição:** a lista de valores ditada na aula veio com aparente erro de reconhecimento de voz (os números "15" e "17" não batem com os cálculos que o professor fez a seguir). Reconstruí a sequência ordenada como **2, 4, 5, 7, 8, 8, 9, 10, 10** porque é a única que é compatível com os três resultados que ele de fato calculou (mediana = 8; Q1 = média entre 4 e 5 = 4,5; Q3 = média entre 9 e 10 = 9,5) e com a afirmação dele de que os dados "já estavam em ordem". Vale conferir essa lista no material oficial da plataforma antes de levar pro caderno como exemplo fixo.

### 3. 🧠 Raciocínio Lógico
- Conjunto de dados ordenados (9 valores, conforme nota de transcrição acima): `2, 4, 5, 7, 8, 8, 9, 10, 10`.
- Quantidade total é **ímpar (9)** → o valor central (5º valor da lista) já é a mediana geral → **Q2 = 8**.
- Metade inferior (os 4 valores antes do Q2): `2, 4, 5, 7`.
  - Quantidade **par (4)** → Q1 é a média dos dois valores centrais dessa metade (4 e 5) → **Q1 = (4 + 5) / 2 = 4,5**.
- Metade superior (os 4 valores depois do Q2): `8, 9, 10, 10`.
  - Quantidade **par (4)** → Q3 é a média dos dois valores centrais dessa metade (9 e 10) → **Q3 = (9 + 10) / 2 = 9,5**.
- Resultado final do exercício: **Q1 = 4,5 | Q2 = 8 | Q3 = 9,5**.

---
**Salvar como:** `02-rocketseat-da-medidas-de-posicao-quartis-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Restam 6 aulas neste módulo.