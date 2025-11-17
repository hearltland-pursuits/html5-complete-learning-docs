# Lazy Loading Images and Media

## Overview
Lazy loading is a performance optimization technique that defers loading of images and other media until they're needed (typically when they enter the viewport). This significantly improves initial page load time and reduces bandwidth usage.

## Native Lazy Loading

### The loading Attribute

HTML5 provides a native `loading` attribute for `<img>` and `<iframe>` elements.

```html
<img src="image.jpg" alt="Description" loading="lazy">
```

**Values:**
- `lazy`: Load when near viewport (deferred loading)
- `eager`: Load immediately (default behavior)
- `auto`: Browser decides (default)

### Image Lazy Loading

```html
<!-- Lazy load -->
<img src="photo.jpg"
     alt="Landscape photo"
     width="800"
     height="600"
     loading="lazy">

<!-- Eager load (above-the-fold content) -->
<img src="hero-banner.jpg"
     alt="Hero banner"
     width="1920"
     height="800"
     loading="eager">
```

### Iframe Lazy Loading

```html
<!-- Lazy load YouTube embed -->
<iframe src="https://www.youtube.com/embed/VIDEO_ID"
        width="560"
        height="315"
        title="Video title"
        loading="lazy">
</iframe>

<!-- Lazy load external content -->
<iframe src="https://example.com/widget"
        width="400"
        height="300"
        loading="lazy">
</iframe>
```

## When to Use Lazy Loading

### ✅ Use lazy loading for:
- Images below the fold
- Gallery/carousel images
- Long-form content with many images
- User-generated content
- Third-party embeds (ads, social media)
- Product listings
- Infinite scroll implementations

### ❌ Don't use lazy loading for:
- Hero images (above the fold)
- Logo
- Critical UI elements
- First few images on page
- Small images (<10KB)

### Example: Strategic Loading

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Strategic Lazy Loading</title>
</head>
<body>
  <!-- Hero: Eager load (critical content) -->
  <header>
    <img src="hero.jpg"
         alt="Welcome banner"
         width="1920"
         height="800"
         loading="eager">
  </header>

  <!-- Logo: Eager load (always visible) -->
  <nav>
    <img src="logo.png"
         alt="Company logo"
         width="150"
         height="50"
         loading="eager">
  </nav>

  <!-- Main content: Lazy load (below fold) -->
  <main>
    <article>
      <img src="article-image-1.jpg"
           alt="Article image"
           width="800"
           height="600"
           loading="lazy">

      <img src="article-image-2.jpg"
           alt="Article image"
           width="800"
           height="600"
           loading="lazy">
    </article>
  </main>

  <!-- Footer: Lazy load (far below fold) -->
  <footer>
    <img src="footer-banner.jpg"
         alt="Footer banner"
         width="1200"
         height="300"
         loading="lazy">
  </footer>
</body>
</html>
```

## Best Practices

### 1. Always Specify Dimensions

Prevents layout shift when images load.

```html
<!-- ❌ Bad: No dimensions -->
<img src="photo.jpg" alt="Photo" loading="lazy">

<!-- ✅ Good: Include dimensions -->
<img src="photo.jpg"
     alt="Photo"
     width="800"
     height="600"
     loading="lazy">
```

### 2. Use with Responsive Images

```html
<img src="image-800.jpg"
     srcset="image-400.jpg 400w,
             image-800.jpg 800w,
             image-1200.jpg 1200w"
     sizes="(max-width: 600px) 400px,
            (max-width: 1000px) 800px,
            1200px"
     alt="Responsive image"
     width="1200"
     height="800"
     loading="lazy">
```

### 3. Combine with Modern Formats

```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg"
       alt="Modern format with lazy loading"
       width="800"
       height="600"
       loading="lazy">
</picture>
```

### 4. Add Placeholder or Background Color

Prevents empty space while loading.

```html
<img src="photo.jpg"
     alt="Photo"
     width="800"
     height="600"
     loading="lazy"
     style="background: #f0f0f0;">
