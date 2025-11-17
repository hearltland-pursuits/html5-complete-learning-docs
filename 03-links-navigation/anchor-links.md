---
title: Anchor Links and Hyperlinks
category: Links and Navigation
order: 1
---

# Anchor Links and Hyperlinks

> **Quick Summary:** The anchor element (a) creates hyperlinks that connect web pages, sections within pages, files, email addresses, and phone numbers, forming the foundation of web navigation and the interconnected nature of the World Wide Web.

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

## Introduction

The anchor element (`<a>`) is one of the most fundamental elements in HTML, enabling the hyperlink functionality that makes the web "a web." Hyperlinks allow users to navigate between pages, jump to specific sections within a document, download files, send emails, or initiate phone calls—all with a single click or tap.

The `href` (hypertext reference) attribute defines the link's destination, accepting absolute URLs (complete web addresses), relative URLs (paths relative to the current page), fragment identifiers (anchors to page sections), or special protocols like `mailto:` and `tel:`. Understanding how to construct proper href values is essential for creating functional, maintainable navigation systems.

Links serve multiple critical functions beyond navigation: they establish relationships between content (rel attribute), improve SEO through internal linking structures, and provide context to assistive technologies through accessible link text. The HTML5 specification expanded the anchor element's flexibility, allowing it to wrap block-level elements like entire article previews, not just inline text.

**Key Concept:** Anchors create connections—between pages (external links), within pages (fragment links), and to resources (files, emails, phone numbers). The href attribute defines the destination, while link text describes it.

## Basic Syntax

**Basic link structure:**
```html
<a href="destination">Link Text</a>
```

**Core Attributes:**

| Attribute | Purpose | Value Examples | Required |
|-----------|---------|----------------|----------|
| `href` | Link destination (URL) | `https://example.com`, `/page.html`, `#section` | Yes |
| `target` | Where to open link | `_self` (default), `_blank`, `_parent`, `_top` | No |
| `rel` | Relationship to destination | `noopener`, `noreferrer`, `nofollow`, `external` | No |
| `download` | Prompt download instead of navigate | Filename or boolean | No |
| `hreflang` | Language of linked resource | `en`, `es`, `fr`, etc. | No |
| `type` | MIME type of destination | `application/pdf`, `image/jpeg` | No |
| `title` | Advisory information (tooltip) | Descriptive text | No |

**Link Types:**

```html
<!-- Absolute URL (external link) -->
<a href="https://www.example.com">Visit Example Site</a>

<!-- Relative URL (same site) -->
<a href="/about.html">About Us</a>
<a href="../contact.html">Contact</a>
<a href="products/item.html">View Product</a>

<!-- Fragment identifier (same page) -->
<a href="#top">Back to Top</a>
<a href="#section-2">Jump to Section 2</a>

<!-- Different page + fragment -->
<a href="/docs/guide.html#installation">Installation Guide</a>

<!-- Email link -->
<a href="mailto:contact@example.com">Email Us</a>

<!-- Phone link -->
<a href="tel:+1-555-123-4567">Call Us</a>

<!-- File download -->
<a href="/files/report.pdf" download>Download Report (PDF)</a>
```

## Examples

### Example 1: Basic Website Navigation
**Use Case:** Standard website navigation menu with internal links

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Company Website</title>
  <style>
    nav {
      background-color: #2c3e50;
      padding: 1em 0;
    }
    nav ul {
      list-style: none;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      gap: 2em;
    }
    nav a {
      color: white;
      text-decoration: none;
      padding: 0.5em 1em;
      border-radius: 4px;
      transition: background-color 0.3s;
    }
    nav a:hover,
    nav a:focus {
      background-color: #34495e;
      outline: 2px solid #3498db;
      outline-offset: 2px;
    }
    nav a:active {
      background-color: #1abc9c;
    }
  </style>
</head>
<body>
  <header>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about.html">About</a></li>
        <li><a href="/services.html">Services</a></li>
        <li><a href="/portfolio.html">Portfolio</a></li>
        <li><a href="/blog/">Blog</a></li>
        <li><a href="/contact.html">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <h1>Welcome to Our Company</h1>
    <p>
      Learn more <a href="/about.html">about our team</a> or
      <a href="/contact.html">get in touch</a> to discuss your project.
    </p>
  </main>
