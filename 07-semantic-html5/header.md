---
title: Header Element
category: Semantic HTML5
order: 2
---

# Header Element

> **Quick Summary:** The `<header>` element represents introductory content or navigational aids, typically containing logos, site titles, navigation menus, and search forms. It can be used for the page header or as headers within `<article>` and `<section>` elements.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<header>` element is a semantic HTML5 container for introductory content. It typically appears at the top of a page (site header) or at the beginning of sections/articles (section headers). Unlike older `<div class="header">` patterns, `<header>` explicitly communicates its purpose to browsers and assistive technologies.

**Key points:**
- Can appear multiple times per page (one page header, plus headers for articles/sections)
- Often contains logo, site title, navigation (`<nav>`), search forms
- Screen readers announce it as a "banner" landmark when it's the page's main header
- Not required to be first child of parent element

**Key Concept:** Use `<header>` for introductory content at the page or section level. The page's main header becomes a "banner" landmark for screen readers, improving navigation.

---

## Basic Syntax

```html
<!-- Page header (main site header) -->
<header>
  <h1>Site Name</h1>
  <nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
  </nav>
</header>

<!-- Article header -->
<article>
  <header>
    <h2>Article Title</h2>
    <p>By Author Name | <time datetime="2025-11-17">Nov 17, 2025</time></p>
  </header>
  <p>Article content...</p>
</article>
```

---

## Examples

### Example 1: Site Header with Logo and Navigation

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Website</title>
  <style>
    header { background: #333; color: white; padding: 1rem; display: flex; justify-content: space-between; align-items: center; }
    header h1 { margin: 0; }
    nav a { color: white; margin-left: 1rem; text-decoration: none; }
  </style>
</head>
<body>
  <header>
    <h1>My Website</h1>
    <nav>
      <a href="/">Home</a>
      <a href="/products">Products</a>
      <a href="/about">About</a>
      <a href="/contact">Contact</a>
    </nav>
  </header>

  <main>
    <h2>Welcome</h2>
    <p>Page content...</p>
  </main>
</body>
</html>
```

### Example 2: Blog Post with Article Header

```html
<article>
  <header>
    <h2>Understanding Semantic HTML</h2>
    <p>
      <strong>By:</strong> John Doe |
      <strong>Published:</strong> <time datetime="2025-11-17">November 17, 2025</time>
    </p>
    <p class="excerpt">A comprehensive guide to HTML5 semantic elements...</p>
  </header>

  <section>
    <h3>Introduction</h3>
    <p>Article body content...</p>
  </section>

  <footer>
    <p>Tags: HTML5, Semantics, Accessibility</p>
  </footer>
</article>
```

### Example 3: Multiple Headers in Sections

```html
<main>
  <section>
    <header>
      <h2>Our Services</h2>
      <p>Discover what we can do for you</p>
    </header>
    <p>Service content...</p>
  </section>

  <section>
    <header>
      <h2>Testimonials</h2>
      <p>What our clients say about us</p>
    </header>
    <blockquote>...</blockquote>
  </section>
</main>
```

---

## Common Use Cases

### Site Header (Banner Landmark)
```html
<header>
  <img src="logo.svg" alt="Company Logo">
  <nav>
    <a href="/">Home</a>
    <a href="/services">Services</a>
  </nav>
  <form role="search">
    <input type="search" placeholder="Search...">
  </form>
</header>
```

### Article Metadata Header
```html
<article>
  <header>
    <h2>Article Title</h2>
    <p>Author: Jane Smith</p>
    <p>Published: <time datetime="2025-11-17">Nov 17, 2025</time></p>
    <p>Reading time: 5 minutes</p>
  </header>
  <p>Article content...</p>
</article>
```

---

## Best Practices

### Do This
1. **Use for Introductory Content**
   ```html
   <header>
     <h1>Page Title</h1>
     <nav>Navigation</nav>
   </header>
   ```

2. **Multiple Headers Allowed**
   ```html
   <header>Site Header</header>
   <main>
     <article>
       <header>Article Header</header>
       <p>Content...</p>
     </article>
   </main>
   ```

### Avoid This
1. **Don't Nest Headers**
   ```html
   <!-- WRONG -->
   <header>
     <header>Nested header</header>
   </header>
   ```

2. **Don't Use for All Headings**
   ```html
   <!-- WRONG: header not needed for simple h1 -->
   <header><h1>Title</h1></header>

   <!-- GOOD: use header when grouping related intro content -->
   <header>
     <h1>Title</h1>
     <p>Subtitle</p>
   </header>
   ```

---

## Related Topics
- [Semantic HTML Overview](semantic-overview.md)
- [Nav Element](nav.md)
- [Footer Element](footer.md)

---

**Last Updated:** November 17, 2025
**Category:** Semantic HTML5
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
