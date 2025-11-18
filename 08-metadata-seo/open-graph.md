---
title: Open Graph Protocol
category: Metadata & SEO
order: 13
---

# Open Graph Protocol

> **Quick Summary:** The Open Graph Protocol controls how URLs display when shared on Facebook, LinkedIn, Discord, Slack, and 200+ other platforms. It defines the title, description, image, and type for rich social media previews.

## Table of Contents
- [Introduction](#introduction)
- [Required Properties](#required-properties)
- [Optional Properties](#optional-properties)
- [Content Types](#content-types)
- [Image Guidelines](#image-guidelines)
- [Examples](#examples)
- [Testing and Debugging](#testing-and-debugging)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The Open Graph Protocol (OGP) was created by Facebook in 2010 to standardize how web pages are represented when shared on social media. When you paste a URL into Facebook, LinkedIn, Discord, or Slack, these platforms read Open Graph tags to generate rich previews with images, titles, and descriptions.

**Without Open Graph:**
```
https://example.com/article
```
Just a plain link—no image, no description, low engagement.

**With Open Graph:**
```
┌─────────────────────────────────────┐
│ [Large preview image]               │
│ Article Title - Site Name           │
│ Engaging description that makes     │
│ people want to click...             │
└─────────────────────────────────────┘
```
Rich preview—increases click-through by 2-3x.

**Key points:**
- Used by Facebook, LinkedIn, Discord, Slack, WhatsApp, iMessage
- Meta tags with `property` attribute (not `name`)
- Placed in `<head>` section
- Overrides default title/description from page content
- Critical for social media marketing

**Key Concept:** Open Graph tags are your "social media business card." They control what people see when your content is shared, directly impacting engagement and traffic.

---

## Required Properties

### The Four Essential Tags

Every page should have these four Open Graph tags:

```html
<head>
  <!-- 1. Title: What is the name of this page? -->
  <meta property="og:title" content="10 Proven SEO Strategies That Actually Work">

  <!-- 2. Type: What kind of content is this? -->
  <meta property="og:type" content="article">

  <!-- 3. Image: What image should be shown? -->
  <meta property="og:image" content="https://example.com/images/seo-strategies.jpg">

  <!-- 4. URL: What is the canonical URL? -->
  <meta property="og:url" content="https://example.com/seo-strategies">
</head>
```

### Property Details

#### 1. `og:title`
```html
<meta property="og:title" content="Page Title Goes Here">
```
- **Recommended length:** 60-90 characters
- **What it does:** Appears as bold headline in social previews
- **Tip:** Can differ from `<title>` tag (social vs SEO optimization)

#### 2. `og:type`
```html
<meta property="og:type" content="article">
```
- **Common types:** `website`, `article`, `product`, `video`, `music`
- **What it does:** Tells platforms how to categorize content
- **Homepage:** Use `website`
- **Blog posts:** Use `article`
- **Products:** Use `product`

#### 3. `og:image`
```html
<meta property="og:image" content="https://example.com/image.jpg">
```
- **Must be absolute URL** (not relative)
- **Recommended size:** 1200x630 pixels (1.91:1 ratio)
- **What it does:** The visual shown in social previews
- **Critical:** No image = low engagement

#### 4. `og:url`
```html
<meta property="og:url" content="https://example.com/page">
```
- **Must be absolute URL** (not relative)
- **Should be canonical URL** (the preferred version)
- **What it does:** The URL shown when shared (may differ from current URL)

---

## Optional Properties

### Highly Recommended

```html
<!-- Description (150-200 characters) -->
<meta property="og:description" content="Discover 10 proven SEO strategies that have helped 1000+ businesses rank #1 on Google. Includes step-by-step implementation guide and case studies.">

<!-- Site name (your brand) -->
<meta property="og:site_name" content="Marketing Pro Blog">

<!-- Locale (language and region) -->
<meta property="og:locale" content="en_US">
```

### Image Enhancement

```html
<!-- Image secure URL (HTTPS version) -->
<meta property="og:image:secure_url" content="https://example.com/image.jpg">

<!-- Image dimensions (helps platforms render faster) -->
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">

<!-- Image alt text (accessibility) -->
<meta property="og:image:alt" content="Infographic showing 10 SEO strategies">

<!-- Image type (helps platforms process correctly) -->
<meta property="og:image:type" content="image/jpeg">
```

### Article-Specific (for blog posts)

```html
<!-- Article published time -->
<meta property="article:published_time" content="2025-11-17T09:00:00Z">

<!-- Article modified time -->
<meta property="article:modified_time" content="2025-11-17T14:30:00Z">

<!-- Article author -->
<meta property="article:author" content="https://example.com/author/joshua">

<!-- Article section/category -->
<meta property="article:section" content="SEO">

<!-- Article tags (multiple allowed) -->
<meta property="article:tag" content="SEO">
<meta property="article:tag" content="Digital Marketing">
<meta property="article:tag" content="Google">
```

### Product-Specific (for e-commerce)

```html
<!-- Product price -->
<meta property="product:price:amount" content="99.99">
<meta property="product:price:currency" content="USD">

<!-- Product availability -->
<meta property="product:availability" content="in stock">

<!-- Product condition -->
<meta property="product:condition" content="new">
```

### Video-Specific

```html
<!-- Video URL -->
<meta property="og:video" content="https://example.com/video.mp4">

<!-- Video secure URL -->
<meta property="og:video:secure_url" content="https://example.com/video.mp4">

<!-- Video dimensions -->
<meta property="og:video:width" content="1280">
<meta property="og:video:height" content="720">

<!-- Video type -->
<meta property="og:video:type" content="video/mp4">
```

---

## Content Types

### Type: website (Homepage)

```html
<meta property="og:type" content="website">
<meta property="og:title" content="TechCorp - Cloud Solutions for Enterprise">
<meta property="og:description" content="Leading cloud infrastructure provider serving 5,000+ businesses worldwide.">
<meta property="og:image" content="https://techcorp.com/og-homepage.jpg">
<meta property="og:url" content="https://techcorp.com">
<meta property="og:site_name" content="TechCorp">
```

### Type: article (Blog Post)

```html
<meta property="og:type" content="article">
<meta property="og:title" content="10 Proven SEO Strategies for 2025">
<meta property="og:description" content="Boost your rankings with these proven strategies.">
<meta property="og:image" content="https://blog.com/seo-strategies.jpg">
<meta property="og:url" content="https://blog.com/seo-strategies">
<meta property="article:published_time" content="2025-11-17T09:00:00Z">
<meta property="article:author" content="Joshua P. Hickman">
<meta property="article:section" content="SEO">
<meta property="article:tag" content="SEO">
<meta property="article:tag" content="Marketing">
```

### Type: product (E-Commerce)

```html
<meta property="og:type" content="product">
<meta property="og:title" content="Wireless Noise-Canceling Headphones">
<meta property="og:description" content="Premium headphones with 30-hour battery life. Free shipping.">
<meta property="og:image" content="https://store.com/headphones.jpg">
<meta property="og:url" content="https://store.com/products/headphones">
<meta property="product:price:amount" content="99.99">
<meta property="product:price:currency" content="USD">
<meta property="product:availability" content="in stock">
```

### Type: video.movie (Video Content)

```html
<meta property="og:type" content="video.movie">
<meta property="og:title" content="How to Build a Website in 10 Minutes">
<meta property="og:description" content="Step-by-step video tutorial for beginners.">
<meta property="og:image" content="https://videos.com/thumbnail.jpg">
<meta property="og:url" content="https://videos.com/website-tutorial">
<meta property="og:video" content="https://videos.com/website-tutorial.mp4">
<meta property="og:video:width" content="1280">
<meta property="og:video:height" content="720">
```

---

## Image Guidelines

### Recommended Dimensions

| Platform | Recommended Size | Aspect Ratio | Notes |
|----------|-----------------|--------------|-------|
| **Facebook** | 1200x630px | 1.91:1 | Minimum 600x315px |
| **LinkedIn** | 1200x627px | 1.91:1 | Same as Facebook |
| **Twitter** | 1200x675px | 16:9 | If using summary_large_image |
| **Discord** | 1200x630px | 1.91:1 | Same as Facebook |

**Universal safe choice: 1200x630px (1.91:1 ratio)**

### Image Best Practices

1. **Use absolute URLs (not relative)**
   ```html
   <!-- WRONG -->
   <meta property="og:image" content="/images/photo.jpg">

   <!-- CORRECT -->
   <meta property="og:image" content="https://example.com/images/photo.jpg">
   ```

2. **Use HTTPS**
   ```html
   <!-- GOOD: Secure URL -->
   <meta property="og:image" content="https://example.com/image.jpg">

   <!-- AVOID: May not display on some platforms -->
   <meta property="og:image" content="http://example.com/image.jpg">
   ```

3. **Specify dimensions (faster rendering)**
   ```html
   <meta property="og:image" content="https://example.com/image.jpg">
   <meta property="og:image:width" content="1200">
   <meta property="og:image:height" content="630">
   ```

4. **Include alt text (accessibility)**
   ```html
   <meta property="og:image:alt" content="Person using laptop with graphs showing website traffic growth">
   ```

5. **Keep file size under 8MB**
   - Facebook limit: 8MB
   - Recommended: Under 1MB for fast loading

6. **Avoid text-heavy images**
   - Facebook suppresses images with >20% text
   - Use minimal text, focus on visuals

---

## Examples

### Example 1: Blog Post

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Standard meta tags -->
  <title>10 Proven SEO Strategies for 2025 | Marketing Blog</title>
  <meta name="description" content="Boost your search rankings with these proven strategies.">

  <!-- Open Graph tags -->
  <meta property="og:type" content="article">
  <meta property="og:title" content="10 Proven SEO Strategies That Actually Work in 2025">
  <meta property="og:description" content="Discover the exact SEO strategies that helped 1000+ businesses rank #1 on Google. Includes step-by-step guide and real case studies.">
  <meta property="og:image" content="https://blog.example.com/images/seo-2025.jpg">
  <meta property="og:image:width" content="1200">
  <meta property="og:image:height" content="630">
  <meta property="og:image:alt" content="Infographic showing 10 SEO strategies">
  <meta property="og:url" content="https://blog.example.com/seo-strategies-2025">
  <meta property="og:site_name" content="Marketing Pro Blog">
  <meta property="og:locale" content="en_US">

  <!-- Article metadata -->
  <meta property="article:published_time" content="2025-11-17T09:00:00Z">
  <meta property="article:modified_time" content="2025-11-17T14:30:00Z">
  <meta property="article:author" content="Joshua P. Hickman">
  <meta property="article:section" content="SEO">
  <meta property="article:tag" content="SEO">
  <meta property="article:tag" content="Digital Marketing">
  <meta property="article:tag" content="Google Rankings">
</head>
<body>
  <!-- Article content -->
</body>
</html>
```

### Example 2: E-Commerce Product

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Wireless Headphones - $99.99 | TechStore</title>

  <!-- Open Graph tags -->
  <meta property="og:type" content="product">
  <meta property="og:title" content="Wireless Noise-Canceling Headphones">
  <meta property="og:description" content="Premium wireless headphones with 30-hour battery, active noise cancellation, and Bluetooth 5.0. Free shipping over $50.">
  <meta property="og:image" content="https://store.example.com/images/headphones-1200x630.jpg">
  <meta property="og:image:width" content="1200">
  <meta property="og:image:height" content="630">
  <meta property="og:image:alt" content="Black wireless headphones on white background">
  <meta property="og:url" content="https://store.example.com/products/wireless-headphones">
  <meta property="og:site_name" content="TechStore">

  <!-- Product metadata -->
  <meta property="product:price:amount" content="99.99">
  <meta property="product:price:currency" content="USD">
  <meta property="product:availability" content="in stock">
  <meta property="product:condition" content="new">
</head>
<body>
  <!-- Product page content -->
</body>
</html>
```

### Example 3: Company Homepage

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>TechCorp - Cloud Solutions for Enterprise</title>

  <!-- Open Graph tags -->
  <meta property="og:type" content="website">
  <meta property="og:title" content="TechCorp - Cloud Infrastructure for Growing Businesses">
  <meta property="og:description" content="Trusted by 5,000+ companies worldwide. 99.9% uptime, enterprise-grade security, 24/7 support. Start your free trial today.">
  <meta property="og:image" content="https://techcorp.com/og-homepage.jpg">
  <meta property="og:image:width" content="1200">
  <meta property="og:image:height" content="630">
  <meta property="og:image:alt" content="TechCorp cloud infrastructure dashboard">
  <meta property="og:url" content="https://techcorp.com">
  <meta property="og:site_name" content="TechCorp">
  <meta property="og:locale" content="en_US">
</head>
<body>
  <!-- Homepage content -->
</body>
</html>
```

---

## Testing and Debugging

### Facebook Sharing Debugger

**URL:** https://developers.facebook.com/tools/debug/

**How to use:**
1. Paste your URL
2. Click "Debug"
3. Review how Facebook will display your link
4. Click "Scrape Again" if you made changes

**What to check:**
- Is the image displayed correctly?
- Is the title compelling?
- Is the description truncated?
- Are there any warnings?

### LinkedIn Post Inspector

**URL:** https://www.linkedin.com/post-inspector/

**How to use:**
1. Paste your URL
2. Click "Inspect"
3. Review preview

### Twitter Card Validator

**URL:** https://cards-dev.twitter.com/validator

**Note:** Checks Twitter Cards (covered in [twitter-cards.md](twitter-cards.md)), but also shows Open Graph fallback.

### Discord Embed Visualizer

**URL:** https://leovoel.github.io/embed-visualizer/

**Tip:** Discord uses Open Graph tags but has unique rendering.

---

## Best Practices

### Do This

1. **Use Compelling Images**
   ```html
   <!-- GOOD: High-quality, relevant image -->
   <meta property="og:image" content="https://blog.com/infographic-seo.jpg">

   <!-- BAD: Generic stock photo -->
   <meta property="og:image" content="https://blog.com/generic-laptop.jpg">
   ```

2. **Write Social-Optimized Titles**
   ```html
   <!-- GOOD: Engaging, benefit-driven -->
   <meta property="og:title" content="10 SEO Strategies That Doubled Our Traffic in 90 Days">

   <!-- BAD: Boring, generic -->
   <meta property="og:title" content="SEO Strategies">
   ```

3. **Include All Four Required Tags**
   ```html
   <meta property="og:title" content="...">
   <meta property="og:type" content="article">
   <meta property="og:image" content="...">
   <meta property="og:url" content="...">
   ```

4. **Test Before Publishing**
   - Use Facebook Sharing Debugger
   - Share in private Discord/Slack channel
   - Check mobile and desktop views

### Avoid This

1. **Don't Use Relative URLs**
   ```html
   <!-- WRONG -->
   <meta property="og:image" content="/images/photo.jpg">
   <meta property="og:url" content="/article">

   <!-- CORRECT -->
   <meta property="og:image" content="https://example.com/images/photo.jpg">
   <meta property="og:url" content="https://example.com/article">
   ```

2. **Don't Forget Image Dimensions**
   ```html
   <!-- BAD: No dimensions (slower rendering) -->
   <meta property="og:image" content="https://example.com/image.jpg">

   <!-- GOOD: Includes dimensions -->
   <meta property="og:image" content="https://example.com/image.jpg">
   <meta property="og:image:width" content="1200">
   <meta property="og:image:height" content="630">
   ```

3. **Don't Use Clickbait**
   ```html
   <!-- BAD: Misleading clickbait -->
   <meta property="og:title" content="You Won't BELIEVE What Happened Next!!!">

   <!-- GOOD: Honest, compelling -->
   <meta property="og:title" content="How We Increased Sales by 150% Using This Simple Strategy">
   ```

---

## Quick Reference

### Essential Open Graph Template

```html
<head>
  <!-- Required (minimum 4) -->
  <meta property="og:title" content="Page Title">
  <meta property="og:type" content="article">
  <meta property="og:image" content="https://example.com/image.jpg">
  <meta property="og:url" content="https://example.com/page">

  <!-- Highly recommended -->
  <meta property="og:description" content="Page description">
  <meta property="og:site_name" content="Site Name">
  <meta property="og:locale" content="en_US">

  <!-- Image optimization -->
  <meta property="og:image:width" content="1200">
  <meta property="og:image:height" content="630">
  <meta property="og:image:alt" content="Image description">
</head>
```

---

## Browser Support

Open Graph tags are **not displayed by browsers**—they're read by social media platforms. All major platforms support Open Graph:

| Platform | Support |
|----------|---------|
| Facebook | ✅ Full support (creator of OGP) |
| LinkedIn | ✅ Full support |
| Discord | ✅ Full support |
| Slack | ✅ Full support |
| WhatsApp | ✅ Full support |
| iMessage | ✅ Full support |
| Twitter | ✅ Falls back to OG if no Twitter Card |

---

## Related Topics
- [Twitter Cards](twitter-cards.md)
- [Meta Tags](meta-tags.md)
- [Head Element](head-element.md)

---

**Last Updated:** November 17, 2025
**Category:** Metadata & SEO
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
