# My Org Blog

A Jekyll blog that supports writing posts in Org-mode format, automatically converted to Markdown during the build process.

## Features

- Write blog posts in Org-mode (`.org` files)
- Automatic conversion to Markdown using Pandoc
- Deployed to GitHub Pages via GitHub Actions

## How to Enable GitHub Pages Deployment

This repository includes a GitHub Actions workflow (`.github/workflows/pages.yml`) that automatically converts Org files to Markdown and deploys to GitHub Pages.

**To enable this workflow:**

1. Go to your repository on GitHub
2. Click on **Settings** → **Pages** (in the left sidebar)
3. Under **Build and deployment**, change the **Source** from:
   - ❌ "Deploy from a branch" 
   - ✅ **"GitHub Actions"**
4. Click **Save**

That's it! On the next push to the `main` branch, GitHub Actions will:
- Convert your Org files to Markdown
- Build your Jekyll site
- Deploy it to GitHub Pages

Your posts will now appear in the "Recent Posts" section on your site!

## Writing Posts

1. Create a new `.org` file in the `_posts/` directory
2. Name it using the pattern: `YYYY-MM-DD-title.org`
3. Add Org-mode metadata at the top:
   ```org
   #+TITLE: Your Post Title
   #+AUTHOR: Your Name
   #+DATE: YYYY-MM-DD
   ```
4. Write your content using Org-mode syntax
5. Commit and push - the workflow will handle the rest!

## Local Development

To build and preview the site locally:

```bash
# Install dependencies
bundle install

# Convert Org files to Markdown (requires Pandoc)
for f in _posts/*.org; do
  base=$(basename "$f" .org)
  output="_posts/${base}.md"
  pandoc "$f" -f org -t markdown --standalone -o "$output"
  # Note: On macOS, use: sed -i '' '1a layout: post' "$output"
  sed -i '1a layout: post' "$output"
done

# Build and serve the site
bundle exec jekyll serve

# Visit http://localhost:4000/test-jekyll-ci/ in your browser
```

## Requirements

- Ruby 3.2+
- Bundler
- Pandoc (for Org-to-Markdown conversion)
