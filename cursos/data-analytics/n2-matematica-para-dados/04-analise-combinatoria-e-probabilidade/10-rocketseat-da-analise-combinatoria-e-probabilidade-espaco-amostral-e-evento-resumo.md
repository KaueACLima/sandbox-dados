# 📌 Espaço Amostral e Evento

### 1. Conceito Central
Antes das fórmulas, a aula apresenta a base da probabilidade: os números que ela usa e os dois conceitos centrais, **espaço amostral** (tudo o que pode acontecer) e **evento** (o que você quer que aconteça).

A probabilidade varia **entre 0 e 1** (ou 0% e 100%). O espaço amostral é o conjunto de todos os resultados possíveis, e o evento é um **subconjunto** dele.

### 2. Pontos-chave e Sintaxe

#### A escala da probabilidade
- **0% = 0/100 = 0:** o evento não tem como ocorrer. Exemplo: jogar um dado e sair o número 7.
- **100% = 100/100 = 1:** o evento sempre ocorre. Exemplo: jogar um dado e sair um número natural (1 a 6 são todos naturais).
- **Moeda, cara:** há 2 possibilidades (cara ou coroa), então `1/2 = 50% = 0,5`.
- Logo, a probabilidade **sempre fica entre 0 e 1**.

#### Espaço amostral (S)
- É o **conjunto de todos os resultados possíveis**.
- Representa-se pela letra **S** ou pela letra grega **Ω (ômega)**. A aula usa o S.
- **Dado:** `S = {1, 2, 3, 4, 5, 6}`

#### Evento (E)
- É **tudo aquilo que você quer**, um **subconjunto** do espaço amostral.
- Exemplos com o dado:

| Evento | Descrição | Conjunto | Nº de elementos |
|---|---|---|---|
| E₁ | ocorrer face par | `{2, 4, 6}` | 3 |
| E₂ | ocorrer face 5 | `{5}` | 1 |
| E₃ | ocorrer face ímpar | `{1, 3, 5}` | 3 |

#### Os 3 tipos de evento
- **Evento certo:** `E = S`. O evento é igual ao espaço amostral. Exemplo: sair um número natural no dado (100%).
- **Evento impossível:** `E = ∅` (**conjunto vazio**, sem nenhum elemento). Exemplo: sair no dado um número que ele não tem, como o 8. A chance é 0.
- **Eventos complementares:** dois eventos em que um completa o outro. Exemplo: E₁ (par) e E₃ (ímpar). As duas condições são:
  - `E₁ ∪ E₃ = S`: a **união** deles dá todo o espaço amostral (2, 4, 6 + 1, 3, 5 = 1 a 6).
  - `E₁ ∩ E₃ = ∅`: a **interseção** deles é vazia, porque nenhum número se repete nos dois.

- ⚠️ **Divergência entre o áudio, o print e o exemplo:** no print e na primeira fala do professor, a condição aparece como `E₁ ∩ E₃ ≠ ∅`. Mas, ao verificar com o exemplo, ele diz que nenhum número se repete e que a interseção é **igual a vazio**. O exemplo (par × ímpar) confirma **interseção vazia**. Para o caderno, vale anotar `∩ = ∅` e conferir a definição formal na doc/aula seguinte.
- 🔎 **Observação:** o áudio do evento impossível ficou confuso (o professor fala "diferente de vazio" e depois "igual a vazio"). O print mostra `E = ∅` para o impossível, e foi isso que se registrou.
- 💡 **Dica (fala do professor):** espaço amostral é "tudo aquilo que eu tenho" e evento é "o que eu quero".

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** listar todos os resultados possíveis. Esse é o espaço amostral **S**.
- **Passo 2:** separar o que se quer. Esse é o evento **E**, que está contido em S.
- **Passo 3:** comparar E com S:
  - E igual a S → **certo** (probabilidade 1).
  - E vazio → **impossível** (probabilidade 0).
  - Qualquer evento intermediário fica **entre 0 e 1**.
- **Passo 4 (complementares):** dois eventos são complementares se juntos cobrem todo o S (união = S) e não têm nenhum elemento em comum (interseção vazia).

### 4. Links e Referências Oficiais
Aula de teoria pura, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Espaço amostral (S ou Ω):** conjunto de todos os resultados possíveis de um experimento.
- **Evento (E):** subconjunto do espaço amostral; o que se quer que ocorra.
- **Evento certo, evento impossível e eventos complementares:** os três tipos de evento apresentados, com definições em conjuntos (E = S, E = ∅, união = S com interseção vazia).
- **Conjunto vazio (∅):** conjunto sem elementos; representa o evento impossível.
- **União (∪) e interseção (∩):** operações entre conjuntos usadas para definir eventos complementares. A aula só as aplica ao exemplo, sem formalizar.
- **Probabilidade (escala de 0 a 1):** chance de um evento ocorrer, de 0 (impossível) a 1 (certo).