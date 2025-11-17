# Images in HTML5

## Overview
The `<img>` element embeds images into HTML documents. It's a void (self-closing) element that requires the `src` attribute to specify the image source and the `alt` attribute for accessibility.

## Basic Syntax

```html
<img src="path/to/image.jpg" alt="Description of image">
```

## Essential Attributes

### src (Required)
Specifies the image source URL (relative or absolute path).

```html
<!-- Relative path -->
<img src="images/logo.png" alt="Company Logo">

<!-- Absolute path -->
<img src="https://example.com/images/photo.jpg" alt="Photo">

<!-- Root-relative path -->
<img src="/assets/banner.jpg" alt="Banner">
```

### alt (Required)
Provides alternative text for screen readers and when images fail to load.

```html
<!-- Decorative image (empty alt) -->
<img src="decorative-border.png" alt="">

<!-- Functional image -->
<img src="search-icon.png" alt="Search">

<!-- Informative image -->
<img src="graph.png" alt="Sales increased 45% in Q4 2024">
```

**Alt Text Best Practices:**
- Be concise but descriptive
- Don't start with "image of" or "picture of"
- For decorative images, use empty alt (`alt=""`)
- For functional images (buttons, links), describe the action
- For complex images (charts, diagrams), provide detailed description

## Common Attributes

### width and height
Specify image dimensions in pixels (helps prevent layout shift).

```html
<img src="photo.jpg" alt="Mountain landscape" width="800" height="600">
```

**Benefits:**
- Browser reserves space before image loads
- Prevents Cumulative Layout Shift (CLS)
- Improves Core Web Vitals scores

### title
Provides advisory information (displays as tooltip on hover).

```html
<img src="logo.png" alt="Acme Corp" title="Acme Corporation - Since 1985">
```

**Note:** `title` should supplement, not replace `alt` text.

### loading (HTML5)
Controls lazy loading behavior.

```html
<!-- Lazy load (default for off-screen images) -->
<img src="large-image.jpg" alt="Detailed view" loading="lazy">

<!-- Eager load (load immediately) -->
<img src="hero-banner.jpg" alt="Welcome banner" loading="eager">
```

**When to use:**
- `loading="lazy"`: Below-the-fold images, image galleries
- `loading="eager"`: Above-the-fold critical images

### decoding
Hints at image decoding preference.

```html
<!-- Asynchronous decoding (better for large images) -->
<img src="large-photo.jpg" alt="High-res photo" decoding="async">

<!-- Synchronous decoding (default) -->
<img src="small-icon.png" alt="Icon" decoding="sync">

<!-- Auto (browser decides) -->
<img src="image.jpg" alt="Image" decoding="auto">
```

## Responsive Images

### Using CSS
```html
<img src="photo.jpg" alt="Responsive photo" style="max-width: 100%; height: auto;">
```

### Using srcset (Better approach)
```html
<img src="image-800.jpg"
     srcset="image-400.jpg 400w,
             image-800.jpg 800w,
             image-1200.jpg 1200w"
     sizes="(max-width: 600px) 400px,
            (max-width: 1000px) 800px,
            1200px"
     alt="Responsive image">
```

**How it works:**
- `srcset`: List of image sources with width descriptors
- `sizes`: Media conditions and image display sizes
- Browser selects appropriate image based on viewport and pixel density

## Image Formats

| Format | Use Case | Transparency | Animation |
|--------|----------|--------------|-----------|
| **JPEG** | Photos, complex images | ❌ No | ❌ No |
| **PNG** | Graphics, logos, icons | ✅ Yes | ❌ No |
| **GIF** | Simple animations | ✅ Yes | ✅ Yes |
| **SVG** | Vector graphics, icons | ✅ Yes | ✅ Yes (CSS/JS) |
| **WebP** | Modern replacement (smaller files) | ✅ Yes | ✅ Yes |
| **AVIF** | Next-gen format (best compression) | ✅ Yes | ✅ Yes |

### Format Selection Guide
```html
<!-- Photo -->
<img src="photo.jpg" alt="Landscape photo">

<!-- Logo with transparency -->
<img src="logo.png" alt="Company logo">

<!-- Icon (best as SVG) -->
<img src="icon.svg" alt="Menu icon">

<!-- Modern format with fallback -->
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Fallback image">
</picture>
```

## Accessibility Considerations

### Informative Images
```html
<img src="warning.png" alt="Warning: This action cannot be undone">
```

### Functional Images (in links/buttons)
```html
<a href="home.html">
  <img src="home-icon.png" alt="Go to homepage">
</a>

<button>
  <img src="delete-icon.png" alt="Delete item">
</button>
```

### Decorative Images
```html
<!-- Use empty alt for purely decorative images -->
<img src="decorative-divider.png" alt="">
```

### Complex Images
```html
<!-- Link to long description -->
<img src="complex-chart.png"
     alt="Sales performance chart showing 45% growth"
     longdesc="chart-description.html">

<!-- Or use adjacent text -->
<img src="diagram.png" alt="Network architecture diagram">
<p>The diagram shows three layers: presentation, business logic, and data...</p>
```

## Common Use Cases

### Logo
```html
<img src="logo.png" alt="Acme Corporation" width="150" height="50">
```

### Profile Picture
```html
<img src="avatar.jpg" alt="Jane Doe profile picture" width="100" height="100">
```

### Product Image
```html
<img src="product-001.jpg"
     alt="Blue wireless headphones with noise cancellation"
     width="400"
     height="400"
     loading="lazy">
```

