# 📌 Arranjo Simples

### 1. Conceito Central
**Arranjo simples** é usado quando você escolhe uma parte dos elementos de um conjunto e **a ordem importa**. Os elementos **não se repetem**.

A pergunta-chave ao ler um problema é: **"A ordem faz diferença?"** Se sim, é arranjo. O professor lembra que existe também o **arranjo com repetição**, mas ele não é tratado nesta aula.

O arranjo nasce do Princípio Fundamental da Contagem (PFC). Dá para resolver qualquer problema só com o PFC, sem fórmula. A fórmula é um atalho, e a aula mostra de onde ela vem.

### 2. Pontos-chave e Sintaxe
- **Quando usar:** a ordem importa e não há repetição.
- **Exemplo de ordem importando:** no pódio, ser 1º, 2º ou 3º faz diferença. Ao organizar produtos, a ordem em que aparecem também pode fazer diferença.
- ⚠️ **Ponto de atenção:** antes de calcular, responda duas perguntas:
  - A ordem importa?
  - Algum elemento se repete?
  
  Se a ordem importa e nada se repete, é arranjo simples.

#### Resolução pelo PFC (sem fórmula)
Cada posição do pódio tem um candidato a menos que a anterior, porque quem já ficou numa posição não pode ocupar outra. As posições são ocupadas **uma E outra E outra**, então multiplica.

| Pódio | Cálculo | Resultado |
|---|---|---|
| 3 posições entre 5 atletas | `5 × 4 × 3` | **60** |
| 4 posições entre 7 atletas | `7 × 6 × 5 × 4` | **840** |
| 3 posições entre 10 atletas | `10 × 9 × 8` | **720** |

- O áudio do cálculo de 7 atletas saiu confuso. O resultado 840 foi confirmado pelo print da aula.

#### De onde surge a fórmula
- O produto `5 × 4 × 3` lembra o fatorial `5!`, mas pararia no 3 e não iria até o 1.
- Para completar o fatorial sem alterar o resultado, multiplica-se e **divide-se** pelo trecho que faltava:

```
5 × 4 × 3 = (5 × 4 × 3 × 2 × 1) / (2 × 1) = 5! / 2!
```
  O `2 × 1` de cima corta com o de baixo e volta a ser `5 × 4 × 3`.
- Mesma lógica nos outros casos:
  - 7 atletas, 4 posições: `7! / 3!`
  - 10 atletas, 3 posições: `10! / 7!`

#### Fórmula do arranjo simples
```
A(n, p) = n! / (n − p)!
```
- **n** = quantidade de elementos que você tem.
- **p** = quantidade que você vai escolher (as posições).
- **n − p** = o que sobra, que é o que se divide embaixo.
- **Conferindo com os exemplos:**
  - 5 atletas, 3 posições: `5! / (5−3)! = 5! / 2!`
  - 7 atletas, 4 posições: `7! / (7−4)! = 7! / 3!`
  - 10 atletas, 3 posições: `10! / (10−3)! = 10! / 7!`
- 💡 **Dica:** a fórmula surge porque se completa o fatorial até 1 e se divide pelo excedente para não mudar o valor.
- O print da aula escreve a fórmula como `A` com *p* em cima e *N* embaixo. No áudio o professor a lê como "n em p".

#### Outras aplicações citadas
- Organizar **3 produtos** numa prateleira, quando a ordem faz diferença.
- Ranquear os **3 melhores entre 5 produtos**. O professor mostra que isso se resolve sem fórmula, pelo PFC, e que a fórmula também serve.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** a ordem importa? Há repetição? Se a ordem importa e nada se repete, é arranjo simples.
- **Passo 2:** identifique **n** (quantos elementos existem) e **p** (quantas posições serão preenchidas).
- **Passo 3 (pelo PFC):** para a 1ª posição há *n* candidatos, para a 2ª há *n−1*, e assim por diante até preencher as *p* posições. As posições acontecem juntas (conectivo **E**), então **multiplica**.
- **Passo 4 (pela fórmula):** o mesmo resultado sai de `n! / (n−p)!`. O fatorial de cima completa a sequência até 1 e o de baixo remove o trecho que não faz parte da conta.
- **Relação com a permutação simples (aula 04):** quando *p* = *n*, usa-se todos os elementos e a conta vira `n!`. Isso decorre da própria fórmula, já que `(n − n)! = 0! = 1`. A aula não afirma isso explicitamente.

### 4. Links e Referências Oficiais
Aula de teoria pura, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Arranjo simples:** escolha de *p* elementos entre *n*, com a ordem importando e sem repetição. Fórmula `n! / (n−p)!`.
- **Arranjo com repetição:** outro tipo de arranjo, só mencionado na aula e não explicado.
- **Princípio Fundamental da Contagem (PFC):** visto na aula 02. Resolve o arranjo sem fórmula, multiplicando as possibilidades de cada posição.
- **Fatorial (n!):** visto na aula 03. É a base da fórmula e do cancelamento entre fatoriais.
- **"A ordem importa":** critério de decisão para identificar que o problema é de arranjo.
