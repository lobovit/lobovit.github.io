# AGENTS.md

Hugo static site for `https://lobovit.github.io/` — personal blog by Vitor Lobo.

## Commands

```bash
# Dev server (run from blog/), includes drafts
hugo server -D

# Build (writes to repo root via publishDir: '..')
hugo
```

- `hugo` **publishes to the repo root** (`../` relative to `blog/`). Root-level `.html`, `.xml`, `css/`, `js/`, `fonts/`, `vendor/`, `post/`, `page/`, `tags/`, `categories/`, `en/`, `pt/`, `index.html`, `sitemap.xml`, `sw.js` are all **generated output** — never edit them directly.
- `hugo server -D` serves from memory; does **not** write to disk. The `-D` flag includes draft posts (most content is draft).
- Hugo **extended** v0.161+ required (Mermaid/SCSS support).
- **Never use `--cleanDestinationDir`** — `publishDir: '..'` makes it delete the blog source directory.

## Content editing

- Posts: `blog/content/post/*.org` — Org-mode body with TOML frontmatter (`+++` delimiters)
- Pages: `blog/content/page/*.org` or `*.md`; English translations: `blog/content/en/page/*.md`
- Draft posts set `draft = true` in frontmatter; excluded from production builds unless `-D`
- Default language is `pt-br`; posts are written in Portuguese
- Goldmark `unsafe: true` — raw HTML in content is allowed
- Permalink pattern: `/:contentbasename/` (e.g., `/comp01/` not `/post/comp01/`)
- Diagrams: use `#+BEGIN_SRC mermaid` blocks in Org files

## Theme & templates

- Custom theme: `blog/themes/lobovit/` (Emacs-inspired purple palette)
- CSS: `blog/themes/lobovit/static/css/main.css` (hand-written, no build pipeline)
- **Layout override precedence**: `blog/layouts/` > `blog/themes/lobovit/layouts/`
  - `blog/layouts/_default/_markup/render-codeblock.html` overrides theme for Mermaid rendering (`<div>` wrapper, store flag)
- Syntax highlighting: **Prism.js** (client-side), loaded in `baseof.html`. Hugo's built-in Chroma is bypassed.
- Mermaid diagrams are rendered client-side via `vendor/mermaid/mermaid.min.js`
- i18n strings: `blog/i18n/en.toml`, `blog/i18n/pt.toml`
- Shortcodes: `blog/themes/lobovit/layouts/shortcodes/video.html` → `{{< video src="..." >}}`

## Config

- `blog/config.yml` — Hugo config (baseURL, menu, taxonomies, etc.)
- `blog/_config.yml` — Jekyll stub for GitHub Pages compatibility (ignore; site is Hugo, not Jekyll)
- `blog/ai-engineering-from-scratch/` — separate project/course, **not** Hugo content; ignore for site work

## Deploy

No CI/CD pipeline. Deploy is manual: build locally with `hugo` from `blog/`, then commit + push.
