---
title: Canvas vs SVG
category: Graphics & Canvas
order: 28
---

# Canvas vs SVG

> **Quick Summary:** Canvas and SVG solve different problems. Canvas is a **bitmap** (pixel-based) drawing surface ideal for games, animations, and real-time rendering. SVG is a **vector** (shape-based) format perfect for scalable graphics, logos, and interactive diagrams. Choose based on performance needs, scalability requirements, and interactivity patterns.

## Table of Contents
- [Introduction](#introduction)
- [Key Differences](#key-differences)
- [Performance Comparison](#performance-comparison)
- [When to Use Canvas](#when-to-use-canvas)
- [When to Use SVG](#when-to-use-svg)
- [Feature Comparison](#feature-comparison)
- [Hybrid Approaches](#hybrid-approaches)
- [Examples](#examples)
- [Decision Matrix](#decision-matrix)
- [Related Topics](#related-topics)

---

## Introduction

Canvas and SVG are both web technologies for creating graphics, but they work in fundamentally different ways:

- **Canvas** - A **raster graphics** API that draws pixels directly to a bitmap surface
- **SVG** - A **vector graphics** format that defines shapes using XML markup

**Key Concept:** Think of Canvas like painting on a physical canvas—once you paint a pixel, it's just part of the surface. SVG is like building with LEGO blocks—each shape is an object you can move, resize, or style independently. Canvas is "immediate mode" (draw and forget), SVG is "retained mode" (browser remembers shapes).

---

## Key Differences

### Fundamental Architecture

| Aspect | Canvas | SVG |
|--------|--------|-----|
| **Graphics Model** | Raster (bitmap) | Vector (shapes) |
| **Rendering Mode** | Immediate mode | Retained mode |
| **API** | JavaScript-only | HTML/CSS/JavaScript |
| **DOM** | Single element | Each shape is a DOM node |
| **Memory** | Stores pixels | Stores shape definitions |
| **Interaction** | Manual coordinate tracking | Built-in event handling |

### Immediate vs Retained Mode

**Canvas (Immediate Mode):**
```javascript
// Draw circle
ctx.beginPath();
ctx.arc(50, 50, 30, 0, 2 * Math.PI);
ctx.fill();

// Canvas "forgets" the circle
// To move it, must clear and redraw everything
```

**SVG (Retained Mode):**
```html
<!-- Define circle -->
<circle id="myCircle" cx="50" cy="50" r="30" fill="blue" />

<script>
// SVG "remembers" the circle
// Can modify it directly
document.getElementById('myCircle').setAttribute('cx', '100');
</script>
```

---

## Performance Comparison

### Canvas Performance

✅ **Advantages:**
- **High object count** - Handles 10,000+ objects efficiently
- **Real-time rendering** - 60fps animations with many elements
- **Pixel manipulation** - Direct access to image data
- **Constant memory** - Uses same memory regardless of complexity

❌ **Disadvantages:**
- **Resolution-dependent** - Pixelated when scaled
- **Redraw overhead** - Must redraw entire scene for changes
- **No built-in interactivity** - Must track clicks manually

**Performance sweet spot:** 1,000+ animated objects, particle effects, games

### SVG Performance

✅ **Advantages:**
- **Infinite scalability** - Perfect quality at any size
- **Individual element control** - Style/animate each shape independently
- **Built-in interactivity** - Click/hover on shapes directly
- **Accessibility** - Screen reader compatible

❌ **Disadvantages:**
- **DOM overhead** - Each shape = DOM node (memory intensive)
- **Slow with many elements** - Performance degrades beyond ~1,000 shapes
- **Complex animations** - CPU-intensive for many simultaneous animations

**Performance sweet spot:** <1,000 interactive shapes, logos, icons, charts

### Benchmark Results

```
Rendering 10,000 Circles:
- Canvas: ~16ms (60fps) ✅
- SVG: ~450ms (2fps) ❌

Scaling 1 Logo:
- Canvas: Pixelated ❌
- SVG: Perfect ✅

Click Detection (100 shapes):
- Canvas: Manual coordinate math ⚠️
- SVG: Built-in event handling ✅
```

---

## When to Use Canvas

### Use Cases

✅ **Perfect for:**

1. **Games and Game Engines**
   - Real-time rendering
   - Particle effects
   - Sprite animations
   - Physics simulations

2. **Data Visualizations (Real-time)**
   - Live stock charts
   - Waveform displays
   - Heat maps
   - Thousands of data points

3. **Image Manipulation**
   - Photo editors
   - Filters and effects
   - Color adjustments
   - Pixel-level operations

4. **Animations (Complex)**
   - Particle systems
   - Fractal generators
   - Generative art
   - Video processing

5. **Performance-Critical Graphics**
   - High object count (10,000+)
   - 60fps requirements
   - Dynamic content

### Example: Canvas Game

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas Game</title>
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
  <h1>Canvas Particle System (1000 particles)</h1>
  <canvas id="game" width="800" height="600"></canvas>

  <script>
    const canvas = document.getElementById('game');
    const ctx = canvas.getContext('2d');

    // Particle class
    class Particle {
      constructor() {
        this.x = Math.random() * 800;
        this.y = Math.random() * 600;
        this.vx = (Math.random() - 0.5) * 2;
        this.vy = (Math.random() - 0.5) * 2;
        this.radius = Math.random() * 3 + 1;
        this.color = `hsl(${Math.random() * 360}, 100%, 50%)`;
      }

      update() {
        this.x += this.vx;
        this.y += this.vy;

        // Bounce off walls
        if (this.x < 0 || this.x > 800) this.vx *= -1;
        if (this.y < 0 || this.y > 600) this.vy *= -1;
      }

      draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, 2 * Math.PI);
        ctx.fillStyle = this.color;
        ctx.fill();
      }
    }

    // Create 1000 particles
    const particles = [];
    for (let i = 0; i < 1000; i++) {
      particles.push(new Particle());
    }

    // Animation loop
    function animate() {
      // Clear canvas
      ctx.fillStyle = 'rgba(0, 0, 0, 0.1)';
      ctx.fillRect(0, 0, 800, 600);

      // Update and draw particles
      particles.forEach(p => {
        p.update();
        p.draw();
      });

      requestAnimationFrame(animate);
    }

    animate();
  </script>
</body>
</html>
```

---

## When to Use SVG

### Use Cases

✅ **Perfect for:**

1. **Logos and Branding**
   - Company logos
   - Icons and badges
   - Branding elements
   - Print-ready graphics

2. **User Interface Elements**
   - Icons
   - Buttons
   - Badges
   - Navigation elements

3. **Charts and Diagrams**
   - Bar/pie/line charts (<1,000 points)
   - Flowcharts
   - Org charts
   - Network diagrams

4. **Interactive Graphics**
   - Clickable maps
   - Interactive infographics
   - Tooltips on hover
   - Animated illustrations

5. **Responsive Graphics**
   - Multi-device support
   - Retina displays
   - Zoom/pan interfaces
   - Accessible graphics

### Example: SVG Interactive Chart

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>SVG Interactive Chart</title>
  <style>
    svg {
      border: 1px solid #ddd;
      display: block;
      margin: 20px auto;
    }

    .bar {
      transition: fill 0.3s;
      cursor: pointer;
    }

    .bar:hover {
      fill: #0056b3;
    }

    .tooltip {
      pointer-events: none;
      opacity: 0;
      transition: opacity 0.3s;
    }

    .tooltip.visible {
      opacity: 1;
    }
  </style>
</head>
<body>
  <h1>SVG Interactive Bar Chart</h1>
  <svg id="chart" width="600" height="400" viewBox="0 0 600 400"></svg>

  <script>
    const data = [
      { label: 'Jan', value: 120, color: '#007bff' },
      { label: 'Feb', value: 200, color: '#28a745' },
      { label: 'Mar', value: 150, color: '#ffc107' },
      { label: 'Apr', value: 280, color: '#dc3545' },
      { label: 'May', value: 220, color: '#17a2b8' }
    ];

    const svg = document.getElementById('chart');
    const maxValue = 300;
    const barWidth = 80;
    const barSpacing = 40;

    // Title
    const title = document.createElementNS('http://www.w3.org/2000/svg', 'text');
    title.setAttribute('x', 300);
    title.setAttribute('y', 30);
    title.setAttribute('text-anchor', 'middle');
    title.setAttribute('font-size', 24);
    title.setAttribute('font-weight', 'bold');
    title.textContent = 'Monthly Sales';
    svg.appendChild(title);

    // Tooltip group
    const tooltip = document.createElementNS('http://www.w3.org/2000/svg', 'g');
    tooltip.classList.add('tooltip');
    const tooltipRect = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
    tooltipRect.setAttribute('width', 100);
    tooltipRect.setAttribute('height', 40);
    tooltipRect.setAttribute('fill', 'white');
    tooltipRect.setAttribute('stroke', 'black');
    tooltipRect.setAttribute('rx', 5);
    const tooltipText = document.createElementNS('http://www.w3.org/2000/svg', 'text');
    tooltipText.setAttribute('x', 50);
    tooltipText.setAttribute('y', 25);
    tooltipText.setAttribute('text-anchor', 'middle');
    tooltipText.setAttribute('font-size', 16);
    tooltip.appendChild(tooltipRect);
    tooltip.appendChild(tooltipText);
    svg.appendChild(tooltip);

    // Draw bars
    data.forEach((item, index) => {
      const x = 50 + index * (barWidth + barSpacing);
      const barHeight = (item.value / maxValue) * 250;
      const y = 320 - barHeight;

      // Bar
      const bar = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
      bar.classList.add('bar');
      bar.setAttribute('x', x);
      bar.setAttribute('y', y);
      bar.setAttribute('width', barWidth);
      bar.setAttribute('height', barHeight);
      bar.setAttribute('fill', item.color);

      // Hover events
      bar.addEventListener('mouseenter', (e) => {
        tooltipText.textContent = `$${item.value}`;
        tooltip.setAttribute('transform', `translate(${x + barWidth / 2 - 50}, ${y - 50})`);
        tooltip.classList.add('visible');
      });

      bar.addEventListener('mouseleave', () => {
        tooltip.classList.remove('visible');
      });

      svg.appendChild(bar);

      // Label
      const label = document.createElementNS('http://www.w3.org/2000/svg', 'text');
      label.setAttribute('x', x + barWidth / 2);
      label.setAttribute('y', 350);
      label.setAttribute('text-anchor', 'middle');
      label.setAttribute('font-size', 14);
      label.textContent = item.label;
      svg.appendChild(label);
    });

    // X-axis
    const axis = document.createElementNS('http://www.w3.org/2000/svg', 'line');
    axis.setAttribute('x1', 30);
    axis.setAttribute('y1', 320);
    axis.setAttribute('x2', 580);
    axis.setAttribute('y2', 320);
    axis.setAttribute('stroke', 'black');
    axis.setAttribute('stroke-width', 2);
    svg.appendChild(axis);
  </script>
</body>
</html>
```

---

## Feature Comparison

### Rendering and Display

| Feature | Canvas | SVG |
|---------|--------|-----|
| **Scalability** | ❌ Pixelated when scaled | ✅ Perfect at any size |
| **Resolution** | Depends on canvas size | Resolution-independent |
| **Quality on Retina** | ⚠️ Needs manual scaling | ✅ Automatic high-DPI |
| **File Size** | ⚠️ Large for complex scenes | ✅ Small for simple graphics |
| **Print Quality** | ❌ Low quality | ✅ High quality |

### Interactivity

| Feature | Canvas | SVG |
|---------|--------|-----|
| **Click Detection** | ❌ Manual coordinate math | ✅ Built-in event handling |
| **Hover Effects** | ❌ Track mouse manually | ✅ CSS :hover works |
| **Drag and Drop** | ⚠️ Custom implementation | ✅ Native browser support |
| **Individual Element Events** | ❌ Not supported | ✅ Each shape has events |

### Styling and Animation

| Feature | Canvas | SVG |
|---------|--------|-----|
| **CSS Styling** | ❌ Not supported | ✅ Full CSS support |
| **CSS Animations** | ❌ Not supported | ✅ CSS transitions/keyframes |
| **JavaScript Animation** | ✅ High performance | ⚠️ Slower for many elements |
| **Filters/Effects** | ⚠️ Manual implementation | ✅ SVG filters |

### Accessibility

| Feature | Canvas | SVG |
|---------|--------|-----|
| **Screen Readers** | ❌ Not accessible | ✅ Can be accessible |
| **SEO** | ❌ Not indexable | ✅ Text content indexable |
| **Semantic Structure** | ❌ No structure | ✅ XML hierarchy |
| **ARIA Support** | ⚠️ Limited (on canvas element) | ✅ Full ARIA support |

### Development

| Feature | Canvas | SVG |
|---------|--------|-----|
| **API Complexity** | ⚠️ JavaScript-heavy | ✅ HTML/CSS familiar |
| **Debugging** | ❌ No DOM inspection | ✅ Inspect elements |
| **Tools** | ⚠️ Limited visual editors | ✅ Many design tools |
| **Learning Curve** | ⚠️ Steeper | ✅ Easier for web devs |

---

## Hybrid Approaches

Sometimes the best solution combines both technologies.

### Approach 1: Layering

Use SVG for static UI, Canvas for dynamic content.

```html
<div style="position: relative;">
  <!-- Canvas layer (background) -->
  <canvas id="background" width="800" height="600"
          style="position: absolute; z-index: 1;"></canvas>

  <!-- SVG layer (UI overlays) -->
  <svg width="800" height="600"
       style="position: absolute; z-index: 2; pointer-events: none;">
    <!-- UI elements, labels, axes -->
  </svg>
</div>
```

### Approach 2: Canvas for Rendering, SVG for Interactivity

Draw complex graphics on Canvas, use invisible SVG for hit detection.

```html
<div style="position: relative;">
  <canvas id="graphics" width="800" height="600"></canvas>

  <svg width="800" height="600"
       style="position: absolute; top: 0; left: 0;">
    <!-- Invisible clickable regions -->
    <circle cx="100" cy="100" r="50"
            fill="transparent"
            style="cursor: pointer;"
            onclick="alert('Circle clicked!')"/>
  </svg>
</div>
```

### Approach 3: Render SVG to Canvas

Use SVG for authoring, Canvas for performance.

```javascript
// Create SVG
const svgString = `
  <svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
    <circle cx="100" cy="100" r="80" fill="blue"/>
  </svg>
`;

// Convert to image
const img = new Image();
const blob = new Blob([svgString], { type: 'image/svg+xml' });
const url = URL.createObjectURL(blob);

img.onload = function() {
  // Draw SVG on Canvas
  ctx.drawImage(img, 0, 0);
  URL.revokeObjectURL(url);
};

img.src = url;
```

---

## Examples

### Example 1: Side-by-Side Comparison

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas vs SVG</title>
  <style>
    .container {
      display: flex;
      gap: 20px;
      justify-content: center;
      margin: 20px;
    }

    .demo {
      text-align: center;
    }

    canvas, svg {
      border: 1px solid #ddd;
    }
  </style>
</head>
<body>
  <h1>Canvas vs SVG: Same Drawing</h1>

  <div class="container">
    <!-- Canvas version -->
    <div class="demo">
      <h2>Canvas (Bitmap)</h2>
      <canvas id="canvas-demo" width="200" height="200"></canvas>
      <p>Try zooming in - pixelated!</p>
    </div>

    <!-- SVG version -->
    <div class="demo">
      <h2>SVG (Vector)</h2>
      <svg id="svg-demo" width="200" height="200" viewBox="0 0 200 200">
        <circle cx="100" cy="100" r="80" fill="#007bff"/>
        <text x="100" y="110" text-anchor="middle" fill="white" font-size="30" font-weight="bold">
          SVG
        </text>
      </svg>
      <p>Try zooming in - crisp!</p>
    </div>
  </div>

  <script>
    const canvas = document.getElementById('canvas-demo');
    const ctx = canvas.getContext('2d');

    // Draw on Canvas
    ctx.beginPath();
    ctx.arc(100, 100, 80, 0, 2 * Math.PI);
    ctx.fillStyle = '#007bff';
    ctx.fill();

    ctx.fillStyle = 'white';
    ctx.font = 'bold 30px Arial';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText('Canvas', 100, 100);
  </script>
</body>
</html>
```

### Example 2: Performance Test

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas vs SVG Performance</title>
  <style>
    .container {
      display: flex;
      gap: 20px;
      margin: 20px;
    }

    canvas, svg {
      border: 1px solid #ddd;
    }

    .stats {
      font-family: monospace;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <h1>Performance Test: 1000 Animated Circles</h1>

  <div class="container">
    <!-- Canvas test -->
    <div>
      <h2>Canvas</h2>
      <canvas id="canvas-perf" width="400" height="300"></canvas>
      <div class="stats" id="canvas-fps">FPS: 0</div>
    </div>

    <!-- SVG test -->
    <div>
      <h2>SVG</h2>
      <svg id="svg-perf" width="400" height="300"></svg>
      <div class="stats" id="svg-fps">FPS: 0</div>
    </div>
  </div>

  <script>
    // Canvas animation
    const canvas = document.getElementById('canvas-perf');
    const ctx = canvas.getContext('2d');
    const canvasFpsEl = document.getElementById('canvas-fps');

    const canvasCircles = [];
    for (let i = 0; i < 1000; i++) {
      canvasCircles.push({
        x: Math.random() * 400,
        y: Math.random() * 300,
        vx: (Math.random() - 0.5) * 2,
        vy: (Math.random() - 0.5) * 2,
        r: 3,
        color: `hsl(${Math.random() * 360}, 70%, 50%)`
      });
    }

    let canvasLastTime = performance.now();
    let canvasFps = 0;

    function animateCanvas() {
      const now = performance.now();
      canvasFps = 1000 / (now - canvasLastTime);
      canvasLastTime = now;
      canvasFpsEl.textContent = `FPS: ${canvasFps.toFixed(1)}`;

      ctx.clearRect(0, 0, 400, 300);

      canvasCircles.forEach(c => {
        c.x += c.vx;
        c.y += c.vy;
        if (c.x < 0 || c.x > 400) c.vx *= -1;
        if (c.y < 0 || c.y > 300) c.vy *= -1;

        ctx.beginPath();
        ctx.arc(c.x, c.y, c.r, 0, 2 * Math.PI);
        ctx.fillStyle = c.color;
        ctx.fill();
      });

      requestAnimationFrame(animateCanvas);
    }
    animateCanvas();

    // SVG animation
    const svg = document.getElementById('svg-perf');
    const svgFpsEl = document.getElementById('svg-fps');

    const svgCircles = [];
    for (let i = 0; i < 1000; i++) {
      const circle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
      circle.setAttribute('r', 3);
      circle.setAttribute('fill', `hsl(${Math.random() * 360}, 70%, 50%)`);

      const data = {
        element: circle,
        x: Math.random() * 400,
        y: Math.random() * 300,
        vx: (Math.random() - 0.5) * 2,
        vy: (Math.random() - 0.5) * 2
      };

      svgCircles.push(data);
      svg.appendChild(circle);
    }

    let svgLastTime = performance.now();
    let svgFps = 0;

    function animateSVG() {
      const now = performance.now();
      svgFps = 1000 / (now - svgLastTime);
      svgLastTime = now;
      svgFpsEl.textContent = `FPS: ${svgFps.toFixed(1)}`;

      svgCircles.forEach(c => {
        c.x += c.vx;
        c.y += c.vy;
        if (c.x < 0 || c.x > 400) c.vx *= -1;
        if (c.y < 0 || c.y > 300) c.vy *= -1;

        c.element.setAttribute('cx', c.x);
        c.element.setAttribute('cy', c.y);
      });

      requestAnimationFrame(animateSVG);
    }
    animateSVG();
  </script>
</body>
</html>
```

---

## Decision Matrix

### Choose Canvas If:

| Requirement | Reason |
|-------------|--------|
| ✅ 1,000+ animated objects | Canvas handles high object count efficiently |
| ✅ Particle effects | Bitmap rendering perfect for particles |
| ✅ Real-time data visualization | Low-latency rendering critical |
| ✅ Image manipulation | Pixel-level access required |
| ✅ Game development | Performance-critical animations |
| ✅ Consistent performance | Performance doesn't degrade with complexity |

### Choose SVG If:

| Requirement | Reason |
|-------------|--------|
| ✅ Scalable graphics | Vector format scales infinitely |
| ✅ Interactive UI elements | Built-in event handling |
| ✅ Accessibility required | Screen reader compatible |
| ✅ <1,000 objects | SVG handles moderate complexity well |
| ✅ Print quality | Vector graphics print perfectly |
| ✅ CSS styling needed | Full CSS support |
| ✅ SEO important | Text content indexable |

### Use Both If:

| Scenario | Approach |
|----------|----------|
| Complex visualization with UI overlays | Canvas background + SVG UI layer |
| High-performance rendering with interactivity | Canvas for graphics + invisible SVG hit areas |
| Dynamic content with static UI | Canvas for animation + SVG for buttons/labels |

---

## Quick Reference

### Canvas Summary

- **Type:** Bitmap (raster)
- **Rendering:** Immediate mode
- **Best for:** Games, animations, high object count
- **Scaling:** Pixelated
- **Interactivity:** Manual
- **Performance:** High (constant)

### SVG Summary

- **Type:** Vector
- **Rendering:** Retained mode
- **Best for:** Logos, icons, interactive charts
- **Scaling:** Perfect
- **Interactivity:** Built-in
- **Performance:** Degrades with object count

### Performance Thresholds

| Metric | Canvas | SVG |
|--------|--------|-----|
| **Object count** | 10,000+ | <1,000 |
| **FPS (1000 objects)** | 60fps | ~2-10fps |
| **Memory** | Low (bitmap) | High (DOM nodes) |
| **File size** | Large for complex | Small for simple |

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| Canvas | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| SVG | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Canvas + SVG hybrid | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |

---

## Related Topics
- [Canvas Introduction](canvas-introduction.md)
- [Canvas Drawing](canvas-drawing.md)
- [SVG Introduction](svg-introduction.md)
- [Responsive Graphics](responsive-graphics.md)

---

**Last Updated:** November 17, 2025
**Category:** Graphics & Canvas
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
