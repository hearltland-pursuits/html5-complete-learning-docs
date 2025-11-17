---
title: HTML Comments
category: Fundamentals
order: 4
---

# HTML Comments

> **Quick Summary:** HTML comments allow developers to add notes, documentation, and explanations to code without affecting the rendered page. They're essential for code maintainability and team collaboration.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Accessibility Considerations](#accessibility-considerations)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

HTML comments are invisible annotations in your code. They exist solely for developers—browsers ignore them when rendering pages, and users never see them (unless they view page source). Comments serve three critical purposes: explaining complex code, temporarily disabling sections during development, and providing context for future maintainers (including your future self).

In professional development, comments become even more important when working in teams. A well-commented codebase allows new developers to understand structure quickly, explains why certain approaches were chosen, and documents known issues or future enhancements. Think of comments as documentation embedded directly in your code.

However, comments come with a caveat: they're visible in page source. Never include sensitive information (passwords, API keys, internal notes about security vulnerabilities) in HTML comments. Malicious users can view source and read every comment. Use comments for code documentation, not secrets.

**Key Concept:** Comments are for developers, not users. Write comments that explain **why** code exists, not just **what** it does. The code itself should be clear enough to show what it does.

---

## Basic Syntax

```html
<!-- This is a single-line comment -->

<!--
  This is a multi-line comment.
  It can span multiple lines.
  Useful for longer explanations.
-->

<!-- Comments can appear anywhere -->
<div class="container"> <!-- Inline comment after element -->
  <p>Content</p>
</div>

<!--
  Comments cannot be nested:
  <!-- This is INVALID -->
-->
```

### Comment Syntax Rules

| Rule | Description | Example |
|------|-------------|---------|
| Start delimiter | `<!--` (no space after `<`) | `<!--` |
| End delimiter | `-->` (no space before `>`) | `-->` |
| Content | Any text except `--` sequence | `<!-- Valid comment -->` |
| Nesting | **NOT** allowed | Cannot put `<!--` inside another comment |
| Location | Anywhere in HTML document | Before DOCTYPE, in head, in body |

### Invalid Comment Syntax

```html
<!-- Invalid: Double dashes inside comment -- are not allowed -->
<!-- Invalid: Missing closing delimiter
<!-- Invalid nesting <!-- inner comment --> -->
<! Invalid: Missing double dashes >
```

---

## Examples

### Example 1: Documenting Code Sections

**Scenario:** Organizing a complex page with clear section markers

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Documented Page</title>
</head>
<body>
  <!-- ========================================
       HEADER SECTION
       Contains site branding and main navigation
       ======================================== -->
  <header>
    <h1>My Website</h1>
    <nav>
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
      </ul>
    </nav>
  </header>

  <!-- ========================================
       MAIN CONTENT AREA
       Primary page content and articles
       ======================================== -->
  <main>
    <article>
      <h2>Article Title</h2>
      <p>Article content...</p>
    </article>
  </main>

  <!-- ========================================
       FOOTER SECTION
       Copyright and secondary navigation
       ======================================== -->
  <footer>
    <p>&copy; 2025 Joshua Hickman</p>
  </footer>
</body>
</html>
```

**Result:** Clear section markers help developers quickly navigate large HTML files. The visual separators (equal signs) make sections obvious when scrolling.

---

### Example 2: Temporarily Disabling Code

**Scenario:** Testing different layouts by commenting out sections

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Testing Layouts</title>
</head>
<body>
  <header>
    <h1>Website Header</h1>
  </header>

  <!-- TODO: Testing new hero section layout
  <section class="hero-old">
    <h2>Old Hero Design</h2>
    <p>This is the old approach we're replacing.</p>
  </section>
  -->

  <!-- New hero section (currently testing) -->
  <section class="hero-new">
    <h2>New Hero Design</h2>
    <p>This is the new responsive hero section.</p>
  </section>

  <!--
  DEBUGGING NOTE:
  The carousel below is causing performance issues on mobile.
  Temporarily disabled until we implement lazy loading.

  <div class="carousel">
    <img src="slide1.jpg" alt="Slide 1">
    <img src="slide2.jpg" alt="Slide 2">
  </div>
  -->

  <main>
    <p>Main content here...</p>
  </main>
</body>
</html>
```

**Result:** Commented-out code remains in the file for reference but doesn't render. This is useful during development but should be removed before production deployment.

---

### Example 3: Developer Notes and TODOs

