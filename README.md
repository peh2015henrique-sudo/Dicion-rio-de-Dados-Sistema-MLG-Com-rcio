# Dicionário de Dados — Sistema MLG Comércio

Dicionário de dados interativo, com governança (DAMA-DMBOK 2, COBIT 2019 e LGPD), do banco MySQL 8.4 LTS do Sistema MLG Comércio — Grupo 5, disciplina Banco de Dados, ADS UNICID.

Base: `mlg_comercio_ddl.sql` v1.2 (12 tabelas, 102 colunas, 16 chaves estrangeiras) e Especificação de Requisitos e Regras de Negócio v1.3.

---

## 1. Estrutura de pastas e arquivos

```text
/meu-dicionario
├── index.html
├── style.css
├── script.js
├── README.md
├── docs/
│   └── Especificacao_Requisitos_Regras_Negocio_BD.pdf
└── assets/
    ├── der.png
    └── der_mlg_comercio.mmd   (fonte editável do DER, em Mermaid)
```

Passo a passo:

1. Crie a pasta `meu-dicionario` e coloque nela `index.html`, `style.css`, `script.js` e este `README.md`.
2. A subpasta `docs` já traz a Especificação v1.3 em PDF, com o nome exato `Especificacao_Requisitos_Regras_Negocio_BD.pdf`. Se gerar uma nova versão, exporte o PDF e salve com esse mesmo nome.
3. A subpasta `assets` já traz o DER corrigido (`der.png`, 7656 px de largura), gerado a partir do DDL v1.2, e a fonte `der_mlg_comercio.mmd`. Para alterar o diagrama, edite o `.mmd` em https://mermaid.live e exporte de novo como PNG com o nome `der.png`.
4. Teste localmente: dê dois cliques em `index.html`. Se preferir um servidor local, rode `python -m http.server 8000` dentro da pasta e abra `http://localhost:8000`.

### Como os caminhos do HTML já estão preparados

Todos os caminhos são **relativos** à pasta onde está o `index.html`, por isso funcionam igual no computador e no GitHub Pages:

| Onde | Código | Arquivo que carrega |
|---|---|---|
| `<head>` do `index.html` | `<link rel="stylesheet" href="style.css">` | `meu-dicionario/style.css` |
| `<head>` do `index.html` | `<script src="script.js" defer></script>` | `meu-dicionario/script.js` (o `defer` executa o script depois que o HTML é lido) |
| Botão "Baixar Especificação" | `href="docs/Especificacao_Requisitos_Regras_Negocio_BD.pdf"` | `meu-dicionario/docs/...pdf` |
| Modal do DER | `CONFIG.der = 'assets/der.png'` no início do `script.js` | `meu-dicionario/assets/der.png` |

As bibliotecas externas vêm de CDNs oficiais e não precisam ser baixadas: Font Awesome 6.5.1 (cdnjs), Panzoom 4.5.1 (jsDelivr) e as fontes IBM Plex (Google Fonts). Se a CDN do Panzoom falhar, o `script.js` usa uma implementação própria de zoom e arraste.

Se mudar o nome do PDF ou da imagem, altere os dois caminhos no objeto `CONFIG`, no início do `script.js`.

### Onde editar o conteúdo

- **Dados do dicionário** (tabelas, colunas, LGPD, linhagem, RBAC): array `TABELAS` no `script.js`. A barra lateral, os indicadores e a pesquisa são gerados a partir dele.
- **Identificação, responsáveis e professor**: seção `#identificacao` do `index.html`.
- **Cores**: variáveis no início do `style.css` (`--cor-primaria`, `--cor-destaque`, `--fundo`).

---

## 2. Deploy no GitHub Pages

### 2.1 Criar o repositório e enviar os arquivos

**Opção A — pelo navegador (sem instalar nada)**

1. Entre em https://github.com e clique em **New** (novo repositório).
2. Nome sugerido: `dicionario-dados-mlg`. Marque **Public**. Clique em **Create repository**.
3. Na página do repositório, clique em **uploading an existing file**.
4. Arraste o **conteúdo** da pasta `meu-dicionario` (os arquivos e as pastas `docs` e `assets`, não a pasta-mãe). O `index.html` precisa ficar na raiz do repositório.
5. Escreva uma mensagem, por exemplo `Publica dicionário de dados v1.0`, e clique em **Commit changes**.

**Opção B — pelo Git (terminal)**

```bash
cd meu-dicionario
git init
git add .
git commit -m "Publica dicionário de dados v1.0"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/dicionario-dados-mlg.git
git push -u origin main
```

### 2.2 Ativar o GitHub Pages

Caminho exato no repositório:

**Settings > Pages > Build and deployment > Source: Deploy from a branch > Select "main" > Save**

Na caixa de pasta ao lado do branch, mantenha `/ (root)`. Depois de um a dois minutos, o endereço aparece no topo da mesma página:

```text
https://SEU-USUARIO.github.io/dicionario-dados-mlg/
```

Cada novo commit no branch `main` publica a atualização automaticamente.

### 2.3 Aviso importante: maiúsculas e minúsculas

No Windows, `Der.PNG`, `der.png` e `DER.png` são o mesmo arquivo. **No servidor do GitHub Pages (Linux), são três arquivos diferentes.** Um caminho com uma letra divergente funciona no seu computador e quebra depois da publicação, com erro 404.

- O DER deve se chamar exatamente `der.png` (tudo minúsculo), dentro de `assets`.
- O PDF deve se chamar exatamente `Especificacao_Requisitos_Regras_Negocio_BD.pdf`, dentro de `docs`, sem acentos e sem espaços.
- As pastas são `docs` e `assets`, em minúsculas.
- Ao exportar pelo Windows, confira se a extensão não ficou `.PNG` ou `.Pdf`. Ative "Extensões de nomes de arquivos" no Explorador de Arquivos para enxergar.

Se a imagem ou o PDF não abrirem no site publicado, compare letra a letra o nome do arquivo no GitHub com o caminho do `CONFIG` no `script.js`.