</body>
</html>
```

### Example 2: External Links with Security Best Practices
**Use Case:** Blog post with external references using proper security attributes

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Web Development Resources</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.7;
    }
    a[target="_blank"]::after {
      content: " ↗";
      font-size: 0.8em;
      vertical-align: super;
    }
    a[rel~="external"] {
      color: #3498db;
    }
    a[rel~="external"]:visited {
      color: #9b59b6;
    }
  </style>
</head>
<body>
  <article>
    <h1>Essential Web Development Resources</h1>

    <section>
      <h2>Official Documentation</h2>
      <ul>
        <li>
          <a href="https://developer.mozilla.org/"
             target="_blank"
             rel="noopener noreferrer external">
            MDN Web Docs
          </a> - Comprehensive web technology documentation
        </li>
        <li>
          <a href="https://html.spec.whatwg.org/"
             target="_blank"
             rel="noopener noreferrer external">
            WHATWG HTML Living Standard
          </a> - Official HTML specification
        </li>
        <li>
          <a href="https://www.w3.org/WAI/WCAG21/quickref/"
             target="_blank"
             rel="noopener noreferrer external">
            WCAG 2.1 Quick Reference
          </a> - Accessibility guidelines
        </li>
      </ul>
    </section>

    <section>
      <h2>Learning Platforms</h2>
      <ul>
        <li>
          <a href="https://www.freecodecamp.org/"
             target="_blank"
             rel="noopener noreferrer external">
            freeCodeCamp
          </a> - Free coding bootcamp
        </li>
        <li>
          <a href="https://www.codecademy.com/"
             target="_blank"
             rel="noopener noreferrer external">
            Codecademy
          </a> - Interactive coding courses
        </li>
      </ul>
    </section>

    <section>
      <h2>Internal Resources</h2>
      <p>
        Check out our <a href="/tutorials/">beginner tutorials</a> or
        join our <a href="/community.html">community forum</a>.
      </p>
    </section>
  </article>
</body>
</html>
```

### Example 3: Skip Links and In-Page Navigation
**Use Case:** Accessible documentation with table of contents and skip links

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>HTML5 Semantic Elements Guide</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    .skip-link {
      position: absolute;
      top: -40px;
      left: 0;
      background-color: #000;
      color: white;
      padding: 8px;
      text-decoration: none;
      z-index: 100;
    }
    .skip-link:focus {
      top: 0;
    }
    .toc {
      background-color: #f4f4f4;
      padding: 1.5em;
      border-left: 4px solid #3498db;
      margin: 2em 0;
    }
    .toc ul {
      margin: 0.5em 0;
    }
    section {
      margin: 3em 0;
      scroll-margin-top: 2em;
    }
    h2 {
      border-bottom: 2px solid #3498db;
      padding-bottom: 0.5em;
    }
    .back-to-top {
      text-align: right;
      margin-top: 1em;
    }
  </style>
