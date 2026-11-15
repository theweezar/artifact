# CLAUDE.md

Static archive of Claude-generated artifacts (HTML articles). No build step, no dependencies, no tests — plain HTML/CSS served as-is. Pushes to `main` deploy the whole repo root to GitHub Pages (`.github/workflows/static.yml`), so every relative link must work from a static file server. Preview locally with `npx serve .`.

## Layout

```
index.html                 root landing page — one link per article folder (has its own inline <style>)
main.css                   shared design system for all article pages (see below)
<article>/
  index.html + index.css   language picker: links to the en / ja / vi versions, back-link to ../index.html
  <article>[-lang].html    the article; no page-local CSS
```

Current articles: `quy-tac-bai-viet-vio-4028` (vi), `viecoi-cache-framework` (en). Content is mostly Vietnamese/English notes about the Viecoi codebase (`viecoi-v3-api`, `viecoi_nextjs`).

## Conventions

- **One folder per article**, named after the article slug. Multi-language articles use `<slug>-{en,ja,vi}.html` in the same folder; single-language ones use `<slug>.html`.
- **Every folder needs an `index.html`** listing all three languages. Languages without a file render as a greyed `.na` item ("not available yet"), never a broken link. Update it (and the root `index.html` + `README.md` contents) when adding, removing or translating an article.
- **Do not translate** content unless explicitly asked; keep the article's original text when restructuring.
- **No page-local CSS in article pages.** All styling comes from `../main.css`. If a page needs a new component, add it to `main.css` (generic, token-based), not inline. Only the folder `index.css` files and the root `index.html` have their own styles.

## `main.css` design system

Extracted from `viecoi-cache-framework`; its header comment documents the skeleton. Key points:

- Tokens on `:root` (colors `--navy/--blue/--green/--amber/--red/--purple` + `-soft`/`-mid`, `--mono`, `--sans`). Change look & feel there only. No dark mode.
- Page skeleton: `<div class="shell"><nav class="nav">…</nav><main class="main">…</main></div>`. The nav is sticky at 230px, `.main` is centered (`margin:auto`, max 1040px), stacks below 860px. Nav font size is 14px.
- Nav contents: `a.nav-back` (→ `index.html`, the parent language/article picker), `.nav-brand` (`-label`, `-title`, `-sub`), then `a[href="#id"]` links and `.nav-section-label` headings. `-sub` holds two `<time>` elements: created and updated. **These timestamps are hand-written** — created = first git commit of the file, updated = last edit; bump "Updated" whenever the article changes.
- Each `<section id="…">` in `main` must have a matching nav link; the active link is highlighted by a small inline script at the bottom of the page.
- Components: `.kpi-row/.kpi`, `.card`, `.callout.{verified,assume,stale}`, `.badge` (`.b-verified/.b-assume/.b-stale/.b-open` or `.blue/.gray/.amber/.green/.red`), `.tbl-wrap > table` with `td.yes/.no/.gated`, `.pill`, `.legend`, `details.collapse`, `.meta > .chip`, `.item` cards, `.rules`, `.section-note`.
- Paragraphs have no max-width on purpose — they inherit the wrapper's width.

## Mermaid diagrams (`viecoi-cache-framework`)

Loaded from cdnjs. Diagrams live in `<details class="collapse">` (collapsed by default) and use `startOnLoad:false`; a script renders each `pre.mermaid` the first time its `<details>` opens, because mermaid cannot size diagrams inside a closed `<details>`. Keep that pattern for new diagrams. Use `\n` in labels, and avoid `<`/`>` characters (use words or `[ ]`) since they are parsed as HTML.

## Content accuracy

The cache-framework article documents a *specific moment* of external repos (sources: `viecoi-v3-api/config/cache_policy.php`, `viecoi_nextjs/src/config/cache-policy.json`, `wct-tools/config/crontab/viecoi-v3-api-cachemanger-precompute`, `CacheClearController.php`). When updating it, re-read those files rather than editing from memory, keep the verified/caveat callouts honest, and update the "cross-checked on" date in its footer.