### Icon
```html
<img src="icon-email.svg" alt="Email" width="24" height="24">
```

### Banner/Hero Image
```html
<img src="hero-banner.jpg"
     alt="Team collaborating in modern office"
     width="1920"
     height="600"
     loading="eager">
```

## Image Performance Tips

1. **Optimize file size**: Compress images before upload
2. **Use appropriate format**: WebP/AVIF for modern browsers
3. **Specify dimensions**: Always include width/height
4. **Lazy load**: Use `loading="lazy"` for below-the-fold images
5. **Use srcset**: Provide multiple resolutions for responsive design
6. **Use CDN**: Serve images from Content Delivery Network
7. **Cache images**: Set proper cache headers

## Common Mistakes to Avoid

❌ **Missing alt attribute**
```html
<img src="photo.jpg">
```

✅ **Always include alt**
```html
<img src="photo.jpg" alt="Mountain landscape at sunset">
```

---

❌ **Using wrong image format**
```html
<img src="logo.jpg" alt="Logo"> <!-- JPEG doesn't support transparency -->
```

✅ **Use PNG or SVG for logos**
```html
<img src="logo.png" alt="Logo">
```

---

❌ **Not specifying dimensions**
```html
<img src="large-image.jpg" alt="Photo">
```

✅ **Include width/height**
```html
<img src="large-image.jpg" alt="Photo" width="800" height="600">
```

---

❌ **Redundant alt text**
```html
<img src="photo.jpg" alt="Image of a photo of a mountain">
```

✅ **Concise alt text**
```html
<img src="photo.jpg" alt="Mountain at sunset">
```

## Browser Support
- **`<img>` element**: Universal support (all browsers)
- **`loading` attribute**: Modern browsers (Chrome 77+, Firefox 75+, Safari 15.4+)
- **`decoding` attribute**: Chrome 65+, Firefox 63+, Safari 11.1+
- **`srcset`/`sizes`**: All modern browsers

## Practice Exercise

Create a photo gallery page with:
1. Gallery title
2. 6 images in 2 rows (3 columns each)
3. Responsive images using srcset
4. Lazy loading for all images
5. Proper alt text
6. Fixed dimensions to prevent layout shift

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Photo Gallery</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
    }

    h1 {
      text-align: center;
      color: #333;
    }

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 20px;
      margin-top: 30px;
    }

    .gallery-item {
      border: 1px solid #ddd;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }

    .gallery-item:hover {
      transform: translateY(-5px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    .gallery-item img {
      width: 100%;
      height: auto;
      display: block;
    }

    .gallery-item figcaption {
      padding: 15px;
      text-align: center;
      background: #f9f9f9;
      color: #555;
    }
  </style>
</head>
<body>
  <h1>Nature Photography Gallery</h1>

  <div class="gallery">
    <figure class="gallery-item">
      <img src="images/mountain-400.jpg"
           srcset="images/mountain-400.jpg 400w,
                   images/mountain-800.jpg 800w"
           sizes="(max-width: 600px) 400px, 800px"
           alt="Snow-capped mountain peak at sunrise"
           width="800"
           height="600"
           loading="lazy">
      <figcaption>Mountain Sunrise</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="images/forest-400.jpg"
           srcset="images/forest-400.jpg 400w,
                   images/forest-800.jpg 800w"
           sizes="(max-width: 600px) 400px, 800px"
           alt="Dense forest with sunlight filtering through trees"
           width="800"
           height="600"
           loading="lazy">
      <figcaption>Forest Light</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="images/ocean-400.jpg"
           srcset="images/ocean-400.jpg 400w,
                   images/ocean-800.jpg 800w"
           sizes="(max-width: 600px) 400px, 800px"
           alt="Ocean waves crashing on rocky shore"
           width="800"
           height="600"
           loading="lazy">
      <figcaption>Coastal Waves</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="images/desert-400.jpg"
           srcset="images/desert-400.jpg 400w,
                   images/desert-800.jpg 800w"
           sizes="(max-width: 600px) 400px, 800px"
           alt="Sand dunes in the desert at golden hour"
           width="800"
           height="600"
           loading="lazy">
      <figcaption>Desert Dunes</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="images/waterfall-400.jpg"
           srcset="images/waterfall-400.jpg 400w,
                   images/waterfall-800.jpg 800w"
           sizes="(max-width: 600px) 400px, 800px"
           alt="Waterfall cascading into crystal clear pool"
           width="800"
           height="600"
           loading="lazy">
      <figcaption>Hidden Waterfall</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="images/canyon-400.jpg"
           srcset="images/canyon-400.jpg 400w,
                   images/canyon-800.jpg 800w"
           sizes="(max-width: 600px) 400px, 800px"
           alt="Red rock canyon with dramatic shadows"
           width="800"
           height="600"
           loading="lazy">
      <figcaption>Canyon Shadows</figcaption>
    </figure>
  </div>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [The Image Embed element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)
- **W3Schools**: [HTML Images](https://www.w3schools.com/html/html_images.asp)
- **WebAIM**: [Alternative Text](https://webaim.org/techniques/alttext/)
- **Web.dev**: [Image Optimization](https://web.dev/fast/#optimize-your-images)

---

**Previous Topic**: [Download Links](../03-links-navigation/download-links.md)
**Next Topic**: [Picture Element](./picture-element.md)
**Category**: [Media Elements](./README.md)
