# 📌 Variância e Desvio Padrão

### 1. Conceito Central
Desvio padrão é a medida que mostra **o quanto, em média, os valores de um conjunto de dados se afastam do centro (da média)**. Diferente da amplitude — que é só uma subtração simples entre o maior e o menor valor — o desvio padrão calcula uma **média das distâncias** de cada valor em relação à média do conjunto, exigindo um processo matemático mais elaborado (a variância) como etapa intermediária. O desvio padrão é a raiz quadrada da variância, e o resultado volta à mesma unidade de medida dos dados originais, tornando a interpretação mais direta que a da variância isolada.

### 2. Pontos-chave e Sintaxe
- **O problema de só usar a média:** assim como na aula de amplitude, a média pode mascarar a realidade. No exemplo da aula, um patrão com três lojas (faturamento de 10%, 100% e 70%) acredita que está tudo bem se a média ficar acima de 50% — mas isso esconde que a Loja A está quase quebrando (10%) enquanto a Loja B está excelente (100%).
- **Passo a passo do cálculo (variância → desvio padrão):**

```
1. Calcular a média dos valores:
   (10 + 100 + 70) / 3 = 180 / 3 = 60%

2. Calcular a diferença de cada valor para a média:
   10 - 60  = -50
   100 - 60 =  40
   70 - 60  =  10
   (a soma dessas diferenças dá 0 — por isso não dá pra tirar a média direto delas)

3. Elevar cada diferença ao quadrado (pra eliminar o sinal negativo,
   já que a soma das diferenças "cruas" sempre zera):
   (-50)² = 2.500
   (40)²  = 1.600
   (10)²  =   100

4. Calcular a média desses quadrados → isso é a VARIÂNCIA:
   (2.500 + 1.600 + 100) / 3 = 4.200 / 3 = 1.400

5. Tirar a raiz quadrada da variância → isso é o DESVIO PADRÃO:
   √1.400 ≈ 37%
```
- **Por que elevar ao quadrado:** a soma das diferenças de cada valor em relação à média sempre resulta em zero (os desvios positivos e negativos se cancelam), inviabilizando o cálculo de uma média direta. Elevar ao quadrado transforma todo valor em positivo (negativo × negativo = positivo), permitindo somar e tirar a média normalmente.
- **Por que tirar a raiz quadrada no final:** elevar ao quadrado tira os dados da unidade de medida original. A raiz quadrada desfaz essa operação (é o inverso do quadrado) e devolve o resultado a uma escala comparável com os dados de origem — por isso o desvio padrão (≈37%) é mais interpretável no dia a dia do que a variância (1.400).
- 💡 **Dica:** o cálculo da variância é só uma etapa intermediária — o objetivo final quase sempre é o desvio padrão, porque ele está na mesma unidade dos dados originais.
- ⚠️ **Ponto de atenção:** quanto maior o desvio padrão, mais distantes os dados estão da média (maior dispersão/incerteza); quanto menor, mais os dados estão concentrados perto da média.

### 3. 🧠 Raciocínio Lógico
- A média sozinha pode dar uma falsa sensação de estabilidade (patrão acha que 60% de média já é suficiente).
- Para entender o afastamento real dos dados, calcula-se a diferença de cada valor para a média.
- Essas diferenças somadas sempre dão zero, pois valores acima e abaixo da média se compensam — logo, não dá pra tirar uma média direta delas.
- Para contornar isso, eleva-se cada diferença ao quadrado, o que elimina os sinais negativos e viabiliza o cálculo de uma média (a variância).
- Como elevar ao quadrado distorce a escala original dos dados, aplica-se a raiz quadrada da variância para voltar à unidade original — esse resultado final é o desvio padrão.
- Quanto maior o desvio padrão resultante, mais os dados estão espalhados em relação à média; quanto menor, mais concentrados.

---
**Salvar como:** `03-rocketseat-da-medidas-de-dispersao-variancia-desvio-padrao-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.