**Scenario:** Documenting future enhancements and known issues

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Project Dashboard</title>
</head>
<body>
  <header>
    <h1>Dashboard</h1>
    <!-- TODO: Add user profile dropdown menu here -->
  </header>

  <main>
    <section class="stats">
      <h2>Statistics</h2>
      <!--
        FIXME: Stats are hardcoded.
        Need to connect to API endpoint: /api/stats
        See ticket #1234 for details.
      -->
      <p>Total Users: 1,250</p>
      <p>Active Sessions: 47</p>
    </section>

    <section class="charts">
      <h2>Analytics</h2>
      <!--
        NOTE: Chart library (Chart.js) loaded via CDN.
        Consider self-hosting for better performance.
        Dependencies: Chart.js v3.9.1
      -->
      <canvas id="traffic-chart"></canvas>
    </section>

    <!--
      SECURITY: This form needs CSRF protection
      before going to production. Currently disabled
      in development environment only.
    -->
    <form action="/api/update" method="post">
      <input type="text" name="username">
      <button type="submit">Update</button>
    </form>
  </main>

  <!--
    PERFORMANCE NOTE:
    This page loads 15 JavaScript files (850KB total).
    Consider bundling and minification before launch.
    Target: < 200KB compressed.
  -->
</body>
</html>
```

**Result:** Comprehensive documentation that helps developers understand context, known issues, and future work. Keywords like TODO, FIXME, NOTE, and SECURITY make comments searchable.

**Notes:**
- Use consistent prefixes (TODO, FIXME, NOTE) to categorize comments
- Reference ticket numbers for issue tracking
- Document **why** decisions were made, not just **what** code does
- Remove or resolve comments before production deployment

---

## Common Use Cases

### Use Case 1: Conditional Comments (Legacy IE)
**When:** Supporting old Internet Explorer browsers (now deprecated)
**How:**
```html
<!-- Historical reference only - no longer needed -->
<!--[if IE]>
  <p>You are using Internet Explorer.</p>
<![endif]-->

<!--[if lt IE 9]>
  <script src="html5shiv.js"></script>
<![endif]-->
```
**Why:** Conditional comments were IE-specific syntax for serving content only to IE. Modern development doesn't use these—IE is deprecated and unsupported.

---

### Use Case 2: Version Control and Change Tracking
**When:** Documenting major changes in HTML files
**How:**
```html
<!--
  CHANGELOG:
  2025-11-17 - Joshua Hickman
    - Added accessibility improvements (ARIA labels)
    - Restructured navigation for mobile-first design
    - Replaced deprecated <font> tags with CSS classes

  2025-10-15 - Joshua Hickman
    - Initial page structure created
-->
<header>
  <nav aria-label="Main navigation">
    <!-- Navigation content -->
  </nav>
</header>
```
**Why:** For small projects without version control systems, comments can track changes. However, Git commit messages are better for this purpose.

---

### Use Case 3: Embedding Data for Tools
**When:** Providing metadata for build tools, CMS, or generators
**How:**
```html
<!--
  Template: homepage.html
  Author: Joshua Hickman
  Last Modified: 2025-11-17
  Description: Main landing page template for bootcamp website
-->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Homepage</title>
</head>
<body>
  <!-- CMS: editable-region-start -->
  <main>
    <h1>Welcome</h1>
    <p>Edit this content in the CMS.</p>
  </main>
  <!-- CMS: editable-region-end -->
</body>
</html>
```
**Why:** Some content management systems and build tools use comments as markers for template regions, includes, or metadata.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | Comments fully supported since browser inception |
| Firefox | All     | Full Support  | Perfect comment support |
| Safari  | All     | Full Support  | Full support on all platforms |
| Edge    | All     | Full Support  | Complete compatibility |
| IE 11   | All     | Full Support  | Standard comments supported (conditional comments deprecated) |

**Fallback Strategy:**
Comments are part of the core HTML specification since HTML 2.0 (1995). No fallback needed—all browsers support comments.

**Can I Use Link:** N/A (universal support)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Comments have no direct accessibility impact (invisible to users)
- Don't rely on comments to communicate with users—use visible text
- Screen readers ignore comments completely

**Level AA Requirements:**
- Comments don't affect accessibility ratings
- Ensure commented-out code doesn't create hidden traps or confusion

### Screen Reader Support

```html
<!-- Screen readers IGNORE this comment completely -->
<p>Screen readers read this paragraph.</p>

<!-- BAD: Don't use comments for user instructions -->
<!-- Click the button below to submit -->
<button>Submit</button>

