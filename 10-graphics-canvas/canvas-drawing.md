---
title: Canvas Drawing
category: Graphics & Canvas
order: 27
---

# Canvas Drawing

> **Quick Summary:** Canvas drawing involves paths, shapes, text, images, gradients, and transformations. Master the path API (`beginPath()`, `moveTo()`, `lineTo()`, `arc()`) to create complex shapes. Use transformations (translate, rotate, scale) for advanced effects. Essential for building interactive graphics, games, and visualizations.

## Table of Contents
- [Introduction](#introduction)
- [Paths](#paths)
- [Shapes](#shapes)
- [Lines and Styles](#lines-and-styles)
- [Text](#text)
- [Images](#images)
- [Gradients and Patterns](#gradients-and-patterns)
- [Transformations](#transformations)
- [State Management](#state-management)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Canvas drawing goes beyond simple rectangles. The **path API** allows you to draw lines, curves, circles, and complex shapes. Combined with text, images, gradients, and transformations, you can create anything from simple icons to full-featured games.

**Key concepts:**
- **Paths** - The foundation of all complex shapes
- **Strokes and fills** - Outlines vs solid shapes
- **Text rendering** - Typography on canvas
- **Image manipulation** - Draw and transform images
- **Gradients/patterns** - Advanced fills
- **Transformations** - Rotate, scale, translate

**Key Concept:** Canvas uses a "state machine" model. You set properties (color, line width, font), then draw. Properties stay set until you change them or restore a previous state. Think of it like a painting setup—once you load your brush with red paint, everything you paint is red until you clean the brush.

---

## Paths

Paths are the foundation of complex canvas drawing. A **path** is a series of points connected by lines or curves.

### Basic Path Workflow

```javascript
ctx.beginPath();      // 1. Start new path
ctx.moveTo(x, y);     // 2. Move to starting point
ctx.lineTo(x, y);     // 3. Draw lines/curves
ctx.closePath();      // 4. Close path (optional)
ctx.stroke();         // 5. Stroke outline OR
ctx.fill();           // 5. Fill shape
```

### Path Methods

| Method | Description |
|--------|-------------|
| `beginPath()` | Start a new path |
| `closePath()` | Connect last point to first |
| `moveTo(x, y)` | Move pen without drawing |
| `lineTo(x, y)` | Draw line to point |
| `stroke()` | Draw outline |
| `fill()` | Fill shape |

### Example: Triangle

```html
<canvas id="triangle-canvas" width="300" height="200"></canvas>

<script>
const canvas = document.getElementById('triangle-canvas');
const ctx = canvas.getContext('2d');

// Triangle using paths
ctx.beginPath();
ctx.moveTo(150, 50);   // Top point
ctx.lineTo(250, 150);  // Bottom-right
ctx.lineTo(50, 150);   // Bottom-left
ctx.closePath();       // Connect back to top

ctx.fillStyle = 'blue';
ctx.fill();

ctx.strokeStyle = 'black';
ctx.lineWidth = 3;
ctx.stroke();
</script>
```

### Example: Multiple Shapes

```html
<canvas id="multi-shapes" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('multi-shapes');
const ctx = canvas.getContext('2d');

// Triangle
ctx.beginPath();
ctx.moveTo(50, 50);
ctx.lineTo(100, 150);
ctx.lineTo(0, 150);
ctx.closePath();
ctx.fillStyle = 'red';
ctx.fill();

// Pentagon (separate path)
ctx.beginPath();
ctx.moveTo(200, 50);
ctx.lineTo(250, 80);
ctx.lineTo(235, 140);
ctx.lineTo(165, 140);
ctx.lineTo(150, 80);
ctx.closePath();
ctx.fillStyle = 'green';
ctx.fill();

// Star
ctx.beginPath();
ctx.moveTo(340, 50);
ctx.lineTo(350, 80);
ctx.lineTo(380, 85);
ctx.lineTo(360, 110);
ctx.lineTo(365, 140);
ctx.lineTo(340, 125);
ctx.lineTo(315, 140);
ctx.lineTo(320, 110);
ctx.lineTo(300, 85);
ctx.lineTo(330, 80);
ctx.closePath();
ctx.fillStyle = 'gold';
ctx.fill();
ctx.strokeStyle = 'orange';
ctx.lineWidth = 2;
ctx.stroke();
</script>
```

---

## Shapes

### Circles and Arcs

```javascript
ctx.arc(x, y, radius, startAngle, endAngle, counterclockwise);
```

**Parameters:**
- `x, y` - Center point
- `radius` - Circle radius
- `startAngle` - Starting angle (radians)
- `endAngle` - Ending angle (radians)
- `counterclockwise` - Direction (true/false)

**Example: Circle**

```html
<canvas id="circle-canvas" width="300" height="200"></canvas>

<script>
const canvas = document.getElementById('circle-canvas');
const ctx = canvas.getContext('2d');

// Full circle (0 to 2π radians = 360°)
ctx.beginPath();
ctx.arc(100, 100, 50, 0, 2 * Math.PI);
ctx.fillStyle = 'blue';
ctx.fill();
ctx.strokeStyle = 'black';
ctx.lineWidth = 2;
ctx.stroke();

// Half circle (0 to π radians = 180°)
ctx.beginPath();
ctx.arc(220, 100, 50, 0, Math.PI);
ctx.fillStyle = 'red';
ctx.fill();
ctx.stroke();
</script>
```

**Example: Pac-Man**

```html
<canvas id="pacman-canvas" width="200" height="200"></canvas>

<script>
const canvas = document.getElementById('pacman-canvas');
const ctx = canvas.getContext('2d');

// Pac-Man (circle with wedge removed)
ctx.beginPath();
ctx.arc(100, 100, 60, 0.2 * Math.PI, 1.8 * Math.PI);
ctx.lineTo(100, 100);
ctx.closePath();
ctx.fillStyle = 'yellow';
ctx.fill();
ctx.strokeStyle = 'black';
ctx.lineWidth = 3;
ctx.stroke();

// Eye
ctx.beginPath();
ctx.arc(100, 70, 5, 0, 2 * Math.PI);
ctx.fillStyle = 'black';
ctx.fill();
</script>
```

### Curves

**Quadratic Curve (1 control point):**

```javascript
ctx.quadraticCurveTo(cpx, cpy, x, y);
```

**Example:**

```html
<canvas id="quad-curve" width="300" height="200"></canvas>

<script>
const canvas = document.getElementById('quad-curve');
const ctx = canvas.getContext('2d');

ctx.beginPath();
ctx.moveTo(50, 150);
ctx.quadraticCurveTo(150, 50, 250, 150);
ctx.strokeStyle = 'blue';
ctx.lineWidth = 3;
ctx.stroke();

// Show control point (for illustration)
ctx.fillStyle = 'red';
ctx.fillRect(148, 48, 4, 4);
</script>
```

**Bézier Curve (2 control points):**

```javascript
ctx.bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y);
```

**Example:**

```html
<canvas id="bezier-curve" width="300" height="200"></canvas>

<script>
const canvas = document.getElementById('bezier-curve');
const ctx = canvas.getContext('2d');

ctx.beginPath();
ctx.moveTo(50, 100);
ctx.bezierCurveTo(90, 20, 210, 20, 250, 100);
ctx.strokeStyle = 'green';
ctx.lineWidth = 3;
ctx.stroke();

// Show control points
ctx.fillStyle = 'red';
ctx.fillRect(88, 18, 4, 4);
ctx.fillRect(208, 18, 4, 4);
</script>
```

---

## Lines and Styles

### Line Properties

```javascript
ctx.lineWidth = 10;              // Line thickness
ctx.lineCap = 'round';           // butt | round | square
ctx.lineJoin = 'round';          // miter | round | bevel
ctx.setLineDash([5, 10]);        // Dashed line pattern
ctx.lineDashOffset = 0;          // Dash offset
```

**Example: Line Styles**

```html
<canvas id="line-styles" width="400" height="300"></canvas>

<script>
const canvas = document.getElementById('line-styles');
const ctx = canvas.getContext('2d');

// Line caps
ctx.lineWidth = 15;

ctx.lineCap = 'butt';
ctx.beginPath();
ctx.moveTo(50, 50);
ctx.lineTo(200, 50);
ctx.stroke();

ctx.lineCap = 'round';
ctx.beginPath();
ctx.moveTo(50, 100);
ctx.lineTo(200, 100);
ctx.stroke();

ctx.lineCap = 'square';
ctx.beginPath();
ctx.moveTo(50, 150);
ctx.lineTo(200, 150);
ctx.stroke();

// Line joins
ctx.lineWidth = 10;

ctx.lineJoin = 'miter';
ctx.beginPath();
ctx.moveTo(250, 50);
ctx.lineTo(300, 100);
ctx.lineTo(250, 150);
ctx.stroke();

ctx.lineJoin = 'round';
ctx.beginPath();
ctx.moveTo(320, 50);
ctx.lineTo(370, 100);
ctx.lineTo(320, 150);
ctx.stroke();

// Dashed line
ctx.setLineDash([10, 5]);
ctx.beginPath();
ctx.moveTo(50, 200);
ctx.lineTo(350, 200);
ctx.stroke();

// Dotted line
ctx.setLineDash([2, 8]);
ctx.beginPath();
ctx.moveTo(50, 250);
ctx.lineTo(350, 250);
ctx.stroke();
</script>
```

---

## Text

### Text Methods

```javascript
ctx.fillText(text, x, y [, maxWidth]);    // Filled text
ctx.strokeText(text, x, y [, maxWidth]);  // Outlined text
ctx.measureText(text);                     // Get text metrics
```

### Text Properties

```javascript
ctx.font = '20px Arial';              // Font size and family
ctx.textAlign = 'center';             // start | end | left | right | center
ctx.textBaseline = 'middle';          // top | hanging | middle | alphabetic | bottom
ctx.direction = 'ltr';                // ltr | rtl
```

**Example: Text Styles**

```html
<canvas id="text-canvas" width="500" height="400"></canvas>

<script>
const canvas = document.getElementById('text-canvas');
const ctx = canvas.getContext('2d');

// Basic text
ctx.font = '30px Arial';
ctx.fillStyle = 'black';
ctx.fillText('Hello Canvas!', 50, 50);

// Styled text
ctx.font = 'bold 40px Georgia';
ctx.fillStyle = 'blue';
ctx.fillText('Bold Blue Text', 50, 100);

// Outlined text
ctx.font = '35px Arial';
ctx.strokeStyle = 'red';
ctx.lineWidth = 2;
ctx.strokeText('Outlined Text', 50, 150);

// Filled + outlined
ctx.font = 'bold 40px Arial';
ctx.fillStyle = 'yellow';
ctx.strokeStyle = 'black';
ctx.lineWidth = 2;
ctx.fillText('Bold Text', 50, 200);
ctx.strokeText('Bold Text', 50, 200);

// Text alignment
ctx.font = '20px Arial';
ctx.fillStyle = 'black';

// Draw center line (for reference)
ctx.strokeStyle = '#ddd';
ctx.lineWidth = 1;
ctx.beginPath();
ctx.moveTo(250, 220);
ctx.lineTo(250, 320);
ctx.stroke();

ctx.textAlign = 'left';
ctx.fillText('Left aligned', 250, 240);

ctx.textAlign = 'center';
ctx.fillText('Center aligned', 250, 270);

ctx.textAlign = 'right';
ctx.fillText('Right aligned', 250, 300);

// Text with shadow
ctx.font = 'bold 35px Arial';
ctx.fillStyle = 'white';
ctx.shadowColor = 'black';
ctx.shadowBlur = 10;
ctx.shadowOffsetX = 3;
ctx.shadowOffsetY = 3;
ctx.fillText('Text with Shadow', 50, 350);

// Reset shadow
ctx.shadowBlur = 0;
ctx.shadowOffsetX = 0;
ctx.shadowOffsetY = 0;
</script>
```

**Example: Measure Text**

```html
<canvas id="measure-text" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('measure-text');
const ctx = canvas.getContext('2d');

const text = 'Measured Text';
ctx.font = '30px Arial';

// Measure text
const metrics = ctx.measureText(text);
const width = metrics.width;

// Draw text
ctx.fillStyle = 'blue';
ctx.fillText(text, 50, 100);

// Draw bounding box
ctx.strokeStyle = 'red';
ctx.lineWidth = 1;
ctx.strokeRect(50, 70, width, 30);

// Display width
ctx.font = '14px Arial';
ctx.fillStyle = 'black';
ctx.fillText(`Width: ${width.toFixed(2)}px`, 50, 140);
</script>
```

---

## Images

### Drawing Images

```javascript
// Simple draw
ctx.drawImage(image, x, y);

// Scaled draw
ctx.drawImage(image, x, y, width, height);

// Cropped and scaled draw
ctx.drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);
```

**Example: Load and Draw Image**

```html
<canvas id="image-canvas" width="500" height="300"></canvas>

<script>
const canvas = document.getElementById('image-canvas');
const ctx = canvas.getContext('2d');

// Create image object
const img = new Image();

img.onload = function() {
  // Draw at original size
  ctx.drawImage(img, 10, 10);

  // Draw scaled (50% size)
  ctx.drawImage(img, 170, 10, img.width * 0.5, img.height * 0.5);

  // Draw cropped
  ctx.drawImage(
    img,
    0, 0, 100, 100,    // Source: crop from (0,0) 100x100
    300, 10, 150, 150  // Destination: draw at (300,10) 150x150
  );
};

// Set image source (triggers onload)
// Note: Using a data URL for demo purposes
// In production, use: img.src = 'path/to/image.jpg';
img.src = 'data:image/svg+xml,' + encodeURIComponent(`
  <svg width="150" height="150" xmlns="http://www.w3.org/2000/svg">
    <rect width="150" height="150" fill="lightblue"/>
    <circle cx="75" cy="75" r="50" fill="blue"/>
  </svg>
`);
</script>
```

**Example: Image Patterns**

```html
<canvas id="pattern-canvas" width="400" height="300"></canvas>

<script>
const canvas = document.getElementById('pattern-canvas');
const ctx = canvas.getContext('2d');

const img = new Image();

img.onload = function() {
  // Create pattern
  const pattern = ctx.createPattern(img, 'repeat');

  // Use pattern as fill
  ctx.fillStyle = pattern;
  ctx.fillRect(0, 0, 400, 300);
};

img.src = 'data:image/svg+xml,' + encodeURIComponent(`
  <svg width="50" height="50" xmlns="http://www.w3.org/2000/svg">
    <rect width="25" height="25" fill="red"/>
    <rect x="25" y="25" width="25" height="25" fill="red"/>
    <rect x="25" width="25" height="25" fill="white"/>
    <rect y="25" width="25" height="25" fill="white"/>
  </svg>
`);
</script>
```

---

## Gradients and Patterns

### Linear Gradient

```javascript
const gradient = ctx.createLinearGradient(x0, y0, x1, y1);
gradient.addColorStop(0, 'red');
gradient.addColorStop(1, 'blue');
ctx.fillStyle = gradient;
```

**Example:**

```html
<canvas id="linear-gradient" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('linear-gradient');
const ctx = canvas.getContext('2d');

// Horizontal gradient
const grad1 = ctx.createLinearGradient(0, 0, 200, 0);
grad1.addColorStop(0, 'red');
grad1.addColorStop(1, 'blue');

ctx.fillStyle = grad1;
ctx.fillRect(10, 10, 180, 80);

// Vertical gradient
const grad2 = ctx.createLinearGradient(0, 0, 0, 180);
grad2.addColorStop(0, 'yellow');
grad2.addColorStop(0.5, 'orange');
grad2.addColorStop(1, 'red');

ctx.fillStyle = grad2;
ctx.fillRect(210, 10, 180, 180);

// Diagonal gradient
const grad3 = ctx.createLinearGradient(10, 110, 180, 180);
grad3.addColorStop(0, '#00ff00');
grad3.addColorStop(1, '#0000ff');

ctx.fillStyle = grad3;
ctx.fillRect(10, 110, 180, 80);
</script>
```

### Radial Gradient

```javascript
const gradient = ctx.createRadialGradient(x0, y0, r0, x1, y1, r1);
gradient.addColorStop(0, 'white');
gradient.addColorStop(1, 'black');
ctx.fillStyle = gradient;
```

**Example:**

```html
<canvas id="radial-gradient" width="400" height="300"></canvas>

<script>
const canvas = document.getElementById('radial-gradient');
const ctx = canvas.getContext('2d');

// Centered radial gradient
const grad1 = ctx.createRadialGradient(100, 100, 10, 100, 100, 80);
grad1.addColorStop(0, 'white');
grad1.addColorStop(0.5, 'yellow');
grad1.addColorStop(1, 'red');

ctx.fillStyle = grad1;
ctx.fillRect(0, 0, 200, 200);

// Off-center radial gradient (spotlight effect)
const grad2 = ctx.createRadialGradient(280, 80, 0, 300, 100, 100);
grad2.addColorStop(0, 'white');
grad2.addColorStop(1, 'blue');

ctx.fillStyle = grad2;
ctx.fillRect(200, 0, 200, 200);
</script>
```

---

## Transformations

### Transform Methods

```javascript
ctx.translate(x, y);      // Move origin
ctx.rotate(angle);        // Rotate (radians)
ctx.scale(x, y);          // Scale
ctx.transform(a, b, c, d, e, f); // Custom matrix
ctx.setTransform(a, b, c, d, e, f); // Reset + transform
ctx.resetTransform();     // Reset to identity
```

**Example: Translation**

```html
<canvas id="translate-canvas" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('translate-canvas');
const ctx = canvas.getContext('2d');

// Draw at origin
ctx.fillStyle = 'red';
ctx.fillRect(0, 0, 50, 50);

// Translate and draw
ctx.translate(100, 50);
ctx.fillStyle = 'blue';
ctx.fillRect(0, 0, 50, 50); // Now at (100, 50)

// Translate again
ctx.translate(100, 50);
ctx.fillStyle = 'green';
ctx.fillRect(0, 0, 50, 50); // Now at (200, 100)
</script>
```

**Example: Rotation**

```html
<canvas id="rotate-canvas" width="400" height="300"></canvas>

<script>
const canvas = document.getElementById('rotate-canvas');
const ctx = canvas.getContext('2d');

ctx.fillStyle = 'blue';

// Rotate around center
for (let i = 0; i < 8; i++) {
  ctx.save();
  ctx.translate(200, 150);
  ctx.rotate((Math.PI / 4) * i); // 45° increments
  ctx.fillRect(50, -10, 100, 20);
  ctx.restore();
}
</script>
```

**Example: Scaling**

```html
<canvas id="scale-canvas" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('scale-canvas');
const ctx = canvas.getContext('2d');

ctx.fillStyle = 'purple';

// Original
ctx.fillRect(10, 10, 50, 50);

// Scaled 2x
ctx.save();
ctx.translate(100, 10);
ctx.scale(2, 2);
ctx.fillRect(0, 0, 50, 50); // Draws as 100x100
ctx.restore();

// Scaled 0.5x
ctx.save();
ctx.translate(250, 10);
ctx.scale(0.5, 0.5);
ctx.fillRect(0, 0, 50, 50); // Draws as 25x25
ctx.restore();
</script>
```

---

## State Management

Canvas maintains a **state stack** for properties like colors, line widths, transformations, etc.

### Save and Restore

```javascript
ctx.save();       // Push current state to stack
// Change properties, draw
ctx.restore();    // Pop state from stack
```

**Example:**

```html
<canvas id="state-canvas" width="400" height="200"></canvas>

<script>
const canvas = document.getElementById('state-canvas');
const ctx = canvas.getContext('2d');

// Original state
ctx.fillStyle = 'black';
ctx.fillRect(10, 10, 50, 50);

// Save state
ctx.save();

// Modify
ctx.fillStyle = 'red';
ctx.translate(100, 0);
ctx.fillRect(10, 10, 50, 50);

// Save again
ctx.save();

// Modify more
ctx.fillStyle = 'blue';
ctx.scale(2, 2);
ctx.fillRect(60, 5, 25, 25); // Draws at (160, 10) as 50x50

// Restore to red state
ctx.restore();
ctx.fillRect(10, 70, 50, 50);

// Restore to original state
ctx.restore();
ctx.fillRect(10, 130, 50, 50);
</script>
```

---

## Examples

### Example 1: Clock

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas Clock</title>
  <style>
    canvas {
      border: 1px solid #ddd;
      display: block;
      margin: 20px auto;
    }
  </style>
</head>
<body>
  <h1>Analog Clock</h1>
  <canvas id="clock" width="300" height="300"></canvas>

  <script>
    const canvas = document.getElementById('clock');
    const ctx = canvas.getContext('2d');

    function drawClock() {
      const now = new Date();
      const hours = now.getHours() % 12;
      const minutes = now.getMinutes();
      const seconds = now.getSeconds();

      // Clear canvas
      ctx.clearRect(0, 0, 300, 300);

      // Clock face
      ctx.save();
      ctx.translate(150, 150);

      // Outer circle
      ctx.beginPath();
      ctx.arc(0, 0, 140, 0, 2 * Math.PI);
      ctx.fillStyle = 'white';
      ctx.fill();
      ctx.strokeStyle = 'black';
      ctx.lineWidth = 4;
      ctx.stroke();

      // Hour markers
      ctx.strokeStyle = 'black';
      ctx.lineWidth = 3;
      for (let i = 0; i < 12; i++) {
        const angle = (i * Math.PI) / 6;
        ctx.save();
        ctx.rotate(angle);
        ctx.beginPath();
        ctx.moveTo(0, -120);
        ctx.lineTo(0, -130);
        ctx.stroke();
        ctx.restore();
      }

      // Hour hand
      const hourAngle = ((hours + minutes / 60) * Math.PI) / 6 - Math.PI / 2;
      ctx.save();
      ctx.rotate(hourAngle);
      ctx.beginPath();
      ctx.moveTo(-20, 0);
      ctx.lineTo(60, 0);
      ctx.strokeStyle = 'black';
      ctx.lineWidth = 6;
      ctx.lineCap = 'round';
      ctx.stroke();
      ctx.restore();

      // Minute hand
      const minuteAngle = ((minutes + seconds / 60) * Math.PI) / 30 - Math.PI / 2;
      ctx.save();
      ctx.rotate(minuteAngle);
      ctx.beginPath();
      ctx.moveTo(-20, 0);
      ctx.lineTo(90, 0);
      ctx.strokeStyle = 'black';
      ctx.lineWidth = 4;
      ctx.lineCap = 'round';
      ctx.stroke();
      ctx.restore();

      // Second hand
      const secondAngle = (seconds * Math.PI) / 30 - Math.PI / 2;
      ctx.save();
      ctx.rotate(secondAngle);
      ctx.beginPath();
      ctx.moveTo(-20, 0);
      ctx.lineTo(100, 0);
      ctx.strokeStyle = 'red';
      ctx.lineWidth = 2;
      ctx.lineCap = 'round';
      ctx.stroke();
      ctx.restore();

      // Center dot
      ctx.beginPath();
      ctx.arc(0, 0, 8, 0, 2 * Math.PI);
      ctx.fillStyle = 'red';
      ctx.fill();

      ctx.restore();
    }

    // Update clock every second
    setInterval(drawClock, 1000);
    drawClock(); // Initial draw
  </script>
</body>
</html>
```

### Example 2: Bar Chart

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Canvas Bar Chart</title>
  <style>
    canvas {
      border: 1px solid #ddd;
      display: block;
      margin: 20px auto;
    }
  </style>
</head>
<body>
  <h1>Sales Chart</h1>
  <canvas id="chart" width="600" height="400"></canvas>

  <script>
    const canvas = document.getElementById('chart');
    const ctx = canvas.getContext('2d');

    const data = [
      { label: 'Jan', value: 120 },
      { label: 'Feb', value: 200 },
      { label: 'Mar', value: 150 },
      { label: 'Apr', value: 280 },
      { label: 'May', value: 220 }
    ];

    const barWidth = 80;
    const barSpacing = 40;
    const chartHeight = 300;
    const chartBottom = 350;
    const maxValue = 300;

    // Title
    ctx.font = 'bold 24px Arial';
    ctx.fillStyle = 'black';
    ctx.textAlign = 'center';
    ctx.fillText('Monthly Sales', 300, 30);

    // Draw bars
    data.forEach((item, index) => {
      const x = 50 + index * (barWidth + barSpacing);
      const barHeight = (item.value / maxValue) * chartHeight;
      const y = chartBottom - barHeight;

      // Bar gradient
      const gradient = ctx.createLinearGradient(0, y, 0, chartBottom);
      gradient.addColorStop(0, '#007bff');
      gradient.addColorStop(1, '#0056b3');

      // Draw bar
      ctx.fillStyle = gradient;
      ctx.fillRect(x, y, barWidth, barHeight);

      // Bar outline
      ctx.strokeStyle = '#003d82';
      ctx.lineWidth = 2;
      ctx.strokeRect(x, y, barWidth, barHeight);

      // Value label
      ctx.font = 'bold 16px Arial';
      ctx.fillStyle = 'black';
      ctx.textAlign = 'center';
      ctx.fillText(`$${item.value}`, x + barWidth / 2, y - 10);

      // X-axis label
      ctx.font = '14px Arial';
      ctx.fillText(item.label, x + barWidth / 2, chartBottom + 25);
    });

    // X-axis
    ctx.beginPath();
    ctx.moveTo(30, chartBottom);
    ctx.lineTo(580, chartBottom);
    ctx.strokeStyle = '#333';
    ctx.lineWidth = 2;
    ctx.stroke();
  </script>
</body>
</html>
```

---

## Best Practices

### Do This

1. **Use beginPath() for Each Shape**
   ```javascript
   // GOOD: Separate paths
   ctx.beginPath();
   ctx.arc(50, 50, 30, 0, 2 * Math.PI);
   ctx.fill();

   ctx.beginPath();
   ctx.arc(150, 50, 30, 0, 2 * Math.PI);
   ctx.fill();
   ```

2. **Save/Restore State for Transformations**
   ```javascript
   // GOOD: Isolate transformations
   ctx.save();
   ctx.translate(100, 100);
   ctx.rotate(Math.PI / 4);
   drawShape();
   ctx.restore(); // Back to normal
   ```

3. **Preload Images**
   ```javascript
   // GOOD: Wait for image to load
   const img = new Image();
   img.onload = function() {
     ctx.drawImage(img, 0, 0);
   };
   img.src = 'image.png';
   ```

### Avoid This

1. **Don't Forget beginPath()**
   ```javascript
   // WRONG: Paths accumulate
   ctx.arc(50, 50, 30, 0, 2 * Math.PI);
   ctx.fill();
   ctx.arc(150, 50, 30, 0, 2 * Math.PI);
   ctx.fill(); // Draws both circles again!

   // CORRECT: Use beginPath()
   ctx.beginPath();
   ctx.arc(50, 50, 30, 0, 2 * Math.PI);
   ctx.fill();
   ctx.beginPath();
   ctx.arc(150, 50, 30, 0, 2 * Math.PI);
   ctx.fill();
   ```

2. **Don't Transform Without Save/Restore**
   ```javascript
   // WRONG: Transformations stack up
   ctx.rotate(Math.PI / 4);
   drawShape1();
   ctx.rotate(Math.PI / 4); // Now rotated 90°!
   drawShape2();
   ```

---

## Quick Reference

### Path Methods

| Method | Description |
|--------|-------------|
| `beginPath()` | Start new path |
| `closePath()` | Close path |
| `moveTo(x, y)` | Move without drawing |
| `lineTo(x, y)` | Draw line |
| `arc(x, y, r, start, end)` | Draw arc/circle |
| `quadraticCurveTo(cpx, cpy, x, y)` | Quadratic curve |
| `bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)` | Bézier curve |

### Text Methods

| Method | Description |
|--------|-------------|
| `fillText(text, x, y)` | Filled text |
| `strokeText(text, x, y)` | Outlined text |
| `measureText(text)` | Get text metrics |

### Transform Methods

| Method | Description |
|--------|-------------|
| `translate(x, y)` | Move origin |
| `rotate(angle)` | Rotate (radians) |
| `scale(x, y)` | Scale |
| `save()` | Save state |
| `restore()` | Restore state |

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| Paths | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Text | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Images | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Gradients | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Transforms | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |

---

## Related Topics
- [Canvas Introduction](canvas-introduction.md)
- [Canvas vs SVG](canvas-vs-svg.md)
- [Responsive Graphics](responsive-graphics.md)

---

**Last Updated:** November 17, 2025
**Category:** Graphics & Canvas
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
