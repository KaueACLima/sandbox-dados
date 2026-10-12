# 📌 Quartil para Dados Agrupados em Intervalos de Classe

### 1. Conceito Central
Esta aula retoma o quartil, mas aplicado a um cenário diferente do visto antes: em vez de uma lista simples de valores individuais, os dados vêm organizados em **intervalos de classe** (faixas), cada um com sua **frequência (Fi)** — quantidade de ocorrências naquele intervalo — e sua **frequência acumulada (Fac)** — soma das frequências até aquele intervalo, inclusive. Para esse formato, usa-se uma fórmula específica em duas etapas: primeiro descobre-se **em que posição** (dentro do total de observações) o quartil buscado está localizado; depois, usa-se essa posição para identificar **em qual intervalo** ela cai, e aplica-se a fórmula do quartil para achar o valor exato dentro daquele intervalo.

### 2. Pontos-chave e Sintaxe
- **Fi (frequência do intervalo):** quantidade de observações que caem naquele intervalo.
- **Fac (frequência acumulada):** soma de todas as frequências até aquele intervalo (inclusive).
- **Etapa 1 — achar a posição do quartil:**
  ```
  Posição = K × ΣFi
  ```
  onde `ΣFi` é a soma total de todas as frequências (o total de observações da pesquisa), e `K` depende de qual quartil se busca:
  - Q1 → K = 1/4
  - Q2 → K = 1/2
  - Q3 → K = 3/4
- A posição encontrada indica **onde**, na sequência ordenada de observações, está o valor do quartil — é a mesma lógica de achar a posição da mediana numa lista simples, só que generalizada pelas frações.
- **Etapa 2 — localizar o intervalo e aplicar a fórmula do valor:**
  ```
  Quartil = Li + ((Posição − Fac_anterior) / Fi) × h
  ```
  - `Li` = limite inferior do intervalo onde a posição calculada foi localizada.
  - `Fac_anterior` = frequência acumulada do intervalo **anterior** ao que contém a posição (não o do próprio intervalo).
  - `Fi` = frequência do intervalo que contém a posição.
  - `h` = amplitude do intervalo (limite superior − limite inferior daquele intervalo).
- **Como achar o intervalo certo:** compara-se a posição calculada na Etapa 1 com a coluna de Fac — o intervalo correto é aquele cuja faixa de posições (do fim do Fac anterior até o próprio Fac) contém a posição buscada.
- **Tabela de exemplo usada no exercício** (pesquisa de estatura, amplitude de 4 em cada intervalo):

| Intervalo (altura) | Fi | Fac |
|---|---|---|
| 160–164 | 7 | 7 |
| 164–168 | 4 | 11 |
| 168–172 | 5 | 16 |
| 172–176 | 8 | 24 |
| 176–180 | 16 | 40 |

### 3. 🧠 Raciocínio Lógico (exercício resolvido)
- **Q1:** Posição = 1/4 × 40 = **10ª posição**. A 7ª posição termina no intervalo 160–164; logo, a 10ª posição está no intervalo **164–168** (Li = 164, Fac_anterior = 7, Fi = 4, h = 4).
  - Q1 = 164 + ((10 − 7) / 4) × 4 = 164 + 3 = **167**
- **Q2:** Posição = 1/2 × 40 = **20ª posição**. A 16ª posição termina no intervalo 168–172; logo, a 20ª posição está no intervalo **172–176** (Li = 172, Fac_anterior = 16, Fi = 8, h = 4).
  - Q2 = 172 + ((20 − 16) / 8) × 4 = 172 + 2 = **174**
- **Q3:** Posição = 3/4 × 40 = **30ª posição**. A 24ª posição termina no intervalo 172–176; logo, a 30ª posição está no intervalo **176–180** (Li = 176, Fac_anterior = 24, Fi = 16, h = 4).
  - Q3 = 176 + ((30 − 24) / 16) × 4 = 176 + 1,5 = **177,5**
- **Resultado final:** Q1 = 167 | Q2 = 174 | Q3 = 177,5.

---
**Salvar como:** `03-rocketseat-da-medidas-de-posicao-quartil-dados-agrupados-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.
Restam 5 aulas neste módulo. Próximo assunto anunciado: **percentil**.