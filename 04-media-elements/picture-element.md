# The Picture Element

## Overview
The `<picture>` element is an HTML5 container that allows you to specify multiple image sources for different scenarios (art direction, format support, screen densities). The browser selects the most appropriate image based on device capabilities and viewport conditions.

## Basic Syntax

```html
<picture>
  <source srcset="image.webp" type="image/webp">
  <source srcset="image.avif" type="image/avif">
  <img src="image.jpg" alt="Fallback image">
</picture>
```

**Key Points:**
- Contains one or more `<source>` elements and one `<img>` element
- Browser evaluates `<source>` elements from top to bottom
- First matching `<source>` is used
- `<img>` serves as fallback and provides alt text
- `<img>` is **required** (picture won't display without it)

## Use Cases

### 1. Modern Image Formats with Fallback

Serve next-gen formats (AVIF, WebP) with JPEG/PNG fallback.

```html
<picture>
  <source srcset="photo.avif" type="image/avif">
  <source srcset="photo.webp" type="image/webp">
  <img src="photo.jpg" alt="Beautiful landscape" width="800" height="600">
</picture>
```

**How it works:**
1. Browser checks if it supports AVIF → uses `photo.avif`
2. If not, checks WebP support → uses `photo.webp`
3. If neither supported → falls back to `photo.jpg`

**File Size Comparison:**
- JPEG: 100 KB (baseline)
- WebP: ~60 KB (40% smaller)
- AVIF: ~40 KB (60% smaller)

### 2. Art Direction (Different Images for Different Viewports)

Display different crops/compositions based on screen size.

```html
<picture>
  <!-- Mobile: Portrait crop -->
  <source media="(max-width: 600px)"
          srcset="mobile-portrait.jpg">

  <!-- Tablet: Square crop -->
  <source media="(max-width: 1024px)"
          srcset="tablet-square.jpg">

  <!-- Desktop: Landscape crop -->
  <img src="desktop-landscape.jpg"
       alt="Team collaboration"
       width="1200"
       height="600">
</picture>
```

**Real-world example:**
```html
<picture>
  <!-- Mobile: Show just the product -->
  <source media="(max-width: 767px)"
          srcset="product-closeup-mobile.jpg">

  <!-- Desktop: Show product with context/lifestyle -->
  <img src="product-lifestyle-desktop.jpg"
       alt="Wireless headphones on wooden desk"
       width="1920"
       height="800">
</picture>
```

### 3. Resolution Switching (Pixel Density)

Serve higher resolution images for high-DPI displays (Retina, 4K).

```html
<picture>
  <source srcset="image-1x.jpg 1x,
                  image-2x.jpg 2x,
                  image-3x.jpg 3x">
  <img src="image-1x.jpg" alt="High-quality photo" width="600" height="400">
</picture>
```

**Density descriptors:**
- `1x`: Standard displays (96 DPI)
- `2x`: Retina displays (192 DPI) - iPhone, MacBook
- `3x`: Super Retina displays (288 DPI) - iPhone Pro models

### 4. Combining Formats and Media Queries

```html
<picture>
  <!-- Mobile + WebP -->
  <source media="(max-width: 600px)"
          srcset="mobile.webp"
          type="image/webp">

  <!-- Mobile + JPEG fallback -->
  <source media="(max-width: 600px)"
          srcset="mobile.jpg">

  <!-- Desktop + WebP -->
  <source srcset="desktop.webp" type="image/webp">

  <!-- Desktop + JPEG fallback -->
  <img src="desktop.jpg" alt="Responsive image" width="1200" height="600">
</picture>
```

## Attributes

### source Attributes

#### srcset (Required for source)
Comma-separated list of image URLs with optional descriptors.

```html
<!-- Width descriptors -->
<source srcset="small.jpg 400w, medium.jpg 800w, large.jpg 1200w">

<!-- Density descriptors -->
<source srcset="image-1x.jpg 1x, image-2x.jpg 2x">

<!-- Single image -->
<source srcset="image.jpg">
```

#### type
MIME type of the image format.

```html
<source srcset="image.avif" type="image/avif">
<source srcset="image.webp" type="image/webp">
<source srcset="image.png" type="image/png">
```

**Common MIME types:**
- `image/avif` - AVIF format
- `image/webp` - WebP format
- `image/jpeg` - JPEG format
- `image/png` - PNG format
- `image/svg+xml` - SVG format

#### media
Media query condition for art direction.

```html
<source media="(max-width: 767px)" srcset="mobile.jpg">
<source media="(min-width: 768px) and (max-width: 1023px)" srcset="tablet.jpg">
<source media="(min-width: 1024px)" srcset="desktop.jpg">
```

**Common breakpoints:**
- `(max-width: 767px)` - Mobile
- `(min-width: 768px)` - Tablet and up
- `(min-width: 1024px)` - Desktop and up
- `(min-width: 1440px)` - Large desktop

#### sizes
Similar to img srcset sizes attribute.

```html
<source srcset="small.jpg 400w, large.jpg 800w"
        sizes="(max-width: 600px) 400px, 800px">
```

### img Attributes (Inside picture)

```html
<img src="fallback.jpg"
     alt="Description"
     width="800"
     height="600"
     loading="lazy"
     decoding="async">
```

## Complete Examples

### Example 1: Format Optimization
```html
<picture>
  <!-- Next-gen formats -->
  <source srcset="hero.avif" type="image/avif">
  <source srcset="hero.webp" type="image/webp">

  <!-- Fallback -->
  <img src="hero.jpg"
       alt="Modern office workspace with natural lighting"
       width="1920"
       height="1080"
       loading="eager">
</picture>
```

### Example 2: Art Direction (Hero Banner)
```html
<picture>
  <!-- Mobile: Portrait orientation, focus on person -->
  <source media="(max-width: 767px)"
          srcset="hero-mobile-portrait.jpg"
          type="image/jpeg">

  <!-- Tablet: Square crop -->
  <source media="(min-width: 768px) and (max-width: 1023px)"
          srcset="hero-tablet-square.jpg"
          type="image/jpeg">

  <!-- Desktop: Full landscape scene -->
  <img src="hero-desktop-landscape.jpg"
       alt="Team brainstorming in creative studio"
       width="1920"
       height="800">
</picture>
```

### Example 3: Responsive + Format + Density
```html
<picture>
  <!-- Mobile, WebP, 1x and 2x -->
  <source media="(max-width: 767px)"
          srcset="mobile-1x.webp 1x, mobile-2x.webp 2x"
          type="image/webp">

  <!-- Mobile, JPEG fallback -->
  <source media="(max-width: 767px)"
          srcset="mobile-1x.jpg 1x, mobile-2x.jpg 2x">

  <!-- Desktop, WebP, 1x and 2x -->
  <source srcset="desktop-1x.webp 1x, desktop-2x.webp 2x"
          type="image/webp">

  <!-- Desktop, JPEG fallback -->
  <img src="desktop-1x.jpg"
       srcset="desktop-1x.jpg 1x, desktop-2x.jpg 2x"
       alt="Product showcase"
       width="1200"
       height="800">
</picture>
```

### Example 4: Dark Mode Support
```html
<picture>
  <!-- Dark mode version -->
  <source srcset="logo-dark.svg"
          media="(prefers-color-scheme: dark)">

  <!-- Light mode version (default) -->
  <img src="logo-light.svg"
       alt="Company logo"
       width="200"
       height="60">
</picture>
```

### Example 5: Product Grid with Modern Formats
```html
<div class="product-grid">
  <div class="product">
    <picture>
      <source srcset="product-1.avif" type="image/avif">
      <source srcset="product-1.webp" type="image/webp">
      <img src="product-1.jpg"
           alt="Blue wireless headphones"
           width="400"
           height="400"
           loading="lazy">
    </picture>
    <h3>Wireless Headphones</h3>
    <p>$99.99</p>
  </div>
</div>
```

## Picture vs img with srcset

### When to use `<picture>`:
- ✅ Art direction (different crops/compositions)
- ✅ Format fallbacks (AVIF → WebP → JPEG)
- ✅ Complex media query logic
- ✅ Different aspect ratios per viewport

### When to use `<img>` with srcset:
- ✅ Same image, different sizes/resolutions
- ✅ Simple responsive images
- ✅ Less complex markup needed

**Example comparison:**

```html
<!-- img with srcset (simpler, same image different sizes) -->
<img src="photo-800.jpg"
     srcset="photo-400.jpg 400w,
             photo-800.jpg 800w,
             photo-1200.jpg 1200w"
     sizes="(max-width: 600px) 400px,
            (max-width: 1000px) 800px,
            1200px"
     alt="Landscape photo">

<!-- picture (art direction, different crops) -->
<picture>
  <source media="(max-width: 600px)" srcset="photo-mobile-portrait.jpg">
  <source media="(max-width: 1000px)" srcset="photo-tablet-square.jpg">
  <img src="photo-desktop-landscape.jpg" alt="Landscape photo">
</picture>
```

## Accessibility

Always include proper alt text on the `<img>` element:

```html
<picture>
  <source srcset="banner.webp" type="image/webp">
  <img src="banner.jpg"
       alt="Summer sale: 50% off all items, limited time offer"
       width="1200"
       height="400">
</picture>
```

**Decorative images:**
```html
<picture>
  <source srcset="decorative.webp" type="image/webp">
  <img src="decorative.jpg" alt="" width="800" height="200">
</picture>
```

## Performance Best Practices

1. **Order matters**: Place most efficient formats first (AVIF before WebP)
2. **Include dimensions**: Always add width/height to prevent layout shift
3. **Lazy load**: Use `loading="lazy"` for below-the-fold images
4. **Optimize all formats**: Compress JPEG fallbacks too
5. **Test format support**: Verify formats work in target browsers
6. **Use async decoding**: Add `decoding="async"` for better performance

```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg"
       alt="Optimized image"
       width="800"
       height="600"
       loading="lazy"
       decoding="async">
</picture>
```

## Browser Support

- **`<picture>` element**: All modern browsers (Chrome 38+, Firefox 38+, Safari 9.1+, Edge 13+)
- **AVIF format**: Chrome 85+, Firefox 93+, Safari 16+ (2022)
- **WebP format**: Chrome 32+, Firefox 65+, Safari 14+ (2020)

**Fallback strategy ensures images work in all browsers.**

## Common Mistakes

❌ **Missing img element**
```html
<picture>
  <source srcset="image.webp" type="image/webp">
  <!-- Missing img! -->
</picture>
```

✅ **Always include img**
```html
<picture>
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Description">
</picture>
```

---

❌ **Wrong attribute order (media after non-media)**
```html
<picture>
  <source srcset="desktop.jpg">
  <source media="(max-width: 600px)" srcset="mobile.jpg"> <!-- Too late! -->
  <img src="default.jpg" alt="Image">
</picture>
```

✅ **Most specific first**
```html
<picture>
  <source media="(max-width: 600px)" srcset="mobile.jpg">
  <source srcset="desktop.jpg">
  <img src="default.jpg" alt="Image">
</picture>
```

---

❌ **Alt on source instead of img**
```html
<picture>
  <source srcset="image.webp" type="image/webp" alt="Wrong place">
  <img src="image.jpg">
</picture>
```

✅ **Alt on img element**
```html
<picture>
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Correct place">
</picture>
```

## Practice Exercise

Create a responsive hero section with:
1. Different image crops for mobile (portrait), tablet (square), desktop (landscape)
2. Modern format support (WebP with JPEG fallback)
3. Proper alt text and dimensions
4. Overlay text with heading and call-to-action

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Hero Section</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
    }

    .hero {
      position: relative;
      width: 100%;
      min-height: 400px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }

    .hero picture {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 1;
    }

    .hero img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .hero-content {
      position: relative;
      z-index: 2;
      text-align: center;
      color: white;
      padding: 20px;
      max-width: 800px;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.7);
    }

    .hero h1 {
      font-size: clamp(2rem, 5vw, 4rem);
      margin-bottom: 20px;
      font-weight: bold;
    }

    .hero p {
      font-size: clamp(1rem, 2vw, 1.5rem);
      margin-bottom: 30px;
    }

    .cta-button {
      display: inline-block;
      padding: 15px 40px;
      background: #ff6b6b;
      color: white;
      text-decoration: none;
      border-radius: 50px;
      font-size: 1.1rem;
      font-weight: bold;
      transition: transform 0.3s, box-shadow 0.3s;
      box-shadow: 0 4px 15px rgba(255,107,107,0.4);
    }

    .cta-button:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 20px rgba(255,107,107,0.6);
    }

    /* Dark overlay for better text readability */
    .hero::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.4);
      z-index: 1;
    }
  </style>
