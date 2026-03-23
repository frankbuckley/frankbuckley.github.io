# Copilot Instructions

## Project Overview

Personal website for frankbuckley.com, built with Astro 6 and deployed to GitHub Pages via GitHub Actions. Static site with a blog, biography, and CV.

## Commands

- `npm run dev` — Start local dev server
- `npm run build` — Production build (outputs to `dist/`)
- `npm run preview` — Preview production build locally

There are no tests or linters configured.

## Architecture

- **Astro 6** static site using `.astro` single-file components
- **Bootstrap 5** for styling (CSS only, no JS bundle), with **Bootstrap Icons** via icon font — global styles and theme in `src/styles/default.css`
- **Content collections** for blog posts — Markdown files in `src/content/blog/`, schema defined in `src/content.config.ts`
- `src/layouts/Layout.astro` — Base HTML layout with nav, main, footer and an optional `title` prop
- `src/layouts/BlogPost.astro` — Blog post layout (title, date, tags, content), wraps `Layout`
- `src/pages/` — File-based routing: home, about, cv, blog index, blog `[slug]` dynamic routes
- `src/components/` — Shared components (e.g. `Nav.astro`)
- `public/` — Static assets served as-is
- RSS feed at `/rss.xml` via `@astrojs/rss`

## Blog Posts

Add new posts as Markdown files in `src/content/blog/`. Required frontmatter:

```yaml
title: Post Title
description: A short summary
pubDate: 2026-03-23
tags: [tag1, tag2]  # optional, defaults to []
draft: false         # optional, defaults to false
```

The filename (without `.md`) becomes the URL slug: `src/content/blog/my-post.md` → `/blog/my-post/`.

## Conventions

- Site is configured with `trailingSlash: "always"` in `astro.config.mjs` — all internal links must end with `/`
- TypeScript uses Astro's `strict` preset
- Use Bootstrap utility classes for styling; use Bootstrap Icons via `<i class="bi bi-*">` elements; reference custom theme colours via `var(--color-*)`:
  - `--color-text` (`#1a1a1a`), `--color-text-muted` (`#555`), `--color-accent` (`#2563eb`), `--color-border` (`#e5e5e5`)
- Blog post Markdown content is rendered inside a `.prose` wrapper that styles headings, paragraphs, lists, links, and code blocks
- Pages import and wrap content in the `Layout` component
- Deployment targets Node 25 (see `.github/workflows/deploy.yml`)
