# lulov-note-app

Gerador de Orçamentos para a **Marmoraria Santa Cruz** (Embu das Artes/SP).

Aplicação web de página única que permite:

- Preencher dados do cliente (nome e endereço)
- Adicionar itens ao orçamento (descrição, quantidade, unidade e valor unitário)
- Calcular o valor total automaticamente com base nos itens
- Escolher uma paleta de cores para o PDF (3 opções: Graceland, Grupo Marmor, Marmor Salomé)
- Gerar e baixar um PDF formatado da ordem de serviço, com cabeçalho da empresa, dados do cliente, tabela de itens, condições comerciais e área de assinatura

A geração do PDF é feita via a biblioteca `html2pdf.js` diretamente no navegador, sem necessidade de backend.

## Deploy no GitHub Pages

O site possui proteção por senha. O hash da senha é injetado automaticamente via GitHub Actions durante o deploy.

### Como configurar

Vá em **Settings → Secrets and variables → Actions** no repositório e cadastre:

**Secrets** (dados sensíveis — ficam ocultos nos logs):

| Nome       | Descrição            | Exemplo              |
|------------|----------------------|----------------------|
| `PASSWORD` | Senha de acesso ao site | `minha-senha-secreta` |

**Variables** (dados não sensíveis — visíveis nos logs):

| Nome               | Descrição              | Exemplo                                                      |
|--------------------|------------------------|--------------------------------------------------------------|
| `COMPANY_NAME`     | Nome da empresa        | `Marmoraria Santa Cruz`                                      |
| `COMPANY_ADDRESS`  | Endereço completo      | `Rua dos Trabalhadores, 12, Jd. N. S. de Fátima – Embu das Artes/SP` |
| `COMPANY_CNPJ`     | CNPJ                   | `51.909.664/0001-20`                                         |
| `COMPANY_CITY`     | Cidade/UF              | `Embu das Artes/SP`                                          |

Em seguida:
1. Em **Settings → Pages**, defina o source como **GitHub Actions**
2. Faça push para a branch `main` — o workflow fará o deploy automaticamente

### Como funciona

- O `index.html` no repositório contém placeholders (`__COMPANY_NAME__`, `__COMPANY_CNPJ__`, etc.)
- O workflow do GitHub Actions substitui todos os placeholders pelos valores configurados antes de publicar
- A senha e os dados da empresa nunca ficam expostos no código-fonte do repositório
