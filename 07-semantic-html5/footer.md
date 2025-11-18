---
title: Footer Element
category: Semantic HTML5
order: 8
---

# Footer Element

> **Quick Summary:** The `<footer>` element represents footer content for its nearest sectioning element (page, article, section). It typically contains copyright info, author details, related links, and contact information. Screen readers announce it as "contentinfo" landmark when it's the page footer.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `<footer>` element represents footer content—information about its containing element. It can be used for the page footer (site-wide footer) or for footers within articles, sections, or other sectioning content. Content typically includes copyright notices, author information, related links, and contact details.

**Key points:**
- Can appear multiple times per page (page footer + article footers)
- Page-level footer is "contentinfo" landmark for screen readers
- Often contains copyright, links, contact info, social media
- Not restricted to bottom of page (though commonly placed there)

**Key Concept:** Use `<footer>` for footer content at the page or section level. Page footer becomes "contentinfo" landmark for screen readers, improving navigation.

---

## Basic Syntax

```html
<!-- Page footer -->
<footer>
  <p>&copy; 2025 Company Name. All rights reserved.</p>
  <nav>
    <a href="/privacy">Privacy Policy</a>
    <a href="/terms">Terms of Service</a>
  </nav>
</footer>

<!-- Article footer -->
<article>
  <h1>Article Title</h1>
  <p>Article content...</p>

  <footer>
    <p>Published: <time datetime="2025-11-17">Nov 17, 2025</time></p>
    <p>Tags: HTML5, Semantics</p>
  </footer>
</article>
```

---

## Examples

### Example 1: Site Footer

```html
<footer>
  <div class="footer-content">
    <section>
      <h2>About Us</h2>
      <p>We are a company dedicated to...</p>
    </section>

    <section>
      <h2>Quick Links</h2>
      <nav>
        <ul>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
          <li><a href="/careers">Careers</a></li>
        </ul>
      </nav>
    </section>

    <section>
      <h2>Contact</h2>
      <p>Email: info@company.com</p>
      <p>Phone: (555) 123-4567</p>
    </section>

    <section>
      <h2>Follow Us</h2>
      <nav aria-label="Social media">
        <a href="https://twitter.com/company">Twitter</a>
        <a href="https://facebook.com/company">Facebook</a>
      </nav>
    </section>
  </div>

  <div class="footer-bottom">
    <p>&copy; 2025 Company Name. All rights reserved.</p>
    <nav>
      <a href="/privacy">Privacy Policy</a>
      <a href="/terms">Terms of Service</a>
    </nav>
  </div>
</footer>
```

### Example 2: Blog Post Footer

```html
<article>
  <header>
    <h1>Understanding HTML5 Footer Element</h1>
    <p>By John Doe</p>
  </header>

  <section>
    <h2>Introduction</h2>
    <p>Article content...</p>
  </section>

  <footer>
    <p>
      <strong>Published:</strong> <time datetime="2025-11-17">November 17, 2025</time> |
      <strong>Updated:</strong> <time datetime="2025-11-17">November 17, 2025</time>
    </p>

    <p><strong>Tags:</strong>
      <a href="/tags/html5">HTML5</a>,
      <a href="/tags/semantics">Semantics</a>,
      <a href="/tags/accessibility">Accessibility</a>
    </p>

    <p><strong>Share:</strong>
      <a href="#">Twitter</a>
      <a href="#">Facebook</a>
      <a href="#">LinkedIn</a>
    </p>

    <section>
      <h3>About the Author</h3>
      <p>John Doe is a web developer with 10 years of experience...</p>
    </section>
  </footer>
</article>
```

### Example 3: Newsletter Footer

```html
<footer>
  <section>
    <h2>Subscribe to Our Newsletter</h2>
    <form action="/subscribe" method="POST">
      <label for="email">Email:</label>
      <input type="email" id="email" name="email" required>
      <button type="submit">Subscribe</button>
    </form>
  </section>

  <section>
    <h2>Company</h2>
    <nav>
      <ul>
        <li><a href="/about">About</a></li>
        <li><a href="/team">Team</a></li>
        <li><a href="/careers">Careers</a></li>
      </ul>
    </nav>
  </section>

  <p>&copy; 2025 Company. All rights reserved.</p>
</footer>
```

---

## Best Practices

### Do This

1. **Include Copyright and Legal Links**
   ```html
   <footer>
     <p>&copy; 2025 Company Name</p>
     <nav>
       <a href="/privacy">Privacy</a>
       <a href="/terms">Terms</a>
     </nav>
   </footer>
   ```

2. **Use for Article Metadata**
   ```html
   <article>
     <h1>Article Title</h1>
     <p>Content...</p>

     <footer>
       <p>Author: Jane Doe</p>
       <p>Published: Nov 17, 2025</p>
     </footer>
   </article>
   ```

3. **Organize with Sections**
   ```html
   <footer>
     <section>
       <h2>About</h2>
       <p>Info...</p>
     </section>

     <section>
       <h2>Contact</h2>
       <p>Contact details...</p>
     </section>
   </footer>
   ```

### Avoid This

1. **Don't Nest Footers**
   ```html
   <!-- WRONG -->
   <footer>
     <footer>Nested footer</footer>
   </footer>
   ```

2. **Don't Use for Non-Footer Content**
   ```html
   <!-- WRONG: Main navigation isn't footer content -->
   <footer>
     <nav>
       <a href="/">Home</a>
       <a href="/products">Products</a>
     </nav>
   </footer>

   <!-- CORRECT: Use header for main nav -->
   <header>
     <nav>
       <a href="/">Home</a>
       <a href="/products">Products</a>
     </nav>
   </header>
   ```

---

## Related Topics
- [Semantic HTML Overview](semantic-overview.md)
- [Header Element](header.md)
- [Article Element](article.md)

---

**Last Updated:** November 17, 2025
**Category:** Semantic HTML5
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
