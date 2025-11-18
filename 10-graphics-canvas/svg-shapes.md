---
title: SVG Shapes
category: Graphics & Canvas
order: 24
---

# SVG Shapes

> **Quick Summary:** SVG provides basic shape elements—rect, circle, ellipse, line, polyline, polygon, and text. These building blocks create complex graphics through combination, styling, and transformation. Master these shapes to build icons, diagrams, charts, and illustrations.

## Table of Contents
- [Introduction](#introduction)
- [Rectangle](#rectangle)
- [Circle](#circle)
- [Ellipse](#ellipse)
- [Line](#line)
- [Polyline](#polyline)
- [Polygon](#polygon)
- [Text](#text)
- [Examples](#examples)
- [Quick Reference](#quick-reference)
- [Related Topics](#related-topics)

---

## Introduction

SVG basic shapes are predefined elements for common geometric forms. Each shape has specific attributes that define its size, position, and appearance.

**Available shapes:**
- `<rect>` - Rectangle/square
- `<circle>` - Circle
- `<ellipse>` - Ellipse/oval
- `<line>` - Straight line
- `<polyline>` - Connected line segments
- `<polygon>` - Closed shape with straight sides
- `<text>` - Text content

---

## Rectangle

### Syntax

```html
<rect x="x-position" y="y-position" width="width" height="height" />
```

### Attributes

| Attribute | Description | Required |
|-----------|-------------|----------|
| `x` | X-coordinate of top-left corner | No (default: 0) |
| `y` | Y-coordinate of top-left corner | No (default: 0) |
| `width` | Rectangle width | Yes |
| `height` | Rectangle height | Yes |
| `rx` | Horizontal corner radius | No |
| `ry` | Vertical corner radius | No |

### Examples

```html
<svg width="400" height="300">
  <!-- Basic rectangle -->
  <rect x="10" y="10" width="100" height="80" fill="blue" />

  <!-- Rectangle with stroke -->
  <rect x="130" y="10" width="100" height="80"
        fill="red"
        stroke="black"
        stroke-width="3" />

  <!-- Rounded corners (rx, ry) -->
  <rect x="250" y="10" width="100" height="80"
        rx="15" ry="15"
        fill="green" />

  <!-- Square (width = height) -->
  <rect x="10" y="120" width="80" height="80" fill="orange" />

  <!-- Semi-transparent -->
  <rect x="130" y="120" width="100" height="80"
        fill="purple"
        opacity="0.5" />
</svg>
```

---

## Circle

### Syntax

```html
<circle cx="center-x" cy="center-y" r="radius" />
```

### Attributes

| Attribute | Description | Required |
|-----------|-------------|----------|
| `cx` | X-coordinate of center | No (default: 0) |
| `cy` | Y-coordinate of center | No (default: 0) |
| `r` | Radius | Yes |

### Examples

```html
<svg width="400" height="200">
  <!-- Basic circle -->
  <circle cx="60" cy="100" r="50" fill="blue" />

  <!-- Circle with stroke -->
  <circle cx="180" cy="100" r="50"
          fill="red"
          stroke="black"
          stroke-width="4" />

  <!-- Hollow circle (no fill) -->
  <circle cx="300" cy="100" r="50"
          fill="none"
          stroke="green"
          stroke-width="5" />
</svg>
```

---

## Ellipse

### Syntax

```html
<ellipse cx="center-x" cy="center-y" rx="x-radius" ry="y-radius" />
```

### Attributes

| Attribute | Description | Required |
|-----------|-------------|----------|
| `cx` | X-coordinate of center | No (default: 0) |
| `cy` | Y-coordinate of center | No (default: 0) |
| `rx` | Horizontal radius | Yes |
| `ry` | Vertical radius | Yes |

### Examples

```html
<svg width="400" height="200">
  <!-- Horizontal ellipse (rx > ry) -->
  <ellipse cx="100" cy="100" rx="80" ry="50" fill="blue" />

  <!-- Vertical ellipse (ry > rx) -->
  <ellipse cx="250" cy="100" rx="50" ry="80"
           fill="red"
           stroke="black"
           stroke-width="3" />

  <!-- Circle (rx = ry) -->
  <ellipse cx="350" cy="100" rx="50" ry="50" fill="green" />
</svg>
```

---

## Line

### Syntax

```html
<line x1="start-x" y1="start-y" x2="end-x" y2="end-y" />
```

### Attributes

| Attribute | Description | Required |
|-----------|-------------|----------|
| `x1` | X-coordinate of start point | Yes |
| `y1` | Y-coordinate of start point | Yes |
| `x2` | X-coordinate of end point | Yes |
| `y2` | Y-coordinate of end point | Yes |

### Examples

```html
<svg width="400" height="200">
  <!-- Horizontal line -->
  <line x1="10" y1="50" x2="200" y2="50"
        stroke="black"
        stroke-width="2" />

  <!-- Vertical line -->
  <line x1="220" y1="10" x2="220" y2="100"
        stroke="blue"
        stroke-width="3" />

  <!-- Diagonal line -->
  <line x1="250" y1="10" x2="380" y2="100"
        stroke="red"
        stroke-width="4" />

  <!-- Dashed line -->
  <line x1="10" y1="120" x2="200" y2="120"
        stroke="green"
        stroke-width="2"
        stroke-dasharray="5,5" />

  <!-- Dotted line -->
  <line x1="10" y1="160" x2="200" y2="160"
        stroke="purple"
        stroke-width="2"
        stroke-dasharray="2,4" />
</svg>
```

**Note:** Lines require `stroke` (no `fill` because they have no area).

---

## Polyline

### Syntax

```html
<polyline points="x1,y1 x2,y2 x3,y3 ..." />
```

### Attributes

| Attribute | Description | Required |
|-----------|-------------|----------|
| `points` | Space-separated list of x,y coordinates | Yes |

### Examples

```html
<svg width="400" height="200">
  <!-- Zigzag line -->
  <polyline points="10,50 60,100 110,50 160,100 210,50"
            fill="none"
            stroke="blue"
            stroke-width="3" />

  <!-- Wave pattern -->
  <polyline points="10,150 40,130 70,150 100,130 130,150 160,130"
            fill="none"
            stroke="red"
            stroke-width="2" />

  <!-- Triangle (not closed) -->
  <polyline points="250,50 300,150 200,150"
            fill="yellow"
            stroke="black"
            stroke-width="2" />

  <!-- Connected points -->
  <polyline points="320,50 340,80 360,70 380,100"
            fill="none"
            stroke="green"
            stroke-width="2"
            stroke-linecap="round" />
</svg>
```

---

## Polygon

### Syntax

```html
<polygon points="x1,y1 x2,y2 x3,y3 ..." />
```

### Attributes

| Attribute | Description | Required |
|-----------|-------------|----------|
| `points` | Space-separated list of x,y coordinates | Yes |

**Difference from polyline:** Polygon automatically closes (connects last point to first).

### Examples

```html
<svg width="400" height="300">
  <!-- Triangle -->
  <polygon points="60,20 110,100 10,100"
           fill="blue" />

  <!-- Square -->
  <polygon points="140,20 220,20 220,100 140,100"
           fill="red"
           stroke="black"
           stroke-width="2" />

  <!-- Pentagon -->
  <polygon points="300,20 340,60 320,110 260,110 240,60"
           fill="green" />

  <!-- Star -->
  <polygon points="60,150 70,180 100,185 75,205 80,235 60,220 40,235 45,205 20,185 50,180"
           fill="gold"
           stroke="orange"
           stroke-width="2" />

  <!-- Hexagon -->
  <polygon points="180,150 210,165 210,195 180,210 150,195 150,165"
           fill="purple" />

  <!-- Arrow -->
  <polygon points="300,150 350,170 350,160 380,160 380,200 350,200 350,190 300,210"
           fill="teal" />
</svg>
```

---

## Text

### Syntax

```html
<text x="x-position" y="y-position">Text content</text>
```

### Attributes

| Attribute | Description |
|-----------|-------------|
| `x` | X-coordinate of text start |
| `y` | Y-coordinate of text baseline |
| `font-family` | Font family |
| `font-size` | Font size |
| `font-weight` | Font weight (normal, bold) |
| `text-anchor` | Alignment (start, middle, end) |
| `fill` | Text color |

### Examples

```html
<svg width="500" height="300">
  <!-- Basic text -->
  <text x="10" y="30" font-size="20" fill="black">
    Hello, SVG!
  </text>

  <!-- Styled text -->
  <text x="10" y="70" font-size="24" font-weight="bold" fill="blue">
    Bold Blue Text
  </text>

  <!-- Centered text -->
  <text x="250" y="110" font-size="18" text-anchor="middle" fill="red">
    Centered Text
  </text>

  <!-- Rotated text -->
  <text x="10" y="150" font-size="20" fill="green" transform="rotate(15 10 150)">
    Rotated Text
  </text>

  <!-- Multi-line text using tspan -->
  <text x="10" y="200" font-size="16">
    <tspan x="10" dy="0">Line 1</tspan>
    <tspan x="10" dy="20">Line 2</tspan>
    <tspan x="10" dy="20">Line 3</tspan>
  </text>

  <!-- Text on path (curved) -->
  <defs>
    <path id="curve" d="M 50,250 Q 150,200 250,250" fill="none"/>
  </defs>
  <path d="M 50,250 Q 150,200 250,250" stroke="#ddd" fill="none"/>
  <text font-size="14" fill="purple">
    <textPath href="#curve">
      Text following a curved path!
    </textPath>
  </text>
</svg>
```

---

## Examples

### Example 1: Traffic Light

```html
<svg width="150" height="350" viewBox="0 0 150 350">
  <!-- Outer casing -->
  <rect x="25" y="25" width="100" height="300" rx="10" fill="#333" stroke="black" stroke-width="3"/>

  <!-- Red light -->
  <circle cx="75" cy="80" r="30" fill="red" opacity="1"/>

  <!-- Yellow light -->
  <circle cx="75" cy="175" r="30" fill="yellow" opacity="0.3"/>

  <!-- Green light -->
  <circle cx="75" cy="270" r="30" fill="green" opacity="0.3"/>
</svg>
```

### Example 2: House Icon

```html
<svg width="200" height="200" viewBox="0 0 200 200">
  <!-- Roof (triangle) -->
  <polygon points="100,30 40,90 160,90" fill="#8B4513"/>

  <!-- House body -->
  <rect x="50" y="90" width="100" height="80" fill="#DEB887"/>

  <!-- Door -->
  <rect x="80" y="120" width="40" height="50" fill="#654321"/>

  <!-- Windows -->
  <rect x="60" y="100" width="20" height="20" fill="#87CEEB"/>
  <rect x="120" y="100" width="20" height="20" fill="#87CEEB"/>

  <!-- Door knob -->
  <circle cx="110" cy="145" r="3" fill="gold"/>
</svg>
```

### Example 3: Pie Chart

```html
<svg width="300" height="300" viewBox="0 0 300 300">
  <!-- Center circle -->
  <circle cx="150" cy="150" r="100" fill="none" stroke="#ddd" stroke-width="2"/>

  <!-- Slice 1 (40% - blue) - uses path for complex shapes -->
  <path d="M 150,150 L 150,50 A 100,100 0 0,1 221,103 Z" fill="#007bff"/>

  <!-- Slice 2 (30% - green) -->
  <path d="M 150,150 L 221,103 A 100,100 0 0,1 221,197 Z" fill="#28a745"/>

  <!-- Slice 3 (30% - yellow) -->
  <path d="M 150,150 L 221,197 A 100,100 0 0,1 150,50 Z" fill="#ffc107"/>

  <!-- Labels -->
  <text x="130" y="90" font-size="14" fill="white" font-weight="bold">40%</text>
  <text x="210" y="150" font-size="14" fill="white" font-weight="bold">30%</text>
  <text x="130" y="210" font-size="14" fill="black" font-weight="bold">30%</text>
</svg>
```

---

## Quick Reference

### Shape Comparison

| Shape | Key Attributes | Use Case |
|-------|---------------|----------|
| `<rect>` | x, y, width, height, rx, ry | Boxes, backgrounds, UI elements |
| `<circle>` | cx, cy, r | Icons, buttons, indicators |
| `<ellipse>` | cx, cy, rx, ry | Ovals, rounded shapes |
| `<line>` | x1, y1, x2, y2 | Connectors, dividers, axes |
| `<polyline>` | points | Charts, zigzag patterns |
| `<polygon>` | points | Stars, arrows, custom shapes |
| `<text>` | x, y, content | Labels, annotations |

### Common Styling Attributes

| Attribute | Description | Example |
|-----------|-------------|---------|
| `fill` | Fill color | `fill="blue"` |
| `stroke` | Outline color | `stroke="black"` |
| `stroke-width` | Outline thickness | `stroke-width="3"` |
| `opacity` | Transparency | `opacity="0.5"` |
| `stroke-dasharray` | Dashed outline | `stroke-dasharray="5,5"` |

---

## Browser Support

| Shape | Chrome | Firefox | Safari | Edge | IE |
|-------|--------|---------|--------|------|----|
| All basic shapes | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Rounded rectangles | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| Text | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |

---

## Related Topics
- [SVG Introduction](svg-introduction.md)
- [SVG Paths](svg-paths.md)
- [Responsive Graphics](responsive-graphics.md)

---

**Last Updated:** November 17, 2025
**Category:** Graphics & Canvas
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