```

### 5. Use Low-Quality Image Placeholders (LQIP)

```html
<style>
  .lazy-img {
    background-size: cover;
    background-position: center;
  }
</style>

<img src="high-quality.jpg"
     alt="Photo"
     width="800"
     height="600"
     loading="lazy"
     class="lazy-img"
     style="background-image: url('tiny-placeholder.jpg');">
```

## JavaScript Lazy Loading (Polyfill)

For older browsers that don't support native lazy loading.

### Using Intersection Observer API

```html
<img data-src="image1.jpg" alt="Image 1" class="lazy" width="800" height="600">
<img data-src="image2.jpg" alt="Image 2" class="lazy" width="800" height="600">
<img data-src="image3.jpg" alt="Image 3" class="lazy" width="800" height="600">

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Check for native lazy loading support
  if ('loading' in HTMLImageElement.prototype) {
    // Native lazy loading supported
    const images = document.querySelectorAll('img[data-src]');
    images.forEach(img => {
      img.src = img.dataset.src;
      img.loading = 'lazy';
    });
  } else {
    // Fallback to Intersection Observer
    const images = document.querySelectorAll('img[data-src]');

    const imageObserver = new IntersectionObserver((entries, observer) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          const img = entry.target;
          img.src = img.dataset.src;
          img.classList.remove('lazy');
          imageObserver.unobserve(img);
        }
      });
    });

    images.forEach(img => imageObserver.observe(img));
  }
});
</script>
```

### Advanced: Fade-in Effect

```html
<style>
  .lazy {
    opacity: 0;
    transition: opacity 0.3s;
  }

  .lazy.loaded {
    opacity: 1;
  }
</style>

<img data-src="image.jpg"
     alt="Image"
     class="lazy"
     width="800"
     height="600"
     style="background: #f0f0f0;">

<script>
const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;

      img.addEventListener('load', () => {
        img.classList.add('loaded');
      });

      imageObserver.unobserve(img);
    }
  });
}, {
  rootMargin: '50px' // Start loading 50px before entering viewport
});

document.querySelectorAll('img[data-src]').forEach(img => {
  imageObserver.observe(img);
});
</script>
```

## Lazy Loading Libraries

### lazysizes (Popular Library)

```html
<!-- Include library -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/lazysizes/5.3.2/lazysizes.min.js" async></script>

<!-- Use data-src and lazyload class -->
<img data-src="image.jpg"
     alt="Image"
     class="lazyload"
     width="800"
     height="600">

<!-- With responsive images -->
<img data-srcset="image-400.jpg 400w,
                  image-800.jpg 800w,
                  image-1200.jpg 1200w"
     data-sizes="auto"
     alt="Responsive lazy image"
     class="lazyload">
```

### lozad.js (Lightweight)

```html
<script src="https://cdn.jsdelivr.net/npm/lozad/dist/lozad.min.js"></script>

<img class="lozad" data-src="image.jpg" alt="Image">

<script>
const observer = lozad();
observer.observe();
</script>
```

### vanilla-lazyload

```html
<script src="https://cdn.jsdelivr.net/npm/vanilla-lazyload@17/dist/lazyload.min.js"></script>

<img class="lazy" data-src="image.jpg" alt="Image">

