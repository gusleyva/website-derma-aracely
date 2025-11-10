# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview
Professional landing page for Dra. Aracely Castillo (Dermatóloga) built as a static site with Astro + Tailwind CSS. Focus on SEO optimization and deployment to self-hosted Nginx server.

## Development Commands

### Core workflow
- `npm run dev` - Start development server
- `npm run build` - Build static site to `dist/`
- `npm run preview` - Preview production build locally

### Testing
No test framework is currently configured.

## Architecture

### Static Site Generation (SSG)
This is a 100% static Astro site with no runtime required in production. All pages are pre-rendered at build time.

### Color System
Custom CSS variables defined in `src/styles/global.css`:
- `--primary: #b88a8f` (primary brand color)
- `--secondary: #dcb7b9` (secondary brand color)
- `--text: #4e3a3c` (main text color)

Use these variables in Tailwind classes: `text-[var(--primary)]`, `bg-[var(--secondary)]`, etc.

### Layout System
- **Base Layout**: `src/layouts/Layout.astro` - Contains HTML structure, SEO meta tags, and global styles import
- All pages should use this layout and override SEO props as needed

### SEO Configuration
Default SEO setup in `Layout.astro` includes:
- Title, description, keywords meta tags
- Open Graph tags (title, description, type, locale)
- Theme color matching primary brand color

**Future SEO enhancements needed**:
- Add `og:image` and `twitter:card` meta tags
- Implement Schema.org JSON-LD for medical professional markup
- Add `sitemap.xml` and `robots.txt` (place in `public/`)

### Project Structure
```
src/
├── layouts/       # Base HTML layouts
├── pages/         # File-based routing (.astro files become routes)
├── components/    # Reusable Astro components
├── styles/        # Global CSS (Tailwind + custom variables)
└── assets/        # Images and static assets for optimization

public/           # Static files copied directly to dist/ (favicon, robots.txt, etc.)
```

## Deployment

### Build Process
1. Run `npm run build` to generate `dist/` folder
2. Copy entire `dist/` contents to server (e.g., `/var/www/derma`)

### Nginx Configuration
Site requires basic static file serving. Key configuration points:
- Root directory points to build output
- Fallback to `index.html` for SPA-style routing
- Cache headers for static assets (CSS, JS, images) with 30-day expiration
- HTTPS via Certbot/Let's Encrypt recommended

## Language & Locale
- Content language: Spanish (es_MX)
- HTML lang attribute: `es`
- Target audience: Medical patients in Navojoa, Sonora, Mexico
