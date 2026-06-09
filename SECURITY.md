# 🔐 Security Policy — PortfolioHUB

> Repositório: [RafaelGuimaraens/PortifolioHUB](https://github.com/RafaelGuimaraens/PortifolioHUB)  
> Bootcamp UniCEUB · Última atualização: Junho de 2026

---

## 📋 Sumário

- [Versões Suportadas](#-versões-suportadas)
- [Reportando uma Vulnerabilidade](#-reportando-uma-vulnerabilidade)
- [Proteção de Branch](#-proteção-de-branch)
- [Política de Commits e Controle de Acesso](#-política-de-commits-e-controle-de-acesso)
- [Dados Sensíveis e Boas Práticas](#-dados-sensíveis-e-boas-práticas)
- [Checklist de Segurança](#-checklist-de-segurança)
- [Ferramentas e Referências](#-ferramentas-e-referências)

---

## ✅ Versões Suportadas

A tabela abaixo indica quais versões do PortfolioHUB recebem atualizações de segurança:

| Versão | Branch   | Status de Suporte        |
|--------|----------|--------------------------|
| 1.x    | `main`   | ✅ Suportada ativamente  |
| < 1.0  | —        | ❌ Sem suporte           |

> Apenas a branch `main` é considerada a versão estável e recebe patches de segurança.

---

## 🚨 Reportando uma Vulnerabilidade

Se você identificar uma vulnerabilidade de segurança neste repositório, **não abra uma Issue pública**. Siga o processo abaixo:

### Como reportar

1. **Envie um e-mail** para o mantenedor do repositório com o assunto:  
   `[SECURITY] Vulnerabilidade em PortfolioHUB`

2. **Inclua no relatório:**
   - Descrição detalhada da vulnerabilidade
   - Passos para reproduzir o problema
   - Impacto potencial (ex: exposição de dados, acesso não autorizado)
   - Sugestão de correção (opcional, mas bem-vinda)

3. **Prazo de resposta esperado:** até **5 dias úteis** após o recebimento.

4. Após a confirmação da vulnerabilidade:
   - Será aberta uma branch privada para correção
   - Um patch será aplicado e um novo commit feito na `main`
   - A vulnerabilidade será documentada nas notas de versão após a correção

> ⚠️ Não divulgue publicamente a vulnerabilidade antes de receber confirmação de que o problema foi corrigido (*responsible disclosure*).

---

## 🛡️ Proteção de Branch

A branch `main` possui **regras de proteção ativas** no GitHub para garantir a integridade do histórico do projeto:

| Regra                              | Status   |
|------------------------------------|----------|
| Exigir Pull Request antes do merge | ✅ Ativo |
| Bloquear force push (`--force`)    | ✅ Ativo |
| Bloquear exclusão da branch        | ✅ Ativo |
| Exigir revisão de código (review)  | ⚙️ Recomendado para times |
| Exigir status checks (CI/CD)       | ⚙️ Opcional |

> Contribuições diretas na `main` via `git push --force` são **bloqueadas** pelo GitHub. Todo código novo deve passar por Pull Request.

---

## 🔑 Política de Commits e Controle de Acesso

### Regras de acesso

- O repositório é **público** (`public`) para fins de portfólio e avaliação acadêmica.
- Apenas o mantenedor (`RafaelGuimaraens`) possui permissão de **write** e **admin** no repositório.
- Colaboradores externos devem realizar **fork** + **Pull Request**.

### Boas práticas de commit

- ✅ Escreva mensagens de commit claras e descritivas
- ✅ Use commits atômicos (uma mudança por commit)
- ❌ Nunca commite credenciais, tokens ou senhas
- ❌ Nunca commite arquivos `.env` ou com dados pessoais sensíveis
- ✅ Utilize `.gitignore` para excluir arquivos desnecessários ou sensíveis

### Exemplo de `.gitignore` recomendado

```gitignore
# Variáveis de ambiente e segredos
.env
.env.local
*.key
*.pem
secrets/

# Sistemas operacionais
.DS_Store
Thumbs.db

# Editores
.vscode/
.idea/

# Dependências
node_modules/
```

---

## 🔒 Dados Sensíveis e Boas Práticas

Este repositório armazena apenas arquivos de portfólio público (HTML, PDFs, PPTX). Ainda assim, as seguintes práticas são adotadas:

### O que NÃO deve ser armazenado

| Tipo de dado                  | Exemplo                        | Ação recomendada              |
|-------------------------------|--------------------------------|-------------------------------|
| Tokens de API                 | `ghp_xxxxxxxxxxxx`             | Usar GitHub Secrets           |
| Senhas                        | `password=abc123`              | Nunca versionado              |
| Dados pessoais de terceiros   | CPF, e-mails de alunos         | Remover antes do commit       |
| Chaves privadas SSH/SSL       | `-----BEGIN PRIVATE KEY-----`  | Manter fora do repositório    |

### Transmissão segura

- Todo acesso ao repositório é feito via **HTTPS** ou **SSH** com chave autenticada.
- O repositório está hospedado na infraestrutura do **GitHub**, que utiliza criptografia TLS em trânsito.

### GitHub Secrets (para projetos futuros com CI/CD)

Caso o projeto evolua para pipelines automatizadas, utilize o recurso de **Secrets** do GitHub Actions:

```yaml
# Exemplo de uso seguro em workflow
- name: Deploy
  env:
    API_TOKEN: ${{ secrets.API_TOKEN }}
```

---

## ✔️ Checklist de Segurança

Use esta lista antes de cada Pull Request ou release:

- [ ] Nenhuma credencial, token ou senha está presente nos arquivos
- [ ] O `.gitignore` está configurado corretamente
- [ ] A branch `main` está protegida contra force push
- [ ] Os arquivos HTML não contêm scripts externos de origens não confiáveis
- [ ] Certificados e documentos pessoais no repositório são de uso público e intencional
- [ ] O histórico de commits não contém dados sensíveis em commits anteriores
- [ ] O repositório não possui dependências com vulnerabilidades conhecidas (verificar via `Dependabot` ou `npm audit`)

---

## 🧰 Ferramentas e Referências

| Ferramenta / Recurso             | Descrição                                              | Link |
|----------------------------------|--------------------------------------------------------|------|
| GitHub Branch Protection         | Configura regras para branches críticas                | [Docs](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches) |
| GitHub Secret Scanning           | Detecta automaticamente segredos expostos              | [Docs](https://docs.github.com/en/code-security/secret-scanning/about-secret-scanning) |
| GitHub Dependabot                | Alertas sobre dependências vulneráveis                 | [Docs](https://docs.github.com/en/code-security/dependabot) |
| Google Gemini (IA de apoio)      | Utilizado como guia de implantação e segurança no projeto | [Gemini](https://gemini.google.com) |
| OWASP Top 10                     | Referência global para vulnerabilidades web             | [owasp.org](https://owasp.org/www-project-top-ten/) |
| GitHub Security Best Practices   | Guia oficial do GitHub sobre segurança                 | [Docs](https://docs.github.com/en/code-security) |

---

## 📄 Licença e Responsabilidade

Este repositório é de caráter **educacional**, desenvolvido como parte do Bootcamp da UniCEUB. O conteúdo armazenado (currículo, certificados, portfólio) é de responsabilidade exclusiva do autor.

Qualquer contribuição ao projeto implica concordância com as políticas descritas neste documento e com o [Código de Ética da EaD UniCEUB](https://drive.google.com/file/d/1FcCNRziZlHZhWk5L3ImLBAQNXhGWzsW8/view).

---

*Documento gerado com apoio do Google Gemini · PortfolioHUB · UniCEUB Bootcamp 2026*
