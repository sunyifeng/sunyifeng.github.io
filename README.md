# sunyifeng.github.io

[![License](https://img.shields.io/github/license/sunyifeng/sunyifeng.github.io?style=flat-square)](LICENSE)

A personal blog and portfolio powered by [Hugo](https://gohugo.io/) and the [Ananke](https://github.com/theNewDynamic/gohugo-theme-ananke) theme. Hosted on GitHub Pages with automated deployment via GitHub Actions.

---

## 🚀 Quick Start

1. **Clone the repository**  
   ```bash
   git clone https://github.com/sunyifeng/sunyifeng.github.io.git
   cd sunyifeng.github.io
   ```

2. **Install Hugo Extended**  
   ```bash
   # macOS (Homebrew)
   brew install hugo

   # Ubuntu (Snap)
   sudo snap install hugo --channel=extended --classic
   ```

3. **Run the development server**  
   ```bash
   hugo server -D
   ```  
   Visit `http://localhost:1313/` in your browser.

4. **Build the static files**  
   ```bash
   hugo --minify
   ```

5. **Deploy**  
   Automatic deployment is configured in `.github/workflows/deploy.yml`. Pushing to `main` triggers a build and publishes to the `gh-pages` branch.

---

## 🛠️ Configuration

- **Site settings**: `config.toml`  
  - `baseURL`, `title`, `languageCode`, `theme`, and menu entries.

- **Theme customization**: `themes/ananke`  
  - Override layouts in `layouts/` or add custom CSS in `assets/`.

- **Content**: Markdown files in `content/`  
  - `posts/` for blog posts.  
  - `about.md` for your personal profile.

- **Static assets**: `static/`  
  - Images, JavaScript, and other files are copied as-is.

---

## 💡 Suggestions & Next Steps

- **SEO & Metadata**: Add front-matter fields (e.g., `description`, `tags`) and configure an SEO partial.  
- **Analytics**: Integrate Google Analytics or Plausible.io.  
- **Comments**: Enable [Disqus](https://disqus.com/) or [Gitalk](https://github.com/gitalk/gitalk).  
- **Search**: Implement client-side search with [Lunr.js](https://lunrjs.com/) or Algolia.  
- **Design tweaks**: Customize colors, fonts, and layouts in `assets/css` or override theme HTML templates.  
- **Accessibility**: Audit with Lighthouse and improve ARIA labels and keyboard navigation.  
- **Performance**: Use image optimization (e.g., [Hugo Image Processing](https://gohugo.io/functions/resource-image/`)).  

---

## 📂 Project Structure

```
├── archetypes/        # Content templates
├── assets/            # Hugo Pipes assets (SCSS, JS)
├── content/           # Markdown content files
├── layouts/           # Override theme templates
├── static/            # Static files (images, scripts)
├── themes/ananke/     # Ananke theme
├── config.toml        # Main configuration
├── .gitignore         # Ignored files (public/, resources/)
└── .github/workflows/
    └── deploy.yml     # CI/CD pipeline
```

---

## 📜 Custom License

This repository and its contents (including markdown, text, and assets) are distributed under the following terms:

1. **Attribution (署名)**: You must give appropriate credit to the author (sunyifeng), provide a link to the original repository, and indicate if changes were made.  
2. **Non-Commercial (非商业用途)**: You may not use the material for commercial purposes.  
3. **No Redistribution (禁止转载)**: You may not publish or redistribute the content in any form (print, digital, or other platforms) without express permission.  
4. **Contributions via Pull Requests (提交 Commit 修改)**: You are welcome to propose improvements or fixes by submitting pull requests to this repository. Any such contributions will be reviewed and incorporated by the maintainer.

By contributing to this repository, you agree that your contributions will be licensed under these same terms.

