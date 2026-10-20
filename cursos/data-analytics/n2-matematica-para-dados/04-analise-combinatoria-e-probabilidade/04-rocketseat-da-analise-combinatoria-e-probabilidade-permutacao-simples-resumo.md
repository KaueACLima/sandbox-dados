# 📌 Permutação Simples

### 1. Conceito Central
**Permutação simples** é o número de maneiras de **mudar a ordem de *n* elementos distintos**. Como os elementos são todos diferentes entre si, cada reordenação conta como uma possibilidade nova.

O resultado é sempre **n!** (n fatorial). A permutação simples é resolvida pelo **Princípio Fundamental da Contagem** (aula 02) com o **fatorial** (aula 03). Por isso o professor avisa que, sem dominar o fatorial, vale voltar às aulas anteriores.

### 2. Pontos-chave e Sintaxe
- **Fórmula:** mudar a ordem de *n* objetos distintos = **n!**
- ⚠️ **Condição essencial: elementos distintos.** Não pode haver dois elementos idênticos. Na fila de pessoas, são pessoas diferentes.

#### Exemplo 1: fila com 5 pessoas
- 1ª posição: 5 pessoas podem ocupá-la.
- 2ª posição: sobram 4, porque uma já ocupou a 1ª.
- Depois 3, 2 e 1.
- Cálculo: `5 × 4 × 3 × 2 × 1 = 5! = 120`

#### Exemplo 2: fila com 8 pessoas
- Mesma ideia: `8 × 7 × 6 × 5 × 4 × 3 × 2 × 1 = 8!`
- A aula deixou indicado como `8!`, sem calcular o valor.

#### Exemplo 3: organizar 6 relatórios diferentes
- Os relatórios são todos distintos.
- Cálculo: `6 × 5 × 4 × 3 × 2 × 1 = 6! = 720` formas de organizá-los.

#### Caso geral
- Fila com *n* pessoas ou *n* objetos distintos → **n!** formas de ordená-los.
- 💡 **Dica:** para resolver, basta reconhecer que o problema é "mudar a ordem de *n* elementos distintos" e responder **n!**. O professor reforça que esse é o essencial a gravar.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** identificar se o problema pede a mudança de ordem de elementos que são **todos diferentes** entre si.
- **Passo 2:** preencher as posições uma a uma. A 1ª tem *n* candidatos e, a cada posição ocupada, sobra um candidato a menos (*n*, *n−1*, *n−2*, ... , 1).
- **Passo 3:** as escolhas das posições acontecem **juntas** (a 1ª **E** a 2ª **E** a 3ª ...), então se **multiplica**, como no princípio multiplicativo.
- **Passo 4:** esse produto de *n* até 1 é, por definição, **n!**, o resultado da permutação simples.

### 4. Links e Referências Oficiais
Aula de teoria pura, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Permutação simples:** forma de mudar a ordem de *n* elementos distintos. O total é *n!*.
- **Elementos distintos:** elementos todos diferentes entre si, sem repetição. É a condição para aplicar *n!* diretamente.
- **Fatorial (n!):** produto de *n* até 1, visto na aula 03. É a base do cálculo da permutação.
- **Princípio Fundamental da Contagem:** visto na aula 02. É o raciocínio que justifica multiplicar as possibilidades de cada posição.
