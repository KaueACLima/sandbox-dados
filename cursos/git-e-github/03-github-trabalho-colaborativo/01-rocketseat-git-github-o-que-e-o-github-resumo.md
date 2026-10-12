# 📌 O que é o GitHub?

### 1. Conceito Central
O Git é uma ferramenta **local** de controle de versão — ela roda dentro da sua máquina e versiona o projeto ali, sem depender de internet. O GitHub é outra coisa: uma **plataforma online** que hospeda esses repositórios na nuvem e permite colaboração entre pessoas. A analogia usada na aula resume bem: se o Git é um editor de texto, o GitHub é o Google Docs — o lugar onde o que foi versionado localmente fica acessível, compartilhável e editável em conjunto com outras pessoas. Tecnicamente, o Git guarda o código na sua máquina; o GitHub guarda esse mesmo histórico em um servidor remoto.

### 2. Pontos-chave e Sintaxe
- **Diferença central:** Git = repositório local (na sua máquina). GitHub = repositório remoto (hospedado no servidor do GitHub), feito para hospedagem e colaboração.
- **Por que usar o GitHub** (motivos citados na aula):
  - Backup na nuvem / segurança — o código não depende só da sua máquina (perda, roubo, formatação).
  - Acesso de qualquer lugar, mesmo de uma máquina que não é a sua.
  - Compartilhamento de código — outras pessoas podem ver, avaliar e colaborar no que você está construindo.
  - Portfólio profissional — hoje em processo seletivo se pede o GitHub, não um `.zip` do projeto.
  - Trabalho colaborativo entre múltiplas pessoas no mesmo projeto.
- **Configuração inicial:** antes de usar o GitHub, é preciso ter nome de usuário e e-mail configurados no Git localmente (passo já feito em aulas anteriores) e, depois, criar uma conta gratuita em github.com (via Google, Apple ou e-mail/senha).
- **Autenticação — duas formas possíveis:**
  - **HTTPS:** o GitHub não aceita mais senha para autenticação via terminal. No lugar da senha, usa-se um **Personal Access Token** — uma chave de acesso temporária. Ele é gerado em *Settings → Developer Settings → Personal Access Tokens → Tokens (classic) → Generate new token*, com: uma nota de identificação, um prazo de expiração (a aula recomenda 30–90 dias) e a permissão `repo` marcada (controle completo sobre os repositórios da conta). O token só aparece uma vez na tela — precisa ser copiado e usado imediatamente. Tokens antigos podem ser revogados na mesma tela.
  - **SSH:** gera um **par de chaves criptografadas** — uma privada (fica só na sua máquina) e uma pública (é cadastrada no GitHub, em *Settings → SSH and GPG Keys → New SSH Key*). Na autenticação, o GitHub compara a chave pública cadastrada com a privada da sua máquina para confirmar identidade, sem pedir login repetido.
- ⚠️ **Ponto de atenção:** a aula recomenda explicitamente SSH em vez de HTTPS, porque o token por HTTPS é descrito como menos seguro, expira e frequentemente exige regeneração manual — enquanto o SSH, uma vez configurado, elimina a necessidade de reautenticar a cada operação.
- 🔎 **Observação:** no Windows, o processo de geração de chave SSH deve ser feito pelo **Git Bash** (instalado junto com o Git), porque o PowerShell ou o terminal padrão do Windows podem não reconhecer os comandos usados.
- A transcrição descreveu os comandos verbalmente (sem ditar a sintaxe exata), então não há bloco de código a reconstruir aqui — apenas a sequência lógica das etapas.

### 3. 🏗️ Arquitetura / Diagrama Lógico
```
[Preciso autenticar minha máquina no GitHub]
  -> Qual método escolher?
     -> HTTPS: [gera Personal Access Token] -> [token com validade e permissão "repo"] -> [usado como senha no terminal] -> [expira e precisa ser regenerado periodicamente]
     -> SSH: [gera par de chaves (privada + pública)] -> [chave pública cadastrada no GitHub] -> [chave privada fica na máquina] -> [GitHub compara as duas chaves a cada acesso] -> [teste de conexão confirma autenticação com sucesso]
```

### 4. Links e Referências Oficiais
- **Git** — ferramenta local de controle de versão, já trabalhada em aulas anteriores do módulo. Documentação oficial: [git-scm.com/doc](https://git-scm.com/doc).
- **GitHub** — plataforma de hospedagem remota e colaboração sobre repositórios Git. Documentação oficial: [docs.github.com](https://docs.github.com).
- **Personal Access Token (token de acesso pessoal)** — credencial temporária usada no lugar de senha na autenticação via HTTPS.
- **SSH (Secure Shell)** — protocolo de autenticação por par de chaves criptografadas (privada/pública), usado como alternativa mais segura ao HTTPS.
- **Git Bash** — terminal instalado junto com o Git no Windows, necessário para rodar corretamente os comandos de geração de chave SSH.

---
**Salvar como:** `NN-rocketseat-git-github-o-que-e-o-github-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.

Me diz o número desta aula dentro do módulo "GitHub e trabalho colaborativo" pra eu fechar o `NN` do nome do arquivo — não vou chutar.