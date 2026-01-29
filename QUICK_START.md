# Quick Start Guide

## Local Development

```bash
# Install dependencies (first time only)
bundle install

# Run local server
bundle exec jekyll serve

# View at: http://localhost:4000/OCMblog/
```

## Essential Commands

```bash
# Test locally BEFORE pushing
bundle exec jekyll serve

# Stage changes
git add .

# Commit with message
git commit -m "Your descriptive message"

# Push to deploy
git push origin gh-pages

# Check build status
gh run list --repo scotgl/OCMblog --limit 3
```

## File Locations

| What to Edit | File Location |
|--------------|---------------|
| Site title, description | `_config.yml` |
| Navigation menu | `_data/navigation.yml` |
| Author info | `_data/authors.yml` |
| Social links | `_data/socialmedia.yml` |
| Colors/styling | `_sass/_01_settings_colors.scss` |
| Homepage | `pages/pages-root-folder/index.md` |
| New blog posts | `_posts/YYYY-MM-DD-title.md` |
| Images | `images/` |
| New pages | `pages/pagename.md` |

## Create New Blog Post

1. Create: `_posts/2026-01-29-my-title.md`
2. Add front matter:
```yaml
---
layout: page
title: "Post Title"
categories:
  - blog
tags:
  - tag1
---

Post content here...
```
3. Test: `bundle exec jekyll serve`
4. Deploy: `git add . && git commit -m "Add new post" && git push origin gh-pages`

## Workflow

1. ✅ Edit files
2. ✅ Test locally (`bundle exec jekyll serve`)
3. ✅ Commit changes (`git commit`)
4. ✅ Push to GitHub (`git push origin gh-pages`)
5. ✅ Wait 1-3 minutes for build
6. ✅ Verify at: https://scotgl.github.io/OCMblog/

## Image Sizes

- Header: 1600x500px
- Thumbnail: 302x182px
- Gallery: 800x600px

## Live Site

🌐 https://scotgl.github.io/OCMblog/

📚 Full guide: See `SETUP_GUIDE.md`
