# Registro de Alterações — presentations

## 2026-08-29 — Publicação: git init, remote, GitHub Pages e correção de bug do Quarto

Com autorização explícita do autor, completado o que faltava desde a criação:

1. **`git init` + primeiro commit** (27 arquivos), **remote público criado** (`mancano-tales/presentations`, via `gh repo create`) e **push**.
2. **Bug de render descoberto e corrigido**: o passo interno do Quarto (1.9.37) que move páginas renderizadas para o `output-dir` aborta o lote inteiro na primeira página processada — reproduzido tanto localmente (Windows) quanto no runner do GitHub Actions (Linux), então não é peculiaridade de plataforma. Efeito: só a última página (e nenhum recurso binário) sobrevivia em `_site/`. Workaround aplicado em `.github/workflows/publish.yml` e documentado no `README.md`: renderizar um `.qmd` por vez (lote de tamanho 1, imune ao bug) e copiar manualmente os `slides.pdf`/`.pptx` que o mesmo bug impedia de propagar.
3. **GitHub Pages habilitado** (branch `gh-pages`, path `/`) via `gh api`. Site verificado no ar: listagem, página de talk e download de PDF todos respondendo HTTP 200.

**Site publicado**: https://mancano-tales.github.io/presentations/

Pendente: PR em `mancano-tales.github.io` linkando esta página na navegação (WP7 do plano).

## 2026-08-25 — Criação do repositório

Estrutura inicial criada (Quarto + revealjs, GitHub Actions → gh-pages) com 8 talks migrados (copiados, não movidos) de `Nahoum-Mancano-2026-Antitrust` e `Mancano2026-MA-Thesis`. Metadados (título/data/venue) inferidos do nome dos arquivos de origem — ver aviso no `README.md`.

Plano de criação: `MancanoSync/0-meta/plan/2026-08-25_Plano_Criar_Repo_Presentations.md`.

`git init`, primeiro commit e criação do remote GitHub ainda pendentes (ação do autor).
