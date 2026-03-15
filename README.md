# Samaritan Bio

Marketing website for [samaritan.bio](https://samaritan.bio) — an AI-powered biomarker intelligence company developing AroBag, a smart urine monitoring device for early detection of acute kidney injury (AKI).

## Stack

- **Static site generator:** [Eleventy (11ty)](https://www.11ty.dev/) v3 with Nunjucks templates
- **CSS:** [Tailwind CSS](https://tailwindcss.com/) v4 with `@theme` design tokens + custom CSS
- **Fonts:** TASA Explorer (headings), Schibsted Grotesk (body)
- **Icons:** Phosphor Icons (CDN)

## Getting started

```bash
npm install
```

## Development

Run the dev server with live reload and CSS watching:

```bash
npm run dev
```

This starts Eleventy's dev server and Tailwind's watcher in parallel.

## Build

```bash
npm run build
```

Runs `build:11ty` (generates HTML into `_site/`) then `build:css` (compiles and minifies Tailwind into `_site/css/main.css`).

Individual steps:

```bash
npm run build:11ty   # Eleventy only
npm run build:css    # Tailwind only
```

## Project structure

```
src/
  index.njk              # Landing page
  pages/
    arobag.njk            # Product page
    about.njk             # Team, advisors, careers
    blog.njk              # Blog listing
    design-system.njk     # Internal design reference
    savings-calculator.njk
  blog/                   # Blog posts (Markdown)
  jobs/                   # Career listings (Markdown)
  css/
    main.css              # Full design system (Tailwind v4 + custom CSS)
  js/                     # Client-side scripts
  assets/                 # Images and static files
  _includes/
    layouts/base.njk      # Base layout with nav and footer
  _data/                  # Global data files
```

Output is written to `_site/`.

## Content (CMS)

Content is managed as flat files — no external CMS. Eleventy collections are configured via directory-level `*.json` files that set the layout, tag, and permalink pattern for all files in that folder.

### Blog posts

Add a Markdown file to `src/blog/`. The directory data file (`blog.json`) automatically assigns the `post` tag, `layouts/post.njk` layout, and `/blog/{slug}/` URL.

Frontmatter fields:

```yaml
---
title: "Post Title"
description: "Short description for SEO and social cards"
date: 2026-01-15
author: Samaritan Team
tags:
  - Clinical Science
  - AKI
draft: false        # set true to hide from listing
---
```

Posts also get a CTA block at the bottom, controlled by the `cta` field in `blog.json` (defaults to `"demo"`). Available CTA keys are defined in `_data/site.json` under `ctas`.

### Job listings

Add a Markdown file to `src/jobs/`. The directory data file (`jobs.json`) assigns the `job` tag, `layouts/job-detail.njk` layout, and `/careers/{slug}/` URL.

Frontmatter fields:

```yaml
---
title: Embedded Systems Engineer (Firmware), Medical Devices
location: Delhi NCR
type: Full-time
active: true        # set false to unlist
---
```

### Global site data

`src/_data/site.json` holds company info, team members, advisors, and reusable CTA blocks. Templates access this data via `{{ site.title }}`, `{{ site.team.founders }}`, `{{ site.ctas.demo }}`, etc.
