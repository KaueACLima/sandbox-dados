# 🗝️ Gabarito Consolidado — Análise Combinatória e Probabilidade

> Rocketseat · Data Analytics · Nível 2 · Quiz de fixação do fechamento (20/10/2026) · resultado: **3/3 corretas**.
> Vai para o **caderno + repo**. **Não sobe na base** (mantém o fechamento sem spoiler para a revisão de 30 dias, a partir de 19/11/2026).
> Cada questão traz: a pergunta, a resposta original como foi enviada (só a notação matemática foi convertida para texto simples) e a resposta corrigida e completa.

---

## Questão 1 — Escolher entre somar e multiplicar

**Pergunta:** uma loja vai disparar uma campanha por **um único canal**: ou e-mail (3 modelos de mensagem), ou SMS (2 modelos), ou WhatsApp (4 modelos). Cada disparo vai para **um** de 2 públicos (clientes novos ou recorrentes). Quantas ações diferentes (canal + modelo + público) a loja consegue montar? Explique onde somou, onde multiplicou e por quê.

**Resposta original:**
> A loja consegue montar 18 ações diferentes de campanha.
> - Onde somou: na escolha dos modelos de mensagem por canal. Como a campanha será disparada por um único canal (ou e-mail, ou SMS, ou WhatsApp), as opções se excluem mutuamente. Total de modelos = 3 (e-mail) + 2 (SMS) + 4 (WhatsApp) = 9 modelos.
> - Onde multiplicou: na combinação do modelo escolhido com o público-alvo. Como cada disparo precisa obrigatoriamente de um modelo E de um público (2 opções), usamos o Princípio Multiplicativo. Total de ações = 9 modelos × 2 públicos = 18 ações.

**Resposta corrigida e completa:** ✅ **18 ações.**
- **Leitura do enunciado pelos conectivos:** `(e-mail OU SMS OU WhatsApp) E (público)`. O **OU** pede **soma** (princípio aditivo) e o **E** pede **multiplicação** (princípio multiplicativo), a regra de ouro da aula de PFC.
- **Passo 1 (OU → soma):** como só um canal é usado por disparo, os modelos de canais diferentes são alternativas que não acontecem juntas: `3 + 2 + 4 = 9` modelos possíveis.
- **Passo 2 (E → multiplica):** cada disparo precisa de um modelo **e** de um público: `9 × 2 = 18`.
- **Conferência por outro caminho (mesma estrutura do exemplo dos caminhos de A até E):** multiplicar dentro de cada alternativa e somar no fim:
  - e-mail: `3 × 2 = 6`
  - SMS: `2 × 2 = 4`
  - WhatsApp: `4 × 2 = 8`
  - total: `6 + 4 + 8 = 18` ✔️
- **Lição:** o mesmo problema usa os dois princípios. Dentro de uma alternativa as escolhas acontecem juntas (**E**, multiplica), e entre alternativas só uma acontece (**OU**, soma).

---

## Questão 2 — A ordem importa?

**Pergunta:** você testou 7 assuntos de e-mail. (a) Indicar o 1º e o 2º melhores, nessa ordem: de quantas formas? (b) Escolher 3 assuntos para um novo teste, sem ordem: de quantas formas? Diga a técnica e por que a ordem importa ou não.

**Resposta original:**
> (a) Indicar o 1º e o 2º melhores assuntos: 42 formas diferentes. Técnica: Arranjo, calculado por 7 × 6 = 42. A ordem importa porque a posição define a classificação: escolher o Assunto A para 1º e o B para 2º é um resultado totalmente diferente de ter o B em 1º e o A em 2º.
> (b) Escolher 3 assuntos para um novo teste: 35 formas diferentes. Técnica: Combinação, calculada por (7 × 6 × 5) / (3 × 2 × 1) = 35. A ordem NÃO importa porque o grupo final testado será o mesmo: selecionar [A, B, C] ou [C, B, A] resulta exatamente no mesmo conjunto de e-mails para o teste.

**Resposta corrigida e completa:** ✅ **(a) 42 · (b) 35.**

