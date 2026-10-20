# 📌 Probabilidade Condicional

### 1. Conceito Central
**Probabilidade condicional** é a chance de um evento acontecer **dado que outro evento já aconteceu**. Escreve-se **P(A | B)**, lido como "a probabilidade de A, dado B".

Na prática, a condição **reduz o espaço amostral** aos casos em que B ocorreu, e a conta é feita só dentro desse grupo. O professor lembra que a aula anterior (funil do e-mail) já usou essa lógica ao calcular as compras entre os 200 que clicaram.

### 2. Pontos-chave e Sintaxe
- **Notação:** `P(A | B)` = probabilidade de **A** acontecer, dado que **B** já aconteceu.
- ⚠️ **Ponto de atenção:** a pergunta decisiva é "qual é o meu espaço amostral?". A expressão "sabendo que..." ou "entre os que..." indica que o espaço amostral é o grupo da condição, e não o total.

#### Exemplo: e-commerce
- **Dados:** 1.000 pessoas visitaram o site, **300** colocaram produtos no carrinho e **90** finalizaram a compra.
- **Pergunta:** qual a probabilidade de alguém comprar, **sabendo que colocou algo no carrinho**?
- **Espaço amostral:** `n(S) = 300`, só quem colocou algo no carrinho.
- **Evento:** `n(E) = 90`, quem finalizou a compra.
- **Cálculo:**

```
P(E) = 90 / 300
     = 9 / 30        (corta um zero em cima e embaixo)
     = 3 / 10        (divide em cima e embaixo por 3)
     = 30 / 100      (multiplica em cima e embaixo por 10, para ficar sobre 100)
     = 30%
```

- 🔎 **Observação:** o número **1.000** (visitantes) **não entra na conta**. Como a condição é "colocou algo no carrinho", ele não faz parte do espaço amostral. O professor destaca que é preciso ter atenção a essa escolha.
- 💡 **Dica (fala do professor):** para converter para porcentagem, coloque a fração com denominador 100. Se está sobre 10, multiplique em cima e embaixo por 10.
- A aula **não traz a fórmula formal** da probabilidade condicional, só a notação e a lógica do espaço amostral reduzido.

#### Onde o analista usa (print e áudio)
- **Testes A/B:** chance de um caso dar certo condicionada a algo que já aconteceu ou a um evento de interesse.
- **Análise de churn:** probabilidade de uma pessoa sair, dados os comportamentos que ela já teve no passado.
- **Modelos preditivos:** por exemplo, a probabilidade de comprar dado que a pessoa entrou no site, colocou itens no carrinho e preencheu quase tudo.
- **Ideia central (fala do professor):** o analista trabalha muito com algo que já aconteceu e com a chance de acontecer novamente. Segundo ele, quase tudo o que o analista faz é probabilidade condicional.

#### Frase de encerramento (Laplace)
- Citação mostrada no slide, de Pierre-Simon Laplace: a teoria das probabilidades é "bom senso reduzido ao cálculo".
- **Leitura do professor:** probabilidade não é só matemática. É o **cálculo junto com o bom senso**, e os dois precisam andar juntos para uma boa análise dos dados.
- ⚠️ **Fora do conteúdo técnico:** o professor também atribui a Laplace a criação do teste A/B. Isso não consta nos prints e não foi confirmado, então não vale levar para o caderno como fato.

### 3. 🧠 Raciocínio Lógico
- **Passo 1:** ler a pergunta e procurar a **condição** ("sabendo que...", "entre os que...", "dado que...").
- **Passo 2:** a condição define o **espaço amostral**, que passa a ser só o grupo em que ela ocorreu (aqui, 300 pessoas, e não 1.000).
- **Passo 3:** o **evento** é o que se quer contar dentro desse grupo (aqui, 90 compras).
- **Passo 4:** calcular `n(E) / n(S)` e simplificar, ou converter para %. Resultado: 90/300 = 30%.
- **Passo 5:** interpretar o resultado como "dos que fizeram B, quantos fizeram A".

### 4. Links e Referências Oficiais
Aula de teoria aplicada, sem documentação oficial correspondente, então os termos ficam sem hyperlink:
- **Probabilidade condicional, P(A | B):** probabilidade de A acontecer dado que B já aconteceu. O espaço amostral é reduzido ao grupo de B.
- **Espaço amostral reduzido:** o grupo definido pela condição, que vira o denominador da conta.
- **Teste A/B:** citado como aplicação da probabilidade condicional. A aula não o explica.
- **Churn:** saída de clientes. Na aula, aparece como probabilidade de saída dado o comportamento passado.
- **Modelos preditivos:** citados como uso frequente de probabilidade condicional. A aula não os desenvolve.
- **Pierre-Simon Laplace:** autor da frase sobre probabilidade e bom senso.