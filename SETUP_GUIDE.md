# OCMblog Setup & Customization Guide

## Table of Contents
1. [Local Development Setup](#local-development-setup)
2. [Customizing Your Site](#customizing-your-site)
3. [Adding Content](#adding-content)
4. [Git Workflow](#git-workflow)
5. [Deployment Process](#deployment-process)

---

## Local Development Setup

### Prerequisites
- Ruby (2.4+ recommended)
- Bundler gem
- Git

### Installation Steps

```bash
# Navigate to your project
cd /Users/scot/enochian-watchtower/GitBlog

# Install Bundler if not already installed
gem install bundler

# Install Jekyll and dependencies
bundle install

# Serve the site locally
bundle exec jekyll serve

# Or use the development config for faster builds
bundle exec jekyll serve --config _config.yml,_config_dev.yml
```

Your site will be available at: `http://localhost:4000/OCMblog/`

**Important:** Always test locally before pushing to GitHub!

---

## Customizing Your Site

### 1. Basic Site Information

Edit `_config.yml`:

```yaml
# Lines 11-17: Update site identity
title: 'Your Blog Title'
slogan: 'Your tagline here'
description: 'Brief description of your blog (max 150 chars for SEO)'

# Lines 20: Update credits (optional)
credits: '<p>Created by Your Name</p>'

# Lines 24: Update author
author: yourname  # Must match entry in _data/authors.yml
```

### 2. Author Information

Edit `_data/authors.yml`:

```yaml
yourname:
  name: "Your Full Name"
  siterole: "webmaster, developer, author"
  uri: https://yoursite.com
  email: your@email.com
  twitter: "@yourhandle"
  # Add your bio, avatar, etc.
```

### 3. Navigation Menu

Edit `_data/navigation.yml`:

```yaml
- title: "Home"
  url: "/"
  side: left

- title: "Blog"
  url: "/blog/"
  side: left

- title: "About"
  url: "/about/"
  side: left

# Add more menu items as needed
```

### 4. Social Media Links

Edit `_data/socialmedia.yml`:

```yaml
- name: GitHub
  url: https://github.com/yourusername
  class: icon-github
  title: "Code on GitHub"

- name: Twitter
  url: https://twitter.com/yourhandle
  class: icon-twitter
  title: "Follow on Twitter"
```

### 5. Colors and Styling

Edit `_sass/_01_settings_colors.scss`:

```scss
// Primary colors
$ci-1: #334D5C;  // Dark blue-grey
$ci-2: #45B29D;  // Teal
$ci-3: #EFC94C;  // Yellow
$ci-4: #E27A3F;  // Orange
$ci-5: #DF4949;  // Red
$ci-6: #A1D044;  // Green

// Customize these to match your brand
```

### 6. Homepage Widgets

Edit `pages/pages-root-folder/index.md` for frontpage widgets:

```yaml
---
layout: frontpage
header:
  image_fullwidth: header_unsplash_12.jpg
widget1:
  title: "Widget 1 Title"
  url: '/blog/'
  image: widget-1-302x182.jpg
  text: 'Description of widget 1'
widget2:
  # ... similar structure
widget3:
  # ... similar structure
---
```

---

## Adding Content

### Creating Blog Posts

Create files in `_posts/` with format: `YYYY-MM-DD-title.md`

Example: `_posts/2026-01-29-my-first-post.md`

```yaml
---
layout: page
title: "My First Blog Post"
subheadline: "Getting Started"
teaser: "A brief preview of the post content"
categories:
  - blog
tags:
  - jekyll
  - tutorial
image:
  header: header_unsplash_1.jpg
  thumb: thumbnail.jpg
  caption: Photo by Person
  caption_url: https://unsplash.com/
---

Your post content here in Markdown format.

## Section Headers

Regular paragraph text with **bold** and *italic* formatting.

### Subsections

- Bullet points
- Work great
- In Markdown

```code blocks are supported```

[Links work too](https://example.com)
```

### Adding Images

1. **Place images in `/images/` directory**
2. **Reference in posts:**

```markdown
![Alt text]({{ site.urlimg }}your-image.jpg)
```

Or use the image front matter:

```yaml
image:
  title: image-filename.jpg
  caption: Image description
```

**Image Size Recommendations:**
- Header images: 1600x500px
- Thumbnails: 302x182px
- Gallery images: 800x600px

### Creating Pages

Create files in `pages/` directory:

Example: `pages/about.md`

```yaml
---
layout: page
title: "About"
subheadline: "Learn more about this site"
teaser: "Brief description"
permalink: "/about/"
---

Your about page content here.
```

### Creating a Gallery

```yaml
---
layout: page
title: "Gallery"
subheadline: "Photo Collection"
teaser: "Browse our photos"
images:
  - image_url: gallery-example-1.jpg
    caption: First image
  - image_url: gallery-example-2.jpg
    caption: Second image
---

{% include gallery %}
```

---

## Git Workflow

### Recommended Workflow

#### 1. **Make Changes Locally**

```bash
cd /Users/scot/enochian-watchtower/GitBlog

# Create a new branch for your changes (recommended)
git checkout -b my-new-feature

# Make your edits...
```

#### 2. **Test Locally**

```bash
# Start local server
bundle exec jekyll serve

# View at http://localhost:4000/OCMblog/
# Test everything works before committing
```

#### 3. **Stage and Commit Changes**

```bash
# Check what changed
git status

# Stage specific files
git add _posts/2026-01-29-my-new-post.md
git add images/my-new-image.jpg
git add _config.yml

# Or stage all changes
git add .

# Commit with descriptive message
git commit -m "Add new blog post about Jekyll customization"
```

#### 4. **Push to GitHub**

```bash
# First time pushing a new branch
git push -u origin my-new-feature

# Subsequent pushes
git push

# Or push directly to gh-pages if not using branches
git checkout gh-pages
git merge my-new-feature
git push origin gh-pages
```

#### 5. **Wait for Build**

```bash
# Check build status
gh run list --repo scotgl/OCMblog --limit 3

# View specific run logs if needed
gh run view <run-id> --log
```

### Alternative: Direct to gh-pages

For quick updates (not recommended for major changes):

```bash
# Make sure you're on gh-pages branch
git checkout gh-pages

# Make changes, then:
git add .
git commit -m "Quick update"
git push origin gh-pages
```

### Pulling Latest Changes

```bash
# Fetch latest from GitHub
git fetch origin

# Pull changes from gh-pages
git pull origin gh-pages

# Or if you're already on gh-pages
git pull
```

### Handling Merge Conflicts

```bash
# If you get conflicts when pulling
git status  # Shows conflicted files

# Edit conflicted files, then:
git add resolved-file.md
git commit -m "Resolve merge conflict"
git push
```

---

## Deployment Process

### Automatic Deployment (Current Setup)

GitHub Pages automatically builds and deploys when you push to `gh-pages` branch.

**Build Process:**
1. Push commits to `gh-pages` branch
2. GitHub Actions triggers build
3. Jekyll generates static site
4. Site deploys to https://scotgl.github.io/OCMblog/
5. Usually takes 1-3 minutes

**Monitoring Deployments:**

```bash
# Check deployment status
gh api repos/scotgl/OCMblog/pages

# View recent runs
gh run list --repo scotgl/OCMblog --limit 5

# Watch current build
gh run watch
```

### Local Build Testing

Test the production build locally:

```bash
# Build site (same way GitHub Pages does)
JEKYLL_ENV=production bundle exec jekyll build

# Check _site/ directory for output
ls -la _site/

# Serve the built site
cd _site && python -m SimpleHTTPServer 8000
# Visit http://localhost:8000/OCMblog/
```

---

## Best Practices

### Content Creation

1. **Always use front matter** in posts and pages
2. **Optimize images** before adding (use tools like ImageOptim, TinyPNG)
3. **Test internal links** locally before pushing
4. **Use descriptive filenames** for images and posts
5. **Write SEO-friendly descriptions** (150 chars max)

### Development Workflow

1. ✅ **Create feature branch** for new work
2. ✅ **Test locally** with `bundle exec jekyll serve`
3. ✅ **Check for errors** in terminal output
4. ✅ **Commit small, logical changes** with clear messages
5. ✅ **Push to GitHub** when ready
6. ✅ **Verify deployment** succeeded
7. ✅ **Test live site** in browser

### Git Best Practices

```bash
# Good commit messages
git commit -m "Add blog post about OCM philosophy"
git commit -m "Update homepage hero image"
git commit -m "Fix broken link in about page"

# Bad commit messages (avoid these)
git commit -m "updates"
git commit -m "stuff"
git commit -m "fixed it"
```

### Branch Strategy

**Recommended:**
- `master`: Main development branch (optional)
- `gh-pages`: Production branch (auto-deploys)
- `feature/post-name`: Feature branches for new content
- `fix/issue-description`: Bug fix branches

```bash
# Example workflow
git checkout -b feature/new-about-page
# ... make changes ...
git commit -m "Create new about page with bio"
git checkout gh-pages
git merge feature/new-about-page
git push origin gh-pages
git branch -d feature/new-about-page
```

---

## Common Tasks Quick Reference

### Add a new blog post
```bash
# 1. Create file
touch _posts/2026-01-29-my-post.md

# 2. Edit with your preferred editor
code _posts/2026-01-29-my-post.md

# 3. Test locally
bundle exec jekyll serve

# 4. Commit and push
git add _posts/2026-01-29-my-post.md
git commit -m "Add new post: My Post Title"
git push origin gh-pages
```

### Update site configuration
```bash
# 1. Edit _config.yml
code _config.yml

# 2. Restart Jekyll server (if running)
# Ctrl+C to stop, then:
bundle exec jekyll serve

# 3. Commit and push
git add _config.yml
git commit -m "Update site title and description"
git push origin gh-pages
```

### Add new images
```bash
# 1. Copy images to images/ directory
cp ~/Desktop/my-photo.jpg images/

# 2. Optimize image size if needed
# (use ImageOptim or similar tool)

# 3. Reference in post/page
# {{ site.urlimg }}my-photo.jpg

# 4. Commit and push
git add images/my-photo.jpg
git commit -m "Add photo for blog post"
git push origin gh-pages
```

### Update navigation menu
```bash
# 1. Edit _data/navigation.yml
code _data/navigation.yml

# 2. Test locally
bundle exec jekyll serve

# 3. Commit and push
git add _data/navigation.yml
git commit -m "Add new menu item"
git push origin gh-pages
```

---

## Troubleshooting

### Jekyll won't build locally
```bash
# Try installing dependencies
bundle install

# Update gems
bundle update

# Clear cache
bundle exec jekyll clean
bundle exec jekyll serve
```

### GitHub Pages build fails
```bash
# Check build logs
gh run list --repo scotgl/OCMblog
gh run view <run-id> --log

# Common issues:
# - Sass syntax errors (check _sass/ files)
# - Invalid YAML front matter (check --- markers)
# - Missing images referenced in posts
# - Liquid syntax errors in templates
```

### Changes not showing on live site
1. Wait 2-3 minutes for build to complete
2. Hard refresh browser (Cmd+Shift+R on Mac)
3. Check build succeeded: `gh run list`
4. Verify you pushed to `gh-pages` branch

### Images not displaying
1. Check image path: `{{ site.urlimg }}filename.jpg`
2. Verify image exists in `/images/` directory
3. Check file name matches exactly (case-sensitive)
4. Ensure image was committed and pushed

---

## File Structure Reference

```
GitBlog/
├── _config.yml              # Main configuration
├── _config_dev.yml          # Development config
├── _data/                   # Data files
│   ├── authors.yml          # Author information
│   ├── navigation.yml       # Menu structure
│   └── socialmedia.yml      # Social links
├── _drafts/                 # Unpublished posts
├── _includes/               # Reusable components
├── _layouts/                # Page templates
├── _posts/                  # Blog posts
│   └── design/              # Example posts (delete these)
├── _sass/                   # Sass/CSS files
├── assets/                  # Compiled CSS/JS
├── blog/                    # Blog index pages
├── images/                  # Your images go here
└── pages/                   # Static pages
    ├── pages-root-folder/   # Homepage and special pages
    └── *.md                 # Other pages

```

---

## Resources

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Feeling Responsive Theme Docs](https://phlow.github.io/feeling-responsive/)
- [Liquid Template Language](https://shopify.github.io/liquid/)
- [Markdown Guide](https://www.markdownguide.org/)
- [GitHub Pages Docs](https://docs.github.com/en/pages)

---

## Quick Checklist for New Posts

- [ ] Create file in `_posts/` with format `YYYY-MM-DD-title.md`
- [ ] Add front matter with layout, title, categories, tags
- [ ] Add images to `/images/` directory
- [ ] Reference images with `{{ site.urlimg }}`
- [ ] Test locally with `bundle exec jekyll serve`
- [ ] Check for spelling/grammar errors
- [ ] Commit with descriptive message
- [ ] Push to `gh-pages` branch
- [ ] Wait for build to complete (1-3 minutes)
- [ ] Verify post appears on live site
- [ ] Test all links and images work

---

**Your live site:** https://scotgl.github.io/OCMblog/

**Repository:** https://github.com/scotgl/OCMblog
