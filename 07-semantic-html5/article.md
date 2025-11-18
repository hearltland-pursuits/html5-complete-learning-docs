---
title: Article Element
category: Semantic HTML5
order: 5
---

# Article Element

> **Quick Summary:** The `<article>` element represents self-contained, independently distributable content—blog posts, news articles, forum posts, comments, widgets. Content that could be syndicated, reused, or shared as a standalone piece.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Article vs Section](#article-vs-section)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<article>` element wraps content that makes sense on its own—content you could extract and publish elsewhere without losing meaning. Think blog posts, news articles, product cards, user comments, or social media posts. Each article is a complete, self-contained composition.

**"Would this make sense in an RSS feed?"** If yes, use `<article>`.

**Key points:**
- Self-contained and independently distributable
- Can be nested (e.g., blog post containing comment articles)
- Should have a heading (h1-h6)
- Can have its own `<header>` and `<footer>`

**Key Concept:** Use `<article>` for content that could stand alone—blog posts, news articles, product cards, comments. If you could syndicate it or share it independently, it's an article.

---

## Basic Syntax

```html
<article>
  <h2>Article Title</h2>
  <p>This content makes sense independently...</p>
</article>

<!-- Article with header and footer -->
<article>
  <header>
    <h2>Article Title</h2>
    <p>By Author | <time datetime="2025-11-17">Nov 17, 2025</time></p>
  </header>

  <p>Article content...</p>

  <footer>
    <p>Tags: HTML5, Semantics</p>
  </footer>
</article>
```

---

## Examples

### Example 1: Blog Post

```html
<main>
  <article>
    <header>
      <h1>Understanding HTML5 Article Element</h1>
      <p>
        By <strong>John Doe</strong> |
        Published: <time datetime="2025-11-17">November 17, 2025</time>
      </p>
    </header>

    <section>
      <h2>Introduction</h2>
      <p>The article element represents...</p>
    </section>

    <section>
      <h2>Examples</h2>
      <p>Here are some use cases...</p>
    </section>

    <footer>
      <p><strong>Tags:</strong> HTML5, Semantics, Web Development</p>
      <p><strong>Share:</strong> [Social media links]</p>
    </footer>
  </article>
</main>
```

### Example 2: Nested Articles (Blog Post with Comments)

```html
<main>
  <article>
    <header>
      <h1>Main Blog Post Title</h1>
      <p>Author | Date</p>
    </header>

    <p>Blog post content...</p>

    <section>
      <h2>Comments</h2>

      <!-- Each comment is an article -->
      <article>
        <header>
          <h3>Comment by Jane Smith</h3>
          <p><time datetime="2025-11-17T14:30">Nov 17, 2025 at 2:30 PM</time></p>
        </header>
        <p>Great article! I learned a lot...</p>
      </article>

      <article>
        <header>
          <h3>Comment by Bob Johnson</h3>
          <p><time datetime="2025-11-17T15:45">Nov 17, 2025 at 3:45 PM</time></p>
        </header>
        <p>Thanks for sharing this...</p>
      </article>
    </section>
  </article>
</main>
```

### Example 3: Product Cards

```html
<main>
  <h1>Our Products</h1>

  <article>
    <img src="product1.jpg" alt="Product 1">
    <h2>Wireless Headphones</h2>
    <p>High-quality sound, 30-hour battery life.</p>
    <p><strong>$99.99</strong></p>
    <button>Add to Cart</button>
  </article>

  <article>
    <img src="product2.jpg" alt="Product 2">
    <h2>Smart Watch</h2>
    <p>Track your fitness and stay connected.</p>
    <p><strong>$199.99</strong></p>
    <button>Add to Cart</button>
  </article>
</main>
```

---

## Article vs Section

**Use `<article>` when:**
- Content is self-contained and makes sense independently
- Could be syndicated (RSS feed, social media)
- Examples: blog posts, news articles, product cards, comments

**Use `<section>` when:**
- Content is a thematic grouping within a larger document
- Needs parent context to make sense
- Examples: chapters, tabs, themed content blocks

**Example:**
```html
<!-- Article contains sections -->
<article>
  <h1>Complete Guide to HTML5</h1>

  <section>
    <h2>Chapter 1: Introduction</h2>
    <p>Content...</p>
  </section>

  <section>
    <h2>Chapter 2: Semantic Elements</h2>
    <p>Content...</p>
  </section>
</article>
```

---

## Best Practices

### Do This

1. **Include Heading in Every Article**
   ```html
   <article>
     <h2>Article Must Have Heading</h2>
     <p>Content...</p>
   </article>
   ```

2. **Use for Syndicated Content**
   ```html
   <!-- Each social media post is an article -->
   <article>
     <header>
       <h3>@username</h3>
       <time datetime="2025-11-17">Nov 17</time>
     </header>
     <p>Tweet content...</p>
     <footer>
       <button>Like</button>
       <button>Retweet</button>
     </footer>
   </article>
   ```

3. **Nest Articles When Appropriate**
   ```html
   <article>
     <h2>Blog Post</h2>
     <p>Post content...</p>

     <!-- Comments are nested articles -->
     <section>
       <h3>Comments</h3>
       <article>
         <h4>Comment Title</h4>
         <p>Comment content...</p>
       </article>
     </section>
   </article>
   ```

### Avoid This

1. **Don't Use for Non-Standalone Content**
   ```html
   <!-- WRONG: Navigation isn't standalone content -->
   <article>
     <nav>Menu items</nav>
   </article>

   <!-- CORRECT -->
   <nav>Menu items</nav>
   ```

2. **Don't Replace All Divs with Article**
   ```html
   <!-- WRONG: Using article just for styling -->
   <article class="card">
     <p>Not really standalone content...</p>
   </article>

   <!-- CORRECT: Use div for styling containers -->
   <div class="card">
     <p>Styled content...</p>
   </div>
   ```

---

## Related Topics
- [Semantic HTML Overview](semantic-overview.md)
- [Section Element](section.md)
- [Main Element](main.md)
- [Header Element](header.md)
- [Footer Element](footer.md)

---

**Last Updated:** November 17, 2025
**Category:** Semantic HTML5
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
