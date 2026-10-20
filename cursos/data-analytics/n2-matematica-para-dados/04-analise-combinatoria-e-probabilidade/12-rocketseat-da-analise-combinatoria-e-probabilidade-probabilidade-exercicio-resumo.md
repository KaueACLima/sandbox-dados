# 📌 Probabilidade na prática: funil de e-mail marketing

### 1. Conceito Central
A aula aplica a fórmula `P(E) = n(E) / n(S)` a um caso real: uma campanha de e-mail marketing. O ponto principal é **definir corretamente o espaço amostral** em cada pergunta, porque ele muda conforme a pergunta.

Quando a pergunta traz uma condição ("entre os que clicaram..."), o espaço amostral **diminui**. Isso é a **probabilidade condicional**, apresentada aqui pela primeira vez. Os resultados formam um **funil** que mostra onde a campanha perde clientes.

### 2. Pontos-chave e Sintaxe

#### O cenário
- Um e-mail marketing enviado para **1.000 pessoas**.
- Depois de uma semana (dado do print): **200 clicaram** e **50 compraram**.

#### As três perguntas

| Pergunta | n(S) (espaço amostral) | n(E) (evento) | Cálculo | Resultado |
|---|---|---|---|---|
| 1) Probabilidade de um cliente aleatório ter **clicado** | 1.000 (todos os e-mails enviados) | 200 | `200/1000` | **0,2 = 20%** |
| 2) Probabilidade de um cliente aleatório ter **comprado** | 1.000 | 50 | `50/1000` | **0,05 = 5%** |
| 3) **Entre os que clicaram**, quantos compraram? | **200** (só quem clicou) | 50 | `50/200` | **0,25 = 25%** |

- 💡 **Dica (fala do professor):** a pergunta que o analista deve se fazer é "qual é o meu espaço amostral e quais são os casos favoráveis?".
- ⚠️ **Ponto de atenção:** nas perguntas 1 e 2 o denominador é 1.000. Na 3 a condição "entre os que clicaram" **reduz o espaço amostral para 200**, e o denominador muda.
- 🔎 **Observação:** o cálculo da pergunta 3 só fecha porque os 50 compradores estão entre os 200 que clicaram. A aula usa esse pressuposto sem dizê-lo.
- **Probabilidade condicional:** a aula só a nomeia e aplica a lógica do espaço reduzido, sem fórmula formal.
- **Formatos aceitos para o resultado:** decimal entre 0 e 1, ou porcentagem. O professor mostra `200/1000 = 20/100 = 20% = 0,20`.

#### O funil da campanha (print da aula)

| Etapa | Quantidade | Taxa | Leitura do professor |
|---|---|---|---|
| Enviados | 1.000 pessoas | — | ponto de partida |
| Clicaram | 200 | 20% | **CTR** (taxa de clique) |
| Compraram | 50 | 5% | taxa de conversão baixa |
| Conversão após o clique | — | 25% | 25% dos que clicaram compraram |

#### Leitura analítica (o que o professor sugere investigar)
- **80% não clicaram.** Hipóteses levantadas:
  - texto do e-mail mal elaborado;
  - imagem inadequada;
  - e-mail enviado para as pessoas erradas;
  - público mal analisado.
- **Só 5% compraram**, ou seja, uma conversão geral baixa. Perguntas levantadas: o e-mail ou a propaganda estavam corretos?
- **25% de conversão após o clique** é considerado um número bom, de pessoas realmente decididas.
  - Ideia sugerida: analisar quem foram essas 200 pessoas e destinar mais campanhas a esse público.
- 💡 **Dica (fala do professor):** o analista faz testes em cima dessas análises e **ataca onde há maior dificuldade**. A frase central é "a gente não trabalha em cima de achismo".
- ⚠️ **Divergência áudio × print:** o professor diz "80 pessoas não clicaram", mas o print mostra **80%**. Como foram 1.000 envios e 200 cliques, 80% corresponde a **800 pessoas**. Para o caderno, anotar **80% (800 pessoas)**.
- O trecho do áudio sobre a conversão ficou truncado ("1.005%"). O print confirma o sentido: 5% de 1.000.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** ler a pergunta e identificar **de quem** estamos falando. Esse grupo é o **espaço amostral**.
  - Todos os que receberam o e-mail → n(S) = 1.000.
  - Só quem clicou → n(S) = 200.
- **Passo 2:** identificar **o que se quer contar** dentro desse grupo (cliques, compras). Esse é o **evento**.
- **Passo 3:** verificar se a pergunta traz uma **condição** ("entre os que...").
  - Se traz, o espaço amostral é reduzido e a probabilidade é **condicional**.
  - Se não traz, usa-se o total.
- **Passo 4:** calcular `n(E) / n(S)` e simplificar, ou converter para %.
- **Passo 5:** interpretar o resultado no funil e decidir onde investigar: o clique (20%), a conversão geral (5%) ou a conversão após o clique (25%).

### 4. Links e Referências Oficiais
Aula prática de teoria aplicada, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Probabilidade condicional:** probabilidade calculada dentro de um espaço amostral reduzido por uma condição ("entre os que clicaram..."). Esta aula só a apresenta, sem fórmula.
- **CTR (taxa de clique):** proporção de pessoas que clicaram no e-mail. Na aula, 20% (200 de 1.000).
- **Taxa de conversão:** proporção que finalizou a compra. Na aula, 5% do total enviado.
- **Conversão após o clique:** proporção que comprou entre os que clicaram. Na aula, 25%.
- **Funil:** representação das etapas da campanha (enviados → cliques → compras), usada para localizar onde há perda.
- **Espaço amostral e evento (aula 10), P(E) = n(E)/n(S) (aula 11):** base do cálculo de todas as perguntas.
