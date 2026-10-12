# 📌 Percentil (Centil) — Divisão em 100 Partes

### 1. Conceito Central
Percentil (ou centil) é mais uma medida de posição da mesma família de quartil e decil: em vez de dividir o conjunto de dados em 4 ou 10 partes, ele divide em **100 partes iguais**, onde cada parte vale **1%** do total pesquisado. Cada marco dessa divisão é chamado de P1, P2, P3... até P100. A lógica de cálculo é idêntica à do quartil — muda apenas a fração usada: no quartil, K é 1/4, 1/2 ou 3/4; no percentil, K é sempre **P/100**, onde P é o percentil buscado. Isso cria equivalências diretas entre as três medidas: **P50 = Q2 = mediana** (50%), **P25 = Q1** (25%) e **P75 = Q3** (75%) — são exatamente os mesmos valores, só vistos sob escalas diferentes.

### 2. Pontos-chave e Sintaxe
- **Percentil (Pn):** divide o conjunto de 100% dos dados em 100 partes, cada uma valendo 1%.
- **Leitura direta:** P20 = 20% da pesquisa; P50 = 50%; P33 = 33%; e assim por diante.
- **Equivalências com quartil:** P25 = Q1 · P50 = Q2 (mediana) · P75 = Q3.
- **Fórmula de posição** (igual à do quartil, só muda o K):
  ```
  Posição = K × ΣFi,  onde K = P / 100
  ```
- **Fórmula do valor do percentil** (idêntica à do quartil, trocando o rótulo):
  ```
  Pn = Li + ((Posição − Fac_anterior) / Fi) × h
  ```
  - `Li` = limite inferior do intervalo onde a posição calculada cai.
  - `Fac_anterior` = frequência acumulada do intervalo **anterior** ao que contém a posição.
  - `Fi` = frequência do intervalo que contém a posição.
  - `h` = amplitude do intervalo.
- **Interpretação do resultado:** assumindo os dados organizados em ordem crescente, o valor de Pn indica que **n% das observações têm valor abaixo dele** (e o restante, acima).
- 🔎 **Observação:** o método de achar a posição é sempre o mesmo em quartil, decil e percentil — só a fração (K) muda conforme quantas partes você quer dividir o total (4, 10 ou 100).

### 3. 🧠 Raciocínio Lógico (exercício resolvido: P20, mesma tabela de estatura da aula anterior)

| Intervalo (altura) | Fi | Fac |
|---|---|---|
| 160–164 | 7 | 7 |
| 164–168 | 4 | 11 |
| 168–172 | 5 | 16 |
| 172–176 | 8 | 24 |
| 176–180 | 16 | 40 |

- **Etapa 1 — posição:** K = 20/100. Posição = (20/100) × 40 = **8ª posição**.
- **Etapa 2 — localizar o intervalo:** a 7ª posição termina no intervalo 160–164; logo, a 8ª posição está no intervalo **164–168** (Li = 164, Fac_anterior = 7, Fi = 4, h = 4).
- **Etapa 3 — aplicar a fórmula:**
  - P20 = 164 + ((8 − 7) / 4) × 4 = 164 + 1 = **165**
- **Interpretação:** 20% das pessoas pesquisadas têm estatura menor que 165 (considerando os dados organizados do menor para o maior valor).

---
**Salvar como:** `04-rocketseat-da-medidas-de-posicao-percentil-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Restam 4 aulas neste módulo.