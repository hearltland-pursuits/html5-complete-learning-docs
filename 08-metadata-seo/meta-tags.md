---
title: Meta Tags
category: Metadata & SEO
order: 11
---

# Meta Tags

> **Quick Summary:** Meta tags provide metadata about HTML documents—character encoding, viewport settings, descriptions, keywords, author info, and more. They live in the `<head>` and control how browsers, search engines, and social platforms handle your page.

## Table of Contents
- [Introduction](#introduction)
- [Required Meta Tags](#required-meta-tags)
- [SEO Meta Tags](#seo-meta-tags)
- [Viewport and Mobile](#viewport-and-mobile)
- [Social Media Meta Tags](#social-media-meta-tags)
- [Other Useful Meta Tags](#other-useful-meta-tags)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Meta tags are HTML elements that provide metadata (data about data) about a webpage. They don't display content to users but communicate critical information to browsers, search engines, and social media platforms. Most meta tags use the `name` and `content` attributes, while social media tags use `property` and `content`.

**Key points:**
- Must be placed in `<head>` section
- Self-closing tags (no closing tag needed)
- Not visible to users (except in search results)
- Critical for SEO, accessibility, and social sharing

**Key Concept:** Meta tags are the "instruction manual" for your webpage. They tell browsers how to display content, search engines what the page is about, and social platforms how to format shared links.

---

## Required Meta Tags

### 1. Character Encoding (Always Required)

**Must be first in `<head>` (within first 1024 bytes):**
```html
<meta charset="UTF-8">
```

**Why it matters:**
- Ensures proper text rendering (accents, emojis, symbols)
- UTF-8 supports all languages and special characters
- Without it, text may display as �� or garbled characters

**Alternatives (UTF-8 is recommended):**
```html
<meta charset="UTF-8">        <!-- Recommended: Universal support -->
<meta charset="ISO-8859-1">   <!-- Latin alphabet only -->
<meta charset="windows-1252"> <!-- Windows legacy encoding -->
```

### 2. Viewport (Required for Mobile)

**Essential for responsive design:**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Breakdown:**
- `width=device-width`: Match screen width
- `initial-scale=1.0`: Default zoom level (100%)

**Common variations:**
```html
<!-- Standard responsive -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- Prevent zoom (use cautiously - accessibility issue) -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<!-- Allow zoom but set minimum -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=5.0">
```

**⚠️ Accessibility Warning:** Never disable zoom (`user-scalable=no`) unless absolutely necessary. Users with vision impairments rely on zoom functionality.

---

## SEO Meta Tags

### 1. Description (Highly Important)

**Appears in search results below page title:**
```html
<meta name="description" content="Learn how to use HTML meta tags for SEO, accessibility, and social media. Includes examples, best practices, and common mistakes to avoid.">
```

**Best practices:**
- **Length:** 150-160 characters (Google truncates longer descriptions)
- **Unique:** Every page should have a unique description
- **Actionable:** Include a call-to-action or value proposition
- **Keywords:** Include primary keywords naturally (no stuffing)

**Examples:**
```html
<!-- Blog post -->
<meta name="description" content="Discover 10 proven strategies to boost website traffic by 50% in 90 days. Includes step-by-step implementation guide and case studies.">

<!-- Product page -->
<meta name="description" content="Wireless noise-canceling headphones with 30-hour battery. $99.99. Free shipping over $50. Read 500+ 5-star reviews.">

<!-- Landing page -->
<meta name="description" content="Start your free 14-day trial. No credit card required. Join 10,000+ happy customers using our platform to automate workflows.">
```

### 2. Keywords (Mostly Deprecated)

**Google ignores this, but harmless to include:**
```html
<meta name="keywords" content="HTML, meta tags, SEO, web development">
```

**Why it's deprecated:**
- Google stopped using it in 2009 (keyword stuffing abuse)
- Bing and other engines give it minimal weight
- Can reveal your SEO strategy to competitors

**Verdict:** Skip it or use sparingly. Focus on meta description instead.

### 3. Robots (Control Indexing)

**Tell search engines how to index your page:**
```html
<!-- Default: index and follow links -->
<meta name="robots" content="index, follow">

<!-- Don't index this page -->
<meta name="robots" content="noindex, follow">

<!-- Index but don't follow links -->
<meta name="robots" content="index, nofollow">

<!-- Don't index and don't follow -->
<meta name="robots" content="noindex, nofollow">

<!-- Don't cache this page -->
<meta name="robots" content="noarchive">

<!-- Don't show snippet in search results -->
<meta name="robots" content="nosnippet">
```

**Use cases:**
- `noindex`: Admin pages, login pages, duplicate content
- `nofollow`: Untrusted user-generated content
- `noarchive`: Prevent cached versions (frequently updated content)

### 4. Author and Copyright

```html
<meta name="author" content="Joshua P. Hickman">
<meta name="copyright" content="© 2025 Your Company Name">
```

---

## Viewport and Mobile

### Standard Responsive Setup

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Advanced Viewport Options

```html
<!-- Fixed width (rare, usually for app-like experiences) -->
<meta name="viewport" content="width=400">

<!-- Shrink to fit (iOS Safari) -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, shrink-to-fit=no">

<!-- Control zoom -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=0.5, maximum-scale=3.0">
```

### Mobile Web App Meta Tags

```html
<!-- iOS: Add to home screen -->
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="App Name">

<!-- Android: Theme color (address bar color) -->
<meta name="theme-color" content="#4285f4">

<!-- Windows: Tile color -->
<meta name="msapplication-TileColor" content="#da532c">
```

---

## Social Media Meta Tags

### Open Graph (Facebook, LinkedIn, Discord)

**Covered in detail in [open-graph.md](open-graph.md):**
```html
<meta property="og:title" content="Article Title">
<meta property="og:description" content="Article description">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="og:url" content="https://example.com/article">
<meta property="og:type" content="article">
```

### Twitter Cards

**Covered in detail in [twitter-cards.md](twitter-cards.md):**
```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Article Title">
<meta name="twitter:description" content="Article description">
<meta name="twitter:image" content="https://example.com/image.jpg">
```

---

## Other Useful Meta Tags

### 1. Refresh and Redirect

**Auto-refresh page every 30 seconds:**
```html
<meta http-equiv="refresh" content="30">
```

**Redirect to another page after 5 seconds:**
```html
<meta http-equiv="refresh" content="5; url=https://example.com/new-page">
```

**⚠️ Warning:** Use redirects cautiously. Server-side redirects (301/302) are preferred for SEO.

### 2. Content Security Policy

**Prevent XSS attacks:**
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' https://trusted.cdn.com">
```

### 3. Referrer Policy

**Control what referrer information is sent:**
```html
<meta name="referrer" content="no-referrer">
<meta name="referrer" content="origin">
<meta name="referrer" content="no-referrer-when-downgrade">
```

### 4. Format Detection (iOS)

**Prevent automatic phone number linking:**
```html
<meta name="format-detection" content="telephone=no">
```

### 5. Google-Specific Meta Tags

```html
<!-- Disable automatic translation prompt -->
<meta name="google" content="notranslate">

<!-- Google Search Console verification -->
<meta name="google-site-verification" content="verification_token_here">
```

---

## Examples

### Example 1: Blog Post Meta Tags

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- SEO -->
  <meta name="description" content="Learn 10 proven strategies to boost website traffic by 50% in 90 days. Includes step-by-step implementation guide and real case studies.">
  <meta name="author" content="Joshua P. Hickman">
  <meta name="robots" content="index, follow">

  <!-- Open Graph (Facebook, LinkedIn) -->
  <meta property="og:title" content="10 Proven Strategies to Boost Website Traffic">
  <meta property="og:description" content="Increase your traffic by 50% in 90 days with these proven strategies.">
  <meta property="og:image" content="https://blog.example.com/images/traffic-boost.jpg">
  <meta property="og:url" content="https://blog.example.com/boost-traffic">
  <meta property="og:type" content="article">
  <meta property="article:published_time" content="2025-11-17T09:00:00Z">
  <meta property="article:author" content="Joshua P. Hickman">

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="10 Proven Strategies to Boost Website Traffic">
  <meta name="twitter:description" content="Increase your traffic by 50% in 90 days.">
  <meta name="twitter:image" content="https://blog.example.com/images/traffic-boost-twitter.jpg">
  <meta name="twitter:creator" content="@yourusername">
</head>
```

### Example 2: E-Commerce Product Page

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- SEO -->
  <meta name="description" content="Wireless noise-canceling headphones with 30-hour battery life. $99.99. Free shipping over $50. Read 500+ 5-star reviews. In stock now.">
  <meta name="robots" content="index, follow">

  <!-- Open Graph -->
  <meta property="og:type" content="product">
  <meta property="og:title" content="Wireless Noise-Canceling Headphones">
  <meta property="og:description" content="Premium headphones with 30-hour battery. $99.99.">
  <meta property="og:image" content="https://store.example.com/images/headphones-1200x630.jpg">
  <meta property="og:url" content="https://store.example.com/products/wireless-headphones">
  <meta property="product:price:amount" content="99.99">
  <meta property="product:price:currency" content="USD">
  <meta property="product:availability" content="in stock">

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Wireless Noise-Canceling Headphones - $99.99">
  <meta name="twitter:description" content="30-hour battery, Bluetooth 5.0, free shipping.">
  <meta name="twitter:image" content="https://store.example.com/images/headphones-twitter.jpg">
</head>
```

### Example 3: Mobile Web App

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

  <!-- SEO -->
  <meta name="description" content="Track your fitness goals with our mobile-friendly app. No download required.">

  <!-- Mobile app behavior -->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="apple-mobile-web-app-title" content="Fitness Tracker">

  <!-- Theme colors -->
  <meta name="theme-color" content="#4CAF50">
  <meta name="msapplication-TileColor" content="#4CAF50">

  <!-- Disable format detection -->
  <meta name="format-detection" content="telephone=no">

  <!-- Open Graph -->
  <meta property="og:title" content="Fitness Tracker App">
  <meta property="og:description" content="Track your fitness goals on any device.">
  <meta property="og:image" content="https://app.example.com/og-image.jpg">
</head>
```

---

## Best Practices

### Do This

1. **Always Include Charset and Viewport**
   ```html
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
   </head>
   ```

2. **Write Unique Descriptions for Every Page**
   ```html
   <!-- Homepage -->
   <meta name="description" content="Welcome to TechCorp - Leading provider of cloud solutions for businesses.">

   <!-- About page -->
   <meta name="description" content="Learn about TechCorp's 20-year history serving 5,000+ enterprise clients worldwide.">

   <!-- Product page -->
   <meta name="description" content="Cloud backup solution with 99.9% uptime. Free trial. No credit card required.">
   ```

3. **Use Descriptive, Action-Oriented Language**
   ```html
   <!-- GOOD: Specific, actionable -->
   <meta name="description" content="Download our free SEO checklist to boost rankings. 50+ actionable tips from industry experts.">

   <!-- BAD: Generic, boring -->
   <meta name="description" content="This page contains information about SEO.">
   ```

4. **Test Social Media Tags**
   ```
   Facebook: https://developers.facebook.com/tools/debug/
   Twitter: https://cards-dev.twitter.com/validator
   LinkedIn: https://www.linkedin.com/post-inspector/
   ```

### Avoid This

1. **Don't Duplicate Title in Description**
   ```html
   <title>10 SEO Tips for Beginners</title>

   <!-- WRONG: Duplicates title -->
   <meta name="description" content="10 SEO Tips for Beginners">

   <!-- CORRECT: Adds value beyond title -->
   <meta name="description" content="Boost your search rankings with these beginner-friendly SEO strategies. Includes step-by-step guide and free checklist.">
   ```

2. **Don't Keyword Stuff**
   ```html
   <!-- WRONG: Keyword stuffing -->
   <meta name="description" content="Buy shoes, cheap shoes, running shoes, men's shoes, women's shoes, kids shoes, best shoes, shoes sale, shoes online.">

   <!-- CORRECT: Natural language -->
   <meta name="description" content="Shop running shoes for men, women, and kids. Free shipping over $50. Find your perfect fit with our sizing guide.">
   ```

3. **Don't Forget Mobile Users**
   ```html
   <!-- WRONG: Missing viewport tag -->
   <head>
     <meta charset="UTF-8">
     <title>My Site</title>
   </head>

   <!-- CORRECT: Mobile-friendly -->
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>My Site</title>
   </head>
   ```

---

## Quick Reference

### Essential Meta Tags (Every Page)

```html
<head>
  <!-- 1. Character encoding (required, first) -->
  <meta charset="UTF-8">

  <!-- 2. Viewport (responsive design) -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- 3. Description (SEO, 150-160 chars) -->
  <meta name="description" content="Page description for search engines and social media.">

  <!-- 4. Author -->
  <meta name="author" content="Your Name">

  <!-- 5. Robots (if not default) -->
  <meta name="robots" content="index, follow">
</head>
```

### Meta Tag Categories

| Category | Meta Tags |
|----------|-----------|
| **Required** | `charset`, `viewport` |
| **SEO** | `description`, `robots`, `author` |
| **Social Media** | Open Graph (`og:*`), Twitter Cards (`twitter:*`) |
| **Mobile** | `apple-mobile-web-app-*`, `theme-color` |
| **Security** | `Content-Security-Policy`, `referrer` |
| **Deprecated** | `keywords` (low value) |

---

## Browser Support

| Meta Tag | Chrome | Firefox | Safari | Edge |
|----------|--------|---------|--------|------|
| `charset` | ✅ All | ✅ All | ✅ All | ✅ All |
| `viewport` | ✅ All | ✅ All | ✅ All | ✅ All |
| `description` | ✅ All | ✅ All | ✅ All | ✅ All |
| `robots` | ✅ All | ✅ All | ✅ All | ✅ All |
| Open Graph | ✅ All | ✅ All | ✅ All | ✅ All |
| `theme-color` | ✅ 39+ | ✅ No | ✅ 15+ | ✅ 79+ |
| `apple-mobile-*` | ❌ No | ❌ No | ✅ All | ❌ No |

---

## Related Topics
- [Head Element](head-element.md)
- [Title Element](title-tag.md)
- [Open Graph Protocol](open-graph.md)
- [Twitter Cards](twitter-cards.md)

---

**Last Updated:** November 17, 2025
**Category:** Metadata & SEO
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