<!-- GOOD: Use visible text for user instructions -->
<p>Click the button below to submit your form.</p>
<button>Submit</button>
```

**Key Points:**
- Comments are developer-only—assistive technologies never announce them
- Don't hide important user information in comments
- Commented-out code doesn't create accessibility issues (it's not rendered)

### Keyboard Navigation

Comments have zero impact on keyboard navigation. They don't exist in the accessibility tree or DOM interaction model.

---

## Best Practices

### Do This

1. **Explain Why, Not What**
   ```html
   <!-- GOOD: Explains reasoning -->
   <!-- Using absolute positioning here to keep the modal
        centered during scroll. Flexbox caused issues in Safari 14. -->
   <div class="modal" style="position: absolute;">

   <!-- BAD: States the obvious -->
   <!-- This is a div with class modal -->
   <div class="modal">
   ```
   **Why:** Code should be self-explanatory for "what" it does. Comments add value by explaining "why" decisions were made.

2. **Use Consistent Comment Styles**
   ```html
   <!-- TODO: Add form validation -->
   <!-- FIXME: Button click broken on mobile -->
   <!-- NOTE: This section renders on homepage only -->
   <!-- WARNING: Changing this breaks email templates -->
   ```
   **Why:** Standard prefixes make comments searchable and categorizable. Teams can search for "TODO" to find pending work.

3. **Keep Comments Updated**
   ```html
   <!-- GOOD: Accurate comment -->
   <!-- User avatar loads from CDN: cdn.example.com/avatars/ -->
   <img src="https://cdn.example.com/avatars/user123.jpg" alt="User avatar">

   <!-- BAD: Outdated comment (code changed, comment didn't) -->
   <!-- User avatar loads from local server -->
   <img src="https://cdn.example.com/avatars/user123.jpg" alt="User avatar">
   ```
   **Why:** Outdated comments mislead developers and create bugs. Update or remove comments when code changes.

---

### Avoid This

1. **Don't Leave Sensitive Information in Comments**
   ```html
   <!-- BAD: Exposes credentials -->
   <!-- Database password: SuperSecret123! -->
   <!-- API key: sk_live_abc123xyz789 -->
   <!-- Admin URL: https://example.com/secret-admin-panel -->
   ```
   **Why Not:** Anyone can view page source and read your comments. Attackers search for credentials in comments.
   **Instead:** Store sensitive data in environment variables or server-side configuration files.

2. **Don't Comment Out Large Code Blocks Long-Term**
   ```html
   <!-- BAD: 200 lines of commented-out old code -->
   <!--
   <div class="old-layout">
     ... 200 lines of unused HTML ...
   </div>
   -->
   ```
   **Why Not:** Commented code bloats file size and confuses maintainers. Use version control (Git) to track old code instead.
   **Instead:** Delete unused code. Git history preserves it if you need to reference it later.

3. **Don't Use Comments for Version Control**
   ```html
   <!-- BAD: Manual version tracking -->
   <!-- Version 1.0 - Initial release -->
   <!-- Version 1.1 - Added footer -->
   <!-- Version 1.2 - Fixed navbar -->
   ```
   **Why Not:** Git commit messages handle version tracking better and don't bloat HTML files.
   **Instead:** Use Git for version control and write meaningful commit messages.

---

## Related Topics

**Prerequisites (Learn These First):**
- [HTML5 Introduction](introduction.md) - Basic HTML5 concepts
- [HTML5 Syntax](syntax.md) - Understanding HTML structure

**Related Concepts:**
- [Validation](validation.md) - Comments don't affect validation
- [Document Structure](document-structure.md) - Where comments can appear
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Code that documents itself

**Next Steps (Learn These Next):**
- [Validation](validation.md) - Validate your commented HTML
- [Character Encoding](character-encoding.md) - UTF-8 and special characters in comments
- [Deprecated Elements](deprecated-elements.md) - What to avoid (and comment out)

**External Resources:**
- [MDN - HTML Comments](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started#html_comments)
- [W3Schools - HTML Comments](https://www.w3schools.com/html/html_comments.asp)
- [HTML Living Standard - Comments](https://html.spec.whatwg.org/multipage/syntax.html#comments)

---

## Practice Exercise

### Challenge: Document a Complex Page

**Objective:** Add meaningful comments to an uncommented HTML5 page, improving its documentation and maintainability.

**Requirements:**
- [ ] Add section header comments for major page areas
- [ ] Document at least 2 "why" comments (explaining decisions)
- [ ] Add 1 TODO comment for future enhancements
- [ ] Include 1 NOTE comment about dependencies or requirements
- [ ] Ensure no sensitive information appears in comments
- [ ] Bonus: Use consistent comment style (TODO, NOTE, etc.)

---

### Starter Code

**HTML (needs documentation):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>E-Commerce Product Page</title>
  <link rel="stylesheet" href="styles.css">
  <script src="https://cdn.example.com/analytics.js"></script>
</head>
<body>
  <header>
    <h1>TechStore</h1>
    <nav>
      <a href="/">Home</a>
      <a href="/products">Products</a>
      <a href="/cart">Cart</a>
    </nav>
  </header>

  <main>
    <div class="product">
      <img src="laptop.jpg" alt="Laptop" width="500" height="400">
      <h2>Premium Laptop</h2>
      <p class="price">$1,299.99</p>
      <button class="add-to-cart" data-product-id="12345">Add to Cart</button>
    </div>

    <section class="reviews">
      <h3>Customer Reviews</h3>
      <div class="review">
        <p>Great laptop! Fast shipping.</p>
        <p class="rating">5/5 stars</p>
      </div>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 TechStore. All rights reserved.</p>
  </footer>

  <script src="cart.js"></script>
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**HTML (well-documented):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>E-Commerce Product Page</title>

  <!-- Main stylesheet includes responsive layout and product grid -->
  <link rel="stylesheet" href="styles.css">

  <!--
    NOTE: Analytics loaded early to track page views immediately.
    CDN version 3.2.1 - self-hosted version available in /vendor/
  -->
  <script src="https://cdn.example.com/analytics.js"></script>
</head>
<body>
  <!-- ========================================
       SITE HEADER
       Main navigation and branding
       ======================================== -->
  <header>
    <h1>TechStore</h1>
    <nav>
      <a href="/">Home</a>
      <a href="/products">Products</a>
      <a href="/cart">Cart</a>
      <!-- TODO: Add user account dropdown here -->
    </nav>
  </header>

  <!-- ========================================
       MAIN CONTENT - PRODUCT DETAILS
       Single product display with reviews
       ======================================== -->
  <main>
    <!--
      WHY: Using div instead of semantic <article> here because
      this content is dynamically loaded and replaced via AJAX.
      Semantic elements caused screen reader issues during updates.
    -->
    <div class="product">
      <!--
        NOTE: Product images are 500x400 to maintain aspect ratio
        across all products. Resizing happens server-side.
      -->
      <img src="laptop.jpg" alt="Premium 15-inch laptop with backlit keyboard" width="500" height="400">

      <h2>Premium Laptop</h2>
      <p class="price">$1,299.99</p>

      <!--
        data-product-id connects to cart.js for inventory tracking.
        ID must match database product table primary key.
      -->
      <button class="add-to-cart" data-product-id="12345">Add to Cart</button>
    </div>

    <!-- Customer Reviews Section -->
    <section class="reviews">
      <h3>Customer Reviews</h3>
      <!--
        FIXME: Reviews are hardcoded for testing.
        Connect to API: /api/reviews/{product_id}
        See ticket #456 for backend implementation.
      -->
      <div class="review">
        <p>Great laptop! Fast shipping.</p>
        <p class="rating">5/5 stars</p>
      </div>
    </section>
  </main>

  <!-- ========================================
       FOOTER
       Copyright and legal information
       ======================================== -->
  <footer>
    <p>&copy; 2025 TechStore. All rights reserved.</p>
    <!-- TODO: Add privacy policy and terms of service links -->
  </footer>

  <!--
    WHY: cart.js loaded at end of body (not in head) to ensure
    DOM is fully loaded before script executes. Improves page
    load performance and prevents race conditions.
  -->
  <script src="cart.js"></script>
</body>
</html>
```

**Explanation:**
This solution adds five types of comments: (1) Section headers that divide the page into clear areas, (2) "WHY" comments explaining non-obvious decisions (like using `div` instead of `article`), (3) TODO comments for future work, (4) NOTE comments documenting dependencies and requirements, and (5) FIXME comments identifying known issues. Each comment adds value by explaining context that isn't obvious from code alone.

</details>

---

### Expected Result

**Visual Outcome:** The page looks identical (comments don't affect rendering), but the code is now well-documented and easier for developers to understand and maintain.

**Key Learnings:**
- Comments explain "why" code exists, not "what" it does
- Consistent comment prefixes (TODO, FIXME, NOTE) make code searchable
- Comments should be updated when code changes
- Never include sensitive information in comments (visible in page source)

---

## Navigation

**Previous:** [HTML5 Syntax](syntax.md)
**Next:** [HTML5 Validation](validation.md)
**Up:** [Fundamentals](../README.md#1-fundamentals-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Fundamentals
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
