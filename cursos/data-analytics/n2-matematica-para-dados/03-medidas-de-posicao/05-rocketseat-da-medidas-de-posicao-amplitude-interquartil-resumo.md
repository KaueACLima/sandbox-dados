# 📌 Amplitude Interquartil (Q3 − Q1)

### 1. Conceito Central
A amplitude interquartil é uma medida de dispersão que, em vez de usar o maior e o menor valor do conjunto (como a amplitude total), usa os **quartis** para medir o espalhamento dos dados: ela foca na "parte do meio" da distribuição, descartando os 25% mais baixos e os 25% mais altos. O cálculo é direto: **Q3 − Q1**. Para chegar lá, o caminho é o mesmo já visto para achar quartis em uma lista simples: organizar os dados em ordem crescente (o **rol**), achar a mediana (que é o Q2), e então achar Q1 e Q3 dividindo ao meio cada uma das metades resultantes.

### 2. Pontos-chave e Sintaxe
- **Amplitude interquartil = Q3 − Q1.**
- Mede a dispersão da "parte central" dos dados, diferente da amplitude total (maior valor − menor valor).
- **Passo a passo:**
  1. Fazer o **rol** (organizar os dados em ordem crescente).
  2. Achar a **mediana** (= Q2) do conjunto completo.
  3. Achar **Q1**: repetir a lógica da mediana, mas só na primeira metade dos dados (os valores abaixo de Q2).
  4. Achar **Q3**: repetir a lógica da mediana, mas só na segunda metade dos dados (os valores acima de Q2).
  5. Calcular **Q3 − Q1**.
- Se a quantidade de elementos de uma metade for **par**, o quartil daquela metade é a **média dos dois valores centrais** dessa metade — mesma regra já usada para achar quartis em listas simples.

### 3. 🧠 Raciocínio Lógico (exercício resolvido)
- Conjunto de dados original: `5, 5, 7, 10, 12, 12, 14, 11, 8`.
- **Rol (ordem crescente):** `5, 5, 7, 8, 10, 11, 12, 12, 14` (9 elementos).
- Quantidade total é **ímpar (9)** → o valor central (5º elemento) é a mediana geral → **Q2 = 10**.
- Primeira metade (os 4 valores antes do Q2): `5, 5, 7, 8`.
  - Quantidade **par (4)** → Q1 = média dos dois valores centrais dessa metade (5 e 7) → **Q1 = (5 + 7) / 2 = 6**.
- Segunda metade (os 4 valores depois do Q2): `11, 12, 12, 14`.
  - Quantidade **par (4)** → Q3 = média dos dois valores centrais dessa metade (12 e 12) → **Q3 = (12 + 12) / 2 = 12**.
- **Amplitude interquartil = Q3 − Q1 = 12 − 6 = 6.**

---
**Salvar como:** `05-rocketseat-da-medidas-de-posicao-amplitude-interquartil-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Restam 3 aulas neste módulo.