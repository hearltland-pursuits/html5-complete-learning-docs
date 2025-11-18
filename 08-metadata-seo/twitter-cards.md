---
title: Twitter Cards
category: Metadata & SEO
order: 14
---

# Twitter Cards

> **Quick Summary:** Twitter Cards are meta tags that control how URLs display when shared on Twitter/X. They create rich previews with images, titles, and descriptions—transforming plain links into engaging visual cards that boost engagement by 2-3x.

## Table of Contents
- [Introduction](#introduction)
- [Card Types](#card-types)
- [Required Tags](#required-tags)
- [Summary Card](#summary-card)
- [Summary Large Image](#summary-large-image)
- [App Card](#app-card)
- [Player Card](#player-card)
- [Examples](#examples)
- [Testing and Validation](#testing-and-validation)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Twitter Cards enhance how links appear on Twitter/X. Instead of plain text URLs, they display rich previews with images, titles, descriptions, and additional metadata. Twitter Cards use meta tags with the `name="twitter:*"` pattern, placed in the `<head>` section.

**Without Twitter Card:**
```
Check out this article: https://example.com/article
```
Just a link—no visual appeal, low engagement.

**With Twitter Card:**
```
┌─────────────────────────────────────┐
│ [Large preview image]               │
│ Article Title                       │
│ Engaging description that makes     │
│ people want to click...             │
│ example.com                         │
└─────────────────────────────────────┘
```
Rich visual card—higher click-through rates.

**Key points:**
- Four card types: Summary, Summary Large Image, App, Player
- Falls back to Open Graph if Twitter tags missing
- Requires domain whitelisting for some card types
- Meta tags use `name` attribute (not `property` like Open Graph)

**Key Concept:** Twitter Cards transform boring links into visual stories. They're essential for content marketing, e-commerce, and any business using Twitter/X for promotion.

---

## Card Types

### 1. Summary Card (Default)

**Small square image on the left, text on right:**
```
┌──────────────────────────┐
│ [img] Title              │
│ [img] Description        │
│ [img] example.com        │
└──────────────────────────┘
```

**Use for:** General content, blog posts, articles

### 2. Summary Large Image (Most Popular)

**Large rectangular image above text:**
```
┌──────────────────────────┐
│ [Large image]            │
│                          │
│ Title                    │
│ Description              │
│ example.com              │
└──────────────────────────┘
```

**Use for:** Photo-heavy content, infographics, visual stories

### 3. App Card

**Promotes mobile apps with install button:**
```
┌──────────────────────────┐
│ [App icon] App Name      │
│ Description              │
│ [Install on iOS/Android] │
└──────────────────────────┘
```

**Use for:** Mobile app promotion

### 4. Player Card

**Embeds video/audio directly in tweet:**
```
┌──────────────────────────┐
│ [Video player]           │
│ ▶️  Play button          │
│                          │
│ Title                    │
└──────────────────────────┘
```

**Use for:** Video content, podcasts, music

---

## Required Tags

### Minimum Tags (All Card Types)

```html
<head>
  <!-- 1. Card type -->
  <meta name="twitter:card" content="summary_large_image">

  <!-- 2. Title -->
  <meta name="twitter:title" content="Page Title">

  <!-- 3. Description -->
  <meta name="twitter:description" content="Page description">

  <!-- 4. Image -->
  <meta name="twitter:image" content="https://example.com/image.jpg">
</head>
```

### Optional but Recommended

```html
<!-- Twitter username (@username, without @) -->
<meta name="twitter:site" content="@yourbrand">

<!-- Author's Twitter username -->
<meta name="twitter:creator" content="@authorname">

<!-- Image alt text (accessibility) -->
<meta name="twitter:image:alt" content="Description of image">
```

---

## Summary Card

**Best for:** General content, blog posts, news articles

### Basic Setup

```html
<head>
  <meta name="twitter:card" content="summary">
  <meta name="twitter:site" content="@yourbrand">
  <meta name="twitter:title" content="10 Proven SEO Strategies">
  <meta name="twitter:description" content="Boost your rankings with these proven strategies.">
  <meta name="twitter:image" content="https://example.com/image.jpg">
  <meta name="twitter:image:alt" content="SEO strategies infographic">
</head>
```

### Image Guidelines

- **Recommended size:** 144x144px minimum
- **Aspect ratio:** 1:1 (square)
- **Max file size:** 5MB
- **Format:** JPG, PNG, WEBP, GIF

---

## Summary Large Image

**Best for:** Photo-driven content, infographics, product pages

### Basic Setup

```html
<head>
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:site" content="@yourbrand">
  <meta name="twitter:creator" content="@authorname">
  <meta name="twitter:title" content="10 Proven SEO Strategies That Actually Work">
  <meta name="twitter:description" content="Discover the exact strategies that helped 1000+ businesses rank #1 on Google.">
  <meta name="twitter:image" content="https://example.com/seo-strategies.jpg">
  <meta name="twitter:image:alt" content="Infographic showing 10 SEO strategies with charts">
</head>
```

### Image Guidelines

- **Recommended size:** 1200x675px (16:9 ratio)
- **Minimum size:** 300x157px
- **Max file size:** 5MB
- **Format:** JPG, PNG, WEBP, GIF
- **Aspect ratio:** 2:1 (will be cropped to 1.91:1 in display)

**⚠️ Important:** Images larger than 1MB may cause slow loading.

---

## App Card

**Best for:** Mobile app promotion

### Basic Setup

```html
<head>
  <meta name="twitter:card" content="app">
  <meta name="twitter:site" content="@appname">
  <meta name="twitter:title" content="Fitness Tracker App">
  <meta name="twitter:description" content="Track your workouts and reach your fitness goals.">
  <meta name="twitter:image" content="https://example.com/app-icon.jpg">

  <!-- iOS app -->
  <meta name="twitter:app:name:iphone" content="Fitness Tracker">
  <meta name="twitter:app:id:iphone" content="123456789">
  <meta name="twitter:app:url:iphone" content="fitnessapp://open">

  <!-- Android app -->
  <meta name="twitter:app:name:googleplay" content="Fitness Tracker">
  <meta name="twitter:app:id:googleplay" content="com.example.fitnessapp">
  <meta name="twitter:app:url:googleplay" content="https://play.google.com/store/apps/details?id=com.example.fitnessapp">
</head>
```

---

## Player Card

**Best for:** Video content, podcasts, music

### Basic Setup

```html
<head>
  <meta name="twitter:card" content="player">
  <meta name="twitter:site" content="@videosite">
  <meta name="twitter:title" content="How to Build a Website in 10 Minutes">
  <meta name="twitter:description" content="Step-by-step video tutorial for beginners.">
  <meta name="twitter:image" content="https://example.com/video-thumbnail.jpg">

  <!-- Player URL (must be HTTPS) -->
  <meta name="twitter:player" content="https://example.com/embed/video123">

  <!-- Player dimensions -->
  <meta name="twitter:player:width" content="1280">
  <meta name="twitter:player:height" content="720">

  <!-- Player stream (optional, for audio) -->
  <meta name="twitter:player:stream" content="https://example.com/audio.mp3">
</head>
```

**⚠️ Note:** Player cards require whitelisting by Twitter. Submit your domain at https://cards-dev.twitter.com/validator

---

## Examples

### Example 1: Blog Post (Summary Large Image)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Standard meta tags -->
  <title>10 Proven SEO Strategies for 2025 | Marketing Blog</title>
  <meta name="description" content="Boost your search rankings with these proven strategies.">

  <!-- Open Graph (Facebook, LinkedIn) -->
  <meta property="og:type" content="article">
  <meta property="og:title" content="10 Proven SEO Strategies That Actually Work">
  <meta property="og:description" content="Discover the exact strategies that helped 1000+ businesses rank #1.">
  <meta property="og:image" content="https://blog.example.com/images/seo-2025-og.jpg">
  <meta property="og:url" content="https://blog.example.com/seo-strategies-2025">

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:site" content="@marketingpro">
  <meta name="twitter:creator" content="@joshuahickman">
  <meta name="twitter:title" content="10 Proven SEO Strategies That Actually Work in 2025">
  <meta name="twitter:description" content="Discover the exact strategies that helped 1000+ businesses rank #1 on Google. Includes free checklist.">
  <meta name="twitter:image" content="https://blog.example.com/images/seo-2025-twitter.jpg">
  <meta name="twitter:image:alt" content="Infographic showing 10 SEO strategies with performance charts">
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

  <!-- Open Graph -->
  <meta property="og:type" content="product">
  <meta property="og:title" content="Wireless Noise-Canceling Headphones">
  <meta property="og:image" content="https://store.example.com/images/headphones-og.jpg">
  <meta property="product:price:amount" content="99.99">
  <meta property="product:price:currency" content="USD">

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:site" content="@techstore">
  <meta name="twitter:title" content="Wireless Noise-Canceling Headphones - $99.99">
  <meta name="twitter:description" content="30-hour battery, Bluetooth 5.0, active noise cancellation. Free shipping over $50. ⚡ In stock now!">
  <meta name="twitter:image" content="https://store.example.com/images/headphones-twitter.jpg">
  <meta name="twitter:image:alt" content="Black wireless headphones on white background">
</head>
<body>
  <!-- Product page content -->
</body>
</html>
```

### Example 3: Video Content (Player Card)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>How to Build a Website - Video Tutorial</title>

  <!-- Twitter Player Card -->
  <meta name="twitter:card" content="player">
  <meta name="twitter:site" content="@tutorialsite">
  <meta name="twitter:title" content="How to Build a Website in 10 Minutes">
  <meta name="twitter:description" content="Complete beginner's tutorial. No coding required!">
  <meta name="twitter:image" content="https://videos.example.com/thumbnails/website-tutorial.jpg">
  <meta name="twitter:image:alt" content="Video thumbnail showing website builder interface">
  <meta name="twitter:player" content="https://videos.example.com/embed/website-tutorial">
  <meta name="twitter:player:width" content="1280">
  <meta name="twitter:player:height" content="720">
</head>
<body>
  <!-- Video page content -->
</body>
</html>
```

---

## Testing and Validation

### Twitter Card Validator

**URL:** https://cards-dev.twitter.com/validator

**How to use:**
1. Paste your URL
2. Click "Preview card"
3. Review how Twitter will display your card
4. Check for errors or warnings

**What to check:**
- Does the image display correctly?
- Is the title compelling?
- Is the description truncated?
- Is image alt text present?

### Common Validation Errors

**Error: "Unable to render card"**
- **Cause:** Missing required tags
- **Fix:** Add all four required tags (card, title, description, image)

**Error: "Image could not be loaded"**
- **Cause:** Image URL inaccessible, not HTTPS, or too large
- **Fix:** Use HTTPS, ensure file size <5MB, verify URL is publicly accessible

**Error: "Card type not recognized"**
- **Cause:** Typo in `twitter:card` value
- **Fix:** Use exact values: `summary`, `summary_large_image`, `app`, `player`

---

## Best Practices

### Do This

1. **Use Summary Large Image for Most Content**
   ```html
   <!-- GOOD: Visual impact -->
   <meta name="twitter:card" content="summary_large_image">

   <!-- OK: But less engaging -->
   <meta name="twitter:card" content="summary">
   ```

2. **Include Twitter Handles**
   ```html
   <!-- Brand Twitter handle -->
   <meta name="twitter:site" content="@yourbrand">

   <!-- Author Twitter handle -->
   <meta name="twitter:creator" content="@authorname">
   ```

3. **Write Twitter-Optimized Descriptions**
   ```html
   <!-- GOOD: Engaging, uses emoji, under 200 chars -->
   <meta name="twitter:description" content="🚀 Boost your rankings with these 10 proven SEO strategies. Includes free checklist + case studies. Results in 30 days!">

   <!-- BAD: Generic, boring -->
   <meta name="twitter:description" content="This article discusses SEO strategies.">
   ```

4. **Add Image Alt Text**
   ```html
   <meta name="twitter:image:alt" content="Infographic showing 10 SEO strategies with performance charts">
   ```

5. **Test Before Publishing**
   - Use Twitter Card Validator
   - Share in private tweet (don't publish) to preview
   - Check mobile and desktop views

### Avoid This

1. **Don't Use Low-Quality Images**
   ```html
   <!-- WRONG: Too small, pixelated -->
   <meta name="twitter:image" content="https://example.com/tiny-100x100.jpg">

   <!-- CORRECT: High-quality, proper size -->
   <meta name="twitter:image" content="https://example.com/quality-1200x675.jpg">
   ```

2. **Don't Forget HTTPS for Images**
   ```html
   <!-- WRONG: HTTP (may not display) -->
   <meta name="twitter:image" content="http://example.com/image.jpg">

   <!-- CORRECT: HTTPS -->
   <meta name="twitter:image" content="https://example.com/image.jpg">
   ```

3. **Don't Exceed 5MB File Size**
   - Twitter won't display images >5MB
   - Keep under 1MB for fast loading

4. **Don't Use Clickbait**
   ```html
   <!-- BAD: Misleading clickbait -->
   <meta name="twitter:title" content="You Won't BELIEVE What Happened!!!">

   <!-- GOOD: Honest, compelling -->
   <meta name="twitter:title" content="We Increased Sales 150% Using This Simple Strategy">
   ```

---

## Twitter vs Open Graph

### Can You Use Both?

**Yes! Use both for maximum compatibility:**
```html
<head>
  <!-- Open Graph (Facebook, LinkedIn, Discord) -->
  <meta property="og:title" content="Article Title">
  <meta property="og:description" content="Article description">
  <meta property="og:image" content="https://example.com/og-image.jpg">

  <!-- Twitter Card (Twitter/X) -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Article Title">
  <meta name="twitter:description" content="Article description">
  <meta name="twitter:image" content="https://example.com/twitter-image.jpg">
</head>
```

### Twitter Falls Back to Open Graph

**If Twitter Card tags are missing, Twitter uses Open Graph:**
```html
<head>
  <!-- Only Open Graph tags -->
  <meta property="og:title" content="Article Title">
  <meta property="og:description" content="Description">
  <meta property="og:image" content="https://example.com/image.jpg">

  <!-- Twitter will use these ↑ but as "summary" card (not large image) -->
</head>
```

**To force large image, add just the card type:**
```html
<head>
  <!-- Twitter card type -->
  <meta name="twitter:card" content="summary_large_image">

  <!-- Twitter will use OG tags for title, description, image -->
  <meta property="og:title" content="Article Title">
  <meta property="og:description" content="Description">
  <meta property="og:image" content="https://example.com/image.jpg">
</head>
```

### When to Use Separate Images

**Use different images for Twitter vs Facebook when:**
- Twitter's 16:9 ratio works better for your image
- Facebook's 1.91:1 ratio crops important content
- You want platform-specific text overlays

---

## Quick Reference

### Essential Twitter Card Template

```html
<head>
  <!-- Required -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Page Title">
  <meta name="twitter:description" content="Page description">
  <meta name="twitter:image" content="https://example.com/image.jpg">

  <!-- Recommended -->
  <meta name="twitter:site" content="@yourbrand">
  <meta name="twitter:creator" content="@author">
  <meta name="twitter:image:alt" content="Image description">
</head>
```

### Card Type Quick Reference

| Card Type | Best For | Image Size |
|-----------|----------|------------|
| `summary` | General content | 144x144px (1:1) |
| `summary_large_image` | Visual content | 1200x675px (16:9) |
| `app` | Mobile apps | 144x144px |
| `player` | Video/audio | 1280x720px |

---

## Browser Support

Twitter Cards are **not displayed by browsers**—they're rendered by Twitter/X when URLs are shared. All modern Twitter/X platforms support Twitter Cards:

| Platform | Support |
|----------|---------|
| Twitter Web | ✅ Full support |
| Twitter iOS | ✅ Full support |
| Twitter Android | ✅ Full support |
| TweetDeck | ✅ Full support |
| X (rebranded) | ✅ Full support |

---

## Related Topics
- [Open Graph Protocol](open-graph.md)
- [Meta Tags](meta-tags.md)
- [Head Element](head-element.md)

---

**Last Updated:** November 17, 2025
**Category:** Metadata & SEO
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
