---
title: Main Element
category: Semantic HTML5
order: 4
---

# Main Element

> **Quick Summary:** The `<main>` element represents the dominant content of the `<body>`, excluding headers, footers, sidebars, and navigation. There should be **only one** `<main>` per page, and it helps screen readers and search engines identify primary content.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<main>` element identifies the primary content area of a document—the content unique to this page, excluding repeated elements like headers, footers, and sidebars. Screen readers announce it as the "main" landmark, allowing users to skip directly to the page's core content.

**Critical rule:** Only **one** `<main>` element per page.

**Key points:**
- Contains content unique to this page (not site-wide navigation/footer)
- One per page (multiple `<main>` elements confuse screen readers)
- Screen readers announce as "main" landmark
- Helps search engines identify primary content for indexing

**Key Concept:** Use one `<main>` element per page to wrap the primary content. It excludes site-wide elements (header, nav, footer, aside) and helps accessibility tools identify the document's core content.

---

## Basic Syntax

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Page Title</title>
</head>
<body>
  <header>
    <h1>Site Name</h1>
    <nav><!-- Navigation --></nav>
  </header>

  <main>
    <h2>Page-Specific Content</h2>
    <p>This is the primary content unique to this page.</p>
  </main>

  <footer>
    <p>&copy; 2025 Company</p>
  </footer>
</body>
</html>
```

---

## Examples

### Example 1: Blog Post Page

```html
<body>
  <header>
    <h1>Tech Blog</h1>
    <nav>
      <a href="/">Home</a>
      <a href="/archive">Archive</a>
    </nav>
  </header>

  <main>
    <article>
      <h2>Understanding the Main Element</h2>
      <p>Published: <time datetime="2025-11-17">Nov 17, 2025</time></p>
      <p>The main element is crucial for accessibility...</p>
    </article>

    <section>
      <h3>Related Articles</h3>
      <ul>
        <li><a href="/post1">Article 1</a></li>
        <li><a href="/post2">Article 2</a></li>
      </ul>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 Tech Blog</p>
  </footer>
</body>
```

### Example 2: E-Commerce Product Page

```html
<body>
  <header>
    <nav><!-- Site navigation --></nav>
  </header>

  <main>
    <article>
      <h1>Product Name</h1>

      <section>
        <h2>Description</h2>
        <p>Product details...</p>
      </section>

      <section>
        <h2>Specifications</h2>
        <ul>
          <li>Weight: 2kg</li>
          <li>Dimensions: 30x20x10cm</li>
        </ul>
      </section>

      <section>
        <h2>Reviews</h2>
        <article>
          <h3>Great product!</h3>
          <p>Review content...</p>
        </article>
      </section>
    </article>

    <aside>
      <h2>Related Products</h2>
      <!-- Product recommendations -->
    </aside>
  </main>

  <footer><!-- Site footer --></footer>
</body>
```

### Example 3: Dashboard Application

```html
<body>
  <header>
    <h1>Admin Dashboard</h1>
    <nav><!-- Dashboard navigation --></nav>
  </header>

  <main>
    <h2>Analytics Overview</h2>

    <section>
      <h3>Traffic Stats</h3>
      <!-- Charts and graphs -->
    </section>

    <section>
      <h3>Recent Activity</h3>
      <!-- Activity feed -->
    </section>
  </main>

  <aside>
    <h2>Quick Actions</h2>
    <!-- Sidebar tools -->
  </aside>

  <footer><!-- Dashboard footer --></footer>
</body>
```

---

## Best Practices

### Do This

1. **One Main Per Page**
   ```html
   <body>
     <header>Header</header>
     <main>Primary content</main>
     <footer>Footer</footer>
   </body>
   ```
   **Why:** Multiple `<main>` elements confuse screen readers about which content is primary.

2. **Exclude Site-Wide Content**
   ```html
   <!-- GOOD: Site navigation outside main -->
   <header>
     <nav>Site navigation</nav>
   </header>

   <main>
     <article>Page-specific content</article>
   </main>
   ```
   **Why:** `<main>` should contain only content unique to this page.

3. **Use with Other Semantic Elements**
   ```html
   <main>
     <article>
       <h1>Article Title</h1>
       <section>Introduction</section>
       <section>Body</section>
     </article>
   </main>
   ```
   **Why:** `<main>` works well with `<article>`, `<section>`, and `<aside>` for structured content.

---

### Avoid This

1. **Multiple Main Elements**
   ```html
   <!-- WRONG: Only one main per page -->
   <main>Content area 1</main>
   <main>Content area 2</main>
   ```
   **Why Not:** Violates HTML spec. Screen readers don't know which is the primary content.
   **Instead:** Use `<section>` or `<article>` for multiple content areas within a single `<main>`.

2. **Main Inside Article**
   ```html
   <!-- WRONG: main shouldn't be nested in article -->
   <article>
     <main>Content</main>
   </article>
   ```
   **Why Not:** `<main>` is for page-level primary content, not article-level.
   **Instead:**
   ```html
   <main>
     <article>Content</article>
   </main>
   ```

3. **Including Site-Wide Navigation**
   ```html
   <!-- WRONG: Navigation isn't unique to this page -->
   <main>
     <nav>Site navigation</nav>
     <article>Article content</article>
   </main>
   ```
   **Why Not:** Site navigation appears on every page, so it's not primary content unique to this page.

---

## Related Topics
- [Semantic HTML Overview](semantic-overview.md)
- [Article Element](article.md)
- [Section Element](section.md)
- [Header Element](header.md)
- [Footer Element](footer.md)

---

**Last Updated:** November 17, 2025
**Category:** Semantic HTML5
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
