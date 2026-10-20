# 📌 Fatorial

### 1. Conceito Central
**Fatorial** é o **produto de um número multiplicado por todos os seus antecessores, diminuindo de 1 em 1 até chegar a 1**. Escreve-se com um ponto de exclamação (`n!`).

Ele é a base de muitas contas das próximas aulas de análise combinatória. Por isso o essencial é entender o que ele é e saber simplificar contas entre fatoriais.

### 2. Pontos-chave e Sintaxe
- **Definição:** `n! = n × (n−1) × (n−2) × ... × 1`
- **Exemplos da aula:**
  - `4! = 4 × 3 × 2 × 1 = 24`
  - `7! = 7 × 6 × 5 × 4 × 3 × 2 × 1`
- ⚠️ **Por que para no 1 e não no 0:** se a multiplicação chegasse ao 0, o resultado final seria sempre zero.
- **Fatorial especial:** `0! = 1`. O professor só apresentou o fato, sem aprofundar o porquê, e pediu que o aluno guarde essa informação.

#### Conta entre fatoriais (simplificação)
- 💡 **Dica:** expanda o fatorial maior até aparecer o menor e corte os fatoriais iguais, em vez de calcular tudo.
- **Exemplo 1:** `5! / 4!`
  - `5! = 5 × 4 × 3 × 2 × 1`, e o trecho `4 × 3 × 2 × 1` é o próprio `4!`.
  - Logo `5! / 4! = (5 × 4!) / 4!`. Cortando o `4!`, o resultado é **5**.
- **Exemplo 2:** `(3! × 2!) / 2!`
  - Cortando o `2!`, sobra `3!`.
  - `3 × 2 × 1 = 6`, então o resultado é **6**.

#### Aplicação prática: ordenar 3 clientes VIPs (para uma premiação)
- Há 3 posições: primeiro, segundo e terceiro lugar.
- Se um cliente já ocupou a 1ª posição, restam **2** opções para a 2ª e apenas **1** para a 3ª.
- Cálculo: `3 × 2 × 1 = 6` formas de organizar os clientes, que é `3!`.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** parta do número `n` e multiplique por `n−1`, depois por `n−2`, e assim por diante, parando em 1.
- **Passo 2:** em divisões entre fatoriais, reescreva o maior como o número vezes o fatorial menor. Exemplo: `5! = 5 × 4!`.
- **Passo 3:** com o mesmo fatorial em cima e embaixo, ele se cancela e sobra só o que não foi cortado.
- **Passo 4 (por que serve para contar):** a cada posição preenchida, sobra uma opção a menos. No exemplo dos clientes foram 3, depois 2, depois 1. Multiplicar essas opções, como no princípio multiplicativo da aula 02, resulta em `3!`.

### 4. Links e Referências Oficiais
Aula de teoria pura, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Fatorial (`n!`):** produto de um número por todos os antecessores até 1. É a ferramenta central desta aula.
- **Produto:** resultado de uma multiplicação. A aula define o fatorial como um produto.
- **Simplificação (cortar fatoriais iguais):** técnica de dividir fatoriais cancelando os termos comuns, usada nos exemplos `5!/4!` e `(3!×2!)/2!`.
- **0! = 1:** valor especial do fatorial de zero, apresentado sem aprofundamento.