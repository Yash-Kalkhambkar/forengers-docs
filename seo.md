---
title: SEO on forengers.in — Developer Guide
description: How SEO works on forengers.in, what affects it and best practices for future contributors.
layout: libdoc_page.liquid
permalink: seo.html
tags:
    - seo
    - core-web-vitals
    - accessibility
    - images
    - performance
tocEnabled: false
date: false
eleventyNavigation:
    key: SEO
---

## Table of Contents

1. [Purpose & Why SEO Matters](#purpose--why-seo-matters)
2. [What Impacts SEO on forengers.in](#what-impacts-seo-on-forengersin)
3. [Best Practices for Contributors](#best-practices-for-contributors)
4. [How to Test SEO Locally](#how-to-test-seo-locally)

---

## Purpose & Why SEO Matters

SEO (Search Engine Optimization) helps improve how easily people discover Forengers Foundation online — whether potential volunteers, partners, or donors.

For a public-facing NGO website like forengers.in, strong SEO directly affects:

* Visibility in Google Search
* Discoverability for new volunteers
* Trust, credibility, and how our site appears when shared
* Ranking for environmental and community-impact keywords
* Mobile user performance (important because 70%+ of visitors are on mobile)

Because Google now uses *mobile-first indexing*, our mobile performance and accessibility have a major influence on how we rank.

---

## What Impacts SEO on forengers.in

SEO on our site is influenced by a combination of technical and content factors:

### Technical Factors

* Core Web Vitals (LCP, FCP, CLS, TBT)
* Image optimization
* Accessibility (alt text, aria labels, contrast)
* Structured data (JSON-LD)
* Correct metadata (title, description, canonical)
* Mobile zoom and viewport behavior
* Link structure and internal navigation
* Cache headers and load performance

### Content Factors

* Clarity of page titles and headings
* High-quality text content (800–1200+ words where relevant)
* Consistent branding and messaging
* Keywords related to environmental initiatives, NGO work, Pune, outreach, etc.

---

## Best Practices for Contributors

### Always use the Astro `<Image>` component

Never use raw `<img>`.

### Always include alt text

Alt text should describe the function or content, not the decoration.

### Add aria-labels to icons

Especially when the icon is clickable.

### Avoid layout shift

Always define:

* width
* height
* aspect-ratio
* `contain-intrinsic-size` or similar if needed

### Don’t block zoom

Leave the viewport meta tag standard.

### Check your changes with PageSpeed

Run audits after each major UI change.

---

## How to Test SEO Locally

1. Run:

```bash
pnpm run dev
```

2. Test pages at:

```
http://localhost:3000
```

3. Use:

* AstroDevToolAstro Dev Toolbar
* Lighthouse (Chrome DevTools → Audits)
* PageSpeed Insights (copy local URL into tool after hosting via tunnel if needed)

4. Validate structured data via:
   [https://search.google.com/test/rich-results](https://search.google.com/test/rich-results)

