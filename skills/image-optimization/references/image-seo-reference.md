# Image SEO Reference

Use this reference when auditing or implementing real image optimization work.

## Optimization Areas

### Performance

- Resize images to fit real layout needs.
- Generate responsive variants for common viewport and DPR ranges.
- Prefer AVIF for maximum compression when quality and support are acceptable.
- Prefer WebP when AVIF is unavailable or visual output is better.
- Keep PNG for images needing sharp transparency or lossless UI details.
- Keep SVG for simple vector artwork and icons when safe and appropriate.
- Compress JPEG/WebP/AVIF with visual review, not byte targets alone.
- Remove unnecessary metadata.
- Use CDN transformations when they are reliable, cacheable, and deterministic.
- Avoid serving the same large image to all breakpoints.

### LCP and Loading

- Identify the actual LCP element before changing loading behavior.
- Do not set `loading="lazy"` on the LCP image.
- Use `fetchpriority="high"` only for the primary critical image.
- Preload the LCP image when the browser would otherwise discover it late.
- Add `width` and `height` or CSS `aspect-ratio` to prevent layout shift.
- Lazy-load below-the-fold images.
- Avoid excessive preloads that compete with CSS, fonts, scripts, or the real LCP image.

### Filenames

Good filenames:

- Are short, descriptive, and human-readable.
- Use lowercase ASCII and hyphens.
- Reflect the image subject and page context.
- Avoid repeated target keywords.
- Avoid opaque upload names, timestamps, and camera filenames.

Use this pattern:

```text
<subject>-<specific-context>-<optional-state-or-location>.<extension>
```

Examples:

```text
product-dashboard-keyword-clustering-report.webp
ios-app-store-review-rating-screenshot.webp
technical-seo-audit-core-web-vitals-chart.png
```

### Alt Text

Decision rules:

- Decorative image: use `alt=""`.
- Informative image: describe the information needed to understand the page.
- Functional linked image: describe the action or destination.
- Product image: include product identity and distinguishing visible attributes.
- Screenshot: describe the UI state or workflow shown.
- Chart or diagram: summarize the insight, then rely on nearby text for detail.
- Image containing important text: include the text or an equivalent nearby text alternative.

Avoid:

- Keyword stuffing.
- Repeating adjacent captions word-for-word.
- Generic phrases like `SEO image`, `banner`, or `screenshot`.
- Describing visual style when the page intent needs functional information.

### Markup

Content image:

```html
<img
  src="/images/technical-seo-audit-dashboard.webp"
  srcset="/images/technical-seo-audit-dashboard-640.webp 640w, /images/technical-seo-audit-dashboard-1280.webp 1280w"
  sizes="(max-width: 768px) 100vw, 768px"
  width="1280"
  height="720"
  alt="Technical SEO audit dashboard showing Core Web Vitals and index coverage trends"
  loading="lazy"
  decoding="async"
>
```

Critical LCP image:

```html
<img
  src="/images/seo-pilot-keyword-map-hero.webp"
  width="1440"
  height="810"
  alt="SEO Pilot keyword map showing grouped search intents for a content plan"
  fetchpriority="high"
>
```

Art direction:

```html
<picture>
  <source media="(max-width: 640px)" srcset="/images/site-audit-mobile.webp">
  <source media="(min-width: 641px)" srcset="/images/site-audit-desktop.webp">
  <img
    src="/images/site-audit-desktop.webp"
    width="1280"
    height="720"
    alt="Site audit report comparing crawl errors, index coverage, and page speed"
  >
</picture>
```

## Audit Checklist

### Asset Checks

- File size is appropriate for the rendered role.
- Intrinsic dimensions are not far larger than rendered dimensions.
- Format matches content type and browser support.
- Compression has been visually reviewed.
- EXIF or metadata retention is intentional.
- CDN transformations produce stable URLs and cache keys.

### Accessibility Checks

- Meaningful images have useful alt text.
- Decorative images have empty alt text.
- Linked images describe the destination or action.
- Complex images have nearby detailed explanation.
- Text embedded in images has an accessible equivalent.

### SEO Checks

- Important images use descriptive filenames.
- Important images are crawlable and not blocked.
- Image URLs return successful status codes.
- Canonical pages and image URLs are stable.
- Structured data image fields are accurate and crawlable.
- Relevant image URLs are included in sitemaps when useful.
- Captions and surrounding text support the same page intent.

### Performance Checks

- LCP image is correctly prioritized.
- Below-the-fold images are lazy-loaded.
- `srcset` and `sizes` prevent over-serving.
- Image dimensions prevent layout shift.
- Page image transfer size decreased after optimization.
- Lighthouse, PageSpeed Insights, or equivalent checks show no new regressions.

## Measurement Plan

Before optimization:

1. Record target URL, test date, viewport, network profile, and tool.
2. Capture total image bytes, LCP, CLS, Speed Index, and any image audit failures.
3. Record current image filenames, alt text, and markup issues.
4. Export Search Console image performance if available.

After optimization:

1. Re-run the same performance tests under comparable conditions.
2. Confirm no broken image references or visual regressions.
3. Confirm important images remain crawlable.
4. Track Search Console image search changes after indexing delay.
5. Document unresolved issues and follow-up date.

## Common Risk Patterns

- Renaming public assets without redirects or reference updates.
- Lazy-loading the hero image and worsening LCP.
- Compressing diagrams until labels become unreadable.
- Using CSS backgrounds for meaningful content images.
- Generating generic alt text without checking page context.
- Creating many responsive variants without a build or CDN strategy.
- Optimizing one page while shared template images remain oversized.