<script>
new LazyLoad({
  elements_selector: ".lazy"
});
</script>
```

## Complete Examples

### Photo Gallery with Lazy Loading

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lazy Loading Photo Gallery</title>
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
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 20px;
      margin-top: 30px;
    }

    .gallery-item {
      position: relative;
      overflow: hidden;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }

    .gallery-item:hover {
      transform: translateY(-5px);
    }

    .gallery-item img {
      width: 100%;
      height: 250px;
      object-fit: cover;
      display: block;
      background: #f0f0f0;
    }

    .gallery-item figcaption {
      padding: 15px;
      background: white;
      text-align: center;
      color: #555;
    }
  </style>
</head>
<body>
  <h1>Nature Photography Gallery</h1>
  <p style="text-align: center; color: #666;">
    All images are lazy loaded for optimal performance
  </p>

  <div class="gallery">
    <!-- First 2 images: eager load (above fold) -->
    <figure class="gallery-item">
      <img src="image1.jpg"
           alt="Mountain landscape"
           width="400"
           height="250"
           loading="eager">
      <figcaption>Mountain Peak</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="image2.jpg"
           alt="Forest trail"
           width="400"
           height="250"
           loading="eager">
      <figcaption>Forest Path</figcaption>
    </figure>

    <!-- Rest: lazy load -->
    <figure class="gallery-item">
      <img src="image3.jpg"
           alt="Ocean sunset"
           width="400"
           height="250"
           loading="lazy">
      <figcaption>Ocean Sunset</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="image4.jpg"
           alt="Desert dunes"
           width="400"
           height="250"
           loading="lazy">
      <figcaption>Desert Dunes</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="image5.jpg"
           alt="Waterfall"
           width="400"
           height="250"
           loading="lazy">
      <figcaption>Waterfall</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="image6.jpg"
           alt="Snowy mountain"
           width="400"
           height="250"
           loading="lazy">
      <figcaption>Snow Peak</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="image7.jpg"
           alt="Tropical beach"
           width="400"
           height="250"
           loading="lazy">
      <figcaption>Tropical Beach</figcaption>
    </figure>

    <figure class="gallery-item">
      <img src="image8.jpg"
           alt="Canyon view"
           width="400"
           height="250"
           loading="lazy">
      <figcaption>Grand Canyon</figcaption>
    </figure>
  </div>
</body>
</html>
```