</head>
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>

  <header>
    <h1 id="top">HTML5 Semantic Elements Guide</h1>

    <nav class="toc" aria-labelledby="toc-heading">
      <h2 id="toc-heading">Table of Contents</h2>
      <ul>
        <li><a href="#introduction">Introduction</a></li>
        <li><a href="#header-element">The Header Element</a></li>
        <li><a href="#nav-element">The Nav Element</a></li>
        <li><a href="#main-element">The Main Element</a></li>
        <li><a href="#article-element">The Article Element</a></li>
        <li><a href="#section-element">The Section Element</a></li>
        <li><a href="#footer-element">The Footer Element</a></li>
      </ul>
    </nav>
  </header>

  <main id="main-content">
    <section id="introduction">
      <h2>Introduction</h2>
      <p>
        HTML5 introduced semantic elements that describe the meaning of
        content, not just its presentation. This guide explores the most
        commonly used semantic elements.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="header-element">
      <h2>The Header Element</h2>
      <p>
        The <code>&lt;header&gt;</code> element represents introductory
        content or navigation aids. It typically contains headings, logos,
        search forms, or author information.
      </p>
      <p>
        For more details, see the
        <a href="https://html.spec.whatwg.org/multipage/sections.html#the-header-element"
           target="_blank"
           rel="noopener noreferrer external">
          WHATWG specification
        </a>.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="nav-element">
      <h2>The Nav Element</h2>
      <p>
        The <code>&lt;nav&gt;</code> element contains major navigation
        blocks. Not all links need to be in a nav element—only significant
        navigation sections.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="main-element">
      <h2>The Main Element</h2>
      <p>
        The <code>&lt;main&gt;</code> element contains the primary content
        of the page. There should be only one main element per page, and
        it shouldn't be nested inside article, aside, footer, header, or
        nav elements.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="article-element">
      <h2>The Article Element</h2>
      <p>
        The <code>&lt;article&gt;</code> element represents self-contained
        content that could be distributed independently—like blog posts,
        news articles, or forum posts.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="section-element">
      <h2>The Section Element</h2>
      <p>
        The <code>&lt;section&gt;</code> element represents a thematic
        grouping of content, typically with a heading. Sections group
        related content within an article or page.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="footer-element">
      <h2>The Footer Element</h2>
      <p>
        The <code>&lt;footer&gt;</code> element represents footer content
        for its nearest ancestor sectioning element. It typically contains
        copyright information, links to related documents, or contact details.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>
  </main>

  <footer>
    <p>
      <small>© 2025 | <a href="/privacy.html">Privacy Policy</a> |
      <a href="/terms.html">Terms of Service</a></small>
    </p>
  </footer>
</body>
</html>
```

## Common Use Cases

### 1. Navigation Menus
Create site-wide navigation linking to major sections:

```html
<nav aria-label="Main navigation">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/products/">Products</a></li>
    <li><a href="/about.html">About</a></li>
    <li><a href="/contact.html">Contact</a></li>
  </ul>
</nav>
```

**When to use:** Site headers, footers, sidebars, breadcrumbs

### 2. External Resources (target="_blank")
Link to external sites that open in new tabs:

```html
<a href="https://www.example.com"
   target="_blank"
   rel="noopener noreferrer">
  Visit Example Site
</a>
```

**When to use:** Documentation references, social media links, external tools, affiliate links

**Security note:** Always use `rel="noopener noreferrer"` with `target="_blank"` to prevent security vulnerabilities

### 3. Fragment Links (Jump to Section)
Create table of contents or "back to top" links:

```html
<!-- Link to section -->
<a href="#installation">Jump to Installation</a>

<!-- Target section -->
<section id="installation">
  <h2>Installation</h2>
  <!-- content -->
