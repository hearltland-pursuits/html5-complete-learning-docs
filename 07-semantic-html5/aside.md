---
title: Aside Element
category: Semantic HTML5
order: 7
---

# Aside Element

> **Quick Summary:** The `<aside>` element represents content tangentially related to the main content—sidebars, pull quotes, advertisements, related links. Screen readers announce it as "complementary" content that supplements but isn't essential to the primary content.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<aside>` element contains content that's related to the surrounding content but could be separated from it. Think sidebars, callout boxes, pull quotes, advertisements, or "related articles" sections. Screen readers announce it as "complementary" content, indicating it's supplementary.

**Key points:**
- Tangentially related to main content
- Could be removed without affecting main content's meaning
- Common uses: sidebars, related links, ads, author bios
- Screen readers announce as "complementary" landmark

**Key Concept:** Use `<aside>` for content related to but separate from the main content—sidebars, pull quotes, related links, ads. It supplements but isn't essential to understanding the primary content.

---

## Basic Syntax

```html
<!-- Page-level aside (sidebar) -->
<main>
  <article>Main content</article>

  <aside>
    <h2>Related Articles</h2>
    <ul>
      <li><a href="/post1">Article 1</a></li>
      <li><a href="/post2">Article 2</a></li>
    </ul>
  </aside>
</main>

<!-- Article-level aside (pull quote) -->
<article>
  <p>Article content...</p>

  <aside>
    <blockquote>
      <p>"Important quote from the article"</p>
    </blockquote>
  </aside>

  <p>More article content...</p>
</article>
```

---

## Examples

### Example 1: Blog Sidebar

```html
<body>
  <header>
    <h1>Tech Blog</h1>
    <nav>Menu</nav>
  </header>

  <main>
    <article>
      <h2>Main Blog Post</h2>
      <p>Post content...</p>
    </article>

    <aside>
      <section>
        <h2>About the Author</h2>
        <img src="author.jpg" alt="Author photo">
        <p>John Doe is a web developer...</p>
      </section>

      <section>
        <h2>Recent Posts</h2>
        <ul>
          <li><a href="/post1">Understanding HTML5</a></li>
          <li><a href="/post2">CSS Grid Guide</a></li>
        </ul>
      </section>

      <section>
        <h2>Categories</h2>
        <ul>
          <li><a href="/html">HTML</a></li>
          <li><a href="/css">CSS</a></li>
        </ul>
      </section>
    </aside>
  </main>

  <footer>Footer</footer>
</body>
```

### Example 2: Pull Quote in Article

```html
<article>
  <h1>The Future of Web Development</h1>

  <p>Web development is constantly evolving. New frameworks and tools emerge regularly, making it an exciting field to work in.</p>

  <aside class="pull-quote">
    <blockquote>
      <p>"The web platform continues to grow more powerful every year"</p>
      <footer>— Jane Smith, Web Developer</footer>
    </blockquote>
  </aside>

  <p>One of the most significant changes in recent years has been the adoption of modern JavaScript frameworks...</p>
</article>
```

### Example 3: E-Commerce Product Recommendations

```html
<main>
  <article>
    <h1>Wireless Headphones</h1>

    <section>
      <h2>Description</h2>
      <p>Premium wireless headphones...</p>
    </section>

    <section>
      <h2>Reviews</h2>
      <!-- Customer reviews -->
    </section>
  </article>

  <aside>
    <h2>You May Also Like</h2>

    <article class="product-card">
      <img src="product1.jpg" alt="Product 1">
      <h3>Bluetooth Speaker</h3>
      <p>$49.99</p>
    </article>

    <article class="product-card">
      <img src="product2.jpg" alt="Product 2">
      <h3>Phone Case</h3>
      <p>$19.99</p>
    </article>
  </aside>
</main>
```

---

## Best Practices

### Do This

1. **Use for Supplementary Content**
   ```html
   <article>
     <h1>Main Article</h1>
     <p>Essential content...</p>

     <aside>
       <h2>Related Reading</h2>
       <ul><li>Links...</li></ul>
     </aside>
   </article>
   ```

2. **Include Heading in Aside**
   ```html
   <aside>
     <h2>About the Author</h2>
     <p>Bio...</p>
   </aside>
   ```

3. **Use for Advertisements**
   ```html
   <aside aria-label="Advertisement">
     <h2>Sponsored Content</h2>
     <!-- Ad content -->
   </aside>
   ```

### Avoid This

1. **Don't Use for Essential Content**
   ```html
   <!-- WRONG: Main content shouldn't be in aside -->
   <aside>
     <h1>Primary Article Content</h1>
     <p>Main story...</p>
   </aside>

   <!-- CORRECT -->
   <article>
     <h1>Primary Article Content</h1>
     <p>Main story...</p>
   </article>
   ```

2. **Don't Use Just for Styling**
   ```html
   <!-- WRONG: Using aside just for sidebar layout -->
   <aside class="sidebar">
     <nav>Main navigation</nav>
   </aside>

   <!-- CORRECT: Use nav for navigation -->
   <nav class="sidebar">
     <!-- Navigation links -->
   </nav>
   ```

---

## Related Topics
- [Semantic HTML Overview](semantic-overview.md)
- [Article Element](article.md)
- [Main Element](main.md)

---

**Last Updated:** November 17, 2025
**Category:** Semantic HTML5
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
