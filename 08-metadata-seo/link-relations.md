---
title: Link Relations
category: Metadata & SEO
order: 16
---

# Link Relations

> **Quick Summary:** Link relations (`rel` attribute) define the relationship between the current document and linked resources. They control SEO (canonical URLs), performance (preload, prefetch), and resource types (stylesheet, icon, alternate). Critical for SEO, page speed, and multi-language sites.

## Table of Contents
- [Introduction](#introduction)
- [SEO Link Relations](#seo-link-relations)
- [Resource Link Relations](#resource-link-relations)
- [Performance Link Relations](#performance-link-relations)
- [Alternative Versions](#alternative-versions)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `rel` (relationship) attribute in `<link>` elements defines how the linked resource relates to the current document. It tells browsers, search engines, and other tools what to do with the linked resource.

**Common use cases:**
- **SEO:** Canonical URLs, alternate languages
- **Performance:** Preload critical resources, prefetch next pages
- **Resources:** Stylesheets, icons, feeds
- **Navigation:** Previous/next pages, help pages

**Syntax:**
```html
<link rel="relationship-type" href="URL">
```

**Key Concept:** Link relations are instructions to browsers and search engines: "Here's a resource, and here's how you should handle it." They optimize SEO, performance, and user experience.

---

## SEO Link Relations

### 1. Canonical (Prevent Duplicate Content)

**Tells search engines the preferred version of a page:**
```html
<!-- Current page: https://example.com/product?color=red&size=large -->
<link rel="canonical" href="https://example.com/product">
```

**Use cases:**
- **E-commerce:** Product with multiple URL parameters
  ```html
  <!-- All these URLs point to same canonical -->
  <!-- /product?color=red -->
  <!-- /product?size=large -->
  <!-- /product?utm_source=facebook -->
  <link rel="canonical" href="https://example.com/product">
  ```

- **Paginated content:** Multi-page articles
  ```html
  <!-- Page 2 of article -->
  <link rel="canonical" href="https://example.com/article">
  ```

- **HTTP vs HTTPS:** Prefer HTTPS version
  ```html
  <!-- On http://example.com/page -->
  <link rel="canonical" href="https://example.com/page">
  ```

**Why it matters:**
- Prevents duplicate content penalties
- Consolidates ranking signals to preferred URL
- Google uses this as a strong hint (not absolute directive)

---

### 2. Alternate (Language/Device Versions)

**Points to alternative versions of the page:**

**Alternate language:**
```html
<!-- Current page: English -->
<link rel="alternate" hreflang="es" href="https://example.com/es/page">
<link rel="alternate" hreflang="fr" href="https://example.com/fr/page">
<link rel="alternate" hreflang="de" href="https://example.com/de/page">

<!-- Self-referential (current page) -->
<link rel="alternate" hreflang="en" href="https://example.com/page">
```

**Alternate for mobile:**
```html
<!-- Desktop version points to mobile -->
<link rel="alternate" media="only screen and (max-width: 640px)" href="https://m.example.com/page">
```

**Alternate RSS feed:**
```html
<link rel="alternate" type="application/rss+xml" title="RSS Feed" href="/feed.xml">
```

---

### 3. Prev / Next (Paginated Content)

**For multi-page articles or galleries:**
```html
<!-- Page 2 of 5 -->
<link rel="prev" href="https://example.com/article?page=1">
<link rel="next" href="https://example.com/article?page=3">
```

**Benefits:**
- Helps search engines understand pagination
- Improves user experience (preloading next page)
- Consolidates SEO value across paginated series

---

### 4. Author / License

**Links to author info or license:**
```html
<!-- Author's profile page -->
<link rel="author" href="https://example.com/author/joshua">

<!-- Content license -->
<link rel="license" href="https://creativecommons.org/licenses/by/4.0/">
```

---

## Resource Link Relations

### 1. Stylesheet (CSS)

**Links to external CSS:**
```html
<link rel="stylesheet" href="/css/styles.css">

<!-- With media query -->
<link rel="stylesheet" href="/css/print.css" media="print">
```

---

### 2. Icon (Favicon)

**Covered in detail in [favicon.md](favicon.md):**
```html
<link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
<link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
```

---

### 3. Manifest (Web App)

**Links to web app manifest:**
```html
<link rel="manifest" href="/site.webmanifest">
```

---

## Performance Link Relations

### 1. Preload (Critical Resources)

**Loads resources ASAP (before parser discovers them):**
```html
<!-- Preload critical font -->
<link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>

<!-- Preload critical CSS -->
<link rel="preload" href="/css/critical.css" as="style">

<!-- Preload hero image -->
<link rel="preload" href="/images/hero.jpg" as="image">

<!-- Preload critical script -->
<link rel="preload" href="/js/app.js" as="script">
```

**Required attributes:**
- `as`: Resource type (font, style, script, image, fetch, video, audio)
- `crossorigin`: Required for fonts (CORS)

**When to use:**
- Critical fonts (visible in first 3 seconds)
- Above-the-fold images
- Critical CSS/JS not in `<head>`

**When NOT to use:**
- Non-critical resources (slows down critical ones)
- Resources already in `<head>` (parser finds them anyway)

---

### 2. Prefetch (Future Navigation)

**Loads resources for NEXT page (low priority):**
```html
<!-- User likely to visit this page next -->
<link rel="prefetch" href="/products/popular-item.html">

<!-- Prefetch next page's image -->
<link rel="prefetch" href="/images/next-page-hero.jpg" as="image">
```

**Difference from preload:**
- **Preload:** Current page, high priority
- **Prefetch:** Future page, low priority

**Use cases:**
- Next page in multi-step form
- Likely navigation paths (e.g., product detail from category page)

---

### 3. Preconnect (DNS + Handshake)

**Establishes early connection to third-party domains:**
```html
<!-- Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Analytics -->
<link rel="preconnect" href="https://www.google-analytics.com">

<!-- CDN -->
<link rel="preconnect" href="https://cdn.example.com">
```

**What it does:**
1. DNS lookup
2. TCP handshake
3. TLS negotiation (if HTTPS)

**Performance gain:** 100-500ms saved on first request

**When to use:**
- Critical third-party domains (fonts, analytics, CDN)
- Maximum 3-4 domains (browser limit)

---

### 4. DNS Prefetch (DNS Only)

**Only does DNS lookup (lighter than preconnect):**
```html
<link rel="dns-prefetch" href="https://example.com">
```

**When to use:**
- Many third-party domains (more than 3-4)
- Lower-priority third-party resources

---

### 5. Prerender (Full Page Preload)

**⚠️ Deprecated in Chrome (use Speculation Rules API instead)**
```html
<!-- Old way (deprecated) -->
<link rel="prerender" href="/next-page.html">
```

**Modern way (Chrome 108+):**
```html
<script type="speculationrules">
{
  "prerender": [
    {
      "source": "list",
      "urls": ["/next-page.html"]
    }
  ]
}
</script>
```

---

## Alternative Versions

### Multi-Language Sites (Hreflang)

**Complete example for multi-language site:**
```html
<head>
  <!-- English (current page) -->
  <link rel="alternate" hreflang="en" href="https://example.com/page">

  <!-- Spanish -->
  <link rel="alternate" hreflang="es" href="https://example.com/es/page">

  <!-- French -->
  <link rel="alternate" hreflang="fr" href="https://example.com/fr/page">

  <!-- German -->
  <link rel="alternate" hreflang="de" href="https://example.com/de/page">

  <!-- Default for unmatched languages -->
  <link rel="alternate" hreflang="x-default" href="https://example.com/page">
</head>
```

**Regional variants:**
```html
<!-- Spanish (Spain) -->
<link rel="alternate" hreflang="es-ES" href="https://example.com/es/page">

<!-- Spanish (Mexico) -->
<link rel="alternate" hreflang="es-MX" href="https://example.com/mx/page">

<!-- English (US) -->
<link rel="alternate" hreflang="en-US" href="https://example.com/page">

<!-- English (UK) -->
<link rel="alternate" hreflang="en-GB" href="https://example.com/uk/page">
```

---

### RSS / Atom Feeds

```html
<!-- RSS feed -->
<link rel="alternate" type="application/rss+xml" title="Blog RSS Feed" href="/feed.xml">

<!-- Atom feed -->
<link rel="alternate" type="application/atom+xml" title="Blog Atom Feed" href="/atom.xml">
```

---

### AMP (Accelerated Mobile Pages)

```html
<!-- Standard page points to AMP version -->
<link rel="amphtml" href="https://example.com/amp/article">

<!-- AMP page points back to canonical -->
<link rel="canonical" href="https://example.com/article">
```

---

## Examples

### Example 1: Blog Post with SEO

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>10 SEO Strategies for 2025 | Marketing Blog</title>

  <!-- Canonical URL (no parameters) -->
  <link rel="canonical" href="https://blog.example.com/seo-strategies">

  <!-- Alternate languages -->
  <link rel="alternate" hreflang="en" href="https://blog.example.com/seo-strategies">
  <link rel="alternate" hreflang="es" href="https://blog.example.com/es/estrategias-seo">

  <!-- RSS feed -->
  <link rel="alternate" type="application/rss+xml" title="Blog RSS" href="/feed.xml">

  <!-- Author -->
  <link rel="author" href="https://blog.example.com/author/joshua">

  <!-- Stylesheet -->
  <link rel="stylesheet" href="/css/blog.css">

  <!-- Favicon -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
</head>
<body>
  <!-- Article content -->
</body>
</html>
```

---

### Example 2: E-Commerce Product with Performance

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Wireless Headphones - $99.99 | TechStore</title>

  <!-- Canonical (ignore URL parameters) -->
  <link rel="canonical" href="https://store.example.com/products/wireless-headphones">

  <!-- Preconnect to critical domains -->
  <link rel="preconnect" href="https://cdn.shopify.com">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

  <!-- Preload critical resources -->
  <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
  <link rel="preload" href="/images/headphones-hero.jpg" as="image">

  <!-- Prefetch likely next page -->
  <link rel="prefetch" href="/cart">

  <!-- Stylesheet -->
  <link rel="stylesheet" href="/css/product.css">

  <!-- Favicon -->
  <link rel="icon" href="/favicon.ico">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
</head>
<body>
  <!-- Product page content -->
</body>
</html>
```

---

### Example 3: Multi-Page Article (Pagination)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Page 2 of 5 -->
  <title>Complete HTML5 Guide - Page 2 of 5 | Web Dev Tutorials</title>

  <!-- Canonical points to page 1 (view-all not available) -->
  <link rel="canonical" href="https://example.com/html-guide">

  <!-- Pagination -->
  <link rel="prev" href="https://example.com/html-guide?page=1">
  <link rel="next" href="https://example.com/html-guide?page=3">

  <!-- Prefetch next page for smooth navigation -->
  <link rel="prefetch" href="https://example.com/html-guide?page=3">

  <link rel="stylesheet" href="/css/article.css">
</head>
<body>
  <!-- Article content - page 2 -->
</body>
</html>
```

---

### Example 4: Performance-Optimized Landing Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Get Started - Free Trial | SaaS Platform</title>

  <!-- Preconnect to critical third-party domains -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://www.google-analytics.com">

  <!-- DNS prefetch for lower-priority domains -->
  <link rel="dns-prefetch" href="https://cdn.example.com">
  <link rel="dns-prefetch" href="https://api.example.com">

  <!-- Preload critical resources -->
  <link rel="preload" href="/fonts/heading.woff2" as="font" type="font/woff2" crossorigin>
  <link rel="preload" href="/css/critical.css" as="style">
  <link rel="preload" href="/images/hero.webp" as="image">

  <!-- Stylesheets -->
  <link rel="stylesheet" href="/css/critical.css">
  <link rel="stylesheet" href="/css/styles.css" media="print" onload="this.media='all'">

  <!-- Prefetch likely next step (signup page) -->
  <link rel="prefetch" href="/signup">

  <!-- Favicon -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
  <link rel="manifest" href="/site.webmanifest">
</head>
<body>
  <!-- Landing page content -->
</body>
</html>
```

---

## Best Practices

### Do This

1. **Always Use Canonical on E-Commerce Products**
   ```html
   <!-- Product URL with tracking parameters -->
   <!-- /product?color=red&utm_source=facebook -->
   <link rel="canonical" href="https://store.com/product">
   ```

2. **Preconnect to Critical Third-Party Domains**
   ```html
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
   ```

3. **Preload Critical Fonts**
   ```html
   <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
   ```

4. **Use Hreflang for Multi-Language Sites**
   ```html
   <link rel="alternate" hreflang="en" href="https://example.com/page">
   <link rel="alternate" hreflang="es" href="https://example.com/es/page">
   <link rel="alternate" hreflang="x-default" href="https://example.com/page">
   ```

### Avoid This

1. **Don't Preload Everything**
   ```html
   <!-- WRONG: Too many preloads slow down critical resources -->
   <link rel="preload" href="/fonts/font1.woff2" as="font" crossorigin>
   <link rel="preload" href="/fonts/font2.woff2" as="font" crossorigin>
   <link rel="preload" href="/fonts/font3.woff2" as="font" crossorigin>
   <link rel="preload" href="/images/img1.jpg" as="image">
   <link rel="preload" href="/images/img2.jpg" as="image">

   <!-- CORRECT: Only preload critical resources -->
   <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
   <link rel="preload" href="/images/hero.jpg" as="image">
   ```

2. **Don't Forget `as` Attribute on Preload**
   ```html
   <!-- WRONG: Missing 'as' attribute -->
   <link rel="preload" href="/fonts/main.woff2">

   <!-- CORRECT -->
   <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
   ```

3. **Don't Preconnect to Too Many Domains**
   ```html
   <!-- WRONG: Too many (browser limits to 6, wastes resources) -->
   <link rel="preconnect" href="https://domain1.com">
   <link rel="preconnect" href="https://domain2.com">
   <link rel="preconnect" href="https://domain3.com">
   <link rel="preconnect" href="https://domain4.com">
   <link rel="preconnect" href="https://domain5.com">

   <!-- CORRECT: Only critical domains, use dns-prefetch for rest -->
   <link rel="preconnect" href="https://fonts.googleapis.com">
   <link rel="dns-prefetch" href="https://analytics.com">
   <link rel="dns-prefetch" href="https://cdn.example.com">
   ```

---

## Quick Reference

### SEO Link Relations

| Relation | Purpose | Example |
|----------|---------|---------|
| `canonical` | Preferred URL (avoid duplicates) | `<link rel="canonical" href="/page">` |
| `alternate` | Alternative version (language, mobile, feed) | `<link rel="alternate" hreflang="es" href="/es/page">` |
| `prev` / `next` | Pagination | `<link rel="next" href="/page2">` |
| `author` | Author profile | `<link rel="author" href="/author/name">` |

### Performance Link Relations

| Relation | Purpose | Priority | Example |
|----------|---------|----------|---------|
| `preload` | Load critical resource NOW | High | `<link rel="preload" href="/font.woff2" as="font">` |
| `prefetch` | Load for NEXT page | Low | `<link rel="prefetch" href="/next-page">` |
| `preconnect` | Early connection (DNS + TCP + TLS) | High | `<link rel="preconnect" href="https://fonts.com">` |
| `dns-prefetch` | DNS lookup only | Low | `<link rel="dns-prefetch" href="https://cdn.com">` |

---

## Browser Support

| Relation | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `canonical` | ✅ All | ✅ All | ✅ All | ✅ All |
| `alternate` | ✅ All | ✅ All | ✅ All | ✅ All |
| `preload` | ✅ 50+ | ✅ 56+ | ✅ 11.1+ | ✅ 79+ |
| `prefetch` | ✅ All | ✅ All | ✅ All | ✅ All |
| `preconnect` | ✅ 46+ | ✅ 39+ | ✅ 11.1+ | ✅ 79+ |
| `dns-prefetch` | ✅ All | ✅ All | ✅ 5+ | ✅ All |

---

## Related Topics
- [Head Element](head-element.md)
- [Meta Tags](meta-tags.md)
- [Favicon Implementation](favicon.md)

---

**Last Updated:** November 17, 2025
**Category:** Metadata & SEO
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
