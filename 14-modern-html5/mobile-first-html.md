---
title: Mobile-First HTML
category: Modern HTML5
order: 3
---

# Mobile-First HTML

> **Quick Summary:** Mobile-first design starts with mobile layouts and progressively enhances for larger screens, ensuring optimal performance on constrained devices.

## Why Mobile-First?

- **Mobile traffic:** >60% of web traffic is mobile
- **Performance:** Mobile devices have slower CPUs, less RAM, slower networks
- **Constraints breed creativity:** Designing for small screens forces clarity

---

## Mobile-First Principles

### 1. Viewport Meta Tag

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

**Without it:** Mobile browsers zoom out to desktop width (980px)
**With it:** Page width = device width

### 2. Touch-Friendly Targets

```html
<!-- ✅ Minimum 44x44px touch target -->
<button style="min-width: 44px; min-height: 44px;">
  Tap Me
</button>

<!-- ❌ Too small -->
<button style="width: 20px; height: 20px;">×</button>
```

### 3. Readable Text Sizes

```html
<style>
body {
  font-size: 16px; /* Minimum for mobile readability */
  line-height: 1.5;
}
</style>
```

---

## Responsive Images

### Picture Element

```html
<picture>
  <source media="(min-width: 1024px)" srcset="large.jpg">
  <source media="(min-width: 768px)" srcset="medium.jpg">
  <img src="small.jpg" alt="Responsive image">
</picture>
```

### Srcset for Resolution

```html
<img src="photo-1x.jpg"
     srcset="photo-1x.jpg 1x, photo-2x.jpg 2x, photo-3x.jpg 3x"
     alt="High DPI image">
```

---

## Mobile Navigation Patterns

### Hamburger Menu

```html
<nav>
  <button aria-label="Toggle menu" aria-expanded="false" onclick="toggleMenu()">
    ☰
  </button>

  <ul id="menu" hidden>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>

<script>
function toggleMenu() {
  const menu = document.getElementById('menu');
  const button = document.querySelector('[aria-label="Toggle menu"]');
  const isExpanded = button.getAttribute('aria-expanded') === 'true';

  menu.hidden = isExpanded;
  button.setAttribute('aria-expanded', !isExpanded);
}
</script>
```

---

## Mobile Performance

### Lazy Load Offscreen Content

```html
<img src="hero.jpg" alt="Hero" loading="eager"> <!-- Above fold -->
<img src="feature1.jpg" alt="Feature" loading="lazy"> <!-- Below fold -->
```

### Minimize Initial HTML

```html
<!-- ✅ GOOD - Load critical content first -->
<main>
  <h1>Page Title</h1>
  <p>First paragraph...</p>
</main>

<!-- Defer loading footer -->
<footer id="footer-placeholder"></footer>
<script>
  window.addEventListener('load', () => {
    document.getElementById('footer-placeholder').innerHTML = `<p>Footer content</p>`;
  });
</script>
```

---

## Mobile Form Best Practices

### Input Types for Mobile Keyboards

```html
<!-- Email keyboard (shows @ symbol) -->
<input type="email">

<!-- Numeric keyboard -->
<input type="tel">
<input type="number">

<!-- URL keyboard (shows .com) -->
<input type="url">
```

### Autocomplete

```html
<input type="text" name="name" autocomplete="name">
<input type="email" name="email" autocomplete="email">
<input type="tel" name="phone" autocomplete="tel">
```

---

## Testing Mobile-First

1. **Chrome DevTools:** Toggle device toolbar (Ctrl+Shift+M)
2. **Responsive Design Mode:** Test various screen sizes
3. **Throttle Network:** Simulate 3G
4. **Real Devices:** Test on actual phones/tablets

---

## Related Topics

- [Responsive Images](../04-media-elements/picture-element.md)
- [Performance Optimization](performance-optimization.md)
- [Progressive Enhancement](progressive-enhancement.md)

---

**Last Updated:** November 18, 2025
**Category:** Modern HTML5
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
