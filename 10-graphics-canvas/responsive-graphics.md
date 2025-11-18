---
title: Responsive Graphics
category: Graphics & Canvas
order: 29
---

# Responsive Graphics

> **Quick Summary:** Responsive graphics adapt to different screen sizes, resolutions, and devices. For SVG, use viewBox and CSS for fluid scaling. For Canvas, handle window resize events and adjust for device pixel ratio (retina displays). Modern techniques include responsive SVG patterns, fluid Canvas sizing, and media queries for graphics.

## Table of Contents
- [Introduction](#introduction)
- [Responsive SVG](#responsive-svg)
- [Responsive Canvas](#responsive-canvas)
- [Device Pixel Ratio](#device-pixel-ratio)
- [Media Queries for Graphics](#media-queries-for-graphics)
- [Viewport-Based Sizing](#viewport-based-sizing)
- [Touch and Mobile](#touch-and-mobile)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Responsive graphics ensure visual content looks great on all devices—from mobile phones to 4K monitors. SVG and Canvas require different approaches to responsiveness.

**Key challenges:**
- Multiple screen sizes (320px phones to 4K monitors)
- Different pixel densities (standard vs retina displays)
- Orientation changes (portrait vs landscape)
- Touch vs mouse interaction
- Performance on mobile devices

**Key Concept:** Responsive graphics are like responsive typography—they adapt to their container. SVG "thinks" in relative coordinates (viewBox), while Canvas "thinks" in absolute pixels and needs manual scaling. The goal is fluid, high-quality graphics that work everywhere.

---

## Responsive SVG

SVG is naturally responsive thanks to its vector nature, but you must configure it properly.

### ViewBox for Scalability

The `viewBox` defines the coordinate system independent of display size.

```html
<!-- Fixed size (not responsive) -->
<svg width="400" height="300">
  <circle cx="200" cy="150" r="100" fill="blue" />
</svg>

<!-- Responsive (scales to container) -->
<svg viewBox="0 0 400 300" style="width: 100%; height: auto;">
  <circle cx="200" cy="150" r="100" fill="blue" />
</svg>
```

**How viewBox works:**

```html
<!-- viewBox="min-x min-y width height" -->

<!-- 400x300 coordinate system, displayed at any size -->
<svg viewBox="0 0 400 300" width="100%">
  <!-- Circle always at center (50% of viewBox width/height) -->
  <circle cx="200" cy="150" r="100" fill="blue" />
</svg>
```

### Aspect Ratio Control

Use `preserveAspectRatio` to control how SVG scales.

```html
<!-- Maintain aspect ratio, centered -->
<svg viewBox="0 0 100 100" preserveAspectRatio="xMidYMid meet">
  <circle cx="50" cy="50" r="40" fill="blue" />
</svg>

<!-- Stretch to fill (distorts) -->
<svg viewBox="0 0 100 100" preserveAspectRatio="none">
  <circle cx="50" cy="50" r="40" fill="blue" />
</svg>
```

**preserveAspectRatio values:**

| Value | Description |
|-------|-------------|
| `xMidYMid meet` | Center, maintain aspect ratio (default) |
| `xMinYMin meet` | Align to top-left |
| `xMaxYMax meet` | Align to bottom-right |
| `none` | Stretch to fill (distorts) |

### Responsive SVG Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive SVG</title>
  <style>
    .container {
      max-width: 800px;
      margin: 20px auto;
      padding: 20px;
      border: 2px solid #ddd;
      resize: both;
      overflow: hidden;
    }

    svg {
      width: 100%;
      height: auto;
      border: 1px solid #ccc;
    }
  </style>
</head>
<body>
  <h1>Responsive SVG (Resize container)</h1>

  <div class="container">
    <svg viewBox="0 0 400 300" preserveAspectRatio="xMidYMid meet">
      <!-- Background -->
      <rect width="400" height="300" fill="#f0f0f0" />

      <!-- House -->
      <polygon points="200,80 120,160 280,160" fill="#8B4513" />
      <rect x="140" y="160" width="120" height="100" fill="#DEB887" />
      <rect x="180" y="200" width="40" height="60" fill="#654321" />

      <!-- Windows -->
      <rect x="150" y="170" width="30" height="30" fill="#87CEEB" />
      <rect x="220" y="170" width="30" height="30" fill="#87CEEB" />

      <!-- Text (scales with SVG) -->
      <text x="200" y="280" text-anchor="middle" font-size="20" fill="black">
        Responsive SVG House
      </text>
    </svg>
  </div>
</body>
</html>
```

---

## Responsive Canvas

Canvas requires JavaScript to handle responsiveness since it's pixel-based.

### Basic Responsive Pattern

```html
<canvas id="myCanvas"></canvas>

<style>
  #myCanvas {
    width: 100%;
    height: auto;
    max-width: 800px;
    border: 1px solid #ddd;
  }
</style>

<script>
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

function resizeCanvas() {
  // Get display size (CSS size)
  const rect = canvas.getBoundingClientRect();

  // Set canvas resolution to match display size
  canvas.width = rect.width;
  canvas.height = rect.height;

  // Redraw content
  draw();
}

function draw() {
  // Clear canvas
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Draw responsive content
  ctx.fillStyle = 'blue';
  ctx.fillRect(
    canvas.width * 0.25,
    canvas.height * 0.25,
    canvas.width * 0.5,
    canvas.height * 0.5
  );
}

// Resize on load and window resize
window.addEventListener('resize', resizeCanvas);
resizeCanvas();
</script>
```

### Maintain Aspect Ratio

```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');
const aspectRatio = 16 / 9; // Desired aspect ratio

function resizeCanvas() {
  const container = canvas.parentElement;
  const containerWidth = container.clientWidth;

  // Calculate height to maintain aspect ratio
  const width = containerWidth;
  const height = containerWidth / aspectRatio;

  canvas.width = width;
  canvas.height = height;

  draw();
}

window.addEventListener('resize', resizeCanvas);
resizeCanvas();
```

### Responsive Canvas Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Canvas</title>
  <style>
    .container {
      max-width: 800px;
      margin: 20px auto;
      padding: 20px;
      border: 2px solid #ddd;
      resize: both;
      overflow: hidden;
    }

    canvas {
      width: 100%;
      height: auto;
      border: 1px solid #ccc;
    }
  </style>
</head>
<body>
  <h1>Responsive Canvas (Resize container)</h1>

  <div class="container" id="canvas-container">
    <canvas id="responsive-canvas"></canvas>
  </div>

  <script>
    const canvas = document.getElementById('responsive-canvas');
    const ctx = canvas.getContext('2d');

    function resizeCanvas() {
      const container = document.getElementById('canvas-container');
      const width = container.clientWidth - 40; // Account for padding
      const height = width * 0.75; // 4:3 aspect ratio

      canvas.width = width;
      canvas.height = height;

      draw();
    }

    function draw() {
      const w = canvas.width;
      const h = canvas.height;

      // Clear
      ctx.clearRect(0, 0, w, h);

      // Background
      ctx.fillStyle = '#f0f0f0';
      ctx.fillRect(0, 0, w, h);

      // House (proportional to canvas size)
      // Roof
      ctx.beginPath();
      ctx.moveTo(w * 0.5, h * 0.27);
      ctx.lineTo(w * 0.3, h * 0.53);
      ctx.lineTo(w * 0.7, h * 0.53);
      ctx.closePath();
      ctx.fillStyle = '#8B4513';
      ctx.fill();

      // Body
      ctx.fillStyle = '#DEB887';
      ctx.fillRect(w * 0.35, h * 0.53, w * 0.3, h * 0.33);

      // Door
      ctx.fillStyle = '#654321';
      ctx.fillRect(w * 0.45, h * 0.67, w * 0.1, h * 0.19);

      // Windows
      ctx.fillStyle = '#87CEEB';
      ctx.fillRect(w * 0.37, h * 0.57, w * 0.075, h * 0.1);
      ctx.fillRect(w * 0.555, h * 0.57, w * 0.075, h * 0.1);

      // Text
      const fontSize = Math.max(12, w * 0.04);
      ctx.font = `${fontSize}px Arial`;
      ctx.fillStyle = 'black';
      ctx.textAlign = 'center';
      ctx.fillText('Responsive Canvas House', w * 0.5, h * 0.93);
    }

    // Resize observer for container changes
    const resizeObserver = new ResizeObserver(resizeCanvas);
    resizeObserver.observe(document.getElementById('canvas-container'));

    // Initial draw
    resizeCanvas();
  </script>
</body>
</html>
```

---

## Device Pixel Ratio

High-DPI displays (Retina, 4K) have devicePixelRatio > 1, requiring special handling for Canvas.

### The Problem

```html
<!-- On retina display (devicePixelRatio = 2): -->
<canvas width="400" height="300"></canvas>

<!-- Canvas has 400x300 pixels, but displays as 800x600 CSS pixels -->
<!-- Result: Blurry, pixelated graphics -->
```

### The Solution

```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

function setupCanvas() {
  // Get CSS display size
  const rect = canvas.getBoundingClientRect();
  const dpr = window.devicePixelRatio || 1;

  // Set canvas resolution (accounting for DPR)
  canvas.width = rect.width * dpr;
  canvas.height = rect.height * dpr;

  // Scale context to account for DPR
  ctx.scale(dpr, dpr);

  // Now draw at CSS size (not canvas resolution)
  draw();
}

function draw() {
  // Draw at CSS coordinates (e.g., 0-400)
  // Canvas internally renders at higher resolution
  ctx.fillRect(0, 0, 100, 100); // Crisp on retina!
}

window.addEventListener('resize', setupCanvas);
setupCanvas();
```

### Retina-Ready Canvas Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Retina-Ready Canvas</title>
  <style>
    canvas {
      border: 1px solid #ddd;
      width: 400px;
      height: 300px;
    }
  </style>
</head>
<body>
  <h1>Retina-Ready Canvas</h1>
  <p>Device Pixel Ratio: <span id="dpr"></span></p>

  <canvas id="retina-canvas"></canvas>

  <script>
    const canvas = document.getElementById('retina-canvas');
    const ctx = canvas.getContext('2d');
    const dpr = window.devicePixelRatio || 1;

    document.getElementById('dpr').textContent = dpr;

    // Set canvas resolution for retina
    canvas.width = 400 * dpr;
    canvas.height = 300 * dpr;

    // Scale context
    ctx.scale(dpr, dpr);

    // Draw at CSS size (400x300)
    ctx.fillStyle = '#007bff';
    ctx.fillRect(50, 50, 300, 200);

    ctx.fillStyle = 'white';
    ctx.font = 'bold 30px Arial';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText('Crisp on Retina!', 200, 150);

    // Draw fine details to test sharpness
    ctx.strokeStyle = 'white';
    ctx.lineWidth = 1;
    for (let i = 0; i < 10; i++) {
      ctx.beginPath();
      ctx.moveTo(60 + i * 28, 60);
      ctx.lineTo(60 + i * 28, 240);
      ctx.stroke();
    }
  </script>
</body>
</html>
```

---

## Media Queries for Graphics

Use CSS media queries to adapt graphics to different screen sizes.

### SVG with Media Queries

```html
<svg viewBox="0 0 400 300" class="responsive-svg">
  <style>
    /* Default (mobile) */
    .small-text { display: block; font-size: 12px; }
    .large-text { display: none; }

    /* Tablet and up */
    @media (min-width: 768px) {
      .small-text { display: none; }
      .large-text { display: block; font-size: 20px; }
    }
  </style>

  <circle cx="200" cy="150" r="100" fill="blue" />

  <text class="small-text" x="200" y="155" text-anchor="middle" fill="white">
    Mobile
  </text>

  <text class="large-text" x="200" y="155" text-anchor="middle" fill="white">
    Desktop
  </text>
</svg>
```

### Canvas with Media Queries

```html
<canvas id="responsive-canvas"></canvas>

<script>
const canvas = document.getElementById('responsive-canvas');
const ctx = canvas.getContext('2d');

function draw() {
  const isMobile = window.matchMedia('(max-width: 767px)').matches;

  canvas.width = isMobile ? 320 : 800;
  canvas.height = isMobile ? 240 : 600;

  ctx.fillStyle = 'blue';
  ctx.fillRect(0, 0, canvas.width, canvas.height);

  ctx.fillStyle = 'white';
  ctx.font = isMobile ? '16px Arial' : '40px Arial';
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.fillText(
    isMobile ? 'Mobile View' : 'Desktop View',
    canvas.width / 2,
    canvas.height / 2
  );
}

// Redraw on media query change
const mediaQuery = window.matchMedia('(max-width: 767px)');
mediaQuery.addEventListener('change', draw);

draw();
</script>
```

---

## Viewport-Based Sizing

Use viewport units (vw, vh) for fluid sizing.

### SVG with Viewport Units

```html
<style>
  .viewport-svg {
    width: 80vw;  /* 80% of viewport width */
    height: 60vh; /* 60% of viewport height */
    max-width: 1000px;
  }
</style>

<svg class="viewport-svg" viewBox="0 0 400 300">
  <circle cx="200" cy="150" r="100" fill="blue" />
</svg>
```

### Canvas with Viewport Units

```html
<canvas id="viewport-canvas" style="width: 80vw; height: 60vh;"></canvas>

<script>
const canvas = document.getElementById('viewport-canvas');
const ctx = canvas.getContext('2d');

function resizeCanvas() {
  const rect = canvas.getBoundingClientRect();
  const dpr = window.devicePixelRatio || 1;

  canvas.width = rect.width * dpr;
  canvas.height = rect.height * dpr;
  ctx.scale(dpr, dpr);

  draw();
}

function draw() {
  const w = canvas.width / (window.devicePixelRatio || 1);
  const h = canvas.height / (window.devicePixelRatio || 1);

  ctx.clearRect(0, 0, w, h);
  ctx.fillStyle = 'blue';
  ctx.fillRect(w * 0.25, h * 0.25, w * 0.5, h * 0.5);
}

window.addEventListener('resize', resizeCanvas);
resizeCanvas();
</script>
```

---

## Touch and Mobile

### Touch Events for Canvas

```javascript
const canvas = document.getElementById('touch-canvas');
const ctx = canvas.getContext('2d');

// Mouse events
canvas.addEventListener('mousedown', handleStart);
canvas.addEventListener('mousemove', handleMove);
canvas.addEventListener('mouseup', handleEnd);

// Touch events (mobile)
canvas.addEventListener('touchstart', handleStart);
canvas.addEventListener('touchmove', handleMove);
canvas.addEventListener('touchend', handleEnd);

function handleStart(e) {
  e.preventDefault();
  const pos = getPosition(e);
  // Start drawing at pos.x, pos.y
}

function handleMove(e) {
  e.preventDefault();
  const pos = getPosition(e);
  // Continue drawing
}

function handleEnd(e) {
  e.preventDefault();
  // Stop drawing
}

function getPosition(e) {
  const rect = canvas.getBoundingClientRect();
  const touch = e.touches ? e.touches[0] : e;

  return {
    x: touch.clientX - rect.left,
    y: touch.clientY - rect.top
  };
}
```

### Mobile-Optimized Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>Touch Drawing Canvas</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      touch-action: none; /* Prevent scrolling */
    }

    canvas {
      display: block;
      width: 100vw;
      height: 100vh;
    }

    .controls {
      position: fixed;
      top: 10px;
      left: 10px;
      z-index: 10;
    }

    button {
      padding: 10px 20px;
      font-size: 16px;
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <div class="controls">
    <button id="clear-btn">Clear</button>
    <input type="color" id="color-picker" value="#000000">
  </div>

  <canvas id="draw-canvas"></canvas>

  <script>
    const canvas = document.getElementById('draw-canvas');
    const ctx = canvas.getContext('2d');
    const clearBtn = document.getElementById('clear-btn');
    const colorPicker = document.getElementById('color-picker');

    let drawing = false;
    let lastX = 0;
    let lastY = 0;

    function resizeCanvas() {
      const dpr = window.devicePixelRatio || 1;
      canvas.width = window.innerWidth * dpr;
      canvas.height = window.innerHeight * dpr;
      ctx.scale(dpr, dpr);

      // White background
      ctx.fillStyle = 'white';
      ctx.fillRect(0, 0, window.innerWidth, window.innerHeight);
    }

    function getPosition(e) {
      const rect = canvas.getBoundingClientRect();
      const touch = e.touches ? e.touches[0] : e;

      return {
        x: touch.clientX - rect.left,
        y: touch.clientY - rect.top
      };
    }

    function startDrawing(e) {
      e.preventDefault();
      drawing = true;
      const pos = getPosition(e);
      lastX = pos.x;
      lastY = pos.y;
    }

    function draw(e) {
      if (!drawing) return;
      e.preventDefault();

      const pos = getPosition(e);

      ctx.beginPath();
      ctx.moveTo(lastX, lastY);
      ctx.lineTo(pos.x, pos.y);
      ctx.strokeStyle = colorPicker.value;
      ctx.lineWidth = 3;
      ctx.lineCap = 'round';
      ctx.stroke();

      lastX = pos.x;
      lastY = pos.y;
    }

    function stopDrawing(e) {
      e.preventDefault();
      drawing = false;
    }

    // Mouse events
    canvas.addEventListener('mousedown', startDrawing);
    canvas.addEventListener('mousemove', draw);
    canvas.addEventListener('mouseup', stopDrawing);

    // Touch events
    canvas.addEventListener('touchstart', startDrawing);
    canvas.addEventListener('touchmove', draw);
    canvas.addEventListener('touchend', stopDrawing);

    // Clear button
    clearBtn.addEventListener('click', () => {
      ctx.fillStyle = 'white';
      ctx.fillRect(0, 0, window.innerWidth, window.innerHeight);
    });

    // Resize handling
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();
  </script>
</body>
</html>
```

---

## Examples

### Example 1: Fully Responsive Chart

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Chart</title>
  <style>
    .chart-container {
      width: 90%;
      max-width: 800px;
      margin: 20px auto;
    }

    svg {
      width: 100%;
      height: auto;
    }
  </style>
</head>
<body>
  <h1 style="text-align: center;">Responsive SVG Chart</h1>

  <div class="chart-container">
    <svg viewBox="0 0 600 400" preserveAspectRatio="xMidYMid meet">
      <defs>
        <linearGradient id="bar-gradient" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop offset="0%" style="stop-color:#007bff;stop-opacity:1" />
          <stop offset="100%" style="stop-color:#0056b3;stop-opacity:1" />
        </linearGradient>
      </defs>

      <!-- Title -->
      <text x="300" y="30" text-anchor="middle" font-size="24" font-weight="bold">
        Monthly Sales
      </text>

      <!-- Bars -->
      <rect x="50" y="170" width="80" height="180" fill="url(#bar-gradient)" />
      <rect x="150" y="120" width="80" height="230" fill="url(#bar-gradient)" />
      <rect x="250" y="150" width="80" height="200" fill="url(#bar-gradient)" />
      <rect x="350" y="90" width="80" height="260" fill="url(#bar-gradient)" />
      <rect x="450" y="130" width="80" height="220" fill="url(#bar-gradient)" />

      <!-- Values -->
      <text x="90" y="160" text-anchor="middle" font-size="16" font-weight="bold">$120</text>
      <text x="190" y="110" text-anchor="middle" font-size="16" font-weight="bold">$200</text>
      <text x="290" y="140" text-anchor="middle" font-size="16" font-weight="bold">$150</text>
      <text x="390" y="80" text-anchor="middle" font-size="16" font-weight="bold">$280</text>
      <text x="490" y="120" text-anchor="middle" font-size="16" font-weight="bold">$220</text>

      <!-- Labels -->
      <text x="90" y="375" text-anchor="middle" font-size="14">Jan</text>
      <text x="190" y="375" text-anchor="middle" font-size="14">Feb</text>
      <text x="290" y="375" text-anchor="middle" font-size="14">Mar</text>
      <text x="390" y="375" text-anchor="middle" font-size="14">Apr</text>
      <text x="490" y="375" text-anchor="middle" font-size="14">May</text>

      <!-- Axis -->
      <line x1="40" y1="350" x2="540" y2="350" stroke="black" stroke-width="2" />
    </svg>
  </div>
</body>
</html>
```

---

## Best Practices

### Do This

1. **Use viewBox for SVG**
   ```html
   <!-- GOOD: Scales to any size -->
   <svg viewBox="0 0 400 300" style="width: 100%; height: auto;">
     <circle cx="200" cy="150" r="100" fill="blue" />
   </svg>
   ```

2. **Handle devicePixelRatio for Canvas**
   ```javascript
   // GOOD: Crisp on retina displays
   const dpr = window.devicePixelRatio || 1;
   canvas.width = width * dpr;
   canvas.height = height * dpr;
   ctx.scale(dpr, dpr);
   ```

3. **Use ResizeObserver for Canvas**
   ```javascript
   // GOOD: Detects container size changes
   const resizeObserver = new ResizeObserver(() => {
     resizeCanvas();
   });
   resizeObserver.observe(canvas.parentElement);
   ```

### Avoid This

1. **Don't Use Fixed SVG Dimensions**
   ```html
   <!-- WRONG: Not responsive -->
   <svg width="400" height="300">
     <circle cx="200" cy="150" r="100" />
   </svg>

   <!-- CORRECT: Use viewBox -->
   <svg viewBox="0 0 400 300" width="100%">
     <circle cx="200" cy="150" r="100" />
   </svg>
   ```

2. **Don't Size Canvas with CSS Alone**
   ```html
   <!-- WRONG: Stretches canvas, blurry -->
   <canvas style="width: 100%; height: 400px;"></canvas>

   <!-- CORRECT: Set canvas resolution in JavaScript -->
   <canvas id="myCanvas"></canvas>
   <script>
     canvas.width = actualWidth;
     canvas.height = actualHeight;
   </script>
   ```

---

## Quick Reference

### Responsive SVG Checklist

- ✅ Use `viewBox` instead of fixed `width`/`height`
- ✅ Set CSS `width: 100%; height: auto;`
- ✅ Use `preserveAspectRatio` for aspect control
- ✅ Test on mobile devices
- ✅ Use relative coordinates (percentages)

### Responsive Canvas Checklist

- ✅ Handle `window.resize` events
- ✅ Account for `devicePixelRatio`
- ✅ Use relative/proportional coordinates
- ✅ Test on retina displays
- ✅ Implement touch events for mobile
- ✅ Use `ResizeObserver` for containers

### Device Pixel Ratio Pattern

```javascript
const dpr = window.devicePixelRatio || 1;
canvas.width = cssWidth * dpr;
canvas.height = cssHeight * dpr;
ctx.scale(dpr, dpr);
// Draw at CSS coordinates
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| SVG viewBox | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| devicePixelRatio | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 11+ |
| ResizeObserver | ✅ 64+ | ✅ 69+ | ✅ 13.1+ | ✅ 79+ | ❌ No |
| Touch events | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 11+ |

---

## Related Topics
- [SVG Introduction](svg-introduction.md)
- [Canvas Introduction](canvas-introduction.md)
- [Canvas vs SVG](canvas-vs-svg.md)

---

**Last Updated:** November 17, 2025
**Category:** Graphics & Canvas
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
