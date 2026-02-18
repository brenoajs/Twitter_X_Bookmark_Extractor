# Twitter/X Bookmarks Extractor

Extrai todos os seus tweets salvos (bookmarks) do Twitter/X e exporta para Excel.

## Pré-requisitos

- Python 3.8 ou superior
- Google Chrome com sessão ativa no Twitter/X
- Extensão [Cookie-Editor](https://cookie-editor.com/) instalada no Chrome

## Instalação

Abra o terminal nesta pasta e execute:

```bash
pip install -r requirements.txt
```

## Como usar

1. **Exporte os cookies do Chrome:**
   - Acesse [x.com](https://x.com) já logado
   - Clique no ícone do Cookie-Editor na barra de extensões
   - Clique em **Export → Export as JSON**
   - Salve o arquivo como `cookies.json` na mesma pasta do script

2. **Execute o script:**
   ```bash
   python extract_bookmarks.py
   ```

3. Aguarde a extração terminar
4. O arquivo Excel será gerado na mesma pasta com o nome `bookmarks_YYYYMMDD_HHMMSS.xlsx`

## Colunas do Excel

| Coluna | Descrição |
|--------|-----------|
| ID | ID único do tweet |
| Data | Data e hora de publicação |
| Autor | Nome de exibição do autor |
| @usuario | Nome de usuário do autor |
| Texto | Conteúdo completo do tweet |
| Likes | Número de curtidas |
| Retweets | Número de retweets |
| Replies | Número de respostas |
| Quotes | Número de quote tweets |
| Views | Visualizações |
| Mídia | Tipo de mídia (photo, video, gif) |
| É Retweet | Se é um retweet |
| É Quote | Se é um quote tweet |
| URL | Link direto para o tweet |

## Observações

- Os cookies exportados ficam salvos localmente em `cookies.json` — nenhum dado é enviado a terceiros.
- Os cookies expiram com o tempo. Se ocorrer erro 401, exporte-os novamente seguindo o passo 1.
- O script respeita os rate limits do Twitter automaticamente.

## Problemas comuns

**Erro 401 (Não autorizado)**
- Os cookies expiraram — exporte novamente pelo Cookie-Editor estando logado em x.com

**`cookies.json` não encontrado**
- Certifique-se de salvar o arquivo exportado pelo Cookie-Editor como `cookies.json` na mesma pasta do script

**Erro 404 na API**
- O ID da query GraphQL do Twitter mudou. Abra o DevTools (F12) → aba **Network**, acesse x.com/i/bookmarks e localize a requisição `Bookmarks`. O novo ID estará na URL: `graphql/SEU_ID/Bookmarks`. Atualize `BOOKMARKS_QUERY_ID` em `extract_bookmarks.py`.