**(a) Arranjo simples (a ordem importa):**
- Pelo PFC: 7 candidatos para o 1º lugar **E** 6 para o 2º (quem já está em 1º não pode ocupar o 2º): `7 × 6 = 42`.
- Pela fórmula: `A(7, 2) = 7! / (7 − 2)! = 7! / 5! = (7 × 6 × 5!) / 5! = 7 × 6 = 42`. O `5!` se cancela, como nos exemplos de pódio da aula de arranjo.
- *Por que arranjo:* a ordem faz diferença (1º ≠ 2º) e nenhum assunto se repete.

**(b) Combinação simples (a ordem não importa):**
- Fórmula: `C(7, 3) = 7! / [3! × (7 − 3)!] = 7! / (3! × 4!) = (7 × 6 × 5) / (3 × 2 × 1) = 210 / 6 = 35`.
- *Passo a passo conceitual:* primeiro conta-se como se a ordem importasse (arranjo): `7 × 6 × 5 = 210`. Cada trio, porém, foi contado 6 vezes, uma por ordem possível (`3! = 6`, como ABC, ACB, BAC, BCA, CAB, CBA). Dividindo por `3!`, cada grupo conta uma vez só: `210 / 6 = 35`.
- *Por que combinação:* o que importa é **quais** 3 assuntos entram no teste, não a ordem em que foram escolhidos.

**Lição:** a pergunta "a ordem importa?" decide tudo. Se importa, é arranjo. Se não importa, é arranjo dividido por `p!`, a combinação.

---

## Questão 3 — Probabilidade condicional

**Pergunta:** um time de atendimento acompanhou **800 clientes**. **200** abriram chamado de suporte e, desses, **50** cancelaram o contrato. Entre os **600** que não abriram chamado, **30** cancelaram. (a) Probabilidade de cancelar entre os que abriram chamado? (b) Entre os que não abriram? (c) Qual grupo tem maior chance e qual o espaço amostral de cada item? (d) Clássica, empírica ou subjetiva? Por quê?

**Resposta original:**
> (a) Probabilidade de cancelar entre os que abriram chamado: P = 50/200 = 0,25 → **25%**.
> (b) Probabilidade de cancelar entre os que não abriram chamado: P = 30/600 = 0,05 → **5%**.
> (c) O grupo que abriu chamado tem uma chance muito maior de cancelar (25% contra apenas 5%). O espaço amostral do item (a) é restrito a 200 clientes (apenas quem abriu chamado). O espaço amostral do item (b) é restrito a 600 clientes (apenas quem não abriu chamado).
> (d) Este número é uma probabilidade empírica (ou frequencial). Foi calculada com base na observação e em dados históricos reais (o histórico coletado dos 800 clientes). Não é clássica (que deduz chances puramente na teoria, como em dados de 6 lados) nem subjetiva (que se baseia em palpites ou intuição).

**Resposta corrigida e completa:** ✅ **(a) 25% · (b) 5% · (c) quem abriu chamado · (d) empírica.**
- **Fórmula-base:** `P(E) = n(E) / n(S)`. Aqui a condição ("entre os que...") reduz o espaço amostral ao grupo da condição, que é o que caracteriza a **probabilidade condicional**, `P(A | B)`.
- **(a)** `P(cancelar | abriu chamado)`: `n(S) = 200`, `n(E) = 50` → `50 / 200 = 1/4 = 0,25 = 25%`.
- **(b)** `P(cancelar | não abriu chamado)`: `n(S) = 600`, `n(E) = 30` → `30 / 600 = 1/20 = 0,05 = 5%`.
- **(c)** O grupo que abriu chamado tem maior chance (25% contra 5%). O espaço amostral é **200** no item (a) e **600** no item (b). ⚠️ Usar 800 como denominador ignoraria a condição e responderia outra pergunta. Na escala da aula, 25% é o ponto nomeado como **improvável**.
- **(d)** **Probabilidade empírica:** o número vem de dados reais já observados (o histórico dos 800 clientes), como o exemplo de 300 compras em 1.000 acessos. **Não é clássica**, que vem da lógica matemática com casos igualmente possíveis (sorteio, dado). **Não é subjetiva**, que vem de intuição ou experiência sem levantamento concreto.
- **Lição:** em probabilidade condicional, a primeira decisão é o **denominador**. A pergunta "entre quem?" define o espaço amostral, e cada grupo tem o seu.

---
**Resultado: 3/3.**