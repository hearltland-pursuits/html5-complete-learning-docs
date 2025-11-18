---
title: Section Element
category: Semantic HTML5
order: 6
---

# Section Element

> **Quick Summary:** The `<section>` element represents a thematic grouping of content, typically with its own heading. Use it to divide content into logical chapters, tabs, or themed blocks within a larger document.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Section vs Div vs Article](#section-vs-div-vs-article)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<section>` element groups related content under a common theme. Unlike `<article>` (self-contained), `<section>` content usually needs parent document context. Think of sections as chapters in a book—each has its own theme but relies on the book's overall structure.

**Key points:**
- Thematic grouping of content
- Should have a heading (h1-h6)
- Not for standalone content (use `<article>` instead)
- Not just for styling (use `<div>` instead)

**Key Concept:** Use `<section>` for thematic content groupings that need parent context—chapters, tabs, themed content blocks. If it needs a heading and groups related content, it's probably a section.

---

## Basic Syntax

```html
<section>
  <h2>Section Heading</h2>
  <p>Related content grouped by theme...</p>
</section>

<!-- Sections within an article -->
<article>
  <h1>Article Title</h1>

  <section>
    <h2>Introduction</h2>
    <p>Intro content...</p>
  </section>

  <section>
    <h2>Methods</h2>
    <p>Methods content...</p>
  </section>

  <section>
    <h2>Results</h2>
    <p>Results content...</p>
  </section>
</article>
```

---

## Examples

### Example 1: Product Page Sections

```html
<main>
  <article>
    <h1>Wireless Headphones</h1>

    <section>
      <h2>Description</h2>
      <p>Premium wireless headphones with noise cancellation...</p>
    </section>

    <section>
      <h2>Features</h2>
      <ul>
        <li>30-hour battery life</li>
        <li>Active noise cancellation</li>
        <li>Bluetooth 5.0</li>
      </ul>
    </section>

    <section>
      <h2>Specifications</h2>
      <table>
        <tr><td>Weight</td><td>250g</td></tr>
        <tr><td>Dimensions</td><td>20x18x8cm</td></tr>
      </table>
    </section>

    <section>
      <h2>Customer Reviews</h2>
      <!-- Reviews -->
    </section>
  </article>
</main>
```

### Example 2: Landing Page Sections

```html
<main>
  <section id="hero">
    <h1>Welcome to Our Service</h1>
    <p>Transform your business with our solutions</p>
    <button>Get Started</button>
  </section>

  <section id="features">
    <h2>Features</h2>
    <div class="feature">
      <h3>Fast</h3>
      <p>Lightning-fast performance</p>
    </div>
    <div class="feature">
      <h3>Secure</h3>
      <p>Bank-level security</p>
    </div>
  </section>

  <section id="pricing">
    <h2>Pricing Plans</h2>
    <!-- Pricing cards -->
  </section>

  <section id="testimonials">
    <h2>What Our Customers Say</h2>
    <!-- Testimonials -->
  </section>
</main>
```

### Example 3: Documentation Page

```html
<article>
  <h1>API Documentation</h1>

  <section id="getting-started">
    <h2>Getting Started</h2>
    <p>Install the library...</p>
  </section>

  <section id="authentication">
    <h2>Authentication</h2>
    <p>Use API keys to authenticate...</p>
  </section>

  <section id="endpoints">
    <h2>API Endpoints</h2>

    <section id="users-endpoint">
      <h3>/api/users</h3>
      <p>Retrieve user data...</p>
    </section>

    <section id="posts-endpoint">
      <h3>/api/posts</h3>
      <p>Retrieve posts...</p>
    </section>
  </section>
</article>
```

---

## Section vs Div vs Article

### Use `<section>` when:
- Content has a thematic grouping
- Section has its own heading
- Content is related but not standalone

### Use `<article>` when:
- Content is self-contained and independently distributable
- Could be syndicated (RSS feed, social media)

### Use `<div>` when:
- No semantic meaning (purely for styling or JavaScript)
- Content doesn't fit other semantic elements

**Example:**
```html
<!-- Section: Thematic grouping -->
<section>
  <h2>Our Services</h2>
  <p>Services content...</p>
</section>

<!-- Article: Standalone content -->
<article>
  <h2>Blog Post Title</h2>
  <p>Post content...</p>
</article>

<!-- Div: Styling wrapper -->
<div class="card">
  <p>Styled content...</p>
</div>
```

---

## Best Practices

### Do This

1. **Include Heading in Every Section**
   ```html
   <section>
     <h2>Section Title</h2>
     <p>Content...</p>
   </section>
   ```

2. **Use for Thematic Groupings**
   ```html
   <article>
     <h1>Complete Guide</h1>

     <section>
       <h2>Chapter 1</h2>
       <p>Content...</p>
     </section>

     <section>
       <h2>Chapter 2</h2>
       <p>Content...</p>
     </section>
   </article>
   ```

3. **Nest Sections When Appropriate**
   ```html
   <section>
     <h2>Parent Section</h2>

     <section>
       <h3>Sub-section</h3>
       <p>Content...</p>
     </section>
   </section>
   ```

### Avoid This

1. **Don't Use Section Just for Styling**
   ```html
   <!-- WRONG -->
   <section class="container">
     <p>No heading, just styling...</p>
   </section>

   <!-- CORRECT -->
   <div class="container">
     <p>Styled content...</p>
   </div>
   ```

2. **Don't Skip Headings**
   ```html
   <!-- WRONG: Section without heading -->
   <section>
     <p>Content without heading...</p>
   </section>

   <!-- CORRECT -->
   <section>
     <h2>Proper Heading</h2>
     <p>Content with heading...</p>
   </section>
   ```

---

## Related Topics
- [Semantic HTML Overview](semantic-overview.md)
- [Article Element](article.md)
- [Div vs Semantic](div-vs-semantic.md)

---

**Last Updated:** November 17, 2025
**Category:** Semantic HTML5
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
