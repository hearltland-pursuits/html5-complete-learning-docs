---
title: Head Element
category: Metadata & SEO
order: 10
---

# Head Element

> **Quick Summary:** The `<head>` element contains metadata about the HTML document—information for browsers and search engines, not visible content. It includes the page title, character encoding, viewport settings, stylesheets, scripts, and SEO metadata.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Required Elements](#required-elements)
- [Common Head Elements](#common-head-elements)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<head>` element is the metadata container for an HTML document. It sits between the `<!DOCTYPE>` declaration and the `<body>` element. Content inside `<head>` is not displayed on the page but provides crucial information to browsers, search engines, and social media platforms.

**Key points:**
- Required in all HTML documents
- Contains metadata, not visible content
- Defines page title, character encoding, viewport settings
- Links to external resources (CSS, JavaScript, fonts)
- Provides SEO and social media metadata

**Key Concept:** The `<head>` element is the control center for page metadata. It tells browsers how to render the page, search engines how to index it, and social platforms how to display it when shared.

---

## Basic Syntax

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Metadata goes here -->
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
</head>
<body>
  <!-- Visible content goes here -->
</body>
</html>
```

---

## Required Elements

### 1. Character Encoding (Required)

**Always specify character encoding first:**
```html
<head>
  <meta charset="UTF-8">
  <!-- Other meta tags -->
</head>
```

**Why it matters:**
- Must appear within first 1024 bytes of document
- Ensures proper text rendering (accents, emojis, international characters)
- UTF-8 supports all languages and special characters

### 2. Title Element (Required)

**Every page must have a title:**
```html
<head>
  <title>Page Title - Site Name</title>
</head>
```

**Why it matters:**
- Displayed in browser tabs
- Used by search engines (appears in search results)
- Screen readers announce it when page loads
- Bookmarks use the title
- 50-60 characters ideal for SEO

### 3. Viewport Meta Tag (Highly Recommended)

**Required for responsive design:**
```html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

**Why it matters:**
- Makes site mobile-friendly
- Controls layout on mobile devices
- Google requires it for mobile-first indexing

---

## Common Head Elements

### Complete Head Example

```html
<head>
  <!-- 1. Character encoding (FIRST) -->
  <meta charset="UTF-8">

  <!-- 2. Viewport (responsive design) -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 3. Page title (SEO critical) -->
  <title>Complete Guide to HTML Head Element | Your Site</title>

  <!-- 4. Meta description (SEO) -->
  <meta name="description" content="Learn how to properly structure the HTML head element for SEO, accessibility, and performance. Includes examples and best practices.">

  <!-- 5. Meta keywords (mostly deprecated, but harmless) -->
  <meta name="keywords" content="HTML, head element, metadata, SEO">

  <!-- 6. Author and copyright -->
  <meta name="author" content="Joshua P. Hickman">
  <meta name="copyright" content="© 2025 Your Company">

  <!-- 7. Favicon -->
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">

  <!-- 8. Stylesheets -->
  <link rel="stylesheet" href="/css/styles.css">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap">

  <!-- 9. Open Graph (Facebook/social media) -->
  <meta property="og:title" content="Complete Guide to HTML Head Element">
  <meta property="og:description" content="Learn how to properly structure the HTML head element.">
  <meta property="og:image" content="https://example.com/og-image.jpg">
  <meta property="og:url" content="https://example.com/head-element">
  <meta property="og:type" content="article">

  <!-- 10. Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Complete Guide to HTML Head Element">
  <meta name="twitter:description" content="Learn how to properly structure the HTML head element.">
  <meta name="twitter:image" content="https://example.com/twitter-image.jpg">

  <!-- 11. Canonical URL (avoid duplicate content) -->
  <link rel="canonical" href="https://example.com/head-element">

  <!-- 12. Language and regional settings -->
  <link rel="alternate" hreflang="es" href="https://example.com/es/head-element">

  <!-- 13. RSS/Atom feed -->
  <link rel="alternate" type="application/rss+xml" title="RSS Feed" href="/feed.xml">

  <!-- 14. Scripts (prefer at end of body, but some go in head) -->
  <script src="/js/analytics.js" defer></script>

  <!-- 15. Preload critical resources -->
  <link rel="preload" href="/fonts/main-font.woff2" as="font" type="font/woff2" crossorigin>
</head>
```

---

## Examples

### Example 1: Minimal Blog Post Head

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>10 Tips for Better HTML | Web Dev Blog</title>
  <meta name="description" content="Discover 10 practical tips to improve your HTML code quality, accessibility, and SEO performance.">

  <link rel="icon" href="/favicon.ico">
  <link rel="stylesheet" href="/css/blog.css">

  <meta property="og:title" content="10 Tips for Better HTML">
  <meta property="og:description" content="Practical tips to improve your HTML code.">
  <meta property="og:image" content="https://blog.example.com/images/html-tips.jpg">
  <meta property="og:type" content="article">

  <link rel="canonical" href="https://blog.example.com/10-html-tips">
</head>
<body>
  <!-- Blog content -->
</body>
</html>
```

### Example 2: E-Commerce Product Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Wireless Headphones - $99.99 | Electronics Store</title>
  <meta name="description" content="Premium wireless headphones with noise cancellation. 30-hour battery, Bluetooth 5.0. Free shipping on orders over $50.">

  <!-- Favicon -->
  <link rel="icon" href="/favicon.ico">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">

  <!-- Stylesheets -->
  <link rel="stylesheet" href="/css/product.css">

  <!-- Open Graph (shows product in social shares) -->
  <meta property="og:type" content="product">
  <meta property="og:title" content="Wireless Headphones">
  <meta property="og:description" content="Premium wireless headphones with noise cancellation.">
  <meta property="og:image" content="https://store.example.com/images/headphones.jpg">
  <meta property="og:url" content="https://store.example.com/products/wireless-headphones">
  <meta property="product:price:amount" content="99.99">
  <meta property="product:price:currency" content="USD">

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Wireless Headphones - $99.99">
  <meta name="twitter:description" content="Premium wireless headphones with noise cancellation.">
  <meta name="twitter:image" content="https://store.example.com/images/headphones-twitter.jpg">

  <!-- Canonical URL -->
  <link rel="canonical" href="https://store.example.com/products/wireless-headphones">

  <!-- Structured data (JSON-LD for rich snippets) -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org/",
    "@type": "Product",
    "name": "Wireless Headphones",
    "image": "https://store.example.com/images/headphones.jpg",
    "description": "Premium wireless headphones with noise cancellation.",
    "brand": {
      "@type": "Brand",
      "name": "TechBrand"
    },
    "offers": {
      "@type": "Offer",
      "price": "99.99",
      "priceCurrency": "USD",
      "availability": "https://schema.org/InStock"
    }
  }
  </script>
</head>
<body>
  <!-- Product page content -->
</body>
</html>
```

### Example 3: Performance-Optimized Landing Page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Get Started with Our Service | Free Trial</title>
  <meta name="description" content="Start your free 14-day trial. No credit card required. Join 10,000+ happy customers.">

  <!-- DNS prefetch for external domains -->
  <link rel="dns-prefetch" href="https://fonts.googleapis.com">
  <link rel="dns-prefetch" href="https://cdn.example.com">

  <!-- Preconnect to critical domains -->
  <link rel="preconnect" href="https://fonts.googleapis.com" crossorigin>

  <!-- Preload critical resources -->
  <link rel="preload" href="/fonts/main-font.woff2" as="font" type="font/woff2" crossorigin>
  <link rel="preload" href="/css/critical.css" as="style">

  <!-- Critical CSS inlined -->
  <style>
    /* Critical above-the-fold CSS */
    body { margin: 0; font-family: Arial, sans-serif; }
    .hero { min-height: 100vh; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
  </style>

  <!-- Non-critical CSS deferred -->
  <link rel="stylesheet" href="/css/styles.css" media="print" onload="this.media='all'">

  <!-- Favicon -->
  <link rel="icon" href="/favicon.ico">

  <!-- Open Graph -->
  <meta property="og:title" content="Get Started with Our Service">
  <meta property="og:description" content="Start your free 14-day trial.">
  <meta property="og:image" content="https://service.example.com/og-image.jpg">

  <!-- Canonical -->
  <link rel="canonical" href="https://service.example.com/get-started">

  <!-- Analytics (defer to avoid blocking) -->
  <script src="/js/analytics.js" defer></script>
</head>
<body>
  <!-- Landing page content -->
</body>
</html>
```

---

## Best Practices

### Do This

1. **Order Matters - Put Charset First**
   ```html
   <head>
     <!-- ALWAYS first -->
     <meta charset="UTF-8">

     <!-- Then viewport -->
     <meta name="viewport" content="width=device-width, initial-scale=1.0">

     <!-- Then title -->
     <title>Page Title</title>
   </head>
   ```

2. **Use Descriptive Titles**
   ```html
   <!-- GOOD: Descriptive, includes branding -->
   <title>Wireless Headphones - $99.99 | Electronics Store</title>

   <!-- BAD: Generic, no context -->
   <title>Product</title>
   ```

3. **Include Meta Description**
   ```html
   <!-- 150-160 characters for SEO -->
   <meta name="description" content="Premium wireless headphones with noise cancellation. 30-hour battery, Bluetooth 5.0. Free shipping on orders over $50.">
   ```

4. **Use Defer or Async for Scripts**
   ```html
   <!-- Good: Scripts don't block rendering -->
   <script src="/js/app.js" defer></script>
   <script src="/js/analytics.js" async></script>
   ```

5. **Preload Critical Resources**
   ```html
   <!-- Fonts load faster -->
   <link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>

   <!-- Critical CSS loads faster -->
   <link rel="preload" href="/css/critical.css" as="style">
   ```

### Avoid This

1. **Don't Put Visible Content in Head**
   ```html
   <!-- WRONG: Visible content belongs in body -->
   <head>
     <h1>Welcome to My Site</h1>
   </head>

   <!-- CORRECT -->
   <head>
     <title>Welcome to My Site</title>
   </head>
   <body>
     <h1>Welcome to My Site</h1>
   </body>
   ```

2. **Don't Forget Viewport Meta Tag**
   ```html
   <!-- WRONG: Not mobile-friendly -->
   <head>
     <title>My Site</title>
   </head>

   <!-- CORRECT: Mobile-friendly -->
   <head>
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>My Site</title>
   </head>
   ```

3. **Don't Use Excessive Meta Keywords**
   ```html
   <!-- WRONG: Keyword stuffing (ignored by search engines) -->
   <meta name="keywords" content="html, html5, html tutorial, learn html, html guide, html course, html lessons, html tips, html tricks, html examples">

   <!-- CORRECT: Concise or omit entirely -->
   <meta name="keywords" content="HTML, web development, tutorial">
   ```

---

## Quick Reference

### Essential Head Elements (Every Page Needs)

```html
<head>
  <!-- 1. Character encoding (required, first) -->
  <meta charset="UTF-8">

  <!-- 2. Viewport (responsive design) -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 3. Title (required, 50-60 chars for SEO) -->
  <title>Page Title | Site Name</title>

  <!-- 4. Meta description (SEO, 150-160 chars) -->
  <meta name="description" content="Page description for search engines.">

  <!-- 5. Favicon -->
  <link rel="icon" href="/favicon.ico">

  <!-- 6. Stylesheet -->
  <link rel="stylesheet" href="/css/styles.css">
</head>
```

### Head Elements by Category

| Category | Elements |
|----------|----------|
| **Required** | `<meta charset>`, `<title>` |
| **Responsive** | `<meta name="viewport">` |
| **SEO** | `<meta name="description">`, `<link rel="canonical">` |
| **Social Media** | Open Graph tags, Twitter Cards |
| **Resources** | `<link rel="stylesheet">`, `<script>` |
| **Icons** | `<link rel="icon">`, `<link rel="apple-touch-icon">` |
| **Performance** | `<link rel="preload">`, `<link rel="dns-prefetch">` |

---

## Browser Support

All `<head>` elements are supported in all browsers. Specific child elements may have varying support:

| Element/Attribute | Chrome | Firefox | Safari | Edge |
|-------------------|--------|---------|--------|------|
| `<head>` | ✅ All | ✅ All | ✅ All | ✅ All |
| `<meta charset>` | ✅ All | ✅ All | ✅ All | ✅ All |
| `<meta viewport>` | ✅ All | ✅ All | ✅ All | ✅ All |
| Open Graph | ✅ All | ✅ All | ✅ All | ✅ All |
| `rel="preload"` | ✅ 50+ | ✅ 56+ | ✅ 11.1+ | ✅ 79+ |

---

## Related Topics
- [Meta Tags](meta-tags.md)
- [Title Element](title-tag.md)
- [Open Graph Protocol](open-graph.md)
- [Favicon Implementation](favicon.md)
- [Link Relations](link-relations.md)

---

**Last Updated:** November 17, 2025
**Category:** Metadata & SEO
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
