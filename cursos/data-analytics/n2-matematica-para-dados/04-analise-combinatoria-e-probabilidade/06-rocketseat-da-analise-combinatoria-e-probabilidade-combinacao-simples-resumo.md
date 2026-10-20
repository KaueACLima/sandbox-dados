# 📌 Combinação Simples

### 1. Conceito Central
**Combinação simples** é **escolher *p* elementos entre *n* objetos quando a ordem não faz diferença**. Só importa **quem** foi escolhido, não a ordem em que foi escolhido.

O contraste com o arranjo (aula 05) é o ponto central. No arranjo a ordem importa (pódio, presidente e vice, ordem de sorteio). Na combinação ela não importa (montar um grupo de clientes para uma pesquisa). A fórmula da combinação é a do arranjo com um fator a mais, que elimina os casos repetidos.

### 2. Pontos-chave e Sintaxe
- **Quando usar:** escolher *p* entre *n*, sem repetição, **com a ordem sem importância**.
- ⚠️ **Pergunta de decisão:** a ordem importa?
  - Importa → **arranjo**.
  - Não importa → **combinação**.

#### Exemplo: grupo de 3 clientes entre 5 pessoas (A, B, C, D, E)
**Forma bruta (listando tudo):** ABC, ABD, ABE, ACD, ACE, ADE, BCD, BCE, BDE, CDE → **10 grupos**.

**Pelo PFC, e o erro que aparece:**
- `5 × 4 × 3 = 60`, mas a listagem deu 10.
- O 60 está errado para este problema porque conta o **mesmo grupo várias vezes, em ordens diferentes**.
- O grupo ABC, por exemplo, aparece como ABC, ACB, BAC, BCA, CAB e CBA. São 6 ordens para as mesmas 3 pessoas, e `6 = 3!`.
- **Correção:** dividir por `3!` para eliminar as repetições: `60 / 3! = 60 / 6 = 10`.

#### Outros exemplos (pelo mesmo raciocínio)
- **3 clientes entre 10:** `(10 × 9 × 8) / 3!`, em que `10 × 9 × 8 = 720`.
- **4 clientes entre 7:** `(7 × 6 × 5 × 4) / 4!`, em que `7 × 6 × 5 × 4 = 840`.
- Sempre se divide pelo fatorial da quantidade escolhida (*p*).

#### Fórmula da combinação simples
```
C(n, p) = n! / [ p! × (n − p)! ]
```
- **n** = total de elementos que você tem.
- **p** = quantidade que você vai escolher.
- O `p!` no denominador é a "partezinha" que elimina as ordens repetidas.
- **Aplicações:**
  - `C(10, 3) = 10! / (3! × (10−3)!) = 10! / (3! × 7!)`
  - `C(7, 4) = 7! / (4! × (7−4)!) = 7! / (4! × 3!)`

#### Comparação arranjo × combinação
| | Arranjo | Combinação |
|---|---|---|
| A ordem | importa | não importa |
| Fórmula | `n! / (n−p)!` | `n! / [p! × (n−p)!]` |
| Exemplo (7 em 4) | `7! / 3!` | `7! / (4! × 3!)` |

- 💡 **Dica:** a combinação é o arranjo dividido por `p!`. Esse fator a mais elimina os casos repetidos de que a combinação não precisa.
- Nos prints, o arranjo aparece com a letra **A** e a combinação com a letra **C**.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** identificar se a ordem importa. Se não importa, é combinação.
- **Passo 2:** contar como se a ordem importasse, preenchendo as *p* posições com `n × (n−1) × ...`. Esse é o resultado do arranjo.
- **Passo 3:** perceber que esse total conta o mesmo grupo várias vezes, uma para cada ordem possível dos *p* elementos. Essa quantidade de ordens é `p!`.
- **Passo 4:** dividir o total por `p!` para ficar com cada grupo contado uma só vez.
- **Resultado:** `C(n, p) = A(n, p) / p! = n! / [p! × (n−p)!]`.

### 4. Links e Referências Oficiais
Aula de teoria pura, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Combinação simples:** escolha de *p* elementos entre *n* com a ordem sem importância. Fórmula `n! / [p! × (n−p)!]`.
- **Arranjo simples:** visto na aula 05, é o caso em que a ordem importa. Serve de base para a combinação.
- **Fatorial (n!):** visto na aula 03. `p!` é o fator que elimina as ordens repetidas na combinação.
- **Princípio Fundamental da Contagem (PFC):** visto na aula 02. Produz o total inicial (como o 60) antes de remover as repetições.
- **Casos repetidos:** o mesmo grupo contado em ordens diferentes. É o que a divisão por `p!` elimina.
