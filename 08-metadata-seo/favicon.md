---
title: Favicon Implementation
category: Metadata & SEO
order: 15
---

# Favicon Implementation

> **Quick Summary:** Favicons are small icons displayed in browser tabs, bookmarks, and mobile home screens. Modern implementation requires multiple sizes and formats (ICO, PNG, SVG) to support all devices and contexts—from 16x16px browser tabs to 512x512px Android app icons.

## Table of Contents
- [Introduction](#introduction)
- [Required Sizes](#required-sizes)
- [File Formats](#file-formats)
- [Basic Implementation](#basic-implementation)
- [Complete Implementation](#complete-implementation)
- [Favicon Generators](#favicon-generators)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Testing](#testing)
- [Related Topics](#related-topics)

---

## Introduction

Favicons (favorite icons) are small branded icons that appear in:
1. **Browser tabs** - Next to page title
2. **Bookmarks** - When users save your site
3. **History** - In browser history lists
4. **Mobile home screens** - When users add site to home screen
5. **Search results** - Google shows favicons next to site names
6. **Task switchers** - Mobile app switchers

**Key points:**
- Multiple sizes needed (16x16px to 512x512px)
- Multiple formats needed (ICO, PNG, SVG)
- Placed in `<head>` using `<link rel="icon">`
- Default fallback: `/favicon.ico` in root directory

**Key Concept:** Favicons are your site's visual brand in micro-format. They improve brand recognition, help users find your tab among dozens, and signal professionalism.

---

## Required Sizes

### Essential Sizes

| Size | Purpose | Format | Priority |
|------|---------|--------|----------|
| 16x16 | Browser tab (standard) | ICO/PNG | ⭐⭐⭐ High |
| 32x32 | Browser tab (Retina) | ICO/PNG | ⭐⭐⭐ High |
| 48x48 | Windows site icons | ICO/PNG | ⭐⭐ Medium |
| 180x180 | iOS home screen | PNG | ⭐⭐⭐ High |
| 192x192 | Android home screen | PNG | ⭐⭐⭐ High |
| 512x512 | Android splash screen | PNG | ⭐⭐ Medium |
| any | Modern browsers (scalable) | SVG | ⭐⭐⭐ High |

### Complete Size List

**Minimum implementation (2023+):**
- `favicon.ico` (16x16, 32x32, 48x48 multi-size ICO)
- `favicon.svg` (scalable, modern browsers)
- `apple-touch-icon.png` (180x180, iOS)
- `icon-192.png` (192x192, Android)
- `icon-512.png` (512x512, Android splash)

**Legacy/comprehensive implementation:**
- 16x16, 32x32, 48x48, 64x64 (Windows)
- 120x120, 152x152, 167x167, 180x180 (iOS)
- 192x192, 512x512 (Android)

---

## File Formats

### ICO (Icon) - Legacy Standard

**Pros:**
- Supported by all browsers (even IE6)
- Can contain multiple sizes in one file
- Default fallback (`/favicon.ico`)

**Cons:**
- Outdated format
- Larger file size than PNG
- No transparency in older versions

**Use for:** Browser tab icons, Windows compatibility

### PNG - Modern Standard

**Pros:**
- Smaller file size than ICO
- Excellent quality
- Full transparency support
- Universal browser support

**Cons:**
- Requires separate files for each size

**Use for:** Mobile home screen icons, high-quality favicons

### SVG - Future Standard

**Pros:**
- Scalable to any size (one file for all sizes)
- Smallest file size
- Perfect quality at any scale
- Supports CSS animations

**Cons:**
- Not supported in Safari (as of 2025)
- IE/Edge Legacy don't support it

**Use for:** Modern browsers, progressive enhancement

---

## Basic Implementation

### Minimum Viable Favicon (2025)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- Modern browsers (scalable) -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">

  <!-- Fallback for browsers that don't support SVG -->
  <link rel="icon" type="image/png" href="/favicon.png">

  <!-- iOS home screen -->
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">

  <!-- Legacy fallback (place favicon.ico in root, no tag needed) -->
</head>
<body>
  <!-- Page content -->
</body>
</html>
```

**Files required:**
- `/favicon.svg` (any size, scalable)
- `/favicon.png` (32x32 or 192x192)
- `/apple-touch-icon.png` (180x180)
- `/favicon.ico` (16x16, 32x32, 48x48 multi-size)

---

## Complete Implementation

### Full Cross-Platform Support

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <!-- ===== Modern Browsers (SVG, scalable) ===== -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">

  <!-- ===== Standard Favicons (PNG) ===== -->
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
  <link rel="icon" type="image/png" sizes="48x48" href="/favicon-48x48.png">

  <!-- ===== iOS / Apple ===== -->
  <!-- Home screen icon (precomposed = no gloss effect) -->
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
  <link rel="apple-touch-icon" sizes="152x152" href="/apple-touch-icon-152x152.png">
  <link rel="apple-touch-icon" sizes="120x120" href="/apple-touch-icon-120x120.png">

  <!-- ===== Android / Chrome ===== -->
  <link rel="icon" type="image/png" sizes="192x192" href="/android-chrome-192x192.png">
  <link rel="icon" type="image/png" sizes="512x512" href="/android-chrome-512x512.png">

  <!-- ===== Web App Manifest (Android) ===== -->
  <link rel="manifest" href="/site.webmanifest">

  <!-- ===== Microsoft / Windows ===== -->
  <meta name="msapplication-TileColor" content="#da532c">
  <meta name="msapplication-TileImage" content="/mstile-144x144.png">
  <meta name="msapplication-config" content="/browserconfig.xml">

  <!-- ===== Theme Color (Android address bar) ===== -->
  <meta name="theme-color" content="#ffffff">
</head>
<body>
  <!-- Page content -->
</body>
</html>
```

---

## Web App Manifest

### site.webmanifest

**For Android home screen installation:**
```json
{
  "name": "Your Site Name",
  "short_name": "Site",
  "description": "Description of your site",
  "icons": [
    {
      "src": "/android-chrome-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/android-chrome-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ],
  "theme_color": "#ffffff",
  "background_color": "#ffffff",
  "display": "standalone",
  "start_url": "/"
}
```

**Link in `<head>`:**
```html
<link rel="manifest" href="/site.webmanifest">
```

---

## Favicon Generators

### Recommended Tools

**1. RealFaviconGenerator** (https://realfavicongenerator.net/)
- **Best for:** Complete favicon package
- **Features:** All sizes, all platforms, generates manifest files
- **Output:** ZIP with all icons + HTML code

**2. Favicon.io** (https://favicon.io/)
- **Best for:** Quick generation from text, image, or emoji
- **Features:** Simple interface, generates PNG and ICO
- **Output:** ZIP with essential icons

**3. Maskable.app** (https://maskable.app/)
- **Best for:** Android adaptive icons
- **Features:** Preview how icon looks in different Android shapes
- **Output:** Maskable icon PNG

### Manual Creation

**Using design software:**
1. Create square design (512x512px minimum)
2. Keep important content in center "safe zone" (80% of canvas)
3. Export as PNG (transparent background)
4. Use online tool to generate other sizes
5. Convert to ICO using online converter

---

## Examples

### Example 1: Basic Favicon (Blog)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Tech Blog - Latest Web Development News</title>

  <!-- Favicon -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
  <link rel="icon" type="image/png" href="/favicon.png">
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">
</head>
<body>
  <!-- Blog content -->
</body>
</html>
```

**Files needed:**
- `/favicon.svg` (scalable)
- `/favicon.png` (32x32)
- `/apple-touch-icon.png` (180x180)
- `/favicon.ico` (root, no link tag)

---

### Example 2: E-Commerce Site (Complete)

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>TechStore - Electronics & Gadgets</title>

  <!-- Modern favicon -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">

  <!-- Standard sizes -->
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16x16.png">

  <!-- Apple -->
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">

  <!-- Android -->
  <link rel="icon" type="image/png" sizes="192x192" href="/android-chrome-192x192.png">
  <link rel="icon" type="image/png" sizes="512x512" href="/android-chrome-512x512.png">
  <link rel="manifest" href="/site.webmanifest">

  <!-- Windows -->
  <meta name="msapplication-TileColor" content="#2b5797">
  <meta name="msapplication-TileImage" content="/mstile-144x144.png">

  <!-- Theme color -->
  <meta name="theme-color" content="#ffffff">
</head>
<body>
  <!-- Store content -->
</body>
</html>
```

---

### Example 3: Progressive Web App

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Fitness Tracker - PWA</title>

  <!-- Modern favicon -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32x32.png">

  <!-- Apple (no status bar) -->
  <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

  <!-- Android manifest -->
  <link rel="manifest" href="/manifest.json">

  <!-- Theme color (matches app brand) -->
  <meta name="theme-color" content="#4CAF50">
</head>
<body>
  <!-- App content -->
</body>
</html>
```

**manifest.json:**
```json
{
  "name": "Fitness Tracker",
  "short_name": "Fitness",
  "description": "Track your workouts and reach your goals",
  "icons": [
    {
      "src": "/android-chrome-192x192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any maskable"
    },
    {
      "src": "/android-chrome-512x512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any maskable"
    }
  ],
  "theme_color": "#4CAF50",
  "background_color": "#ffffff",
  "display": "standalone",
  "start_url": "/",
  "scope": "/"
}
```

---

## Best Practices

### Do This

1. **Use SVG for Modern Browsers**
   ```html
   <!-- Scalable, future-proof -->
   <link rel="icon" type="image/svg+xml" href="/favicon.svg">
   ```

2. **Provide PNG Fallback**
   ```html
   <!-- SVG first, PNG fallback -->
   <link rel="icon" type="image/svg+xml" href="/favicon.svg">
   <link rel="icon" type="image/png" href="/favicon.png">
   ```

3. **Keep Design Simple**
   - Works at 16x16px (very small!)
   - Clear at low resolution
   - Recognizable shape/letter
   - High contrast

4. **Use Transparent Background**
   - Adapts to light/dark themes
   - Works on any browser UI color

5. **Place favicon.ico in Root**
   ```
   /
   ├── favicon.ico (automatic fallback)
   ├── favicon.svg
   ├── favicon.png
   └── index.html
   ```

### Avoid This

1. **Don't Use Complex Designs**
   ```
   ❌ Detailed logo with tiny text
   ❌ Multiple colors (hard to see at 16x16)
   ✅ Simple shape or letter
   ✅ 2-3 colors maximum
   ```

2. **Don't Forget Mobile Sizes**
   ```html
   <!-- WRONG: Only desktop favicon -->
   <link rel="icon" href="/favicon.ico">

   <!-- CORRECT: Mobile too -->
   <link rel="icon" href="/favicon.ico">
   <link rel="apple-touch-icon" href="/apple-touch-icon.png">
   <link rel="icon" sizes="192x192" href="/android-chrome-192x192.png">
   ```

3. **Don't Use Relative URLs (Usually)**
   ```html
   <!-- OK if favicon is in same directory as HTML -->
   <link rel="icon" href="favicon.png">

   <!-- BETTER: Absolute path from root -->
   <link rel="icon" href="/favicon.png">
   ```

---

## Testing

### Test in Browsers

**Desktop:**
1. Open your site in Chrome, Firefox, Safari, Edge
2. Check browser tab icon
3. Bookmark the page, check bookmark icon
4. Check browser history

**Mobile:**
1. iOS Safari: Tap "Share" > "Add to Home Screen"
2. Android Chrome: Tap menu > "Add to Home screen"
3. Verify icon appears correctly

### Online Tools

**1. Favicon Checker**
- URL: https://realfavicongenerator.net/favicon_checker
- Shows how favicon appears across platforms

**2. Google Search Console**
- Check if Google is indexing your favicon
- Appears next to site name in search results

### Common Issues

**Favicon not updating:**
1. Hard refresh: `Ctrl+F5` (Windows) / `Cmd+Shift+R` (Mac)
2. Clear browser cache
3. Check file path is correct
4. Verify file exists and is publicly accessible

**Wrong icon showing:**
- Browser cache (clear cache)
- Incorrect `href` path
- Missing `type` attribute

---

## Quick Reference

### Minimum 2025 Setup

```html
<head>
  <!-- Modern (SVG) -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">

  <!-- Fallback (PNG) -->
  <link rel="icon" type="image/png" href="/favicon.png">

  <!-- iOS -->
  <link rel="apple-touch-icon" href="/apple-touch-icon.png">

  <!-- Manifest (Android) -->
  <link rel="manifest" href="/site.webmanifest">
</head>
```

### File Sizes Quick Reference

| File | Size | Format | Purpose |
|------|------|--------|---------|
| `favicon.svg` | Any | SVG | Modern browsers (scalable) |
| `favicon.png` | 32x32 | PNG | Standard favicon fallback |
| `favicon.ico` | 16,32,48 | ICO | Legacy browsers (IE, old Edge) |
| `apple-touch-icon.png` | 180x180 | PNG | iOS home screen |
| `android-chrome-192x192.png` | 192x192 | PNG | Android home screen |
| `android-chrome-512x512.png` | 512x512 | PNG | Android splash screen |

---

## Browser Support

| Browser | ICO | PNG | SVG |
|---------|-----|-----|-----|
| Chrome | ✅ All | ✅ All | ✅ 80+ |
| Firefox | ✅ All | ✅ All | ✅ 41+ |
| Safari | ✅ All | ✅ All | ❌ Not yet |
| Edge | ✅ All | ✅ All | ✅ 79+ |
| IE11 | ✅ Yes | ✅ Yes | ❌ No |

---

## Related Topics
- [Head Element](head-element.md)
- [Meta Tags](meta-tags.md)
- [Link Relations](link-relations.md)

---

**Last Updated:** November 17, 2025
**Category:** Metadata & SEO
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
