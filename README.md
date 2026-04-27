# Zhiyuan Cheng Personal Site

This repository contains a Jekyll-based personal website and blog.

## Structure

- `_posts/`: blog posts
- `_layouts/`: page and post layouts
- `_includes/`: shared header, footer, navbar, and helpers
- `_data/`: navigation and resume data
- `assets/`: styles, scripts, images, and favicons

## Local development

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://127.0.0.1:4000` or `http://localhost:4000`.

## Notes

- The site keeps a small custom Jekyll structure instead of the original upstream theme packaging files.
- Generated output such as `_site/` should not be committed.
