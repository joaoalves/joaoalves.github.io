# João Alves — Academic Website

Built with [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) (Jekyll).

## File structure

```
.
├── _config.yml            ← site-wide settings, author sidebar
├── _data/
│   └── navigation.yml     ← top nav links
├── _pages/
│   ├── research.md
│   ├── group.md
│   └── publications.md
├── assets/
│   ├── css/
│   │   ├── main.scss      ← loads theme + custom overrides
│   │   └── custom.scss    ← your CSS tweaks
│   └── images/
│       ├── profile.jpg    ← sidebar photo (recommend ~400×400px)
│       └── group/         ← one photo per member, named consistently
│           ├── placeholder.png
│           ├── joao-alves.jpg
│           ├── andrea-socci.jpg
│           └── ...
├── index.md               ← About / home page
└── Gemfile
```

## Local development

```bash
# 1. Install Ruby (3.1+) and Bundler if not already installed
gem install bundler

# 2. Install dependencies
bundle install

# 3. Serve locally with live reload
bundle exec jekyll serve --livereload

# Site will be at http://localhost:4000
```

## Deploying to GitHub Pages

1. Push this repo to GitHub as `<yourusername>.github.io`
2. Go to Settings → Pages → Source: **GitHub Actions**
3. GitHub will auto-detect Jekyll and deploy on every push

Or add this `.github/workflows/jekyll.yml` for explicit control:

```yaml
name: Deploy Jekyll site
on:
  push:
    branches: ["main"]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/jekyll-build-pages@v1
      - uses: actions/upload-pages-artifact@v3
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

## Updating content

- **Bio / links**: edit `_config.yml` → `author:` block (restart `jekyll serve` after)
- **Research**: edit `_pages/research.md`
- **Group members**: edit `_pages/group.md` + drop photos in `assets/images/group/`
- **Publications**: edit `_pages/publications.md`
- **Nav links**: edit `_data/navigation.yml`

## Group photos

- Recommended size: **400×400px** minimum, square crop
- Name files lowercase with hyphens: `firstname-lastname.jpg`
- The CSS uses `object-fit: cover` so non-square source images crop automatically
