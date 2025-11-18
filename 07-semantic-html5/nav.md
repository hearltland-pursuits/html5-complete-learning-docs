---
title: Nav Element
category: Semantic HTML5
order: 3
---

# Nav Element

> **Quick Summary:** The `<nav>` element represents a section containing navigation links, either to other pages or to sections within the current page. Screen readers announce it as a "navigation" landmark, allowing users to quickly jump to or skip navigation menus.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<nav>` element is specifically designed for major navigation blocks. Before HTML5, developers used `<div class="nav">` or `<ul class="menu">`, which provided no semantic meaning. The `<nav>` element explicitly identifies navigation, improving accessibility and SEO.

**Key points:**
- Use for **major** navigation blocks (main menu, table of contents, breadcrumbs)
- Not every group of links needs `<nav>` (e.g., footer links often don't need it)
- Can appear multiple times per page (main nav, sidebar nav, footer nav)
- Screen readers announce as "navigation" landmark

**Key Concept:** Use `<nav>` for major navigation sections. Screen readers use it as a landmark, allowing users to jump directly to navigation or skip it entirely.

---

## Basic Syntax

```html
<!-- Basic navigation -->
<nav>
  <a href="/">Home</a>
  <a href="/about">About</a>
  <a href="/contact">Contact</a>
</nav>

<!-- Navigation with list structure -->
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/products">Products</a></li>
    <li><a href="/services">Services</a></li>
  </ul>
</nav>
```

---

## Examples

### Example 1: Main Site Navigation

```html
<header>
  <h1>My Company</h1>
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About Us</a></li>
      <li><a href="/services">Services</a></li>
      <li><a href="/portfolio">Portfolio</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
  </nav>
</header>
```

### Example 2: Breadcrumb Navigation

```html
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/products">Products</a></li>
    <li><a href="/products/electronics">Electronics</a></li>
    <li aria-current="page">Laptop</li>
  </ol>
</nav>
```

### Example 3: Multiple Navigation Sections

```html
<body>
  <!-- Primary navigation -->
  <header>
    <nav aria-label="Primary navigation">
      <a href="/">Home</a>
      <a href="/blog">Blog</a>
    </nav>
  </header>

  <!-- Table of contents -->
  <main>
    <article>
      <h1>Article Title</h1>

      <nav aria-label="Table of contents">
        <h2>Contents</h2>
        <ul>
          <li><a href="#intro">Introduction</a></li>
          <li><a href="#methods">Methods</a></li>
          <li><a href="#results">Results</a></li>
        </ul>
      </nav>

      <section id="intro">
        <h2>Introduction</h2>
        <p>Content...</p>
      </section>
    </article>
  </main>

  <!-- Footer navigation -->
  <footer>
    <nav aria-label="Footer navigation">
      <a href="/privacy">Privacy</a>
      <a href="/terms">Terms</a>
    </nav>
  </footer>
</body>
```

---

## Common Use Cases

### Main Menu
```html
<nav aria-label="Main menu">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/shop">Shop</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>
```

### Skip Navigation Link
```html
<a href="#main-content" class="skip-link">Skip to main content</a>

<nav>
  <!-- Many navigation links -->
</nav>

<main id="main-content">
  <!-- Page content -->
</main>
```

### Pagination
```html
<nav aria-label="Pagination">
  <a href="/page/1">Previous</a>
  <a href="/page/2" aria-current="page">2</a>
  <a href="/page/3">3</a>
  <a href="/page/4">Next</a>
</nav>
```

---

## Best Practices

### Do This
1. **Use aria-label for Multiple Navs**
   ```html
   <nav aria-label="Primary">...</nav>
   <nav aria-label="Social media">...</nav>
   ```

2. **Mark Current Page**
   ```html
   <nav>
     <a href="/home">Home</a>
     <a href="/about" aria-current="page">About</a>
   </nav>
   ```

### Avoid This
1. **Don't Use for Every Link Group**
   ```html
   <!-- WRONG: Footer links don't need nav -->
   <footer>
     <nav>
       <a href="/privacy">Privacy</a>
     </nav>
   </footer>

   <!-- BETTER: Simple links in footer -->
   <footer>
     <a href="/privacy">Privacy</a>
   </footer>
   ```

2. **Don't Skip Lists When Appropriate**
   ```html
   <!-- AVOID: Harder to style and navigate -->
   <nav>
     <a href="/">Home</a>
     <a href="/about">About</a>
   </nav>

   <!-- BETTER: Lists provide structure -->
   <nav>
     <ul>
       <li><a href="/">Home</a></li>
       <li><a href="/about">About</a></li>
     </ul>
   </nav>
   ```

---

## Related Topics
- [Semantic HTML Overview](semantic-overview.md)
- [Header Element](header.md)
- [Links & Navigation](../03-links-navigation/anchor-links.md)

---

**Last Updated:** November 17, 2025
**Category:** Semantic HTML5
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
