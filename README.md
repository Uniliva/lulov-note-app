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

1. Vá em **Settings → Secrets and variables → Actions** no seu repositório
2. Crie um secret chamado `PASSWORD` com a senha desejada (ex: `minha-senha-secreta`)
3. Em **Settings → Pages**, defina o source como **GitHub Actions**
4. Faça push para a branch `main` — o workflow fará o deploy automaticamente

### Como funciona

- O arquivo `index.html` contém o placeholder `__PASSWORD_HASH__` no lugar do hash
- O workflow calcula o SHA-256 da senha definida no secret e substitui o placeholder antes de publicar
- A senha nunca fica exposta no código-fonte do repositório
