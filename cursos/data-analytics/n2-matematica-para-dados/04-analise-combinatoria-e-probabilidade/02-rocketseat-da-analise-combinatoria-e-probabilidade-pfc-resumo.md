# 📌 Princípio Fundamental da Contagem (PFC)

### 1. Conceito Central
O **Princípio Fundamental da Contagem (PFC)** é a ferramenta da análise combinatória para descobrir **quantas possibilidades existem** sem listá-las uma a uma. Ele se divide em dois: o **princípio multiplicativo** e o **princípio aditivo**.

Para saber qual usar, é preciso **interpretar o problema** e identificar o conectivo lógico entre as escolhas. Se as escolhas acontecem **juntas**, o conectivo é **E** e usa-se a **multiplicação**. Se são **alternativas** em que só uma acontece, o conectivo é **OU** e usa-se a **soma**.

### 2. Pontos-chave e Sintaxe
- **Regra de ouro:** conectivo **E** → **vezes**; conectivo **OU** → **soma**.
- 🔎 **Macete visual (do print da aula):** o **E** está dentro de V**E**ZES e o **OU** está dentro de S**OU**MA.

#### Princípio multiplicativo (conectivo E)
- Cenário da aula: **3 camisas**, **2 calças** e **4 calçados** (tênis, sapato social, chinelo e pantufa).
- Quem sai de casa veste **camisa E calça E calçado**, nunca "camisa ou calça".
- Cálculo: `3 × 2 × 4` → `3 × 2 = 6` → `6 × 4 = 24` possibilidades de se arrumar.

#### Princípio aditivo (conectivo OU)
- Cenário da aula: sapateira com **2 calçados azuis**, **3 verdes** e **5 laranjas**.
- Ninguém calça os três ao mesmo tempo, então a escolha é **azul OU verde OU laranja**.
- Cálculo: `2 + 3 + 5 = 10` possibilidades de escolher **um** calçado para sair.

#### Exemplo combinado: caminhos de A até E
Há quatro rotas possíveis, e dentro de cada rota as etapas são em sequência:

| Rota | Etapas (nº de caminhos em cada trecho) | Cálculo | Total |
|---|---|---|---|
| A→B→E | AB = 3 e BE = 3 | 3 × 3 | 9 |
| A→C→E | AC = 2 e CE = 3 | 2 × 3 | 6 |
| A→C→D→E | AC = 2, CD = 2 e DE = 2 | 2 × 2 × 2 | 8 |
| A→D→E | AD = 2 e DE = 2 | 2 × 2 | 4 |

- **Total:** `9 + 6 + 8 + 4 = 27` caminhos diferentes de A até E.
- No áudio, o trecho da rota ACE saiu confuso. Os valores 2 × 3 = 6 acima foram confirmados pelo print da aula.
- 💡 **Dica:** dentro de uma rota as etapas são sequenciais (A→B **e** B→E), então multiplica. Entre rotas diferentes só se faz uma por vez (ABE **ou** ACE **ou** ACDE **ou** ADE), então soma.
- ⚠️ **Ponto de atenção:** o mesmo problema pode usar **os dois princípios**. O exemplo de A até E multiplica dentro de cada rota e soma no final.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** ler o problema e se perguntar se as escolhas acontecem **juntas** (camisa e calça e calçado) ou se são **alternativas** (um calçado ou outro).
- **Passo 2:** se acontecem **juntas** (conectivo E), cada escolha de uma etapa pode ser combinada com as escolhas das demais, então se **multiplicam** as quantidades de cada etapa.
- **Passo 3:** se são **alternativas** (conectivo OU), só uma delas ocorre por vez, então se **somam** as quantidades.
- **Passo 4:** em problemas maiores, como os caminhos de A até E:
  - separar o problema em partes (as rotas);
  - **multiplicar** as etapas dentro de cada parte;
  - **somar** os resultados das partes.
- **Por que isso evita listar tudo:** testar peça por peça (trocar a calça, depois o sapato…) é o que a análise combinatória dispensa, porque o PFC dá o número total direto.

### 4. Links e Referências Oficiais
Aula de teoria pura, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Princípio Fundamental da Contagem (PFC):** conjunto de dois princípios (multiplicativo e aditivo) para contar possibilidades sem listá-las.
- **Princípio multiplicativo:** usado quando as escolhas são sucessivas, ligadas pelo conectivo **E**. As quantidades de cada etapa são multiplicadas.
- **Princípio aditivo:** usado quando as escolhas são alternativas, ligadas pelo conectivo **OU**. As quantidades são somadas.
- **Conectivos E / OU:** palavras-chave de interpretação do enunciado. **E** indica multiplicação e **OU** indica soma.
