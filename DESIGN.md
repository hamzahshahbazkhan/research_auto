# Design notes — regenerate me with Claude

The four files below are a hand-written baseline so the pipeline can be built
and tested. They are deliberately plain. Replace them with a Claude-generated
design when you have time; the worker only depends on the file names and the
class list.

```text
templates/base.html      shell: head, header, footer, {{{content}}}
templates/article.html   article body: breadcrumbs, header, TL;DR, TOC, sources
templates/index.html     index page: title, optional categories, article list
assets/style.css         the complete stylesheet
```

## Rules the replacement must keep

- Semantic HTML only, no JavaScript, no external fonts, images, or CDNs.
- System font stack; `prefers-color-scheme` for light and dark.
- Body text max width about 72 characters; readable at 360 px.
- Every class used in `templates/` and referenced in `AGENTS.md` must exist in
  `assets/style.css`. Do not rename classes without updating `AGENTS.md`.
- Printable: hide the header, footer, and TOC when printing.
- Placeholders stay as `{{name}}` so the renderer can substitute them.

## Prompt to give Claude

```text
Design a minimal reading experience for a personal research-notes site.
Deliver four files: templates/base.html, templates/article.html,
templates/index.html and assets/style.css.

Constraints:
- Static HTML, no JavaScript, no external assets or fonts.
- System font stack; light and dark via prefers-color-scheme.
- Comfortable serif body text, max ~72 characters per line.
- Sans-serif headings, a subtle accent colour, restrained borders.
- Components needed: site header with title and two links, breadcrumbs,
  article header with h1 and meta line (date, reading time, category tag),
  an "in short" summary box, a table of contents, section headings,
  code blocks, tables, blockquotes, a sources list, an index list of articles,
  and a footer.
- Use exactly these class names: wrap, site-header, site-title, site-nav,
  footer, breadcrumbs, article, article-header, meta, tag, tldr, toc, section,
  sources, source, callout, index-list, index-item.
- Keep {{name}} placeholders in the templates.

Explain briefly which file to edit to change the accent colour and the
reading width.
```

## After replacing

Render a page and check it at 360 px, 768 px, and desktop, in both light and
dark mode. Then commit with a message like `design: replace the baseline theme`.
