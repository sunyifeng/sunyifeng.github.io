---
title: "Adding Giscus Comments to Your Hugo Site"
date: 2025-07-29
series: ["Hugo Log"]
categories: ["Dev Notes"]
tags: ["hugo", "comments", "giscus"]
description: "Step-by-step guide to integrate Giscus (GitHub Discussions) into your Hugo site—installation, template tweaks, and testing."
---

In this entry of my **Hugo Log** series, I’ll walk you through how I integrated **Giscus**—a free, open-source comment system powered by GitHub Discussions—into my Hugo site running the PaperMod theme. By the end, you’ll have a live comments section under every post, complete with lazy loading, reactions, and GitHub-backed anti-spam protection.

---

## Prerequisites

1. **Public GitHub repo** with Discussions enabled (we used `sunyifeng/sunyifeng.github.io`).  
2. **Giscus app** installed on that repo.  
3. Hugo site built with **PaperMod** (or any theme where you can edit `layouts/partials` and your single post template).

---

## 1. Enable GitHub Discussions & Create a Category

1. Go to **Settings → Features** in your GitHub repo, check **Enable Discussions**, and save.  
2. Click the new **Discussions** tab → **Settings (⚙️)** → **Categories** → **New category**.  
   - **Name**: `General`  
   - **Type**: **Open-ended discussion**  
   - Hit **Create category**.  

---

## 2. Install & Configure Giscus

1. Visit the Giscus config site: https://giscus.app  
2. Select your repo (`yourname/your-blog`) and the `General` category.  
3. Choose **“Discussion title contains pathname”** mapping, enable **Reactions**, disable metadata, position input at **bottom**, turn on **lazy loading**.  
4. Copy the generated `<script>` block—you’ll see something like:

   ```html
   <script src="https://giscus.app/client.js"
           data-repo="sunyifeng/sunyifeng.github.io"
           data-repo-id="R_kgDOXXXXXXXXXXXX"
           data-category="General"
           data-category-id="DIC_kwDOXXXXXXXXXXXX"
           data-mapping="pathname"
           data-reactions-enabled="1"
           data-emit-metadata="0"
           data-input-position="bottom"
           data-loading="lazy"
           data-theme="preferred_color_scheme"
           crossorigin="anonymous"
           async>
   </script>
   ```

---

## 3. Add a `comments.html` Partial

1. In your Hugo project, create a new file:  
   ```
   layouts/partials/comments.html
   ```
2. Paste the `<script>` snippet inside, wrapped in a container:

   ```html
   <div id="giscus-container">
     <!-- Giscus comment widget -->
     <script src="https://giscus.app/client.js"
             data-repo="sunyifeng/sunyifeng.github.io"
             data-repo-id="R_kgDOXXXXXXXXXXXX"
             data-category="General"
             data-category-id="DIC_kwDOXXXXXXXXXXXX"
             data-mapping="pathname"
             data-reactions-enabled="1"
             data-emit-metadata="0"
             data-input-position="bottom"
             data-loading="lazy"
             data-theme="preferred_color_scheme"
             crossorigin="anonymous"
             async>
     </script>
   </div>
   ```

---

## 4. Hook the Partial into Your Post Template

1. Open `layouts/_default/single.html` (or your theme’s equivalent).  
2. Locate the footer area just before `</article>`, and ensure you have:

   ```go
   {{- /* Render comments if enabled */ -}}
   {{- partial "comments.html" . }}
   ```

   If your theme conditionally checks a `comments` param, either set `comments: true` in each post’s Front Matter or remove the `if` guard so it always shows.

---

## 5. Enable Comments in Front Matter

In each Markdown post where you want comments, add:

```yaml
comments: true
```

For example, in `content/posts/second-entry.md`:

```yaml
---
title: "Second Hugo Log Entry"
date: 2025-07-29
series: ["Hugo Log"]
categories: ["Dev Notes"]
tags: ["hugo", "comments", "giscus"]
description: "How to wire up Giscus comments in your Hugo site."
comments: true
---
```

---

## 6. Test Locally & Deploy

1. Run Hugo server:
   ```bash
   hugo server --disableFastRender
   ```
2. Browse to your local site, scroll down any post, and confirm the Giscus comment box appears and you can log in via GitHub to comment.  
3. Build and push to production:
   ```bash
   hugo --gc --minify
   # then git add/commit/push to trigger your deploy
   ```

---

🎉 That’s it! You now have a fully functional, GitHub-powered comment system in your Hugo blog—no ads, no extra servers, and native spam protection courtesy of GitHub. Keep logging your tweaks in **Hugo Log**, and happy blogging!

