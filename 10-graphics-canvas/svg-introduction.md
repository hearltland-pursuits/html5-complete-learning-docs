---
title: SVG Introduction
category: Graphics & Canvas
order: 23
---

# SVG Introduction

> **Quick Summary:** SVG (Scalable Vector Graphics) is an XML-based vector image format for 2D graphics. Unlike raster images (PNG, JPG), SVGs scale infinitely without quality loss, are editable with code, animatable with CSS/JavaScript, and accessible to screen readers. Perfect for logos, icons, charts, and illustrations.

## Table of Contents
- [Introduction](#introduction)
- [SVG vs Raster Images](#svg-vs-raster-images)
- [Basic SVG Structure](#basic-svg-structure)
- [Embedding SVG](#embedding-svg)
- [Basic Concepts](#basic-concepts)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

SVG (Scalable Vector Graphics) is a text-based vector graphics format defined in XML. SVGs are resolution-independent, meaning they look sharp at any size—from tiny icons to billboard-sized graphics.

**Key characteristics:**
- **Vector-based** - Defined by mathematical formulas, not pixels
- **Scalable** - No quality loss at any size
- **Code-editable** - Can manipulate with CSS and JavaScript
- **Accessible** - Screen readers can read SVG content
- **Small file size** - Often smaller than equivalent raster images
- **Animatable** - CSS animations and JavaScript work on SVG elements

**Key Concept:** Think of SVG like giving the browser instructions to draw shapes ("draw a circle with radius 50") vs. raster images which are pixel grids ("pixel 1,1 is red, pixel 1,2 is blue..."). SVG instructions scale perfectly; pixel grids get blurry when enlarged.

---

## SVG vs Raster Images

### Comparison Table

| Feature | SVG (Vector) | PNG/JPG (Raster) |
|---------|--------------|------------------|
| **Scalability** | ✅ Infinite, no quality loss | ❌ Blurry when scaled up |
| **File Size** | ✅ Small for simple graphics | ❌ Large for complex images |
| **Editing** | ✅ Edit with code/CSS/JS | ❌ Requires image editor |
| **Animation** | ✅ CSS/JS animations | ⚠️ Limited (CSS transforms only) |
| **Accessibility** | ✅ Screen reader compatible | ⚠️ Only via alt text |
| **SEO** | ✅ Text content indexable | ❌ Not indexable |
| **Best For** | Icons, logos, charts, illustrations | Photos, complex images |

### When to Use SVG

✅ **Use SVG for:**
- Logos and branding
- Icons and UI elements
- Charts and data visualizations
- Illustrations and diagrams
- Simple animations
- Responsive graphics that need to scale

❌ **Don't use SVG for:**
- Photographs (use JPG)
- Complex images with gradients/effects (use PNG)
- Very detailed illustrations (file size becomes large)

---

## Basic SVG Structure

### Inline SVG

```html
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <!-- SVG content goes here -->
  <circle cx="100" cy="100" r="80" fill="blue" />
</svg>
```

### SVG Anatomy

```html
<svg
  width="200"           <!-- Canvas width -->
  height="200"          <!-- Canvas height -->
  viewBox="0 0 200 200" <!-- Coordinate system (x y width height) -->
  xmlns="http://www.w3.org/2000/svg">

  <!-- Shapes, paths, text, etc. -->
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

### ViewBox Explained

The `viewBox` defines the coordinate system:

```html
<!-- viewBox="min-x min-y width height" -->

<!-- Full view -->
<svg viewBox="0 0 100 100" width="200" height="200">
  <circle cx="50" cy="50" r="40" fill="blue" />
</svg>

<!-- Zoomed in (smaller viewBox = zoomed) -->
<svg viewBox="25 25 50 50" width="200" height="200">
  <circle cx="50" cy="50" r="40" fill="blue" />
</svg>
```

---

## Embedding SVG

### Method 1: Inline SVG (Recommended)

```html
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" fill="red" />
</svg>
```

**Pros:**
- Full CSS/JavaScript control
- Animatable
- Accessible (can add `<title>` and `<desc>`)
- No HTTP request

**Cons:**
- Increases HTML file size
- Not cached separately

### Method 2: IMG Tag

```html
<img src="logo.svg" alt="Company Logo" width="200">
```

**Pros:**
- Cached separately
- Simple syntax
- Lazy loading supported

**Cons:**
- No CSS/JavaScript manipulation
- External HTTP request

### Method 3: CSS Background

```css
.logo {
  background-image: url('logo.svg');
  background-size: contain;
  width: 200px;
  height: 100px;
}
```

**Pros:**
- Cached separately
- Works in responsive designs

**Cons:**
- Not accessible (no alt text)
- No JavaScript manipulation

### Method 4: Object Tag

```html
<object type="image/svg+xml" data="logo.svg" width="200" height="100">
  Fallback text for non-SVG browsers
</object>
```

**Pros:**
- SVG's JavaScript can run
- Accessible

**Cons:**
- External HTTP request
- Limited browser support for manipulation

---

## Basic Concepts

### Coordinate System

```html
<!-- (0,0) is top-left corner -->
<svg width="200" height="200">
  <!-- x increases rightward, y increases downward -->
  <circle cx="50" cy="50" r="20" fill="red" />    <!-- Top-left -->
  <circle cx="150" cy="50" r="20" fill="blue" />  <!-- Top-right -->
  <circle cx="50" cy="150" r="20" fill="green" /> <!-- Bottom-left -->
  <circle cx="150" cy="150" r="20" fill="yellow" /><!-- Bottom-right -->
</svg>
```

### Basic Shapes

```html
<svg width="400" height="300">
  <!-- Rectangle -->
  <rect x="10" y="10" width="100" height="80" fill="red" />

  <!-- Circle -->
  <circle cx="170" cy="50" r="40" fill="blue" />

  <!-- Ellipse -->
  <ellipse cx="300" cy="50" rx="60" ry="40" fill="green" />

  <!-- Line -->
  <line x1="10" y1="120" x2="110" y2="120" stroke="black" stroke-width="2" />

  <!-- Polyline -->
  <polyline points="10,150 60,180 110,150" fill="none" stroke="purple" stroke-width="2" />

  <!-- Polygon (closed shape) -->
  <polygon points="200,150 250,200 150,200" fill="orange" />

  <!-- Text -->
  <text x="10" y="250" font-size="20" fill="black">SVG Text</text>
</svg>
```

### Styling SVG

```html
<!-- Inline styles -->
<circle cx="50" cy="50" r="40"
        fill="blue"
        stroke="black"
        stroke-width="2"
        opacity="0.5" />

<!-- CSS classes -->
<style>
  .my-circle {
    fill: blue;
    stroke: black;
    stroke-width: 2;
  }

  .my-circle:hover {
    fill: red;
  }
</style>

<svg width="200" height="200">
  <circle class="my-circle" cx="100" cy="100" r="80" />
</svg>
```

---

## Examples

### Example 1: Simple Icon

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>SVG Icon</title>
  <style>
    .icon {
      width: 50px;
      height: 50px;
      margin: 10px;
    }

    .icon:hover {
      transform: scale(1.2);
      transition: transform 0.2s;
    }
  </style>
</head>
<body>
  <h1>SVG Icons</h1>

  <!-- Heart icon -->
  <svg class="icon" viewBox="0 0 24 24" fill="red">
    <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
  </svg>

  <!-- Star icon -->
  <svg class="icon" viewBox="0 0 24 24" fill="gold">
    <polygon points="12,2 15,9 22,9 17,14 19,21 12,17 5,21 7,14 2,9 9,9"/>
  </svg>

  <!-- Check icon -->
  <svg class="icon" viewBox="0 0 24 24" fill="none" stroke="green" stroke-width="3">
    <polyline points="20,6 9,17 4,12"/>
  </svg>
</body>
</html>
```

### Example 2: Animated Logo

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Animated SVG Logo</title>
  <style>
    @keyframes rotate {
      from { transform: rotate(0deg); }
      to { transform: rotate(360deg); }
    }

    .rotating-circle {
      animation: rotate 3s linear infinite;
      transform-origin: center;
    }

    .pulsing-circle {
      animation: pulse 2s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { r: 30; opacity: 1; }
      50% { r: 35; opacity: 0.7; }
    }
  </style>
</head>
<body>
  <svg width="200" height="200" viewBox="0 0 200 200">
    <!-- Background circle -->
    <circle cx="100" cy="100" r="90" fill="#f0f0f0" stroke="#333" stroke-width="2"/>

    <!-- Rotating outer circles -->
    <g class="rotating-circle">
      <circle cx="100" cy="30" r="15" fill="#007bff"/>
      <circle cx="170" cy="100" r="15" fill="#28a745"/>
      <circle cx="100" cy="170" r="15" fill="#ffc107"/>
      <circle cx="30" cy="100" r="15" fill="#dc3545"/>
    </g>

    <!-- Center pulsing circle -->
    <circle class="pulsing-circle" cx="100" cy="100" r="30" fill="#6c757d"/>

    <!-- Text -->
    <text x="100" y="108" text-anchor="middle" font-size="24" fill="white" font-weight="bold">
      SVG
    </text>
  </svg>
</body>
</html>
```

### Example 3: Interactive Chart

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>SVG Bar Chart</title>
  <style>
    .bar {
      fill: #007bff;
      transition: fill 0.3s;
    }

    .bar:hover {
      fill: #0056b3;
    }

    .bar-label {
      font-size: 14px;
      text-anchor: middle;
    }
  </style>
</head>
<body>
  <h1>Monthly Sales (SVG Bar Chart)</h1>

  <svg width="600" height="400" viewBox="0 0 600 400">
    <!-- Chart title -->
    <text x="300" y="30" text-anchor="middle" font-size="20" font-weight="bold">
      Sales by Month
    </text>

    <!-- Grid lines -->
    <line x1="50" y1="50" x2="50" y2="350" stroke="#ddd" stroke-width="2"/>
    <line x1="50" y1="350" x2="550" y2="350" stroke="#ddd" stroke-width="2"/>

    <!-- Bars (height = value, y = 350 - height) -->
    <rect class="bar" x="70" y="150" width="80" height="200" />
    <text class="bar-label" x="110" y="370">Jan</text>
    <text class="bar-label" x="110" y="140">$200</text>

    <rect class="bar" x="170" y="100" width="80" height="250" />
    <text class="bar-label" x="210" y="370">Feb</text>
    <text class="bar-label" x="210" y="90">$250</text>

    <rect class="bar" x="270" y="180" width="80" height="170" />
    <text class="bar-label" x="310" y="370">Mar</text>
    <text class="bar-label" x="310" y="170">$170</text>

    <rect class="bar" x="370" y="80" width="80" height="270" />
    <text class="bar-label" x="410" y="370">Apr</text>
    <text class="bar-label" x="410" y="70">$270</text>

    <rect class="bar" x="470" y="120" width="80" height="230" />
    <text class="bar-label" x="510" y="370">May</text>
    <text class="bar-label" x="510" y="110">$230</text>
  </svg>
</body>
</html>
```

---

## Best Practices

### Do This

1. **Use ViewBox for Scalability**
   ```html
   <!-- GOOD: Scales perfectly -->
   <svg viewBox="0 0 100 100" width="50" height="50">
     <circle cx="50" cy="50" r="40" fill="blue" />
   </svg>
   ```

2. **Add Title and Description (Accessibility)**
   ```html
   <svg role="img" aria-labelledby="logo-title logo-desc">
     <title id="logo-title">Company Logo</title>
     <desc id="logo-desc">A blue circle with white text</desc>
     <circle cx="50" cy="50" r="40" fill="blue" />
   </svg>
   ```

3. **Optimize SVG Files**
   ```bash
   # Use SVGO to optimize
   svgo input.svg -o output.svg
   ```

4. **Use CSS for Styling**
   ```html
   <style>
     .icon { fill: blue; }
     .icon:hover { fill: red; }
   </style>
   <svg class="icon">...</svg>
   ```

### Avoid This

1. **Don't Forget Namespace (Standalone SVG)**
   ```html
   <!-- WRONG: Missing xmlns -->
   <svg width="100" height="100">
     <circle cx="50" cy="50" r="40" />
   </svg>

   <!-- CORRECT: Include xmlns -->
   <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100">
     <circle cx="50" cy="50" r="40" />
   </svg>
   ```

2. **Don't Use Pixels for ViewBox**
   ```html
   <!-- WRONG: Defeats scalability -->
   <svg viewBox="0 0 100px 100px">

   <!-- CORRECT: Use unitless numbers -->
   <svg viewBox="0 0 100 100">
   ```

---

## Quick Reference

### Basic SVG Template

```html
<svg width="200" height="200" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
  <!-- Your shapes here -->
</svg>
```

### Common Attributes

| Attribute | Description |
|-----------|-------------|
| `width`, `height` | Canvas size (CSS units or unitless) |
| `viewBox` | Coordinate system (x y width height) |
| `fill` | Fill color |
| `stroke` | Outline color |
| `stroke-width` | Outline thickness |
| `opacity` | Transparency (0-1) |

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| Basic SVG | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Inline SVG | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| SVG in CSS | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| SVG Animation (CSS) | ✅ All | ✅ All | ✅ All | ✅ All | ❌ No |

---

## Related Topics
- [SVG Shapes](svg-shapes.md)
- [SVG Paths](svg-paths.md)
- [Canvas vs SVG](canvas-vs-svg.md)

---

**Last Updated:** November 17, 2025
**Category:** Graphics & Canvas
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
