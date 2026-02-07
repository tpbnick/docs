# Nick's Docs

Documentation, programming notes, and projects. Built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

## Setup

Install dependencies from the lockfile:

```bash
pip install -r requirements.txt
```

### What’s in `requirements.txt`

- **Core:** MkDocs, MkDocs Material, pymdown-extensions (for Material-recommended markdown features).
- **Plugins:** awesome-pages (navigation from `.pages` files), minify, optional glightbox/git-revision-date/git-committers/redirects. Glightbox is installed but currently disabled in `mkdocs.yml` (was breaking image display; can be re-enabled in manual mode if needed).

Navigation is **not** defined in `mkdocs.yml`. It’s driven by [mkdocs-awesome-pages-plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin): each section has a `.pages` file (e.g. `docs/.pages`, `docs/programming-notes/.pages`) that sets order and titles. Most content lives under `docs/programming-notes/` (portfolio, notes, and language docs).

## Commands

### Serve locally

```bash
mkdocs serve
```

The site should reload in the browser when you save a file. If it doesn’t:

- Don’t run with `--no-livereload`.
- Close extra browser tabs that have the docs open.
- After saving, wait a few seconds or make a small edit and save again (some editors delay writing to disk).

### Build static site

```bash
mkdocs build
```

Output goes into the `site/` directory.
