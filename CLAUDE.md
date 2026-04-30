# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
pnpm run dev          # Start dev server at localhost:4321
pnpm run build        # Type-check + build + generate Pagefind search index
pnpm run preview      # Preview production build
pnpm run lint         # ESLint
pnpm run format       # Prettier (write)
pnpm run format:check # Prettier (check only)
```

> `pnpm run build` runs `astro check && astro build && pagefind --site dist && cp -r dist/pagefind public/` — all steps must pass.

## Architecture

### Content

Blog posts live in `src/data/blog/` as `.md` or `.mdx` files. The collection is defined in `src/content.config.ts`.

Required frontmatter fields:
```yaml
pubDatetime: 2026-05-01T00:00:00+08:00  # ISO 8601 with TZ offset
title: Post Title
description: Short description for SEO.
```

Useful optional fields:
```yaml
author: Usak1i          # defaults to SITE.author
featured: true          # shows in homepage "Featured" section
draft: false            # excluded from build if true
tags: [astro, blog]     # defaults to ["others"]
modDatetime: ...        # used for sort order if present
```

### Slug & URL generation

Slugs are **derived from file path**, not a frontmatter `slug` field. `src/utils/getPath.ts` strips the `BLOG_PATH` prefix and slugifies each directory segment. A file at `src/data/blog/tools/my-post.md` becomes `/posts/tools/my-post`.

**Directories prefixed with `_`** (e.g. `_releases/`) are excluded from public routes — useful for draft folders.

### Config

`src/config.ts` exports a single `SITE` object with the site URL, author, locale (`zh-TW`), timezone (`Asia/Taipei`), pagination sizes, and feature flags (`dynamicOgImage`, `showArchives`, etc.).

`src/constants.ts` exports `SOCIALS` and `SHARE_LINKS` arrays used by `Socials.astro` and `ShareLinks.astro`.

### Page & layout hierarchy

```
Layout.astro          ← base HTML shell, head, global styles
└── Main.astro        ← content width container
    └── pages/*.astro ← file-based routes (index, posts, tags, search, archives)

PostDetails.astro     ← wraps individual post pages; handles prev/next navigation
AboutLayout.astro     ← wraps about.md
```

### Scheduled & draft posts

- `draft: true` → excluded from build entirely.
- Future `pubDatetime` → hidden in production until within `SITE.scheduledPostMargin` (15 min). Visible in `dev`.

### Search

Pagefind runs as part of `pnpm run build`. The index is written to `dist/pagefind/` then copied to `public/pagefind/` so `pnpm run preview` can serve it. Only pages with `data-pagefind-body` are indexed.

### OG images

When `SITE.dynamicOgImage = true`, posts without an explicit `ogImage` get a generated image via `src/pages/posts/[...slug]/index.png.ts` using Satori + `@resvg/resvg-js`.

### Linting rules

ESLint bans `console` statements (error). Prettier uses `printWidth: 80`, `tabWidth: 2`, double quotes, `trailingComma: "es5"`.

## Deployment

GitHub Actions (`.github/workflows/deploy.yml`) builds and deploys to GitHub Pages on every push to `main`. The CI workflow (`.github/workflows/ci.yml`) runs lint + build on PRs. Docker files are in `docker/` for local container use.
