# Personal Brand Site — Hugo + GitHub Pages

## Quick Start

### 1. Prerequisites
- [Hugo Extended](https://gohugo.io/installation/) v0.128+
- Git

### 2. Local Development
```bash
cd hugo-site
hugo server -D
# Visit http://localhost:1313
```

### 3. Customise `hugo.toml`
Update these fields:
```toml
baseURL = "https://YOURUSERNAME.github.io/"

[params]
  author       = "Your Name"
  tagline      = "Your tagline"
  description  = "Your one-liner"
  github       = "https://github.com/yourusername"
  linkedin     = "https://linkedin.com/in/yourprofile"
  youtube      = "https://youtube.com/@yourchannel"
```

### 4. Deploy to GitHub Pages
1. Create a repo named `YOURUSERNAME.github.io`
2. Push this folder to the `main` branch
3. In repo Settings → Pages → Source: **GitHub Actions**
4. The `hugo.yml` workflow will build and deploy automatically

---

## Content Structure

```
content/
├── _index.md                          # Homepage
├── blog/_index.md                     # Blog listing
├── books/_index.md                    # Books page
└── series/
    ├── beer-drinkers-guide/
    │   ├── _index.md                  # Series landing
    │   ├── pints-packets-protocols.md # Episode 1 (written)
    │   ├── beer-drinkers-guide-to-vpns.md
    │   └── spf-dkim-dmarc.md
    └── attackers-mindset/
        ├── _index.md                  # Series landing
        ├── ep01-how-attackers-think.md
        └── ep02-reconnaissance.md
```

## Adding a New Blog Post

Create `content/series/beer-drinkers-guide/my-new-post.md`:

```yaml
---
title: "A Beer Drinker's Guide to Firewalls"
description: "One-line summary for cards and SEO."
date: 2025-06-01
series: "beer-drinkers-guide"
readtime: "~8 min read"
tags: ["firewalls", "networking"]
youtube_id: "dQw4w9WgXcQ"   # Optional: embeds the video
# youtube_url: "https://..."  # Alternative: shows a Watch button
---

Your post body here in Markdown.
```

## Adding an Attacker's Mindset Episode

Same pattern, but use `series: "attackers-mindset"` and save to `content/series/attackers-mindset/`.

## Book Covers
To add a real book cover image, add the image to `static/images/` and update `themes/cyberbar/layouts/books/list.html` — replace the `.book-cover` div with an `<img>` tag.

## Fonts Used
- **Bebas Neue** — display headings (Google Fonts)
- **Share Tech Mono** — terminal / monospace accents (Google Fonts)  
- **DM Sans** — body text (Google Fonts)
