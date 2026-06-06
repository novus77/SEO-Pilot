---
name: image-optimization
description: Optimize website images for SEO, accessibility, and page performance. Use when Codex needs to audit or improve image compression, dimensions, modern formats, descriptive filenames, alt text, captions, responsive image markup, lazy/eager loading, image indexability, image sitemap entries, structured data image fields, or before/after SEO and Core Web Vitals measurement.
---

# Image Optimization

## Goal

Improve image-driven SEO and page performance without weakening accessibility, content relevance, or visual quality.

Use this skill as a closed-loop workflow:

1. Audit the current image inventory and page context.
2. Optimize image files, metadata, markup, and discoverability.
3. Verify the impact with measurable SEO and performance checks.

For detailed checklists and thresholds, read `references/image-seo-reference.md` when the task involves a real website, asset set, or page audit.

## Intake

Collect only the context needed for the task:

- Target pages, repository paths, or exported HTML.
- Image asset paths, CDN URLs, or CMS media records.
- Primary page topic, target keyword intent, and surrounding copy.
- Existing performance data if available: Lighthouse, PageSpeed Insights, WebPageTest, Search Console, server logs, or analytics.
- Constraints: CMS naming rules, CDN transformation rules, maximum acceptable quality loss, legal/brand restrictions, and whether files can be renamed safely.

If renaming live image files may break references, redirects, cache keys, CMS records, or backlinks, treat it as a migration and preserve backwards compatibility.

## Workflow

### 1. Build the image inventory

Create a table or structured list with:

- Source path or URL.
- Page usage and surrounding context.
- Rendered size and intrinsic dimensions.
- File type, byte size, compression status, and color profile if relevant.
- `alt`, `title`, caption, `aria-*`, and nearby heading/body copy.
- Loading behavior: `loading`, `decoding`, `fetchpriority`, preload, CSS background usage.
- Responsive markup: `srcset`, `sizes`, `<picture>`, DPR variants, art direction.
- Indexability signals: robots rules, HTTP status, canonical page, sitemap references, structured data image fields.

Prioritize images by business and performance impact:

1. Largest Contentful Paint image or above-the-fold product/content images.
2. High-traffic landing pages and pages with image search potential.
3. Oversized repeated assets used across templates.
4. Decorative or low-value images that can be simplified, lazy-loaded, or removed.

### 2. Compress and resize images

Optimize for displayed size, not original camera or design export size.

- Resize oversized images to the largest needed rendered size plus reasonable high-DPR variants.
- Prefer modern formats such as AVIF or WebP when browser/CDN support and fallback strategy are acceptable.
- Keep original source assets when the workflow needs non-destructive editing.
- Strip unnecessary metadata unless it is legally, editorially, or operationally required.
- Avoid quality loss that harms product inspection, screenshots, diagrams, charts, or editorial credibility.
- Do not lazy-load the LCP image; prioritize it with appropriate preload or `fetchpriority="high"` when justified.

### 3. Use descriptive filenames

Rename files only when references can be updated safely.

Filename rules:

- Use lowercase ASCII words separated by hyphens.
- Describe the actual subject and page intent.
- Avoid keyword stuffing, tracking IDs, opaque hashes, camera names, and generic names like `image1.jpg`.
- Keep filenames stable enough for caching and content operations.
- Preserve extensions that match the final encoded format.

Example:

```text
Before: IMG_4821.jpg
After: swiftui-navigation-split-view-sidebar-example.webp
```

### 4. Write useful alt text

Alt text must describe the image's function in context, not merely its pixels.

- Use empty alt text (`alt=""`) for decorative images that convey no unique information.
- Describe meaningful images concisely and naturally.
- Include text visible inside an image when that text matters to users.
- Mention product names, UI states, charts, or diagrams when they are important to the page intent.
- Avoid starting with "image of" or "picture of" unless the medium itself matters.
- Avoid keyword stuffing and duplicated boilerplate.
- For linked images, describe the link destination or action.
- For complex charts, diagrams, or screenshots, provide a concise alt and put the detailed explanation in nearby text.

### 5. Improve image markup

Apply markup changes according to how the image is used:

- Use `<img>` for content images that need alt text and indexing.
- Use CSS backgrounds only for decorative images.
- Add `width` and `height` or equivalent aspect-ratio constraints to reduce layout shift.
- Use `srcset` and `sizes` for responsive variants.
- Use `<picture>` for art direction or AVIF/WebP fallback needs.
- Lazy-load below-the-fold images with `loading="lazy"` and keep critical images eager.
- Use `decoding="async"` for non-critical images where it improves rendering behavior.
- Ensure important images are not blocked by robots rules, auth walls, broken redirects, or unstable JavaScript rendering.

### 6. Connect images to SEO signals

When relevant, strengthen image discoverability:

- Add important image URLs to image sitemaps or page sitemaps.
- Ensure structured data image fields use crawlable, representative images.
- Keep Open Graph and Twitter/X card images aligned with the page's primary content.
- Use captions or nearby copy when it helps clarify the image's relevance.
- Confirm canonical pages and image URLs resolve consistently across CDN variants.

### 7. Verify impact

Always compare before and after when enough data is available.

Measure:

- Total transferred image bytes per page.
- Largest Contentful Paint and LCP element identity.
- Cumulative Layout Shift caused by images without dimensions.
- Lighthouse or PageSpeed image audits.
- Broken image URLs and missing/empty inappropriate alt text.
- Google Search Console image indexing and query changes when available.
- Visual quality at common desktop and mobile viewport sizes.

Report both the direct changes and the remaining constraints. If SEO lift cannot be measured immediately, explain the expected lag and define a follow-up measurement window.

## Output Formats

For an audit, return:

- Prioritized findings with page/image references.
- Concrete fixes grouped by file, template, CMS field, or CDN rule.
- A before/after measurement plan.
- Risks such as filename migrations, CDN cache invalidation, or visual quality regressions.

For implementation, make small reviewable changes:

- Update assets and references together.
- Preserve existing naming and build patterns where possible.
- Add or adjust tests only where the repository already has image, markup, accessibility, or performance checks.
- Run available build, lint, accessibility, or page-render checks before claiming completion.

## Guardrails

- Do not invent image subject matter when writing alt text. Use the actual image, surrounding page copy, or user-provided context.
- Do not rename public assets without updating every reference and considering redirects or cache behavior.
- Do not optimize only for file size when visual fidelity is part of conversion, trust, documentation, or product evaluation.
- Do not hide meaningful images in CSS backgrounds if they need alt text or image-search discoverability.
- Do not claim SEO improvement from markup changes alone; verify with performance metrics and, when possible, Search Console data.
