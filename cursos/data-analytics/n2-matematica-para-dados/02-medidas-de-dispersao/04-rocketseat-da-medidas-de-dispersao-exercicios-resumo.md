# 📌 Exercício de Fixação — Amplitude, Variância e Desvio Padrão

### 1. Conceito Central
Aula de exercício prático que aplica, num único conjunto de dados real (vendas diárias de uma loja online ao longo de uma semana), todas as medidas vistas até aqui: mínimo, máximo, amplitude, média, moda, mediana, variância e desvio padrão. O objetivo é mostrar como essas medidas se combinam numa análise só, e como a leitura conjunta delas (não cada uma isolada) revela o comportamento real dos dados — nesse caso, uma forte concentração/estabilidade nas vendas.

### 2. Pontos-chave e Sintaxe
- **Dados da semana (vendas diárias):** Segunda = 10, Terça = 12, Quarta = 8, Quinta = 10, Sexta = 10.

```
1. Mínimo e máximo:
   Mínimo = 8 (quarta-feira)
   Máximo = 12 (terça-feira)

2. Amplitude = máximo - mínimo:
   Amplitude = 12 - 8 = 4

3. Média = soma dos valores / quantidade de valores:
   (10 + 12 + 8 + 10 + 10) / 5 = 50 / 5 = 10

4. Moda = valor que mais se repete:
   10 (aparece 3 vezes)

5. Mediana = valor central, com os dados em ordem (rol):
   8, 10, 10, 10, 12 -> valor central = 10

6. Variância:
   - Diferença de cada valor para a média, já elevada ao quadrado:
     (10 - 10)² = 0
     (12 - 10)² = 4
     (8  - 10)² = 4
     (10 - 10)² = 0
     (10 - 10)² = 0
   - Média dessas diferenças ao quadrado:
     (0 + 4 + 4 + 0 + 0) / 5 = 8 / 5 = 1,6
   - Variância = 1,6

7. Desvio padrão = raiz quadrada da variância:
   √1,6 ≈ 1,26
```

- 💡 **Dica:** quando média, moda e mediana coincidem no mesmo valor (aqui, as três deram 10), é um indício forte de que os dados estão bem concentrados/simétricos em torno desse valor central.
- ⚠️ **Ponto de atenção:** amplitude baixa (4) **e** variância/desvio padrão baixos (1,6 / ≈1,26) contam a mesma história por ângulos diferentes — os valores não estão distantes uns dos outros, o que indica estabilidade nas vendas. Quanto menor a variância, maior a assertividade de quem está analisando os dados para prever cenários futuros (ex: planejamento de estoque, ações com o time de vendas).

### 3. 🧠 Raciocínio Lógico
- Primeiro se identificam mínimo e máximo, que já permitem calcular a amplitude (medida mais simples e rápida).
- Em seguida calcula-se a média, que serve de base tanto para a leitura geral quanto para o cálculo da variância.
- Moda e mediana são calculadas à parte (observação de repetição e ordenação dos valores), mas aqui coincidem com a média — reforçando a leitura de concentração.
- Para a variância, repete-se o processo das aulas anteriores: diferença de cada valor para a média → elevar ao quadrado (eliminar sinais negativos) → tirar a média desses quadrados.
- O desvio padrão é a raiz quadrada da variância, trazendo o resultado de volta à escala original dos dados (vendas), facilitando a interpretação.
- Conclusão da análise: amplitude pequena + variância/desvio padrão pequenos + média=moda=mediana → dados concentrados, vendas estáveis, maior previsibilidade.

---
**Salvar como:** `04-rocketseat-da-medidas-de-dispersao-exercicios-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.