</head>
<body>
  <section class="hero">
    <picture>
      <!-- Mobile: Portrait crop (600x800) - Focus on person -->
      <source media="(max-width: 767px)"
              srcset="hero-mobile-portrait.webp"
              type="image/webp">
      <source media="(max-width: 767px)"
              srcset="hero-mobile-portrait.jpg">

      <!-- Tablet: Square crop (1024x1024) -->
      <source media="(min-width: 768px) and (max-width: 1023px)"
              srcset="hero-tablet-square.webp"
              type="image/webp">
      <source media="(min-width: 768px) and (max-width: 1023px)"
              srcset="hero-tablet-square.jpg">

      <!-- Desktop: Landscape crop (1920x800) - Full scene -->
      <source srcset="hero-desktop-landscape.webp" type="image/webp">

      <!-- Fallback -->
      <img src="hero-desktop-landscape.jpg"
           alt="Modern creative workspace with team collaborating"
           width="1920"
           height="800">
    </picture>

    <div class="hero-content">
      <h1>Transform Your Workspace</h1>
      <p>Discover innovative solutions for modern teams</p>
      <a href="#learn-more" class="cta-button">Get Started</a>
    </div>
  </section>

  <main style="padding: 40px 20px; max-width: 1200px; margin: 0 auto;">
    <h2>Welcome to Our Platform</h2>
    <p>Below the hero section, your main content continues...</p>
  </main>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [The Picture element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)
- **W3Schools**: [HTML picture Element](https://www.w3schools.com/tags/tag_picture.asp)
- **Web.dev**: [Use WebP images](https://web.dev/serve-images-webp/)
- **CSS-Tricks**: [A Guide to the Responsive Images Syntax](https://css-tricks.com/a-guide-to-the-responsive-images-syntax-in-html/)

---

**Previous Topic**: [Images](./images.md)
**Next Topic**: [Figure and Figcaption](./figure-figcaption.md)
**Category**: [Media Elements](./README.md)
