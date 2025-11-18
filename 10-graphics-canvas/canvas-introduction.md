---
title: Canvas Introduction
category: Graphics & Canvas
order: 26
---

# Canvas Introduction

> **Quick Summary:** The HTML5 `<canvas>` element provides a bitmap-based drawing surface for dynamic graphics, animations, and game development. Unlike SVG (vector), Canvas is pixel-based and manipulated entirely through JavaScript. Perfect for real-time rendering, data visualizations, games, and image manipulation.

## Table of Contents
- [Introduction](#introduction)
- [Canvas vs SVG](#canvas-vs-svg)
- [Basic Canvas Setup](#basic-canvas-setup)
- [Drawing Context](#drawing-context)
- [Coordinate System](#coordinate-system)
- [Basic Drawing](#basic-drawing)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<canvas>` element creates a drawable region on your webpage where you can render graphics using JavaScript. Canvas is a **raster-based** (pixel) graphics system, meaning it draws directly to pixels rather than storing shapes as objects.

**Key characteristics:**
- **Bitmap-based** - Draws pixels, not shapes
- **JavaScript-driven** - All drawing done via script
- **Immediate mode** - No memory of shapes after drawing
- **High performance** - Efficient for animations and games
- **Pixel manipulation** - Direct access to image data

**Key Concept:** Think of Canvas like a physical canvas—once you paint on it, the paint becomes part of the surface. You can't "select" a circle you drew and move it; you'd have to clear that area and redraw. This is the opposite of SVG, which remembers each shape as an object.

---

## Canvas vs SVG

### Quick Comparison

| Feature | Canvas (Raster) | SVG (Vector) |
|---------|-----------------|--------------|
| **Graphics Type** | Bitmap (pixels) | Vector (shapes) |
| **Rendering** | Immediate mode | Retained mode |
| **Performance** | ✅ Better for many objects | ❌ Slower with thousands of shapes |
| **Scalability** | ❌ Pixelated when scaled | ✅ Perfect at any size |
| **Interactivity** | ⚠️ Manual (track coordinates) | ✅ Built-in (click on shapes) |
| **Animation** | ✅ High-performance | ⚠️ CSS/SMIL only |
| **Accessibility** | ❌ Not screen-reader friendly | ✅ Can be accessible |
| **Best For** | Games, real-time graphics, image editing | Logos, icons, charts, UI elements |

### When to Use Canvas

✅ **Use Canvas for:**
- Games and animations
- Real-time data visualization (live charts)
- Image manipulation and filters
- Particle effects
- Rendering thousands of objects
- Performance-critical graphics

❌ **Don't use Canvas for:**
- Static logos or icons (use SVG)
- Accessibility-critical graphics
- Simple shapes that need to scale
- Graphics that need to be searchable/indexable

---

## Basic Canvas Setup

### HTML Structure

```html
<canvas id="myCanvas" width="400" height="300">
  Your browser does not support the HTML5 canvas element.
</canvas>
```

### Important Attributes

| Attribute | Description | Notes |
|-----------|-------------|-------|
| `width` | Canvas width in pixels | Default: 300 |
| `height` | Canvas height in pixels | Default: 150 |
| `id` | Unique identifier | For JavaScript access |

**⚠️ Important:** Use `width` and `height` attributes, NOT CSS! CSS will stretch the canvas, distorting the image.

```html
<!-- CORRECT: Use attributes -->
<canvas width="400" height="300"></canvas>

<!-- WRONG: CSS distorts the canvas -->
<canvas style="width: 400px; height: 300px;"></canvas>
```

---

## Drawing Context

To draw on Canvas, you need a **drawing context**—an object that provides drawing methods.

### Getting 2D Context

```html
<canvas id="myCanvas" width="400" height="300"></canvas>

<script>
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

// Now you can draw using ctx
ctx.fillStyle = 'blue';
ctx.fillRect(50, 50, 100, 100);
</script>
```

### Context Types

| Context | Description | Browser Support |
|---------|-------------|-----------------|
| `'2d'` | 2D drawing operations | ✅ All browsers |
| `'webgl'` | 3D graphics (OpenGL ES) | ✅ Modern browsers |
| `'webgl2'` | WebGL 2.0 (advanced 3D) | ✅ Modern browsers |
| `'bitmaprenderer'` | ImageBitmap rendering | ⚠️ Limited support |

**For this course, we focus on `'2d'` context.**

---

## Coordinate System

Canvas uses a standard **Cartesian coordinate system** with origin at top-left.

```
(0,0) ──────────────> X (increases right)
  │
  │
  │
  │
  ▼
  Y (increases down)
```

### Examples

```html
<canvas id="coords-demo" width="300" height="200"></canvas>

<script>
const canvas = document.getElementById('coords-demo');
const ctx = canvas.getContext('2d');

// Top-left corner (0, 0)
ctx.fillStyle = 'red';
ctx.fillRect(0, 0, 50, 50);

// Top-right corner (250, 0)
ctx.fillStyle = 'blue';
ctx.fillRect(250, 0, 50, 50);

// Bottom-left corner (0, 150)
ctx.fillStyle = 'green';
ctx.fillRect(0, 150, 50, 50);

// Bottom-right corner (250, 150)
ctx.fillStyle = 'yellow';
ctx.fillRect(250, 150, 50, 50);

// Center (125, 75)
ctx.fillStyle = 'purple';
ctx.fillRect(125, 75, 50, 50);
</script>
```

---

## Basic Drawing

### Rectangles

Canvas provides three methods for rectangles:

```javascript
// Filled rectangle
ctx.fillRect(x, y, width, height);

// Stroked (outlined) rectangle
ctx.strokeRect(x, y, width, height);

// Clear rectangle (erase)
ctx.clearRect(x, y, width, height);
```

**Example:**

```html
<canvas id="rect-demo" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('rect-demo');
const ctx = canvas.getContext('2d');

// Filled rectangle
ctx.fillStyle = 'blue';
ctx.fillRect(10, 10, 100, 80);

// Outlined rectangle
ctx.strokeStyle = 'red';
ctx.lineWidth = 3;
ctx.strokeRect(130, 10, 100, 80);

// Filled + outlined
ctx.fillStyle = 'green';
ctx.strokeStyle = 'black';
ctx.lineWidth = 2;
ctx.fillRect(250, 10, 100, 80);
ctx.strokeRect(250, 10, 100, 80);

// Clear rectangle (erases area)
ctx.fillStyle = 'orange';
ctx.fillRect(10, 110, 200, 80);
ctx.clearRect(50, 130, 120, 40); // Punch hole
</script>
```

### Colors and Styles

```javascript
// Fill color (solid)
ctx.fillStyle = 'blue';
ctx.fillStyle = '#007bff';
ctx.fillStyle = 'rgb(0, 123, 255)';
ctx.fillStyle = 'rgba(0, 123, 255, 0.5)'; // Semi-transparent

// Stroke color
ctx.strokeStyle = 'red';

// Line width
ctx.lineWidth = 5;

// Transparency
ctx.globalAlpha = 0.5; // 0-1 (0 = invisible, 1 = opaque)
```

**Example:**

```html
<canvas id="colors-demo" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('colors-demo');
const ctx = canvas.getContext('2d');

// Solid colors
ctx.fillStyle = 'red';
ctx.fillRect(10, 10, 80, 80);

ctx.fillStyle = '#28a745';
ctx.fillRect(110, 10, 80, 80);

ctx.fillStyle = 'rgb(0, 123, 255)';
ctx.fillRect(210, 10, 80, 80);

// Semi-transparent
ctx.fillStyle = 'rgba(255, 0, 0, 0.5)';
ctx.fillRect(310, 10, 80, 80);

// Overlapping transparency
ctx.fillStyle = 'rgba(0, 0, 255, 0.5)';
ctx.fillRect(330, 30, 80, 80);
</script>
```

---

## Examples

### Example 1: Simple Drawing

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas Simple Drawing</title>
  <style>
    canvas {
      border: 1px solid #ddd;
      display: block;
      margin: 20px auto;
    }
  </style>
</head>
<body>
  <h1>Canvas Simple Drawing</h1>

  <canvas id="simple-canvas" width="400" height="300"></canvas>

  <script>
    const canvas = document.getElementById('simple-canvas');
    const ctx = canvas.getContext('2d');

    // Background
    ctx.fillStyle = '#f0f0f0';
    ctx.fillRect(0, 0, 400, 300);

    // House body
    ctx.fillStyle = '#8B4513';
    ctx.fillRect(100, 150, 200, 120);

    // Roof (will learn paths later)
    ctx.fillStyle = '#DC143C';
    ctx.fillRect(80, 120, 240, 30);

    // Door
    ctx.fillStyle = '#654321';
    ctx.fillRect(180, 200, 40, 70);

    // Windows
    ctx.fillStyle = '#87CEEB';
    ctx.fillRect(120, 170, 40, 40);
    ctx.fillRect(240, 170, 40, 40);

    // Window frames
    ctx.strokeStyle = 'black';
    ctx.lineWidth = 2;
    ctx.strokeRect(120, 170, 40, 40);
    ctx.strokeRect(240, 170, 40, 40);
  </script>
</body>
</html>
```

### Example 2: Color Gradient Effect

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas Color Gradient</title>
  <style>
    canvas {
      border: 1px solid #ddd;
      display: block;
      margin: 20px auto;
    }
  </style>
</head>
<body>
  <h1>Canvas Color Gradient</h1>

  <canvas id="gradient-canvas" width="500" height="300"></canvas>

  <script>
    const canvas = document.getElementById('gradient-canvas');
    const ctx = canvas.getContext('2d');

    // Draw gradient using rectangles
    for (let i = 0; i < 100; i++) {
      const red = Math.floor(255 * (i / 100));
      const green = Math.floor(255 * (1 - i / 100));
      const blue = 128;

      ctx.fillStyle = `rgb(${red}, ${green}, ${blue})`;
      ctx.fillRect(i * 5, 0, 5, 300);
    }

    // Text overlay (white with shadow)
    ctx.fillStyle = 'white';
    ctx.font = 'bold 40px Arial';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';

    // Shadow
    ctx.shadowColor = 'black';
    ctx.shadowBlur = 10;
    ctx.shadowOffsetX = 2;
    ctx.shadowOffsetY = 2;

    ctx.fillText('Canvas Gradient', 250, 150);
  </script>
</body>
</html>
```

### Example 3: Interactive Drawing

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Interactive Canvas Drawing</title>
  <style>
    canvas {
      border: 2px solid #333;
      display: block;
      margin: 20px auto;
      cursor: crosshair;
    }

    .controls {
      text-align: center;
      margin: 20px;
    }

    button {
      padding: 10px 20px;
      margin: 5px;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <h1>Click to Draw Squares</h1>

  <div class="controls">
    <button id="clear-btn">Clear Canvas</button>
    <label>
      Color:
      <input type="color" id="color-picker" value="#007bff">
    </label>
  </div>

  <canvas id="interactive-canvas" width="600" height="400"></canvas>

  <script>
    const canvas = document.getElementById('interactive-canvas');
    const ctx = canvas.getContext('2d');
    const clearBtn = document.getElementById('clear-btn');
    const colorPicker = document.getElementById('color-picker');

    // White background
    ctx.fillStyle = 'white';
    ctx.fillRect(0, 0, 600, 400);

    // Draw square on click
    canvas.addEventListener('click', function(event) {
      const rect = canvas.getBoundingClientRect();
      const x = event.clientX - rect.left;
      const y = event.clientY - rect.top;

      ctx.fillStyle = colorPicker.value;
      ctx.fillRect(x - 25, y - 25, 50, 50);

      ctx.strokeStyle = 'black';
      ctx.lineWidth = 2;
      ctx.strokeRect(x - 25, y - 25, 50, 50);
    });

    // Clear button
    clearBtn.addEventListener('click', function() {
      ctx.fillStyle = 'white';
      ctx.fillRect(0, 0, 600, 400);
    });
  </script>
</body>
</html>
```

### Example 4: Animation Loop

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas Animation</title>
  <style>
    canvas {
      border: 1px solid #ddd;
      display: block;
      margin: 20px auto;
      background: #000;
    }
  </style>
</head>
<body>
  <h1>Bouncing Square Animation</h1>

  <canvas id="animation-canvas" width="600" height="400"></canvas>

  <script>
    const canvas = document.getElementById('animation-canvas');
    const ctx = canvas.getContext('2d');

    // Square properties
    let x = 50;
    let y = 50;
    let dx = 2; // Velocity X
    let dy = 3; // Velocity Y
    const size = 50;

    function animate() {
      // Clear canvas
      ctx.clearRect(0, 0, 600, 400);

      // Draw square
      ctx.fillStyle = '#007bff';
      ctx.fillRect(x, y, size, size);

      ctx.strokeStyle = '#0056b3';
      ctx.lineWidth = 3;
      ctx.strokeRect(x, y, size, size);

      // Update position
      x += dx;
      y += dy;

      // Bounce off walls
      if (x + size > 600 || x < 0) {
        dx = -dx;
      }
      if (y + size > 400 || y < 0) {
        dy = -dy;
      }

      // Loop animation
      requestAnimationFrame(animate);
    }

    // Start animation
    animate();
  </script>
</body>
</html>
```

---

## Best Practices

### Do This

1. **Use Attributes for Canvas Size**
   ```html
   <!-- GOOD: Attributes define resolution -->
   <canvas width="400" height="300"></canvas>
   ```

2. **Check for Canvas Support**
   ```javascript
   const canvas = document.getElementById('myCanvas');
   if (canvas.getContext) {
     const ctx = canvas.getContext('2d');
     // Draw here
   } else {
     // Fallback for old browsers
     console.log('Canvas not supported');
   }
   ```

3. **Clear Before Redrawing (Animations)**
   ```javascript
   function animate() {
     ctx.clearRect(0, 0, canvas.width, canvas.height); // Clear
     // Draw new frame
     requestAnimationFrame(animate);
   }
   ```

4. **Use requestAnimationFrame for Animations**
   ```javascript
   // GOOD: Smooth 60fps animation
   function animate() {
     // Drawing code
     requestAnimationFrame(animate);
   }
   animate();

   // WRONG: Inconsistent timing
   setInterval(animate, 16); // Don't use this
   ```

### Avoid This

1. **Don't Use CSS for Canvas Size**
   ```html
   <!-- WRONG: Stretches canvas, distorts image -->
   <canvas style="width: 400px; height: 300px;"></canvas>

   <!-- CORRECT: Use attributes -->
   <canvas width="400" height="300"></canvas>
   ```

2. **Don't Forget to Save/Restore Context State**
   ```javascript
   // WRONG: State changes affect all subsequent drawing
   ctx.fillStyle = 'red';
   drawSomething();
   // fillStyle is still red!

   // CORRECT: Save/restore state
   ctx.save();
   ctx.fillStyle = 'red';
   drawSomething();
   ctx.restore(); // Back to previous state
   ```

3. **Don't Redraw Everything on Every Frame**
   ```javascript
   // WRONG: Inefficient for complex scenes
   function animate() {
     ctx.clearRect(0, 0, 800, 600);
     drawBackground();      // Redraws every frame
     drawStaticObjects();   // Redraws every frame
     drawMovingObject();
   }

   // BETTER: Use layering (multiple canvases)
   // Background canvas (drawn once)
   // Objects canvas (redrawn as needed)
   ```

---

## Quick Reference

### Canvas Setup

```javascript
// 1. Get canvas element
const canvas = document.getElementById('myCanvas');

// 2. Get 2D context
const ctx = canvas.getContext('2d');

// 3. Draw
ctx.fillRect(x, y, width, height);
```

### Basic Drawing Methods

| Method | Description |
|--------|-------------|
| `fillRect(x, y, w, h)` | Draw filled rectangle |
| `strokeRect(x, y, w, h)` | Draw outlined rectangle |
| `clearRect(x, y, w, h)` | Erase rectangular area |

### Style Properties

| Property | Description | Example |
|----------|-------------|---------|
| `fillStyle` | Fill color/gradient | `ctx.fillStyle = 'red'` |
| `strokeStyle` | Stroke color | `ctx.strokeStyle = '#000'` |
| `lineWidth` | Line thickness | `ctx.lineWidth = 5` |
| `globalAlpha` | Transparency | `ctx.globalAlpha = 0.5` |

### Animation Pattern

```javascript
function animate() {
  // 1. Clear canvas
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // 2. Update state
  x += dx;
  y += dy;

  // 3. Draw
  ctx.fillRect(x, y, width, height);

  // 4. Loop
  requestAnimationFrame(animate);
}

animate();
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| Basic Canvas | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| 2D Context | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| WebGL | ✅ 9+ | ✅ 4+ | ✅ 8+ | ✅ All | ✅ 11+ |

---

## Related Topics
- [Canvas Drawing](canvas-drawing.md)
- [Canvas vs SVG](canvas-vs-svg.md)
- [SVG Introduction](svg-introduction.md)

---

**Last Updated:** November 17, 2025
**Category:** Graphics & Canvas
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
