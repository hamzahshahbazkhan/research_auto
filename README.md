# Research notes

Static notes generated from Telegram or the `watson` CLI and published here.

- `content/<category>/<slug>.html` — one article, self-contained
- `content/<category>/<slug>.json` — its metadata, used to build indexes
- `templates/` and `assets/` — the design
- `AGENTS.md` — the contract the generating agent follows
- `DESIGN.md` — how to regenerate the theme with Claude

Everything is plain HTML. There is no build step; the hosted copy serves the
committed files directly.

The site asks search engines not to index it (`robots.txt` and a `noindex`
meta tag). It is public by URL, not promoted.