### Blog Post with Lazy Images

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog Post with Lazy Loading</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
      color: #333;
    }

    h1 {
      font-size: 2.5rem;
      margin-bottom: 10px;
    }

    .meta {
      color: #666;
      margin-bottom: 30px;
    }

    article img {
      width: 100%;
      height: auto;
      border-radius: 8px;
      margin: 30px 0;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      background: #f0f0f0;
    }

    figure {
      margin: 40px 0;
    }

    figcaption {
      text-align: center;
      font-style: italic;
      color: #666;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <article>
    <h1>The Art of Landscape Photography</h1>
    <p class="meta">Published on January 15, 2024 | By Jane Doe</p>

    <!-- Hero image: Eager load -->
    <figure>
      <img src="hero-landscape.jpg"
           alt="Stunning mountain landscape at golden hour"
           width="800"
           height="500"
           loading="eager">
      <figcaption>Golden hour in the Rockies</figcaption>
    </figure>

    <p>
      Landscape photography is about capturing the beauty of nature in its
      purest form. From towering mountains to serene coastlines, every
      landscape tells a unique story...
    </p>

    <!-- Content images: Lazy load -->
    <figure>
      <img src="image-composition.jpg"
           alt="Example of rule of thirds in landscape photo"
           width="800"
           height="500"
           loading="lazy">
      <figcaption>Rule of thirds composition technique</figcaption>
    </figure>

    <p>
      Understanding composition is crucial. The rule of thirds helps create
      balanced and visually appealing images...
    </p>

    <figure>
      <img src="image-lighting.jpg"
           alt="Different lighting conditions in landscape photography"
           width="800"
           height="500"
           loading="lazy">
      <figcaption>Importance of lighting in landscape photography</figcaption>
    </figure>

    <p>
      Lighting can make or break your landscape photos. The golden hours—just
      after sunrise and before sunset—provide the most dramatic lighting...
    </p>

    <figure>
      <img src="image-equipment.jpg"
           alt="Camera equipment for landscape photography"
           width="800"
           height="500"
           loading="lazy">
      <figcaption>Essential equipment for landscape photographers</figcaption>
    </figure>

    <p>
      You don't need expensive equipment to start. A basic DSLR or mirrorless
      camera with a wide-angle lens is sufficient for beginners...
    </p>
  </article>
</body>
</html>
```

### E-commerce Product Grid

```html
<div class="product-grid">
  <!-- First row: Eager load -->
  <div class="product">
    <img src="product-1.jpg"
         alt="Wireless headphones"
         width="300"
         height="300"
         loading="eager">
    <h3>Wireless Headphones</h3>
    <p>$99.99</p>
  </div>

  <div class="product">
    <img src="product-2.jpg"
         alt="Smartwatch"
         width="300"
         height="300"
         loading="eager">
    <h3>Smartwatch Pro</h3>
    <p>$299.99</p>
  </div>

  <!-- Remaining products: Lazy load -->
  <div class="product">
    <img src="product-3.jpg"
         alt="Bluetooth speaker"
         width="300"
         height="300"
         loading="lazy">
    <h3>Portable Speaker</h3>
    <p>$79.99</p>
  </div>

  <!-- ... 20 more products with loading="lazy" ... -->
</div>
```

## Performance Impact

### Benefits of Lazy Loading

1. **Faster initial page load**: Only critical images load immediately
2. **Reduced bandwidth**: Don't load images user never sees
3. **Better Core Web Vitals**: Improves LCP, FID, CLS scores
4. **Lower server load**: Fewer simultaneous image requests
5. **Improved mobile experience**: Saves data on cellular connections

### Metrics Improvement

**Before lazy loading:**
- Initial load: 5.2s
- Images loaded: 50
- Data transferred: 15 MB
- LCP: 4.1s

**After lazy loading:**
- Initial load: 1.8s
- Images loaded: 8
- Data transferred: 3.2 MB
- LCP: 1.2s

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `loading="lazy"` | ✅ 77+ | ✅ 75+ | ✅ 15.4+ | ✅ 79+ |
| Intersection Observer | ✅ 51+ | ✅ 55+ | ✅ 12.1+ | ✅ 15+ |

**Fallback strategy**: Use feature detection and polyfills for older browsers.

## Common Mistakes

❌ **Lazy loading above-the-fold content**
```html
<img src="hero.jpg" alt="Hero" loading="lazy"> <!-- Bad! -->
```

✅ **Eager load critical content**
```html
<img src="hero.jpg" alt="Hero" loading="eager">
```

---

❌ **No dimensions specified**
```html
<img src="photo.jpg" alt="Photo" loading="lazy">
```

✅ **Include width/height**
```html
<img src="photo.jpg" alt="Photo" width="800" height="600" loading="lazy">
```

---

❌ **Lazy loading tiny images**
```html
<img src="icon-16x16.png" alt="Icon" loading="lazy">
```

✅ **Eager load small images**
```html
<img src="icon-16x16.png" alt="Icon" loading="eager">
```

---

❌ **Lazy loading without background placeholder**
```html
<img src="large-photo.jpg" loading="lazy">
```

✅ **Add placeholder color**
```html
<img src="large-photo.jpg" loading="lazy" style="background: #f0f0f0;">
```

## Practice Exercise

Create a blog-style page with:
1. Hero image (eager loaded)
2. 10+ content images (lazy loaded)
3. Proper dimensions to prevent layout shift
4. Placeholder backgrounds
5. Performance optimization

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Travel Blog - Lazy Loading Demo</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
      line-height: 1.6;
      color: #333;
    }

    .hero {
      position: relative;
      height: 70vh;
      overflow: hidden;
    }

    .hero img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }

    .hero-content {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      color: white;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.7);
    }

    .hero h1 {
      font-size: 3rem;
      margin-bottom: 10px;
    }

    .container {
      max-width: 900px;
      margin: 0 auto;
      padding: 40px 20px;
    }

    .content-section {
      margin-bottom: 60px;
    }

    .content-section h2 {
      font-size: 2rem;
      margin-bottom: 20px;
      color: #2c3e50;
    }

    .content-section img {
      width: 100%;
      height: auto;
      border-radius: 12px;
      margin: 25px 0;
      box-shadow: 0 4px 16px rgba(0,0,0,0.1);
      background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
      background-size: 200% 100%;
    }

    .image-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      margin: 30px 0;
    }

    .image-grid img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 8px;
      background: #f0f0f0;
    }

    p {
      margin: 20px 0;
      font-size: 1.1rem;
      line-height: 1.8;
    }
  </style>
</head>
<body>
  <!-- Hero: Eager Load -->
  <section class="hero">
    <img src="hero-travel.jpg"
         alt="Aerial view of tropical island paradise"
         width="1920"
         height="1080"
         loading="eager">
    <div class="hero-content">
      <h1>Discover Paradise</h1>
      <p>Your ultimate travel guide to hidden gems</p>
    </div>
  </section>

  <!-- Main Content -->
  <div class="container">
    <article class="content-section">
      <h2>Exploring Tropical Beaches</h2>
      <p>
        The crystal-clear waters and white sandy beaches of the tropics offer
        an escape from everyday life. From the Maldives to Bali, these
        destinations promise unforgettable experiences...
      </p>

      <img src="beach-1.jpg"
           alt="Pristine white sand beach with turquoise water"
           width="900"
           height="600"
           loading="lazy">

      <p>
        Snorkeling in coral reefs reveals an underwater world teeming with
        colorful fish and marine life...
      </p>

      <img src="beach-2.jpg"
           alt="Snorkeling in coral reef"
           width="900"
           height="600"
           loading="lazy">
    </article>

    <article class="content-section">
      <h2>Mountain Adventures</h2>
      <p>
        The majesty of mountain ranges offers a different kind of beauty.
        Hiking trails wind through forests and alpine meadows...
      </p>

      <img src="mountain-1.jpg"
           alt="Hiker on mountain trail with scenic vista"
           width="900"
           height="600"
           loading="lazy">

      <div class="image-grid">
        <img src="mountain-2.jpg"
             alt="Mountain peak at sunrise"
             width="300"
             height="200"
             loading="lazy">
        <img src="mountain-3.jpg"
             alt="Alpine lake reflection"
             width="300"
             height="200"
             loading="lazy">
        <img src="mountain-4.jpg"
             alt="Mountain village"
             width="300"
             height="200"
             loading="lazy">
      </div>
    </article>

    <article class="content-section">
      <h2>Urban Explorations</h2>
      <p>
        Cities around the world offer unique cultural experiences, from
        historic landmarks to modern architecture...
      </p>

      <img src="city-1.jpg"
           alt="City skyline at dusk"
           width="900"
           height="600"
           loading="lazy">

      <div class="image-grid">
        <img src="city-2.jpg"
             alt="Historic temple"
             width="300"
             height="200"
             loading="lazy">
        <img src="city-3.jpg"
             alt="Street food market"
             width="300"
             height="200"
             loading="lazy">
        <img src="city-4.jpg"
             alt="Modern architecture"
             width="300"
             height="200"
             loading="lazy">
        <img src="city-5.jpg"
             alt="Night market"
             width="300"
             height="200"
             loading="lazy">
      </div>
    </article>
  </div>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [Lazy loading](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading)
- **Web.dev**: [Browser-level image lazy loading](https://web.dev/browser-level-image-lazy-loading/)
- **Can I Use**: [Loading attribute support](https://caniuse.com/loading-lazy-attr)
- **lazysizes**: [Popular lazy loading library](https://github.com/aFarkas/lazysizes)

---

**Previous Topic**: [Image Maps](./image-maps.md)
**Next Topic**: [Ordered Lists](../05-lists-tables/ordered-lists.md)
**Category**: [Media Elements](./README.md)
