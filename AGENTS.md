# Research site — agent contract

This repository is a static site. An automated worker runs an OpenCode agent in
this directory to add one article per job, then validates the result, regenerates
the index pages, commits, and pushes. Vercel serves the committed files.

Read this file completely before writing anything.

## What you may write

Exactly two files per job, inside one category directory:

```text
content/<category>/<slug>.html
content/<category>/<slug>.json
```

- `<category>` is given to you in the brief, for example `hobby/cubing/f2l`.
- `<slug>` is a lowercase, hyphenated slug derived from the title, at most 60
  characters, `^[a-z0-9][a-z0-9-]*$`.
- Never write anywhere else. Never modify `index.html`, category indexes,
  `templates/`, `assets/`, `robots.txt`, `AGENTS.md`, or this repository's Git
  state. The worker owns those.

If you need a new visual element, use an existing class from the list below. Do
not invent classes and do not add CSS.

## The HTML file

Produce a complete document, not a fragment. Structure:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="robots" content="noindex, nofollow">
  <title>…</title>
  <meta name="description" content="…">
  <link rel="stylesheet" href="../../assets/style.css">
</head>
<body>
  <header class="site-header">…</header>
  <main class="wrap">
    <nav class="breadcrumbs">…</nav>
    <article class="article">
      <header class="article-header">
        <h1>…</h1>
        <p class="meta">…</p>
      </header>
      <div class="tldr"><strong>In short</strong><p>…</p></div>
      <nav class="toc"><strong>Contents</strong><ol>…</ol></nav>
      <section class="section" id="example">
        <h2 id="example">Section title</h2>
        <p>…</p>
      </section>
      <section class="sources"><h2 id="sources">Sources</h2><ol>…</ol></section>
    </article>
  </main>
  <footer class="footer">…</footer>
</body>
</html>
```

`templates/base.html` and `templates/article.html` are the reference layout.
Copy their structure; fill in the placeholders.

The stylesheet path depends on depth. A file lives at
`content/<category>/<slug>.html`, so the number of `../` segments is one more
than the number of category segments:

| Category | Stylesheet link |
|---|---|
| `inbox` | `../../assets/style.css` |
| `hobby/cubing` | `../../../assets/style.css` |
| `hobby/cubing/f2l` | `../../../../assets/style.css` |

Index links follow the same rule: from `content/inbox/x.html`, the root index is
`../../index.html`.

## Allowed classes

```text
wrap  site-header  site-title  site-nav  footer
breadcrumbs  article  article-header  meta  tag
tldr  toc  section  sources  source  callout
index-list  index-item
```

No inline `style=` attributes. No `<script>`. No external fonts, images, or
stylesheets. No iframes. No trackers. No `<form>`.

## Content rules

- Open with a TL;DR of two or three sentences in `.tldr`.
- Use `<h2>` for top-level sections and `<h3>` for subsections. Never skip a
  level. Give every `<h2>` an `id`, including Sources, and list the main
  sections in the TOC.
- Cite sources inline as `[1]`, `[2]` and repeat the same numbers in `.sources`.
  Every non-obvious claim needs a citation. Never invent a URL.
- Prefer concrete detail over generic advice. If the sources disagree, say so.
- Include at least one worked example, code block, or short list that someone
  could apply immediately.
- Do not mention the model, the prompt, or the process. Write for a reader.
- No personal data, no secrets, no internal hostnames, no localhost links.

Length targets, set by the job level:

| Level | Words | Sections |
|---|---|---|
| shallow | 400–700 | 2–3 |
| deep | 1200–1800 | 4–6 |
| verydeep | 2500–3500 | 6–9 |

## The JSON file

```json
{
  "title": "Plain-language title",
  "summary": "One or two sentences for the index page.",
  "category": "hobby/cubing/f2l",
  "slug": "f2l-lookahead",
  "date": "2026-11-22",
  "words": 1420,
  "sources": [
    { "title": "Source title", "url": "https://example.com/page" }
  ],
  "model": "opencode-go/deepseek-v4.1-flash",
  "job_id": "a1b2c3d4"
}
```

`job_id` and `model` come from the brief. Keep the source order identical to the
HTML: entry 1 in the array is `[1]` in the text.

## Before you finish

- The two files exist and nothing else changed.
- **Every `<h2>` has an `id` attribute, including Sources, and every TOC link
  points at one of those ids.** A note without ids is rejected automatically.
- Every `[n]` citation has a matching source, and every source is cited.
- The stylesheet link resolves from the article's directory to `assets/style.css`.
- The document has no `<script>`, no inline styles, and only allowed classes.
- The stylesheet path resolves for the category depth.
