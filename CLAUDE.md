# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Essential Commands

```bash
# Development
pnpm dev          # Start development server (localhost:4321)
pnpm build        # Build production site to ./dist/
pnpm preview      # Preview production build locally

# Package manager: pnpm@10.12.2 (required)
```

## Architecture Overview

This is an **Astro v5 blog** using server-side rendering with Vercel deployment. The architecture follows Astro's file-based routing with content collections for type-safe blog management.

### Content Management System

Blog posts are managed through **Astro Content Collections**:

- **Location**: `src/content/blog/` (supports `.md` and `.mdx`)
- **Schema**: Type-safe frontmatter validation in `src/content.config.ts`
- **Required fields**: `title`, `description`, `pubDate`
- **Optional fields**: `updatedDate`, `heroImage`
- **Auto-routing**: Content at `src/content/blog/post.md` → `/blog/post/`

### Key Components Architecture

- **BaseHead.astro**: Handles all SEO metadata, Open Graph, Twitter cards, canonical URLs
- **BlogPost.astro** (layout): Main template for individual blog posts
- **[...slug].astro**: Dynamic routing handler for all blog posts using `getStaticPaths()`

### Global Configuration

- **Site constants**: `src/consts.ts` contains `SITE_TITLE` and `SITE_DESCRIPTION`
- **Astro config**: `astro.config.mjs` configured for Vercel serverless with web analytics
- **Site URL**: Currently `https://example.com` in config (update after deployment)

### Built-in Features

- **RSS feed**: Auto-generated at `/rss.xml` from blog content
- **Sitemap**: Automatic generation via `@astrojs/sitemap`
- **Image optimization**: Uses Sharp for asset processing
- **Custom fonts**: Atkinson Regular/Bold preloaded from `public/fonts/`

## Development Workflow

1. **Add blog posts**: Create `.md`/`.mdx` files in `src/content/blog/`
2. **Images**: Reference from `src/assets/` in frontmatter `heroImage` field
3. **Styling**: Global styles in `src/styles/global.css`
4. **Components**: Reusable UI components in `src/components/`

## Deployment Configuration

Configured for **Vercel serverless** deployment:
- **Adapter**: `@astrojs/vercel` with web analytics enabled
- **Output mode**: `server` (SSR enabled)
- **Build**: Outputs to `dist/` directory

The repository is connected to GitHub and ready for Vercel deployment via GitHub integration.