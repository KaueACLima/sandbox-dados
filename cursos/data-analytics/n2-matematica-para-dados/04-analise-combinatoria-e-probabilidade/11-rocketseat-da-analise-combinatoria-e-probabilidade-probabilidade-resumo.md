# 📌 Probabilidade: Escala, Tipos e Cálculo

### 1. Conceito Central
A aula reúne três coisas. Primeiro, as regras da escala da probabilidade (sempre positiva, de 0 a 1). Segundo, os **três tipos de probabilidade** (clássica, empírica e subjetiva). Terceiro, o **cálculo básico**: casos favoráveis divididos pelo total de casos.

Na fórmula, o evento (o que você quer) vai no numerador e o espaço amostral (tudo o que existe) no denominador. É a aplicação direta dos conceitos de **evento** e **espaço amostral** da aula anterior.

### 2. Pontos-chave e Sintaxe

#### Regras da escala
- **Não existe probabilidade negativa**: ela é sempre um número positivo.
- **Amplitude:** vai de **0 a 1**, ou de **0% a 100%**, que são duas formas de escrever a mesma coisa.
  - `0% = 0/100 = 0`
  - `100% = 100/100 = 1`

#### Nomenclatura dos valores (reta do print)
| Valor | Percentual | Nome |
|---|---|---|
| 0 | 0% | impossível |
| 0,25 (= 1/4) | 25% | improvável |
| 0,50 | 50% | chance igual (meio a meio) |
| 0,75 | 75% | provável (grande chance) |
| 1 | 100% | certeza |

- 💡 **Dica (fala do professor):** em um relatório, vale usar esses nomes para descrever um dado (ex.: "improvável", "certeza"), associando cada termo ao seu número.

#### Os 3 tipos de probabilidade
| Tipo | Base | Exemplo da aula |
|---|---|---|
| **Clássica** (ou teórica) | lógica matemática | sorteio entre 10 clientes, cada um com um único número, ou seja, 1 chance em 10 para cada |
| **Empírica** | dados reais, algo que já aconteceu | 1.000 acessos ao site no último mês, 300 compraram → 30%. Esse dado pode ser usado numa nova análise |
| **Subjetiva** | intuição / experiência | gerente diz "70% de chance de comprarem na sexta" sem ter cálculo nem levantamento |

- A subjetiva se baseia na experiência de quem fala, não em um levantamento concreto. Outro exemplo citado foi o médico que diz "90% de chance" com base em casos anteriores.
- ⚠️ **Ponto de atenção:** o que diferencia os tipos é **de onde vem o número**: matemática, dados reais ou opinião. Um "70%" dito sem cálculo é subjetivo.

#### Cálculo da probabilidade
```
P(E) = n(E) / n(S)
```
- **n(E)** = número de **casos favoráveis** (o evento, o que você quer).
- **n(S)** = **total de casos** (o espaço amostral, também representado por Ω).
- **Exemplo de identificação:** em 1.000 cliques num e-mail promocional, 500 pessoas compraram.
  - Espaço amostral = 1.000 cliques.
  - Evento = 500 compras.
  - A aula identifica os dois termos e não fecha o resultado da conta.

#### Exemplo: lançar um dado
- Espaço amostral: `S = {1, 2, 3, 4, 5, 6}` → `n(S) = 6`.

| Pergunta | Evento | n(E) | Cálculo | Resultado |
|---|---|---|---|---|
| a) sair número par | `{2, 4, 6}` | 3 | `3/6` | `1/2 = 0,5 = 50%` |
| b) sair o número 3 | `{3}` | 1 | `1/6` | `1/6` |
| c) sair número maior que 4 | `{5, 6}` (o 4 não entra) | 2 | `2/6` | `1/3` |

- **Simplificação (item a):** `3/6`, dividindo em cima e embaixo por 3, vira `1/2`. Depois `1/2 = 0,5`, e para percentual `0,5 = 50/100 = 50%`.
- **Regra de apresentação:** o resultado deve ficar na **forma mais simples** da fração ou em **porcentagem**. Deixar `3/6` é considerado errado.
- No item c, simplifica-se dividindo por 2 em cima e embaixo: `2/6 = 1/3`.
- O print só mostra a resolução dos itens a e b. O item c vem do áudio.

#### O que ainda vem
- Essa é a probabilidade **simples (básica)**. A **probabilidade condicional** será vista mais adiante.

- 🔎 **Observação (decorre da aula anterior):** com a fórmula `n(E)/n(S)`, um **evento certo** (E = S) dá `n(S)/n(S) = 1`, e um **evento impossível** (E = ∅) dá `0/n(S) = 0`. Isso explica por que a escala vai de 0 a 1.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** definir o **espaço amostral**, o total de casos possíveis. Exemplo: o dado tem 6 faces.
- **Passo 2:** definir o **evento**, os casos favoráveis dentro desse espaço.
- **Passo 3:** dividir `n(E) / n(S)`.
- **Passo 4:** simplificar a fração ao máximo ou converter para percentual. Convertendo a fração para decimal e multiplicando por 100, obtém-se a porcentagem (`1/2 = 0,5 = 50%`).
- **Passo 5:** interpretar o valor na escala e dar o nome certo: impossível, improvável, chance igual, provável ou certeza.
- **Passo 6 (origem do número):** verificar se a probabilidade vem da lógica matemática (clássica), de dados reais (empírica) ou da intuição (subjetiva).

### 4. Links e Referências Oficiais
Aula de teoria pura, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Amplitude da probabilidade:** a probabilidade vai de 0 a 1 (ou 0% a 100%) e nunca é negativa.
- **Probabilidade clássica (teórica):** baseada em lógica matemática, com casos igualmente possíveis (ex.: sorteio).
- **Probabilidade empírica:** baseada em dados reais já observados (ex.: 300 compras em 1.000 acessos = 30%).
- **Probabilidade subjetiva:** baseada na intuição e experiência, sem levantamento concreto.
- **Casos favoráveis (evento) e total de casos (espaço amostral):** numerador e denominador da fórmula `P(E) = n(E) / n(S)`.
- **Probabilidade condicional:** apenas mencionada como assunto futuro, sem explicação nesta aula.
