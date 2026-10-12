# 📌 Amplitude Interquartil — Exercício com Gráfico de Pontos

### 1. Conceito Central
Esta aula aplica a mesma lógica de amplitude interquartil (Q3 − Q1) vista na aula anterior, mas partindo de um formato de dado diferente: o **gráfico de pontos** (dot plot). Nesse tipo de gráfico, cada valor do eixo horizontal tem uma pilha de bolinhas acima dele, e a quantidade de bolinhas representa a **frequência** daquele valor no conjunto de dados. Para resolver o exercício, o primeiro passo é "traduzir" o gráfico de pontos em uma lista ordenada (o **rol**) — repetindo cada valor tantas vezes quanto indicar sua frequência — e, a partir daí, aplicar exatamente o mesmo método já usado: achar a mediana (Q2), dividir os dados em duas metades, achar o valor central de cada metade (Q1 e Q3), e calcular Q3 − Q1.

### 2. Pontos-chave e Sintaxe
- **Gráfico de pontos (dot plot):** cada bolinha empilhada sobre um valor do eixo representa uma ocorrência daquele valor nos dados.
- **Primeiro passo com gráfico de pontos:** converter as bolinhas em uma lista ordenada (rol), repetindo cada valor conforme sua frequência — valores sem nenhuma bolinha **não entram** na lista.
- Depois de montado o rol, o método é idêntico ao já visto: contar o total de elementos, achar a mediana (Q2), dividir em duas metades e achar o valor central de cada uma (Q1 e Q3).
- Confirmar a contagem total de elementos antes de prosseguir ajuda a saber de antemão se a mediana vai "cair" direto em um valor (quantidade ímpar) ou vai exigir média de dois centrais (quantidade par).
- ⚠️ **Nota de transcrição:** a leitura em áudio do gráfico de pontos trouxe algumas frequências com ambiguidade de reconhecimento de voz (em especial a contagem exata do valor logo após o 7). Por isso, não reconstruí aqui a tabela completa de frequências do dot plot — mantive apenas os elementos e resultados que o professor afirmou com clareza no cálculo: o total de 10 elementos, o conjunto final dos últimos 5 valores (`10, 10, 12, 12, 14`) e os três resultados fechados (Q1 = 8, Q2 = 10, Q3 = 12). Vale conferir a imagem original do gráfico de pontos na plataforma antes de copiar a tabela completa pro caderno.

### 3. 🧠 Raciocínio Lógico (exercício resolvido)
- Total de elementos no rol: **10** (quantidade par → a mediana geral exigirá média de dois valores centrais).
- Dividindo em duas metades de 5 elementos cada:
  - **Primeira metade (5 elementos, quantidade ímpar):** o valor central (3º elemento) já é direto → **Q1 = 8**.
  - **Segunda metade (5 elementos, quantidade ímpar):** `10, 10, 12, 12, 14` — o valor central (3º elemento) já é direto → **Q3 = 12**.
- **Mediana geral (Q2):** média entre o último elemento da primeira metade e o primeiro da segunda metade, ambos iguais a 10 → Q2 = (10 + 10) / 2 = **10**.
- **Amplitude interquartil = Q3 − Q1 = 12 − 8 = 4.**

---
**Salvar como:** `06-rocketseat-da-medidas-de-posicao-amplitude-interquartil-exercicio-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Restam 2 aulas neste módulo.