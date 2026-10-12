# 📌 Segurança dentro do GitHub

### 1. Conceito Central
O GitHub não é apenas um repositório de código — é uma ferramenta com pontos críticos de segurança que precisam ser monitorados ativamente, já que ela impacta diretamente aplicações em produção, dados reais de usuários e a reputação do projeto. A aula percorre os recursos nativos de segurança do GitHub (Dependabot, Security Updates, Code Scanning, Secret Scanning, Security Advisories) e fecha com um conjunto de boas práticas gerais que todo desenvolvedor deveria aplicar no dia a dia, independentemente da stack usada.

### 2. Pontos-chave e Sintaxe
- **Dependabot:** ferramenta automática que analisa o arquivo de dependências do projeto (ex: `package.json`) comparando-as com um banco de vulnerabilidades conhecidas. Classifica o risco em baixo, médio, alto ou crítico, aponta as bibliotecas afetadas e sugere uma versão segura. Vem desabilitado por padrão e precisa do gráfico de dependências ativado junto. Por padrão, ignora vulnerabilidades de baixo impacto em dependências usadas só em ambiente de desenvolvimento (que não chegam à produção).
- **Security Updates:** depende do Dependabot estar ativo. Quando uma vulnerabilidade é detectada, o próprio GitHub **cria automaticamente um pull request** com a correção, para o desenvolvedor apenas revisar e mesclar — reduzindo o esforço manual de manter o projeto atualizado.
- **Code Scanning (via CodeQL):** detecta problemas como SQL Injection (uso de comandos SQL para alterar o banco sem acesso direto) e XSS (Cross-Site Scripting), entre outros riscos inseguros de API. Pode ser configurado em modo padrão (detecta linguagens do projeto automaticamente e roda via GitHub Actions a cada push/pull request, geralmente em branches protegidas) ou de forma avançada/customizada.
- **Branches protegidas:** branches consideradas mais sensíveis — geralmente as que o cliente final acessa ou que recebem código antes de validação — onde o code scanning e outras verificações costumam ser aplicadas a cada push ou pull request.
- **Secret Scanning:** detecta vazamento de credenciais (tokens de API, chaves AWS, senhas hardcoded) que tenham subido acidentalmente ao código. Vem ativado por padrão e pode bloquear a exposição pública, inclusive desfazendo um push que contenha uma informação secreta.
- **Security Advisories:** ativado por padrão, permite criar, discutir, corrigir e publicar avisos de vulnerabilidade do próprio projeto — um processo de draft, ajuste e publicação integrado por e-mail e visível em issues/pull requests.
- ⚠️ **Ponto de atenção:** mesmo que pareça "bobagem", vazar uma chave secreta no código é um problema sério — qualquer pessoa pode usá-la publicamente e gerar custos ou danos para o dono da chave. A prática correta é nunca subir segredos: usar `.gitignore` para bloquear arquivos sensíveis e, para automações, usar **GitHub Secrets** (armazenamento de valores sensíveis dentro do próprio GitHub, fora do código) ou variáveis de ambiente.
- **Two-Factor Authentication (2FA):** recomendado para a conta do GitHub em si (não só para a aplicação), via app autenticador, passkey ou outro método configurável em *Settings → Password and Authentication* — protege contra alguém com acesso à senha conseguir alterar código ou clonar repositórios privados.
- **Boas práticas gerais de segurança citadas na aula:**
  - Verificar alertas do Dependabot regularmente e manter dependências atualizadas; evitar bibliotecas abandonadas (sem publicações recentes) — a aula usa o React como exemplo de biblioteca bem mantida (atualizações frequentes, grande volume de uso).
  - Nunca fazer merge direto sem revisão de código, independentemente de quem o escreveu (dev, outro colaborador ou IA).
  - Aplicar o **princípio do menor privilégio**: tokens criados para ferramentas/bots devem ter apenas as permissões mínimas necessárias (ex: só leitura, nunca escrita, se a ferramenta só precisa ler código).
  - Evitar permissões globais; manter escopos de acesso restritos.
  - Habilitar que mudanças só entrem via pull request, bloqueando push direto em certas branches, e sempre ter um aprovador designado para revisar antes do merge.
  - Usar `.gitignore` consistentemente para impedir que logs e variáveis de ambiente sensíveis subam ao repositório.
- 🔎 **Observação:** a aula reforça que mesmo um repositório marcado como "privado" deve ser tratado como potencialmente público — colaboradores podem ser convidados, contas podem ser invadidas — então as boas práticas de segurança não são opcionais, são parte do desenvolvimento.

### 3. 🧭 Implicações Práticas
- Ativar Dependabot + gráfico de dependências é o primeiro passo de segurança automatizada em qualquer repositório novo, já que a maioria dos projetos modernos depende de bibliotecas de terceiros.
- Antes de adicionar uma dependência nova, vale checar a frequência de atualização dela (ex: no NPM) — bibliotecas abandonadas há muito tempo são um risco de segurança silencioso.
- Nunca commitar chaves de API ou senhas diretamente no código — usar GitHub Secrets ou variáveis de ambiente é a prática correta desde o início do projeto.
- Exigir pull request + aprovador para mudanças em branches sensíveis evita que erros (humanos ou gerados por IA) entrem em produção sem revisão.
- Ativar 2FA na própria conta do GitHub é uma medida simples que reduz drasticamente o risco de alguém comprometer o repositório inteiro via roubo de senha.

### 4. Links e Referências Oficiais
- **Dependabot** — análise automática de vulnerabilidades em dependências do projeto. Documentação: [docs.github.com/code-security/dependabot](https://docs.github.com/en/code-security/dependabot).
- **GitHub Code Scanning (CodeQL)** — detecção automática de vulnerabilidades no código (SQL Injection, XSS, etc.). Documentação: [docs.github.com/code-security/code-scanning](https://docs.github.com/en/code-security/code-scanning).
- **GitHub Secret Scanning** — detecção de credenciais/segredos vazados no repositório. Documentação: [docs.github.com/code-security/secret-scanning](https://docs.github.com/en/code-security/secret-scanning).
- **GitHub Security Advisories** — gestão e publicação de vulnerabilidades encontradas no projeto. Documentação: [docs.github.com/code-security/security-advisories](https://docs.github.com/en/code-security/security-advisories).
- **GitHub Secrets** — armazenamento de informações sensíveis fora do código-fonte, usado em automações/Actions. Documentação: [docs.github.com/actions/security-guides/using-secrets-in-github-actions](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions).
- **.gitignore** — arquivo que impede que arquivos/pastas específicos (como variáveis de ambiente) sejam versionados, já visto em aulas anteriores do módulo de Git.
- **Two-Factor Authentication (2FA)** — autenticação de dois fatores para a conta do GitHub, configurável em Settings.
- **NPM** — gerenciador de pacotes do Node citado como exemplo de onde verificar a frequência de manutenção de uma biblioteca de terceiros.

---
**Salvar como:** `05-rocketseat-git-github-seguranca-dentro-do-github-resumo.md` — no caderno (à mão) + repo do projeto, se quiser cópia digital. **Não** sobe na base de conhecimento.