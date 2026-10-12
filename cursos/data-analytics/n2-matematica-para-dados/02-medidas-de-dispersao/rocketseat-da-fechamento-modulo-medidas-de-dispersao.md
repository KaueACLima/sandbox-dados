# 🏆 Fechamento de Módulo — Medidas de Dispersão
**Trilha:** Rocketseat — Formação Data Analytics
**Nível:** 2 — Matemática para Dados
**Módulo:** Medidas de Dispersão
**Data do fechamento:** 09/10/2026
**Origem:**  módulo resgatado do "buraco de contexto" — aulas assistidas antes do uso do notetaker, processadas a partir da transcrição original recuperada (não é reconstrução por memória; ver Core → "Decisões estruturais").
**Quiz oficial da plataforma:** confirmado em 09/10/2026 com **100% (5/5)**.

### 1. Resumo Executivo
Este módulo resolve um problema que a Estatística Descritiva deixa em aberto: a média (e as demais medidas de tendência central) resume um conjunto de dados num único número, mas **não diz nada sobre o quão espalhados ou concentrados** esses dados estão ao redor dela. Duas bases completamente diferentes — duas empresas com salários muito distintos, três lojas com faturamentos muito díspares — podem ter exatamente a mesma média e ainda assim representar realidades opostas em termos de previsibilidade e risco.

As medidas de dispersão entram para preencher essa lacuna, em ordem crescente de sofisticação. A **amplitude** é a mais simples: só subtrai o menor valor do maior, dando uma noção rápida (mas grosseira) do espalhamento. A **variância** vai além: calcula a distância de cada valor individual em relação à média, eleva ao quadrado para neutralizar os sinais negativos (que, somados, sempre zeram) e tira a média desses quadrados — só que o resultado fica numa unidade de medida distorcida. O **desvio padrão** resolve essa distorção aplicando a raiz quadrada da variância, devolvendo o valor à escala original dos dados e tornando-o diretamente interpretável.

A grande lição prática para um Analista Júnior: **nunca reportar ou confiar só na média isoladamente.** Sempre que possível, complementar com amplitude e/ou desvio padrão — eles revelam se os dados são estáveis e previsíveis (dispersão baixa) ou instáveis e arriscados (dispersão alta), o que muda completamente a decisão ou recomendação de negócio a ser tomada sobre aquele conjunto de dados.

### 2. Glossário Técnico
*Medida de dispersão:* categoria de estatística que mede o quanto os valores de um conjunto de dados se espalham ou se concentram em torno de uma medida de tendência central (geralmente a média).

*Amplitude:* diferença entre o maior e o menor valor de um conjunto de dados (máximo − mínimo). É a medida de dispersão mais simples e rápida de calcular.

*Variância:* média das diferenças, elevadas ao quadrado, entre cada valor do conjunto e a média do conjunto. Serve como etapa intermediária para o desvio padrão, mas fica numa unidade de medida "ao quadrado", difícil de interpretar diretamente.

*Desvio padrão:* raiz quadrada da variância. Mostra, em média, o quanto os valores se afastam da média, já na mesma unidade de medida dos dados originais — por isso é a medida de dispersão mais usada na prática.

*Elevar ao quadrado (na variância):* operação usada para eliminar os sinais negativos das diferenças (valor − média), já que a soma dessas diferenças sempre resulta em zero e impediria o cálculo de uma média direta.

*Raiz quadrada (no desvio padrão):* operação inversa ao quadrado, usada para trazer o resultado da variância de volta à escala original dos dados.

*Concentração vs. dispersão:* quanto menor a amplitude/variância/desvio padrão, mais concentrados (previsíveis) estão os dados; quanto maiores, mais dispersos (incertos) eles são.

### 3. Desafio de Fixação (Quiz Interativo)

**Questão 1.** Dois vendedores de uma loja têm a mesma média de vendas diárias: 20 unidades/dia. O Vendedor A vendeu, nos últimos 5 dias: 19, 20, 21, 20, 20. O Vendedor B vendeu: 5, 35, 10, 30, 20. Sem fazer nenhuma conta, apenas observando os dois conjuntos, qual vendedor você esperaria que tivesse a **maior amplitude**, e por quê?

**Questão 2.** Um conjunto de dados tem variância igual a 81. Qual é o valor do desvio padrão desse conjunto, e qual operação matemática você usou para chegar nele?

**Questão 3.** Durante o cálculo da variância, ao subtrair cada valor da média, um colega seu encontrou os resultados -4, 6 e -2 e, antes de elevar ao quadrado, já foi somando tudo e dividindo por 3 para "economizar um passo". Isso está certo ou errado? Explique o que vai dar errado nesse atalho e por que a etapa de elevar ao quadrado não pode ser pulada.

### 4. Correção Comentada — Gabarito

**Questão 1 — ✅ Correta.**
O **Vendedor B** tem a maior amplitude. A amplitude mede só a distância entre o maior e o menor valor de um conjunto, ignorando tudo que está no meio. Observando os dados sem nenhuma conta:
- Vendedor A: valores entre 19 e 21 — faixa muito estreita.
- Vendedor B: valores entre 5 e 35 — faixa muito mais larga.

Formalmente, isso se confirma calculando a amplitude de cada um:
$$\text{Amplitude}_A = 21 - 19 = 2 \qquad \text{Amplitude}_B = 35 - 5 = 30$$

O ponto central da questão: **mesma média (20) não significa mesmo comportamento** — o Vendedor A é estável e previsível, o Vendedor B é errático, mesmo entregando a mesma média de vendas no período.

**Questão 2 — ✅ Correta.**
O desvio padrão é **9**, obtido pela **raiz quadrada da variância**:
$$\text{Desvio Padrão} = \sqrt{\text{Variância}} = \sqrt{81} = 9$$

Essa é exatamente a relação ensinada no módulo: a variância sempre precede o desvio padrão, e a raiz quadrada é a operação que desfaz a distorção de escala introduzida pelo passo de elevar ao quadrado — devolvendo o resultado à unidade de medida original dos dados.

**Questão 3 — ✅ Correta e bem argumentada.**
O atalho do colega está **totalmente errado**. Somar os desvios brutos (\(-4 + 6 - 2 = 0\)) sempre vai dar **zero**, porque os desvios positivos e negativos em relação à média sempre se cancelam matematicamente — essa soma é zero por definição, não por coincidência dos números escolhidos no exemplo.

A etapa de elevar ao quadrado não pode ser pulada por dois motivos:
- **Eliminar os sinais negativos:** sem isso, a soma das diferenças sempre zera, e não existe uma "variância zero" real escondida atrás disso — o cálculo simplesmente não funciona.
- **Medir a dispersão real:** só depois de todos os valores virarem positivos (via quadrado) é que somar e tirar a média revela, de fato, o tamanho médio do afastamento de cada ponto em relação à média — que é o que a variância se propõe a medir.

**Resultado final: 3 de 3 corretas**, com domínio completo do raciocínio de amplitude, da relação variância↔desvio padrão (raiz quadrada) e do motivo matemático por trás do passo de elevar ao quadrado.

---
**DoD (Definição de Pronto):** 4 aulas resumidas (Introdução, Amplitude, Variância e Desvio Padrão, Exercícios) + quiz oficial da plataforma 100% (5/5) + fechamento de módulo com teste de fixação próprio 100% (3/3) → **Módulo 100% concluído.**