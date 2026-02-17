# Rob J. Wang - Personal Website

A clean, minimal personal website built with [Hugo](https://gohugo.io/) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.

## Quick Start

### 1. Install Hugo

```bash
# macOS
brew install hugo

# Windows
choco install hugo-extended

# Linux
snap install hugo
```

### 2. Clone and Setup

```bash
# Clone this repo (or copy these files to your existing repo)
git clone https://github.com/robjwang/robjwang.github.io.git
cd robjwang.github.io

# Add PaperMod theme as submodule
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

### 3. Run Locally

```bash
hugo server -D
# Visit http://localhost:1313
```

### 4. Build for Production

```bash
hugo
# Output is in /public folder
```

## Structure

```
.
├── hugo.yaml              # Site configuration
├── content/
│   ├── about.md           # About page
│   ├── publications.md    # Publications list
│   └── posts/             # Blog posts (optional)
├── static/
│   ├── images/
│   │   └── profile.jpg    # Your photo (add this)
│   └── cv.pdf             # Your CV (add this)
└── themes/
    └── PaperMod/          # Theme (added via git submodule)
```

## Customization

### Profile Photo
Add your photo to `static/images/profile.jpg` (recommended: square, ~400x400px)

### CV
Add your CV to `static/cv.pdf`

### Colors & Styling
Create `assets/css/extended/custom.css` to override styles:

```css
:root {
    --primary: #1a73e8;  /* Link color */
}
```

### Adding Blog Posts
Create new posts in `content/posts/`:

```bash
hugo new posts/my-new-post.md
```

## Deployment to GitHub Pages

### Option A: GitHub Actions (Recommended)

Create `.github/workflows/hugo.yml`:

```yaml
name: Deploy Hugo site to Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

Then in GitHub repo settings → Pages → Source → "GitHub Actions"

### Option B: Manual

```bash
hugo
# Push /public contents to gh-pages branch
```

## Why PaperMod?

- Fast (minimal JS, optimized CSS)
- Clean typography
- Dark mode support
- SEO optimized
- Active maintenance
- Good documentation

## Resources

- [Hugo Documentation](https://gohugo.io/documentation/)
- [PaperMod Wiki](https://github.com/adityatelange/hugo-PaperMod/wiki)
- [PaperMod Demo](https://adityatelange.github.io/hugo-PaperMod/)