</section>
```

**When to use:** Long documents, documentation, FAQs, legal pages

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| `<a>` element | All | All | All | All | All | All |
| `href` attribute | All | All | All | All | All | All |
| `target="_blank"` | All | All | All | All | All | All |
| `rel="noopener"` | 49+ | 52+ | 10.1+ | 79+ | 10.3+ | 49+ |
| `download` attribute | 14+ | 20+ | 10.1+ | 18+ | 13+ | 18+ |
| Wrapping block elements | 5+ | 4+ | 5+ | All | All | All |

**Browser Support:** Universal for core functionality

The anchor element has been part of HTML since the beginning (HTML 1.0, 1993). All modern browsers fully support anchors, including wrapping block-level elements (HTML5 feature).

**Default Styling:**
- Color: Blue (#0000EE) for unvisited links
- Color: Purple (#551A8B) for visited links
- Cursor: Pointer (hand icon)
- Text decoration: Underline

**Resources:**
- [MDN: a element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a)
- [WHATWG HTML Living Standard: a element](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-a-element)
- [W3Schools: HTML Links](https://www.w3schools.com/html/html_links.asp)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- **Link Purpose (2.4.4):** Link text must describe the link's purpose (or be understandable from context)
- **Keyboard:** All links must be operable via keyboard (default browser behavior)
- **Focus Visible (2.4.7):** Links must have visible focus indicator

**Level AA Requirements:**
- **Link Purpose in Context (2.4.4):** Link text alone should describe purpose (don't rely on surrounding context)
- **Visual Presentation:** Links must have sufficient color contrast (4.5:1 minimum)
- **Multiple Ways (2.4.5):** Provide multiple ways to find pages (navigation, search, sitemap)

### Screen Reader Behavior

**Link List Navigation:**
- Screen readers can generate lists of all links on a page
- Users navigate by jumping between links
- Link text is announced out of context

**Problematic link text:**
```html
<!-- BAD: Meaningless out of context -->
<a href="/report.pdf">Click here</a>
<a href="/more.html">Read more</a>
<a href="/page2.html">Learn more</a>
```

**Accessible link text:**
```html
<!-- GOOD: Descriptive and unique -->
<a href="/report.pdf">Download Q4 2025 Financial Report (PDF)</a>
<a href="/accessibility.html">Read more about web accessibility</a>
<a href="/services.html">Learn more about our consulting services</a>
```

### Best Practices for Screen Readers

1. **Write descriptive link text:**
```html
<!-- GOOD -->
<a href="/contact.html">Contact our customer support team</a>

<!-- BAD -->
<a href="/contact.html">Click here</a>
```

2. **Avoid generic phrases:**
```html
<!-- AVOID: Generic, non-descriptive -->
Click here | Read more | Learn more | More info | This page

<!-- PREFER: Specific, descriptive -->
Download pricing guide | View installation instructions | Explore career opportunities
```

3. **Indicate file type and size for downloads:**
```html
<a href="/manual.pdf">
  Download User Manual (PDF, 2.3 MB)
</a>
```

4. **Warn before opening new windows:**
```html
<a href="https://example.com"
   target="_blank"
   rel="noopener noreferrer">
  Visit Example.com <span class="sr-only">(opens in new tab)</span>
</a>
```

5. **Use aria-label for icon links:**
```html
<a href="https://twitter.com/company"
   aria-label="Follow us on Twitter">
  <svg><!-- Twitter icon --></svg>
</a>
```

**Resources:**
- [WCAG 2.1: Link Purpose (2.4.4)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
- [WebAIM: Links and Hypertext](https://webaim.org/techniques/hypertext/)

## Best Practices

### Do This ✓

1. **Use descriptive link text:**
```html
<!-- Correct -->
<a href="/pricing.html">View pricing plans</a>
<a href="/report.pdf">Download 2025 Annual Report (PDF)</a>
```

2. **Secure external links with rel="noopener noreferrer":**
```html
<!-- Correct: Prevents security vulnerabilities -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Visit Example
</a>
```

3. **Use relative URLs for internal links:**
```html
<!-- Correct: Relative URLs -->
<a href="/about.html">About</a>
<a href="../contact.html">Contact</a>

<!-- AVOID: Absolute URLs for same site -->
<a href="https://mysite.com/about.html">About</a>
```

4. **Ensure keyboard accessibility:**
```css
a:focus {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}
```

5. **Provide visual distinction for links:**
```css
a {
  color: #0066cc;
  text-decoration: underline;
}
a:visited {
  color: #551A8B;
}
a:hover,
a:focus {
  color: #004499;
}
```

### Avoid This ✗

1. **Don't use generic link text:**
```html
<!-- WRONG -->
<a href="/more.html">Click here</a>
<a href="/details.html">Read more</a>

<!-- CORRECT -->
<a href="/accessibility-guide.html">Read our accessibility guide</a>
```

2. **Don't open new windows without warning:**
```html
<!-- WRONG: Opens new tab without warning -->
<a href="https://example.com" target="_blank">Example</a>

<!-- CORRECT: Indicates new window -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
  Example (opens in new tab)
</a>
```

3. **Don't use href="#" for JavaScript-only links:**
```html
<!-- WRONG: Non-functional without JavaScript -->
<a href="#" onclick="doSomething()">Click</a>

