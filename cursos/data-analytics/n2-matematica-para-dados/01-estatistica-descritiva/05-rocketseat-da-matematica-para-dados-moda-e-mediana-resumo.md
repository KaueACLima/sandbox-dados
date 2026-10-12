# 📌 Medidas de Tendência Central: Moda e Mediana

### 1. Conceito Central
A aula apresenta as outras duas medidas de tendência central, complementando a média: **moda** (o valor que mais se repete em um conjunto de dados) e **mediana** (o valor central de um conjunto de dados **ordenado**). Ambas, assim como a média, buscam resumir um conjunto de dados em um único valor representativo, mas cada uma captura um aspecto diferente desse conjunto.

### 2. Pontos-chave e Sintaxe

#### Moda
- Moda é o valor que mais se repete em um conjunto de dados.
- Um conjunto pode ser **unimodal** (uma única moda), **bimodal** (duas modas) ou não ter moda alguma.
- Exemplo: valores de compra registrados foram 50, 75, 100, 50, 150, 200, 50, 100. O valor 50 aparece 3 vezes — mais que qualquer outro — logo, **a moda é 50**.

#### Mediana
- Mediana é o valor central de um conjunto de dados **ordenado**.
- ⚠️ **Ponto de atenção:** para achar a mediana, é obrigatório primeiro **ordenar** os dados do menor para o maior — essa organização é chamada de **rol**. Calcular o "valor do meio" sem ordenar antes gera um resultado incorreto (no exemplo da aula, pegar o meio sem ordenar dava 12, quando o valor correto, após ordenar, era 15).
- **Quantidade ímpar de valores:** a mediana é o número que sobra exatamente no meio após a ordenação (há a mesma quantidade de valores para cada lado).
- **Quantidade par de valores:** não existe um único número central — a mediana é a **média aritmética dos dois valores centrais**.

#### Exemplo prático resolvido (quantidade ímpar — 7 valores)
```
# Tempos de uso de um app, em minutos (dados brutos, desordenados):
22, 5, 7, 12, 15, 25, 18

# Rol (ordenação do menor para o maior):
5, 7, 12, 15, 18, 22, 25

# Com 7 valores, há 3 para cada lado do centro -> o valor central é a mediana
# Mediana = 15
```

#### Exemplo prático resolvido (quantidade par — 8 valores)
```
# Dados ordenados (rol já feito):
3, 7, 9, 12, 16, 18, 22, 25

# Com 8 valores, há 4 para cada lado -> não há um único valor central
# Os dois valores centrais são 12 e 16
# Mediana = média entre os dois centrais: (12 + 16) / 2 = 28 / 2 = 14
```

### 3. 🧠 Raciocínio Lógico
- Para achar a **moda**: percorre-se o conjunto de dados e identifica-se o valor que aparece com mais frequência.
- Para achar a **mediana**: primeiro ordena-se o conjunto de dados (rol), do menor para o maior.
- Em seguida, verifica-se a quantidade de valores do conjunto:
  - Se for **ímpar**, o valor que sobra exatamente no meio, após a divisão igual dos dois lados, é a mediana.
  - Se for **par**, não há um valor único no meio — calcula-se a média entre os dois valores centrais, e esse resultado é a mediana.

---
**Salvar como:** `05-rocketseat-da-matematica-para-dados-moda-e-mediana-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.