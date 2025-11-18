---
title: HTML Performance Optimization
category: Modern HTML5
order: 1
---

# HTML Performance Optimization

> **Quick Summary:** Optimizing HTML performance through lazy loading, resource hints, efficient structure, and minimal DOM depth improves page load speed, Core Web Vitals, and user experience.

## Why Performance Matters

- **User Experience:** 53% of users abandon sites that take >3 seconds to load
- **SEO:** Google ranks faster sites higher
- **Conversions:** Amazon found 100ms delay = 1% revenue loss
- **Accessibility:** Slow sites hurt users on slow connections/devices

---

## Core Web Vitals

### 1. Largest Contentful Paint (LCP)
**Target:** < 2.5 seconds

```html
<!-- ✅ Optimize LCP -->
<img src="hero.jpg" fetchpriority="high" alt="Hero image">

<!-- Preload critical images -->
<link rel="preload" as="image" href="hero.jpg">
```

### 2. First Input Delay (FID)
**Target:** < 100ms

```html
<!-- ✅ Defer non-critical JS -->
<script src="analytics.js" defer></script>
```

### 3. Cumulative Layout Shift (CLS)
**Target:** < 0.1

```html
<!-- ✅ Specify dimensions to prevent layout shift -->
<img src="photo.jpg" width="800" height="600" alt="Photo">

<iframe src="video.html" width="560" height="315"></iframe>
```

---

## Resource Loading

### Lazy Loading

```html
<!-- Images -->
<img src="image.jpg" loading="lazy" alt="Lazy loaded image">

<!-- Iframes -->
<iframe src="video.html" loading="lazy"></iframe>
```

**Benefit:** Loads only when near viewport, saving bandwidth.

### Resource Hints

```html
<!-- DNS Prefetch - Resolve DNS early -->
<link rel="dns-prefetch" href="//fonts.googleapis.com">

<!-- Preconnect - Establish connection early -->
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Prefetch - Load for next page navigation -->
<link rel="prefetch" href="/next-page.html">

<!-- Preload - High priority current page resource -->
<link rel="preload" href="critical.css" as="style">
<link rel="preload" href="hero.jpg" as="image">
```

### Script Loading Strategies

```html
<!-- ❌ BAD - Blocks parsing -->
<script src="app.js"></script>

<!-- ✅ GOOD - Async (doesn't block, no execution order) -->
<script src="analytics.js" async></script>

<!-- ✅ GOOD - Defer (doesn't block, preserves order) -->
<script src="app.js" defer></script>

<!-- ✅ GOOD - Module (always deferred) -->
<script type="module" src="app.mjs"></script>
```

---

## HTML Structure Optimization

### Minimize DOM Depth

```html
<!-- ❌ BAD - Deep nesting (10 levels) -->
<div><div><div><div><div><div><div><div><div><div>
  Content
</div></div></div></div></div></div></div></div></div></div>

<!-- ✅ GOOD - Shallow (3 levels) -->
<article>
  <header><h1>Title</h1></header>
  <p>Content</p>
</article>
```

**Why:** Deep DOM = slower rendering and memory usage.

### Minimize DOM Nodes

**Target:** <1,500 nodes per page

```html
<!-- ❌ BAD - Excessive wrapper divs -->
<div class="outer">
  <div class="inner">
    <div class="wrapper">
      <div class="container">
        <p>Content</p>
      </div>
    </div>
  </div>
</div>

<!-- ✅ GOOD - Minimal markup -->
<p>Content</p>
```

---

## Image Optimization

### Responsive Images

```html
<picture>
  <source media="(min-width: 1024px)" srcset="large.webp" type="image/webp">
  <source media="(min-width: 768px)" srcset="medium.webp" type="image/webp">
  <source media="(min-width: 1024px)" srcset="large.jpg">
  <source media="(min-width: 768px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Responsive image" loading="lazy">
</picture>
```

### Modern Image Formats

```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Optimized image">
</picture>
```

**File Size Comparison:**
- JPEG: 100KB
- WebP: 70KB (30% smaller)
- AVIF: 50KB (50% smaller)

---

## Critical Rendering Path

### Inline Critical CSS

```html
<head>
  <style>
    /* Critical above-the-fold CSS */
    body { margin: 0; font-family: sans-serif; }
    .hero { height: 400px; background: #333; }
  </style>

  <!-- Load full CSS asynchronously -->
  <link rel="preload" href="styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
  <noscript><link rel="stylesheet" href="styles.css"></noscript>
</head>
```

### Font Loading

```html
<!-- Preload critical fonts -->
<link rel="preload" href="fonts/main.woff2" as="font" type="font/woff2" crossorigin>

<!-- Use font-display -->
<style>
@font-face {
  font-family: 'CustomFont';
  src: url('font.woff2') format('woff2');
  font-display: swap; /* Show fallback immediately */
}
</style>
```

---

## Best Practices

### 1. Prioritize Above-the-Fold Content

```html
<!-- High priority hero image -->
<img src="hero.jpg" fetchpriority="high" alt="Hero">

<!-- Low priority footer image -->
<img src="footer.jpg" loading="lazy" fetchpriority="low" alt="Footer">
```

### 2. Avoid Render-Blocking Resources

```html
<!-- ✅ Non-blocking CSS -->
<link rel="stylesheet" href="styles.css" media="print" onload="this.media='all'">
```

### 3. Use Native HTML Where Possible

```html
<!-- ✅ Native details/summary (no JS needed) -->
<details>
  <summary>FAQ Question</summary>
  <p>Answer text...</p>
</details>

<!-- ❌ JS-heavy accordion -->
<div class="accordion" data-accordion-init>...</div>
```

---

## Performance Testing Tools

- **Lighthouse:** Chrome DevTools → Lighthouse tab
- **PageSpeed Insights:** https://pagespeed.web.dev/
- **WebPageTest:** https://www.webpagetest.org/
- **Chrome DevTools:** Network tab, Performance tab

---

## Related Topics

- [Lazy Loading](../04-media-elements/lazy-loading.md)
- [Progressive Enhancement](progressive-enhancement.md)
- [Mobile-First HTML](mobile-first-html.md)

---

**Last Updated:** November 18, 2025
**Category:** Modern HTML5
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