<!-- CORRECT: Use button for actions -->
<button type="button" onclick="doSomething()">Click</button>
```

4. **Don't rely on color alone:**
```html
<!-- WRONG: Only color distinguishes links -->
<style>
a { color: blue; text-decoration: none; }
</style>

<!-- CORRECT: Color + underline -->
<style>
a { color: #0066cc; text-decoration: underline; }
</style>
```

5. **Don't use empty href:**
```html
<!-- WRONG: Empty href -->
<a href="">Home</a>

<!-- CORRECT: Provide actual destination -->
<a href="/">Home</a>
```

## Related Topics

### Prerequisites
- [HTML Syntax](../01-fundamentals/syntax.md) - Element and attribute syntax
- [Document Structure](../01-fundamentals/document-structure.md) - Page structure and navigation

### Related Topics
- [Link States](link-states.md) - Styling link states (hover, visited, active)
- [Email and Telephone Links](email-telephone-links.md) - mailto: and tel: protocols
- [Bookmark Links](bookmark-links.md) - Fragment identifiers and in-page navigation
- [Download Links](download-links.md) - download attribute for file downloads
- [Global Attributes](../09-global-attributes/id-class.md) - id attribute for fragment targets

### Next Steps
- [Link States and Styling](link-states.md) - CSS pseudo-classes for links
- [Navigation Element](../07-semantic-html5/nav.md) - Semantic navigation structure
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Making links accessible

## Practice Exercise

### Requirements
Create a **"Personal Portfolio Website Navigation"** that demonstrates proper use of anchor links. Your HTML document should include:

1. A main navigation menu with at least 5 internal links
2. A "Skip to main content" accessibility link
3. At least 3 external links with proper security attributes
4. A table of contents with fragment links to page sections
5. At least one download link
6. Social media links with proper aria-labels
7. CSS styling that includes:
   - Distinct styles for link states (default, visited, hover, focus, active)
   - Visible focus indicators for keyboard navigation
   - Sufficient color contrast (WCAG AA compliant)

**Accessibility Requirements:**
- Descriptive link text (no "click here" or "read more")
- Skip link for keyboard users
- aria-label for icon links
- Warning for links opening in new tabs
- File type and size for download links

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Portfolio - Your Name</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    /* Add your link styling here */
  </style>
</head>
<body>
  <!-- Add your content here -->

</body>
</html>
```

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Portfolio - Alex Johnson</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: Arial, Helvetica, sans-serif;
      max-width: 1000px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.7;
    }

    /* Skip Link */
    .skip-link {
      position: absolute;
      top: -40px;
      left: 0;
      background-color: #000;
      color: white;
      padding: 10px;
      text-decoration: none;
      z-index: 100;
      font-weight: bold;
    }
    .skip-link:focus {
      top: 0;
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }

    /* Navigation */
    nav {
      background-color: #2c3e50;
      padding: 1em 0;
      margin-bottom: 2em;
      border-radius: 8px;
    }
    nav ul {
      list-style: none;
      display: flex;
      justify-content: center;
      gap: 2em;
      flex-wrap: wrap;
    }
    nav a {
      color: white;
      text-decoration: none;
      padding: 0.5em 1em;
      border-radius: 4px;
      transition: all 0.3s;
      font-weight: 500;
    }
    nav a:hover {
      background-color: #34495e;
    }
    nav a:focus {
      outline: 3px solid #3498db;
      outline-offset: 2px;
      background-color: #34495e;
    }
    nav a:active {
      background-color: #1abc9c;
    }

    /* Link Styling */
    a {
      color: #0066cc;
      text-decoration: underline;
      transition: color 0.2s;
    }
    a:visited {
      color: #551A8B;
    }
    a:hover {
      color: #004499;
      text-decoration-thickness: 2px;
    }
    a:focus {
      outline: 2px solid #FF6B6B;
      outline-offset: 2px;
      border-radius: 2px;
    }
    a:active {
      color: #FF6B6B;
    }

    /* External Link Indicator */
    a[target="_blank"]::after {
      content: " ↗";
      font-size: 0.8em;
      vertical-align: super;
    }

    /* Sections */
    section {
      margin: 3em 0;
      scroll-margin-top: 2em;
    }
    h1, h2 {
      color: #2c3e50;
      margin-bottom: 0.5em;
    }
    h1 {
      border-bottom: 3px solid #3498db;
      padding-bottom: 0.5em;
    }
    h2 {
      border-bottom: 2px solid #95a5a6;
      padding-bottom: 0.3em;
      margin-top: 1.5em;
    }

    /* Table of Contents */
    .toc {
      background-color: #ecf0f1;
      padding: 1.5em;
      border-left: 5px solid #3498db;
      margin: 2em 0;
    }
    .toc ul {
      margin-left: 2em;
    }
    .toc li {
      margin: 0.5em 0;
    }

    /* Social Links */
    .social-links {
      display: flex;
      gap: 1.5em;
      margin: 1em 0;
    }
    .social-links a {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 50px;
      height: 50px;
      background-color: #3498db;
      color: white;
      border-radius: 50%;
      text-decoration: none;
      font-weight: bold;
      font-size: 1.5em;
      transition: all 0.3s;
    }
    .social-links a:hover {
      background-color: #2980b9;
      transform: scale(1.1);
    }
    .social-links a:focus {
      outline: 3px solid #FF6B6B;
      outline-offset: 3px;
    }

    /* Download Button */
    .download-link {
      display: inline-block;
      background-color: #27ae60;
      color: white !important;
      padding: 0.75em 1.5em;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      margin: 1em 0;
      transition: background-color 0.3s;
    }
    .download-link:hover {
      background-color: #229954;
    }
    .download-link:focus {
      outline: 3px solid #FF6B6B;
      outline-offset: 3px;
    }

    /* Back to Top */
    .back-to-top {
      text-align: right;
      margin-top: 1em;
      font-size: 0.9em;
    }

    /* Screen Reader Only */
    .sr-only {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      white-space: nowrap;
      border-width: 0;
    }
  </style>
