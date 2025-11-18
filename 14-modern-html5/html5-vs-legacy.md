---
title: HTML5 vs Legacy HTML
category: Modern HTML5
order: 5
---

# HTML5 vs Legacy HTML (HTML4/XHTML)

> **Quick Summary:** HTML5 simplified web development by removing verbose syntax, adding semantic elements, and introducing powerful APIs. Understanding the differences helps migrate legacy code.

## Key Differences

### DOCTYPE

```html
<!-- HTML5 - Simple -->
<!DOCTYPE html>

<!-- HTML 4.01 Strict - Verbose -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

<!-- XHTML 1.0 - Even more verbose -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
```

### Character Encoding

```html
<!-- HTML5 -->
<meta charset="UTF-8">

<!-- HTML4 -->
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
```

### Syntax Rules

| Feature | HTML4 | XHTML | HTML5 |
|---------|-------|-------|-------|
| Closing tags | Optional for some | Required | Optional for some |
| Attribute quotes | Optional | Required | Optional |
| Self-closing | `<br>` | `<br />` | `<br>` or `<br />` |
| Case | Case-insensitive | Lowercase required | Case-insensitive |
| Boolean attributes | `checked="checked"` | `checked="checked"` | `checked` |

```html
<!-- HTML5 - Flexible -->
<input type="checkbox" checked>

<!-- XHTML - Strict -->
<input type="checkbox" checked="checked" />
```

---

## New Semantic Elements

### HTML5 Additions

```html
<!-- HTML5 semantic structure -->
<header>
  <nav>
    <ul>
      <li><a href="/">Home</a></li>
    </ul>
  </nav>
</header>

<main>
  <article>
    <section>
      <h2>Section Title</h2>
    </section>
  </article>

  <aside>Sidebar</aside>
</main>

<footer>
  <p>&copy; 2025</p>
</footer>
```

**HTML4 Equivalent:**
```html
<div id="header">
  <div id="nav">
    <ul>
      <li><a href="/">Home</a></li>
    </ul>
  </div>
</div>

<div id="main">
  <div class="article">
    <div class="section">
      <h2>Section Title</h2>
    </div>
  </div>

  <div id="sidebar">Sidebar</div>
</div>

<div id="footer">
  <p>&copy; 2025</p>
</div>
```

---

## Deprecated Elements

### Removed in HTML5

| Element | HTML4 Use | HTML5 Alternative |
|---------|-----------|-------------------|
| `<font>` | Styling text | CSS `font-family`, `color` |
| `<center>` | Centering | CSS `text-align: center` |
| `<frame>`, `<frameset>` | Page layout | `<iframe>` or CSS Grid/Flexbox |
| `<marquee>` | Scrolling text | CSS animations |
| `<blink>` | Blinking text | CSS animations (or don't!) |
| `<big>`, `<small>` (presentational) | Text size | CSS `font-size` |

### Migration Example

```html
<!-- ❌ HTML4 -->
<font color="red" size="5">Error!</font>
<center>Centered content</center>

<!-- ✅ HTML5 -->
<span style="color: red; font-size: 1.25em;">Error!</span>
<div style="text-align: center;">Centered content</div>

<!-- ✅ BETTER - Separate concerns -->
<span class="error">Error!</span>
<div class="centered">Centered content</div>

<style>
.error { color: red; font-size: 1.25em; }
.centered { text-align: center; }
</style>
```

---

## New HTML5 Features

### Media Elements

```html
<!-- HTML5 - Native media support -->
<video controls>
  <source src="video.mp4" type="video/mp4">
</video>

<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
</audio>

<!-- HTML4 - Required Flash or plugins -->
<object data="video.swf" type="application/x-shockwave-flash"></object>
```

### Form Enhancements

```html
<!-- HTML5 - New input types -->
<input type="email" required>
<input type="date">
<input type="range" min="0" max="100">
<input type="color">

<!-- HTML4 - Only text inputs -->
<input type="text" name="email">
```

### Canvas & SVG

```html
<!-- HTML5 - Graphics support -->
<canvas id="myCanvas" width="500" height="300"></canvas>

<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" fill="blue" />
</svg>

<!-- HTML4 - No native support, used images or Flash -->
```

---

## APIs Added in HTML5

- **Geolocation:** `navigator.geolocation`
- **Web Storage:** `localStorage`, `sessionStorage`
- **Web Workers:** Background JavaScript threads
- **Drag and Drop:** Native drag/drop API
- **History API:** `pushState()`, `replaceState()`
- **Web Sockets:** Real-time bi-directional communication

---

## Migrating from HTML4 to HTML5

### 1. Update DOCTYPE

```html
<!-- Old -->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">

<!-- New -->
<!DOCTYPE html>
```

### 2. Replace Divs with Semantic Elements

```html
<!-- Before -->
<div id="header">
<div id="nav">
<div id="main">
<div id="sidebar">
<div id="footer">

<!-- After -->
<header>
<nav>
<main>
<aside>
<footer>
```

### 3. Remove Deprecated Attributes

```html
<!-- Before -->
<table border="1" cellpadding="5" cellspacing="0">
<img src="photo.jpg" align="left" hspace="10">

<!-- After -->
<table style="border: 1px solid; padding: 5px;">
<img src="photo.jpg" style="float: left; margin-right: 10px;">

<!-- Better - Use CSS -->
<table class="data-table">
<img src="photo.jpg" class="left-aligned">
```

### 4. Simplify Meta Tags

```html
<!-- Before -->
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta http-equiv="Content-Language" content="en">

<!-- After -->
<meta charset="UTF-8">
<html lang="en">
```

---

## Browser Support

**All modern browsers support HTML5:**
- Chrome, Firefox, Safari, Edge (all recent versions)
- IE 9+ (partial support)
- IE 11 (good support, but deprecated)

**Legacy browser support:**
- Use HTML5 Shiv for IE8 and older
- Provide fallbacks for new input types
- Feature detection with Modernizr

---

## Best Practices

1. **Use HTML5** - It's simpler, more semantic, and better supported
2. **Validate** - Use [W3C Validator](https://validator.w3.org/)
3. **Separate Concerns** - HTML for structure, CSS for presentation, JS for behavior
4. **Use Semantic Elements** - Improves accessibility and SEO
5. **Progressive Enhancement** - Build for HTML5, provide fallbacks

---

## Related Topics

- [Semantic HTML](../07-semantic-html5/semantic-overview.md)
- [Deprecated Elements](../01-fundamentals/deprecated-elements.md)
- [Progressive Enhancement](progressive-enhancement.md)

---

**Last Updated:** November 18, 2025
**Category:** Modern HTML5
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
