# lucasnramos.com

Built with [Hugo](https://gohugo.io/)
using the [Coder](https://github.com/luizdepra/hugo-coder) theme. Published to GitHub
Pages at <https://lucasnramos.com> via GitHub Actions.

The site is bilingual (English and Portuguese) with content under `content/en` and
`content/pt`.

## Project structure

```
content/
  en/            English content (default language, served at /)
    posts/
    about.md
  pt/            Portuguese content (served at /pt/)
    posts/
    about.md
static/images/   Images and other static files
themes/coder/    Coder theme (git submodule — must be initialized, see below)
hugo.toml        Site configuration, languages, menus, params
.github/workflows/hugo.yaml   Build and deploy pipeline
public/          Generated output (gitignored)
```

## Requirements

- [Hugo Extended](https://gohugo.io/installation/) v0.160.0 or newer
  (the CI pipeline pins v0.160.0; the theme requires >= 0.124.0)
- Git
- Optional: [Dart Sass](https://sass-lang.com/dart-sass/) and Node.js — the CI
  pipeline installs both, but a local build only needs Hugo Extended

Check your version:

```bash
hugo version   # must say "extended"
```

## Getting started

### 1. Clone with the theme submodule

The theme lives in a git submodule, so it is **not** included in a plain `git clone`.
Clone recursively:

```bash
git clone --recurse-submodules git@github.com:lucasnramos/website.git
cd website
```

Already cloned without it? Initialize the submodule before building:

```bash
git submodule update --init --recursive
```

If `themes/coder/` is empty, Hugo will build a site with no layouts and you will
get a **"404 page not found"** in the browser with no obvious error. See
[Troubleshooting](#troubleshooting).

### 2. Run the local dev server

```bash
hugo server
```

Open <http://localhost:1313/>. The server watches for changes and reloads the
browser automatically.

Useful options:

```bash
hugo server -D            # include draft posts
hugo server --bind 0.0.0.0   # expose on your network
```

### 3. Build for production

```bash
hugo --gc --minify
```

Output is written to `public/`. To preview the exact production output:

```bash
hugo --gc --minify
cd public && python3 -m http.server 8080
```

## Writing content

Posts live in `content/en/posts/` and `content/pt/posts/`. Create a new post with:

```bash
hugo new content/en/posts/my-post.md
hugo new content/pt/posts/meu-post.md
```

Front matter format used by this site is TOML (`+++`):

```toml
+++
title = "My post"
date = "2026-05-11"
description = "Short summary"
draft = false
+++
```

Notes:

- `draft = true` posts only show with `hugo server -D` or `hugo --buildDrafts`.
- Each content section needs an `_index.md` to render its list page. The `posts`
  sections already have one; if you add a new section, add `_index.md` too,
  otherwise the section URL will return 404 even though its posts work.
- Images and other static files go in `static/images/` (referenced as `/images/...`).

## Deployment

Pushes to `main` trigger the workflow in `.github/workflows/hugo.yaml`, which:

1. Checks out the repo **with submodules**.
2. Installs Hugo Extended, Dart Sass, Go, and Node.js at pinned versions.
3. Builds with `hugo --gc --minify --baseURL <GitHub Pages URL>`.
4. Uploads `public/` and deploys it to GitHub Pages.

You can also trigger it manually from the Actions tab (`workflow_dispatch`).

Note: `baseURL` in `hugo.toml` is `https://lucasnramos.com/`, but `hugo server`
always serves on `http://localhost:1313/`. Do not hardcode absolute URLs in
content if you want them to work in both environments.

## Troubleshooting

**Every page returns 404 locally, but the deployed site works**
The theme submodule is missing/empty. Run:

```bash
git submodule update --init --recursive
```

**`/posts/` (Blog menu) returns 404**
The section has no `_index.md`. It is present in this repo; if you add a new
section, add `content/<lang>/<section>/_index.md`.

**Local build looks different from production**
Check `hugo version` — the CI pins v0.160.0. Also remember that `hugo server`
runs in development mode (`hugo.IsServer`), which affects some theme behaviors
(e.g. unminified CSS with source maps).
