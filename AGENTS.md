# AGENTS.md — scovl.github.io

Static blog generated with Hugo, hosted on GitHub Pages.

## Build

- Hugo source lives in `blog/`. All content, config, layouts, and theme are there.
- Build: `cd blog && hugo`
- Dev server: `cd blog && hugo server`
- `publishDir` is `..` — Hugo writes output to the repo root. Do not be surprised by HTML files in the root.

## Content authoring

- Posts are **Org mode** (`.org`) files with **TOML front matter** delimited by `+++`.
  - Not YAML (`---`) front matter like Hugo's default. Only page Markdown files use YAML.
- Front matter fields: `title`, `description`, `date`, `tags` (array), `draft`, `weight`, `author`.
- Create a new post: `cd blog && hugo new post/slug.org`
- Permalink config: `post: /:contentbasename/` — each post outputs to `/<slug>/index.html`.

## Gotchas

- **Do not commit `hugo server` output.** Run `hugo` (not `hugo server`) to generate production output. The current root HTML has `localhost:1313` and livereload.js injected — these come from a dev server run and should be rebuilt with `hugo` before publishing.
- `.nojekyll` must remain at root — it tells GitHub Pages to skip Jekyll processing.
- `_config.yml` at root is an unused Jekyll config (harmless but ignored because of `.nojekyll`).

## Theme

- Custom minimal theme: `blog/themes/scovl/`.
- Templates: `baseof.html` (wrapper), `single.html` (post page), `list.html` (list pages), `index.html` (homepage).
- Theme CSS: `blog/themes/scovl/static/css/main.css`. The `/css/main.css` at root is a copy.
- Code block render hook (`render-codeblock.html`) wraps Mermaid blocks in `<div class="mermaid">`.

## Static assets

- `vendor/` is committed — Prism.js, Mermaid.js, and Inter font.
- Prism handles client-side syntax highlighting for: bash, c, cpp, rust, go, js, ts, clojure, lisp, swift, zig, sql.
- Mermaid diagrams are rendered client-side via `mermaid.min.js`.
- `vendor/fonts/fonts.css` — Inter font, committed.

## No toolchain

- No `package.json`, no npm, no tests, no linting, no CI config.
- This is a plain Hugo static site. There is no build pipeline beyond running `hugo`.

## Structure

```
blog/               # Hugo project root
  config.yml         # Hugo config (baseURL, theme, permalinks, etc.)
  content/
    post/*.org       # Blog posts (Org mode + TOML front matter)
    page/*.md        # Static pages (about, contact) — YAML front matter
    en/              # English content mirror
  layouts/           # Project-level layout overrides
  themes/scovl/      # Custom theme (templates, CSS, shortcodes)
  archetypes/        # `hugo new` template
vendor/              # Prism, Mermaid, fonts (committed)
css/main.css         # Generated copy of theme CSS
*.html, *.xml        # Hugo output at repo root (git-tracked)
```
