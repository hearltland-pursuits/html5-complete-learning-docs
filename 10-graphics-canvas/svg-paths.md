---
title: SVG Paths
category: Graphics & Canvas
order: 25
---

# SVG Paths

> **Quick Summary:** The SVG `<path>` element creates complex shapes using drawing commands (move, line, curve, arc). It's the most powerful SVG element—capable of drawing anything from simple lines to intricate logos and icons. Mastering path syntax unlocks unlimited SVG capabilities.

## Table of Contents
- [Introduction](#introduction)
- [Path Syntax](#path-syntax)
- [Basic Commands](#basic-commands)
- [Curve Commands](#curve-commands)
- [Arc Command](#arc-command)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<path>` element is the Swiss Army knife of SVG—it can create any shape using a series of drawing commands written in the `d` (data) attribute.

**Key points:**
- Most versatile SVG element
- Uses single-letter commands (M, L, C, Q, A, Z)
- Uppercase = absolute coordinates, lowercase = relative coordinates
- Essential for complex shapes, icons, logos

**Key Concept:** Think of SVG paths like giving a pen drawing instructions: "Move to point A, draw a line to point B, draw a curve to point C." The `d` attribute contains these instructions in compressed form.

---

## Path Syntax

### Basic Structure

```html
<path d="command x y command x y ..." />
```

### Example

```html
<svg width="200" height="200">
  <!-- Draw a triangle -->
  <path d="M 10,10 L 100,10 L 55,80 Z" fill="blue" />
</svg>
```

**Breaking down `d="M 10,10 L 100,10 L 55,80 Z"`:**
- `M 10,10` - Move to (10,10)
- `L 100,10` - Line to (100,10)
- `L 55,80` - Line to (55,80)
- `Z` - Close path (line back to start)

---

## Basic Commands

### M / m - Move To

Moves pen to new position without drawing.

```html
<!-- M = absolute, m = relative -->
<path d="M 10,10" />     <!-- Move to absolute (10,10) -->
<path d="M 10,10 m 20,0" /> <!-- Move to (10,10), then move 20 pixels right -->
```

### L / l - Line To

Draws straight line to specified point.

```html
<svg width="200" height="100">
  <!-- Absolute -->
  <path d="M 10,10 L 100,10 L 100,80 L 10,80 Z"
        fill="none" stroke="blue" stroke-width="2" />

  <!-- Relative (lowercase l) -->
  <path d="M 120,10 l 90,0 l 0,70 l -90,0 Z"
        fill="none" stroke="red" stroke-width="2" />
</svg>
```

### H / h - Horizontal Line

Draws horizontal line to specified x-coordinate.

```html
<svg width="200" height="100">
  <!-- Absolute H -->
  <path d="M 10,50 H 100" stroke="blue" stroke-width="2" />

  <!-- Relative h -->
  <path d="M 120,50 h 80" stroke="red" stroke-width="2" />
</svg>
```

### V / v - Vertical Line

Draws vertical line to specified y-coordinate.

```html
<svg width="200" height="150">
  <!-- Absolute V -->
  <path d="M 50,10 V 100" stroke="blue" stroke-width="2" />

  <!-- Relative v -->
  <path d="M 100,10 v 90" stroke="red" stroke-width="2" />
</svg>
```

### Z / z - Close Path

Draws straight line back to path start.

```html
<svg width="150" height="150">
  <!-- Triangle (Z closes it) -->
  <path d="M 75,10 L 130,130 L 20,130 Z"
        fill="green" stroke="black" stroke-width="2" />
</svg>
```

---

## Curve Commands

### Q / q - Quadratic Bézier Curve

Simple curve with one control point.

**Syntax:** `Q cx,cy x,y` (control point, end point)

```html
<svg width="300" height="200">
  <!-- Quadratic curve -->
  <path d="M 10,100 Q 150,10 290,100"
        fill="none" stroke="blue" stroke-width="2" />

  <!-- Show control point (for illustration) -->
  <circle cx="150" cy="10" r="4" fill="red" />
  <line x1="10" y1="100" x2="150" y2="10" stroke="red" stroke-width="1" opacity="0.5" />
  <line x1="150" y1="10" x2="290" y2="100" stroke="red" stroke-width="1" opacity="0.5" />
</svg>
```

### C / c - Cubic Bézier Curve

More complex curve with two control points.

**Syntax:** `C cx1,cy1 cx2,cy2 x,y` (control point 1, control point 2, end point)

```html
<svg width="300" height="200">
  <!-- Cubic curve (S-shape) -->
  <path d="M 10,100 C 80,10 220,10 290,100"
        fill="none" stroke="blue" stroke-width="3" />

  <!-- Show control points -->
  <circle cx="80" cy="10" r="4" fill="red" />
  <circle cx="220" cy="10" r="4" fill="red" />
  <line x1="10" y1="100" x2="80" y2="10" stroke="red" stroke-width="1" opacity="0.5" />
  <line x1="220" y1="10" x2="290" y2="100" stroke="red" stroke-width="1" opacity="0.5" />
</svg>
```

### S / s - Smooth Cubic Bézier

Continues cubic curve smoothly (first control point is reflection of previous).

**Syntax:** `S cx2,cy2 x,y`

```html
<svg width="400" height="200">
  <!-- Smooth S-curve -->
  <path d="M 10,100 C 80,10 120,10 150,100 S 280,190 390,100"
        fill="none" stroke="blue" stroke-width="3" />
</svg>
```

### T / t - Smooth Quadratic Bézier

Continues quadratic curve smoothly.

**Syntax:** `T x,y`

```html
<svg width="400" height="200">
  <!-- Wave pattern -->
  <path d="M 10,100 Q 60,10 110,100 T 210,100 T 310,100 T 410,100"
        fill="none" stroke="blue" stroke-width="2" />
</svg>
```

---

## Arc Command

### A / a - Elliptical Arc

Draws elliptical arc between two points.

**Syntax:** `A rx,ry rotation large-arc sweep x,y`

**Parameters:**
- `rx, ry` - X and Y radius
- `rotation` - Rotation angle in degrees
- `large-arc` - 0 = small arc, 1 = large arc
- `sweep` - 0 = counter-clockwise, 1 = clockwise
- `x, y` - End point

```html
<svg width="300" height="300">
  <!-- Simple arc (quarter circle) -->
  <path d="M 50,150 A 100,100 0 0,1 150,50"
        fill="none" stroke="blue" stroke-width="3" />

  <!-- Large arc (three-quarters circle) -->
  <path d="M 50,150 A 100,100 0 1,1 150,50"
        fill="none" stroke="red" stroke-width="3" />

  <!-- Full circle (two arcs) -->
  <path d="M 200,150 A 50,50 0 0,1 300,150 A 50,50 0 0,1 200,150"
        fill="yellow" stroke="black" stroke-width="2" />
</svg>
```

---

## Examples

### Example 1: Heart Icon

```html
<svg width="200" height="200" viewBox="0 0 200 200">
  <path d="M 100,170
           C 60,140 20,120 20,80
           C 20,50 40,30 65,30
           C 80,30 90,35 100,50
           C 110,35 120,30 135,30
           C 160,30 180,50 180,80
           C 180,120 140,140 100,170 Z"
        fill="red" stroke="darkred" stroke-width="2"/>
</svg>
```

### Example 2: Star

```html
<svg width="200" height="200" viewBox="0 0 200 200">
  <path d="M 100,20
           L 110,70 L 160,70 L 120,100 L 135,150
           L 100,120 L 65,150 L 80,100 L 40,70
           L 90,70 Z"
        fill="gold" stroke="orange" stroke-width="2"/>
</svg>
```

### Example 3: Logo (Rounded Shapes)

```html
<svg width="300" height="200" viewBox="0 0 300 200">
  <!-- Letter 'S' using curves -->
  <path d="M 80,40
           C 40,40 20,60 20,80
           C 20,100 40,110 60,110
           C 80,110 100,120 100,140
           C 100,160 80,170 60,170
           M 60,175
           C 90,175 110,160 110,140
           C 110,120 90,110 70,110
           C 50,110 30,100 30,80
           C 30,60 50,40 80,40"
        fill="none" stroke="#007bff" stroke-width="8" stroke-linecap="round"/>

  <!-- Letter 'V' -->
  <path d="M 130,50 L 165,150 L 200,50"
        fill="none" stroke="#28a745" stroke-width="8" stroke-linecap="round" stroke-linejoin="round"/>

  <!-- Letter 'G' -->
  <path d="M 280,70
           A 40,40 0 1,0 280,130
           L 280,100
           L 250,100"
        fill="none" stroke="#dc3545" stroke-width="8" stroke-linecap="round"/>
</svg>
```

### Example 4: Pie Chart Slice

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <!-- 40% slice (144 degrees) -->
  <path d="M 150,150
           L 150,50
           A 100,100 0 0,1 221,103
           Z"
        fill="#007bff" stroke="white" stroke-width="2"/>

  <!-- Label -->
  <text x="135" y="90" font-size="20" fill="white" font-weight="bold">40%</text>
</svg>
```

### Example 5: Arrow

```html
<svg width="200" height="100" viewBox="0 0 200 100">
  <path d="M 10,50 L 120,50 L 120,30 L 170,50 L 120,70 L 120,50 Z"
        fill="#007bff" stroke="#0056b3" stroke-width="2"/>
</svg>
```

### Example 6: Speech Bubble

```html
<svg width="300" height="200" viewBox="0 0 300 200">
  <path d="M 20,20
           L 220,20
           Q 240,20 240,40
           L 240,120
           Q 240,140 220,140
           L 100,140
           L 80,180
           L 90,140
           L 20,140
           Q 0,140 0,120
           L 0,40
           Q 0,20 20,20 Z"
        fill="white" stroke="#333" stroke-width="2"/>

  <text x="120" y="80" text-anchor="middle" font-size="24">Hello!</text>
</svg>
```

---

## Best Practices

### Do This

1. **Use Path for Complex Shapes**
   ```html
   <!-- GOOD: Custom icon -->
   <path d="M 10,10 L 50,50 L 10,90" stroke="blue" stroke-width="3" />
   ```

2. **Optimize Path Data**
   ```html
   <!-- VERBOSE -->
   <path d="M 10,10 L 20,10 L 20,20 L 10,20 Z" />

   <!-- OPTIMIZED (use H, V for straight lines) -->
   <path d="M 10,10 H 20 V 20 H 10 Z" />
   ```

3. **Use Relative Commands for Flexibility**
   ```html
   <!-- Absolute (hard to move) -->
   <path d="M 10,10 L 50,50 L 90,10" />

   <!-- Relative (easier to reposition) -->
   <path d="M 10,10 l 40,40 l 40,-40" />
   ```

### Avoid This

1. **Don't Over-Complicate Simple Shapes**
   ```html
   <!-- WRONG: Using path for simple rectangle -->
   <path d="M 10,10 L 110,10 L 110,60 L 10,60 Z" />

   <!-- CORRECT: Use rect -->
   <rect x="10" y="10" width="100" height="50" />
   ```

2. **Don't Forget to Close Paths**
   ```html
   <!-- WRONG: Unclosed (gap at start) -->
   <path d="M 10,10 L 50,50 L 10,90" fill="blue" />

   <!-- CORRECT: Closed with Z -->
   <path d="M 10,10 L 50,50 L 10,90 Z" fill="blue" />
   ```

---

## Quick Reference

### Path Commands

| Command | Name | Parameters | Description |
|---------|------|------------|-------------|
| M / m | Move To | x,y | Move pen (no drawing) |
| L / l | Line To | x,y | Draw line |
| H / h | Horizontal Line | x | Draw horizontal line |
| V / v | Vertical Line | y | Draw vertical line |
| C / c | Cubic Bézier | cx1,cy1 cx2,cy2 x,y | Curve with 2 control points |
| S / s | Smooth Cubic | cx2,cy2 x,y | Smooth continuation |
| Q / q | Quadratic Bézier | cx,cy x,y | Curve with 1 control point |
| T / t | Smooth Quadratic | x,y | Smooth continuation |
| A / a | Arc | rx,ry rot large sweep x,y | Elliptical arc |
| Z / z | Close Path | (none) | Line back to start |

### Uppercase vs Lowercase

- **Uppercase** (M, L, C, etc.) = Absolute coordinates
- **Lowercase** (m, l, c, etc.) = Relative coordinates

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| `<path>` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| All commands | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |

---

## Related Topics
- [SVG Introduction](svg-introduction.md)
- [SVG Shapes](svg-shapes.md)
- [Canvas vs SVG](canvas-vs-svg.md)

---

**Last Updated:** November 17, 2025
**Category:** Graphics & Canvas
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
