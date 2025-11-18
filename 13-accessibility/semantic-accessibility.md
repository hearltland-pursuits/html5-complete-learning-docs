---
title: Semantic HTML for Accessibility
category: Accessibility
order: 4
---

# Semantic HTML for Accessibility

> **Quick Summary:** Using semantic HTML elements (`<nav>`, `<main>`, `<article>`, `<button>`) instead of generic `<div>` and `<span>` provides built-in accessibility, better SEO, and cleaner code.

## Why Semantic HTML Matters

Semantic elements have **implicit roles** and **keyboard behavior**, reducing the need for ARIA attributes and custom JavaScript.

### Example Comparison

```html
<!-- ❌ BAD - Non-semantic (requires ARIA + JS) -->
<div class="button" onclick="submit()">Submit</div>
<!-- Screen readers: "clickable" (vague) -->
<!-- Keyboard: Not accessible -->
<!-- Requires: role="button", tabindex="0", onkeydown handler -->

<!-- ✅ GOOD - Semantic -->
<button onclick="submit()">Submit</button>
<!-- Screen readers: "Submit, button" (clear) -->
<!-- Keyboard: Works automatically (Enter, Space) -->
<!-- No ARIA needed -->
```

---

## Semantic Page Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Accessible Page</title>
</head>
<body>
  <!-- Site header -->
  <header>
    <h1>Site Name</h1>
    <nav aria-label="Main">
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
      </ul>
    </nav>
  </header>

  <!-- Main content -->
  <main>
    <article>
      <h2>Article Title</h2>
      <p>Content...</p>
    </article>

    <aside>
      <h3>Related Links</h3>
    </aside>
  </main>

  <!-- Site footer -->
  <footer>
    <p>&copy; 2025 Company</p>
  </footer>
</body>
</html>
```

**Screen Reader Navigation:**
- Users can jump between landmarks (header, nav, main, footer)
- Headings create an outline for quick scanning
- Articles are announced as distinct content blocks

---

## Semantic vs Non-Semantic

| Use Case | ❌ Non-Semantic | ✅ Semantic |
|----------|----------------|-------------|
| Navigation | `<div class="nav">` | `<nav>` |
| Main content | `<div id="content">` | `<main>` |
| Article | `<div class="post">` | `<article>` |
| Button | `<div class="btn">` | `<button>` |
| Link | `<div onclick="">` | `<a href="">` |
| List | `<div><div>Item</div></div>` | `<ul><li>Item</li></ul>` |

---

## Heading Hierarchy

```html
<!-- ✅ GOOD - Logical hierarchy -->
<h1>Page Title</h1>
  <h2>Section 1</h2>
    <h3>Subsection 1.1</h3>
    <h3>Subsection 1.2</h3>
  <h2>Section 2</h2>

<!-- ❌ BAD - Skipped levels -->
<h1>Page Title</h1>
  <h4>Section</h4> <!-- Skips h2, h3 -->
```

**Why:** Screen reader users navigate by headings (`H` key). Skipping levels creates confusion.

---

## Forms

```html
<!-- ✅ Semantic form -->
<form>
  <label for="name">Name:</label>
  <input type="text" id="name" required>

  <fieldset>
    <legend>Subscription:</legend>
    <label><input type="radio" name="plan" value="free"> Free</label>
    <label><input type="radio" name="plan" value="pro"> Pro</label>
  </fieldset>

  <button type="submit">Submit</button>
</form>
```

**Benefits:**
- `<label>` associates text with input (click label = focus input)
- `<fieldset>` + `<legend>` group related inputs
- `<button>` has implicit role and keyboard support

---

## Best Practices

### 1. One `<main>` Per Page

```html
<body>
  <header>...</header>
  <main>
    <!-- Primary content here -->
  </main>
  <footer>...</footer>
</body>
```

### 2. Use `<nav>` for Navigation

```html
<!-- Multiple nav landmarks need labels -->
<nav aria-label="Main">...</nav>
<nav aria-label="Footer">...</nav>
```

### 3. Descriptive Link Text

```html
<!-- ❌ BAD -->
<a href="article.html">Click here</a>

<!-- ✅ GOOD -->
<a href="article.html">Read the full accessibility guide</a>
```

---

## Related Topics

- [ARIA Roles](aria-roles.md)
- [Keyboard Navigation](keyboard-navigation.md)
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
