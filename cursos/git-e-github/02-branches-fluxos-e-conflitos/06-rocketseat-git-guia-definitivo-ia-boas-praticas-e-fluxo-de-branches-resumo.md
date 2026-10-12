# 📌 Boas Práticas e Fluxo de Branches (GitFlow)

### 1. Conceito Central
Esta aula parte de uma pergunta de fundo — por que usamos Git — para justificar por que só a ferramenta não basta: é preciso também um **workflow** (fluxo de trabalho), um conjunto de regras e convenções que definam como as branches são criadas, nomeadas, integradas e liberadas. Sem esse padrão, um time com dezenas de branches abertas simultaneamente não sabe a partir de qual branch criar a próxima, nem para qual branch mandar cada merge — e isso aumenta drasticamente a chance de conflito e confusão. A aula apresenta o **GitFlow**, criado por Vincent Driessen, um dos fluxos mais conhecidos do mercado, que resolve isso atribuindo um **papel específico** a cada branch: duas branches principais (main e develop) e três tipos de branches auxiliares (feature, release e hotfix), cada uma com uma origem e um destino bem definidos.

### 2. Pontos-chave e Sintaxe
- **Motivações para usar Git** (retomadas do curso): lidar com alterações simultâneas no mesmo arquivo, rastrear quem fez cada mudança, manter um histórico organizado, ter controle de versões, viabilizar trabalho paralelo e ter uma integração de código controlada.
- **Branches principais:**
  - **main:** versão estável em produção — o que o cliente final usa.
  - **develop:** branch de desenvolvimento, onde o time integra as funcionalidades já prontas antes de irem para produção.
- **Branches auxiliares:**
  - **feature:** criada a partir da develop, para desenvolver uma funcionalidade nova (ex: `feature/login`, `feature/payment`). Ao terminar, é mesclada de volta na develop e **deletada** — não faz sentido acumular branches de feature já finalizadas.
  - **release:** criada a partir da develop quando uma versão está pronta para ser preparada (ajustes finais, documentação, testes por pessoas não técnicas do time — design, produto, stakeholders, e até clientes que pediram a funcionalidade). Depois de validada, é integrada tanto na main quanto de volta na develop.
  - **hotfix:** criada a partir da **main** (não da develop), para resolver um problema urgente em produção. Depois de corrigido, é integrada tanto na main quanto na develop — para que ambas as branches fiquem sincronizadas com a correção.
- 💡 **Dica:** a razão de a release existir como etapa intermediária (em vez de ir direto da develop para a main) é ter um ambiente de pré-lançamento: sem ela, qualquer problema só apareceria depois que o cliente final já tivesse acesso, e pessoas externas teriam acesso a funcionalidades ainda em finalização se testassem direto na develop.
- ⚠️ **Ponto de atenção:** a hotfix nasce da main, e não da develop, propositalmente — o objetivo é resolver o problema o mais rápido possível, partindo exatamente de onde ele está acontecendo (produção), sem esperar ou depender do estado atual do desenvolvimento.
- 🔎 **Observação:** GitFlow traz mais verbosidade e mais branches que um fluxo simples, mas essa complexidade extra compra clareza: a qualquer momento, dá para saber de onde uma feature partiu, de onde uma correção deve sair, e para onde cada tipo de mudança deve ir.
- A aula deixa claro que o padrão específico de nomenclatura pode variar por empresa/time — o essencial é que todo o time esteja alinhado e confortável com a convenção adotada, tanto para branches quanto (no futuro, próxima aula) para commits.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[main] -> ponto de partida de versões estáveis em produção

[develop] -> branch de integração do time, recebe merges de features

[feature/nome] -> criada a partir de [develop]
              -> desenvolvimento da funcionalidade
              -> merge de volta em [develop]
              -> branch deletada após o merge

[release/x.y.z] -> criada a partir de [develop] (já com features integradas)
                 -> ajustes finais, testes não-técnicos
                 -> merge em [main] (lançamento oficial)
                 -> merge de volta em [develop] (mantém develop sincronizada com a main)

[hotfix/nome-do-problema] -> criada a partir de [main] (onde o problema está em produção)
                           -> correção urgente
                           -> merge em [main] (resolve o problema em produção)
                           -> merge também em [develop] (evita que o bug reapareça em futuras releases)
```

### 4. Links e Referências Oficiais
- **GitFlow:** modelo de workflow de branches criado por Vincent Driessen, com papéis definidos para cada tipo de branch. Vale consultar o artigo original: [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/).
- **main / develop:** branches principais e permanentes do fluxo — produção e integração de desenvolvimento, respectivamente.
- **feature, release, hotfix:** branches auxiliares e temporárias, cada uma com origem e destino específicos dentro do fluxo.
- **Release:** termo usado para designar o lançamento de uma nova versão ou funcionalidade da aplicação.
- **Conventional Commits:** mencionado como tema da próxima aula — um padrão para escrever mensagens de commit com significado claro.

---
**Salvar como:** `NN-rocketseat-git-guia-definitivo-ia-boas-praticas-e-fluxo-de-branches-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.

Me diga o número desta aula dentro do módulo "Branches, fluxos e conflitos" pra eu fechar o nome do arquivo (troca o `NN`).

### 🏛️ Conexão de Engenharia (Medallion & GCP)
Não há código nesta aula — é um fluxo organizacional de branches, e a conexão aqui é de **processo**, não de camada de dado específica. O modelo GitFlow (feature → develop → release → main, com hotfix saindo direto da main) é diretamente aplicável ao repositório do seu pipeline Dataform: uma feature seria o desenvolvimento de um novo model Silver/Gold, a develop seria onde o time integra e testa as transformações antes de irem para produção, a release seria a janela de validação antes de um deploy agendado no BigQuery, e a hotfix cobriria uma correção urgente num model já rodando em produção (ex: um erro numa agregação da camada Gold que está gerando dado errado para um dashboard). Vale adotar essa estrutura, ainda que de forma simplificada, como convenção do seu projeto de portfólio (Frente 6) — é exatamente o tipo de organização que diferencia um repositório amador de um que segue padrão de mercado.