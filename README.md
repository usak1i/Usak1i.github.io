# Usak1i's Blog

Personal tech blog built with [Astro](https://astro.build) and [AstroPaper](https://github.com/satnaing/astro-paper) theme. Deployed to GitHub Pages at [usak1i.github.io](https://Usak1i.github.io).

## Tech Stack

- **Framework**: [Astro](https://astro.build)
- **Theme**: [AstroPaper v5](https://github.com/satnaing/astro-paper)
- **Styling**: [Tailwind CSS](https://tailwindcss.com)
- **Search**: [Pagefind](https://pagefind.app)
- **Deployment**: GitHub Pages via GitHub Actions

## Features

- Dark / light mode toggle
- Tag-based categorization
- Full-text search
- Auto-generated OG images, RSS feed, sitemap
- TypeScript throughout

## Local Development

```bash
pnpm install
pnpm run dev
```

Open [http://localhost:4321](http://localhost:4321) in your browser.

## Writing Posts

Add a new `.md` or `.mdx` file to `src/data/blog/`:

```markdown
---
author: Usak1i
pubDatetime: 2026-05-01T00:00:00+08:00
title: Post Title
slug: post-slug
featured: false
draft: false
tags:
  - tag1
description: A short description.
---

Post content here.
```

## Build

```bash
pnpm run build
```

Output is generated in `dist/`.

## Docker

```bash
# Development
docker compose -f docker/docker-compose.yml up

# Production build
docker build -f docker/Dockerfile .
```

## License

MIT — see [LICENSE](./LICENSE) for details.
