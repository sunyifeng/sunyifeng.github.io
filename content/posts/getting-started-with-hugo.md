---
title: "Getting Started with Hugo"
date: 2025-07-04
series: ["Hugo Log"]
categories: ["Dev Notes"]
tags: ["hugo", "static site", "setup"]
description: "Quick installation guide and tips for a clean first Hugo project."
---

I recently decided to use Hugo to build my personal blog. It’s fast, clean, and surprisingly customizable. Below is a condensed guide covering installation on macOS & Ubuntu, common pitfalls, SCSS/SASS support, GitHub Pages deployment, and troubleshooting tips.

---

### 🧩 Installation

#### macOS (Homebrew)

```bash
brew update
brew install hugo
```

Verify:
```bash
hugo version
# Expect “extended” if you need SCSS/SASS support
```

#### Ubuntu (Snap – Extended)

```bash
sudo apt update
sudo snap install hugo --channel=extended --classic
```

Clear any shell hash and confirm:
```bash
hash -r
which hugo     # should point to /snap/bin/hugo
hugo version   # shows “extended”
```

---

### ⚙️ Initialize a New Site

```bash
cd ~/github/your-blog
hugo new site .
```

Pick a theme (e.g., Ananke):

```bash
cd themes
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git ananke
cd ..
```

Configure `config.toml`:

```toml
theme = "ananke"
baseURL = "https://<username>.github.io"
languageCode = "en-us"
title = "My Hugo Site"

[pagination]
  pagerSize = 5

[params]
  hero = true
  heroImage = "images/header.jpg"
  heroTitle = "Welcome!"
  heroSubtitle = "Just Hugo things"
```

---

### 🚀 First Preview

Place a hero image under `static/images/header.jpg`, then run:

```bash
hugo server -D
```

Access `http://localhost:1313/` (no extra path).

---

### 🐾 Common Pitfalls & Fixes

1. **TOCSS/SCSS Errors**
   - Error: `failed to transform "/css/main.css"... need Extended version`
   - Fix: install Hugo Extended (see above).

2. **Deprecated `paginate` Setting**
   - Error: `site config key paginate was deprecated… use pagination.pagerSize`
   - Fix:
     ```diff
     - Paginate = 3
     + [pagination]
     +   pagerSize = 3
     ```

3. **Draft Posts Not Showing**
   - Ensure your `content/posts/my-post.md` has:
     ```yaml
     draft: false
     ```
   - Or build with drafts:
     ```bash
     hugo server -D --buildDrafts
     ```

4. **Missing Theme Submodule**
   - Symptom: blank site or missing layouts
   - Fix:
     ```yaml
     uses: actions/checkout@v4
     with:
       submodules: recursive
     ```

5. **Menus Not Defined**
   - Add to `config.toml`:
     ```toml
     [[menu.main]]
       name   = "Home"
       url    = "/"
       weight = 1

     [[menu.main]]
       name   = "Posts"
       url    = "/posts/"
       weight = 2
     ```

---

### 📦 GitHub Pages Deployment

#### Workflow: Push to `gh-pages` branch

```yaml
name: Deploy Hugo site

permissions:
  contents: write
  pages: write
  id-token: write

on:
  push:
    branches: [ main ]

jobs:
  build_deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "0.147.9"
          extended: true

      - run: hugo --minify --destination=public

      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_branch: gh-pages
          publish_dir: ./public
          keep_files: false
```

This preserves a history of each deployment in `gh-pages` for easy rollback.

---

### 🔍 Troubleshooting Tips

- **403 on Deploy**
  Add at top of workflow:
  ```yaml
  permissions:
    contents: write
    pages: write
    id-token: write
  ```

- **404 or XML Landing Page**
  Ensure `public/` is built and pushed fresh.
  Clean remote branch:
  ```bash
  git push origin --delete gh-pages
  ```

- **Verbose Logs**
  Hugo uses `--debug --log --logFile=./hugo.log`; upload via `actions/upload-artifact@v3` for deeper inspection.

---

With these steps and gotchas in mind, your first Hugo project should be smooth and maintainable. Happy blogging!