</head>
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>

  <header>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#experience">Experience</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </nav>

    <h1 id="top">Alex Johnson - Web Developer</h1>

    <nav class="toc" aria-labelledby="toc-heading">
      <h2 id="toc-heading">On This Page</h2>
      <ul>
        <li><a href="#about">About Me</a></li>
        <li><a href="#projects">Featured Projects</a></li>
        <li><a href="#skills">Technical Skills</a></li>
        <li><a href="#experience">Work Experience</a></li>
        <li><a href="#contact">Contact Information</a></li>
      </ul>
    </nav>
  </header>

  <main id="main-content">
    <section id="about">
      <h2>About Me</h2>
      <p>
        I'm a full-stack web developer with 5 years of experience building
        responsive, accessible websites and web applications. I specialize
        in modern JavaScript frameworks and have a passion for creating
        inclusive digital experiences.
      </p>
      <p>
        You can view my work on
        <a href="https://github.com/alexjohnson"
           target="_blank"
           rel="noopener noreferrer">
          GitHub
        </a> or read my technical articles on
        <a href="https://dev.to/alexjohnson"
           target="_blank"
           rel="noopener noreferrer">
          DEV Community
        </a>.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="projects">
      <h2>Featured Projects</h2>

      <article>
        <h3>E-Commerce Platform</h3>
        <p>
          Built a fully responsive e-commerce platform using React, Node.js,
          and MongoDB. Features include user authentication, shopping cart,
          payment integration, and admin dashboard.
        </p>
        <p>
          <a href="https://github.com/alexjohnson/ecommerce-platform"
             target="_blank"
             rel="noopener noreferrer">
            View source code on GitHub
          </a> |
          <a href="https://ecommerce-demo.example.com"
             target="_blank"
             rel="noopener noreferrer">
            View live demo
          </a>
        </p>
      </article>

      <article>
        <h3>Weather Dashboard</h3>
        <p>
          Created an accessible weather dashboard using HTML5, CSS3, and
          vanilla JavaScript. Integrates with OpenWeatherMap API and follows
          WCAG 2.1 Level AA guidelines.
        </p>
        <p>
          <a href="/projects/weather-dashboard.html">
            View project details
          </a>
        </p>
      </article>

      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="skills">
      <h2>Technical Skills</h2>
      <ul>
        <li>Frontend: HTML5, CSS3, JavaScript (ES6+), React, Vue.js</li>
        <li>Backend: Node.js, Express, Python, Django</li>
        <li>Databases: MongoDB, PostgreSQL, MySQL</li>
        <li>Tools: Git, Docker, Webpack, VS Code</li>
        <li>Accessibility: WCAG 2.1, ARIA, Screen reader testing</li>
      </ul>

      <p>
        Download my complete resume:
        <a href="/files/alex-johnson-resume.pdf"
           download
           class="download-link">
          Download Resume (PDF, 250 KB)
        </a>
      </p>

      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="experience">
      <h2>Work Experience</h2>

      <article>
        <h3>Senior Web Developer - Tech Solutions Inc.</h3>
        <p><strong>2022 - Present</strong></p>
        <p>
          Lead development of client web applications, mentor junior developers,
          and establish accessibility standards for the development team.
        </p>
      </article>

      <article>
        <h3>Web Developer - Creative Agency</h3>
        <p><strong>2020 - 2022</strong></p>
        <p>
          Built responsive websites for diverse clients, implemented SEO best
          practices, and conducted accessibility audits.
        </p>
      </article>

      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="contact">
      <h2>Contact Information</h2>
      <p>
        I'm always interested in new opportunities and collaborations.
        Feel free to reach out!
      </p>

      <p>
        <strong>Email:</strong>
        <a href="mailto:alex@example.com">alex@example.com</a><br>
        <strong>Phone:</strong>
        <a href="tel:+1-555-123-4567">+1 (555) 123-4567</a><br>
        <strong>Location:</strong> San Francisco, CA
      </p>

      <h3>Connect With Me</h3>
      <div class="social-links">
        <a href="https://github.com/alexjohnson"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Visit my GitHub profile (opens in new tab)">
          <span aria-hidden="true">GH</span>
        </a>
        <a href="https://linkedin.com/in/alexjohnson"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Connect on LinkedIn (opens in new tab)">
          <span aria-hidden="true">in</span>
        </a>
        <a href="https://twitter.com/alexjohnson"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Follow me on Twitter (opens in new tab)">
          <span aria-hidden="true">𝕏</span>
        </a>
        <a href="https://codepen.io/alexjohnson"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="View my CodePen projects (opens in new tab)">
          <span aria-hidden="true">CP</span>
        </a>
      </div>

      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>
  </main>

  <footer>
    <p>
      <small>
        © 2025 Alex Johnson | <a href="/privacy.html">Privacy Policy</a> |
        <a href="/sitemap.html">Sitemap</a>
      </small>
    </p>
  </footer>
</body>
</html>
```

**Key Features of Solution:**
- Skip link for keyboard accessibility (hidden until focused)
- Main navigation with 5 internal links
- Table of contents with fragment links to page sections
- 6+ external links with `target="_blank"` and `rel="noopener noreferrer"`
- Download link with file type and size indication
- Social media icon links with descriptive `aria-label` attributes
- "Back to top" links in each section
- Comprehensive CSS for all link states (default, visited, hover, focus, active)
- Visible focus indicators (3px outlines with offset)
- Sufficient color contrast (WCAG AA compliant):
  - Links: #0066cc on white = 7.7:1 ratio
  - Visited: #551A8B on white = 8.6:1 ratio
- External link indicator (↗ symbol) via CSS
- Screen reader-only class for hidden text
- Descriptive link text throughout (no "click here")
- Warning for new tab links (via aria-label)
- scroll-margin-top on sections for better fragment navigation

---

## Navigation

- **Previous:** [Text Direction](../02-text-content/text-direction.md)
- **Next:** [Link States and Styling](link-states.md)
- **Up:** [Links and Navigation](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Links and Navigation
- **Difficulty:** Beginner to Intermediate
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
