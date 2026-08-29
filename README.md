# presentations

Repositório de apresentações de Tales Mançano — slides prontos (PDF/PPTX) e, no futuro, decks web construídos em Quarto/revealjs. Publicado via GitHub Pages e linkado a partir do [site pessoal](https://mancano-tales.github.io/).

## Estrutura

- `talks/<slug>/index.qmd` — metadados do talk (título, data, categorias) e link para o arquivo.
- `talks/<slug>/slides.pdf|pptx` — arquivo pronto, versionado como está.
- `talks/<slug>/index.qmd` com `format: revealjs` — para talks feitos como deck web nativo (em vez de arquivo binário).
- `index.qmd` (raiz) — listagem automática de todos os talks, mais recente primeiro.

## Como adicionar uma apresentação nova

1. Crie `talks/<slug>/` (sugestão de nome: `YYYY-MM-DD_titulo-curto` ou `YYYY-MM_titulo-curto` se o dia exato não importa).
2. Coloque o arquivo (`slides.pdf`/`slides.pptx`) ou o deck revealjs (`index.qmd` com formato `revealjs`).
3. Se o talk for um arquivo pronto, crie um `index.qmd` simples com YAML (`title`, `date`, `categories`) e um link `<a class="talk-download" href="slides.pdf">...</a>`.
4. `git add`, commit, push — o GitHub Actions renderiza e publica em `gh-pages` automaticamente.

## Renderizar localmente

`quarto preview` funciona normalmente para conferir o site enquanto edita.

Para gerar o `_site/` completo localmente (o que o CI faz), **não use `quarto render .`** — o Quarto 1.9.x tem um bug onde a etapa final de mover as páginas renderizadas para o `output-dir` aborta o lote inteiro na primeira página processada, deixando as demais de fora mesmo tendo renderizado com sucesso (reproduzido em Windows e Linux). O workaround é renderizar uma página por vez:

```bash
for f in index.qmd $(find talks -name index.qmd); do
  quarto render "$f" || true   # o erro de saída é esperado (ver .github/workflows/publish.yml)
done
# o mesmo bug impede a cópia automática dos slides.pdf/pptx — copie manualmente:
find talks -type f ! -name "*.qmd" | while read -r f; do
  mkdir -p "_site/$(dirname "$f")" && cp "$f" "_site/$f"
done
```

## Aviso sobre metadados

Os talks migrados na criação deste repositório (2026-08-25) tiveram título/data/venue **inferidos a partir do nome do arquivo de origem**, sem confirmação item a item com o autor. Vários têm data aproximada (só o ano é conhecido) ou duas versões concorrentes do mesmo talk mantidas lado a lado. Revise antes de divulgar amplamente — ver `0-meta` do repositório raiz (`MancanoSync/0-meta/plan/2026-08-25_Plano_Criar_Repo_Presentations.md`) para o levantamento completo.
