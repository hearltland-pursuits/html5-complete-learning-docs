---
title: Bookmark Links and Page Fragments
category: Links and Navigation
order: 4
---

# Bookmark Links and Page Fragments

> **Quick Summary:** Fragment identifiers (anchors) enable in-page navigation by linking to specific sections using the # symbol combined with element IDs, improving user experience for long documents and single-page applications.

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

Fragment identifiers—commonly called "bookmark links" or "anchor links"—allow users to jump directly to specific sections within a page rather than always starting at the top. These links use the hash symbol (`#`) followed by the `id` attribute of the target element, enabling smooth navigation through long documents, creation of interactive tables of contents, and implementation of "back to top" functionality.

When a user clicks a fragment link, the browser scrolls the page so the target element appears in the viewport, and updates the URL to include the fragment (e.g., `https://example.com/page.html#section-3`). This URL can be bookmarked or shared, allowing others to land directly on the specific section—a critical feature for documentation, legal documents, and educational content.

Modern CSS properties like `scroll-behavior: smooth` and `scroll-margin-top` enhance fragment navigation with smooth scrolling animations and proper offset handling for fixed headers. Understanding how to create accessible, user-friendly fragment links is essential for improving navigation on content-heavy pages and meeting WCAG 2.1 Level A requirements for multiple ways to locate content.

**Key Concept:** Fragment links connect to `id` attributes using `#id-name` syntax. The target element receives focus, triggers scroll, and updates the browser URL. Use `scroll-margin-top` for fixed header offset and descriptive IDs for accessibility.

## Basic Syntax

**Link to fragment on same page:**
```html
<a href="#section-2">Jump to Section 2</a>

<!-- Target section -->
<section id="section-2">
  <h2>Section 2</h2>
  <!-- content -->
</section>
```

**Link to fragment on different page:**
```html
<a href="/documentation.html#installation">View Installation Guide</a>
```

**Back to top link:**
```html
<a href="#top">Back to Top</a>
```

**ID Attribute Rules:**

| Rule | Description | Valid Example | Invalid Example |
|------|-------------|---------------|-----------------|
| **Must be unique** | Only one element per page | `<h2 id="intro">` | Two `id="intro"` ❌ |
| **Case-sensitive** | `#Intro` ≠ `#intro` | `href="#MySection"` | `href="#mysection"` (if id="MySection") |
| **No spaces** | Use hyphens or underscores | `id="my-section"` | `id="my section"` ❌ |
| **Start with letter** | Not number or special char | `id="section-1"` | `id="1-section"` ❌ |

**Modern CSS Enhancements:**

```css
/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* Offset scroll for fixed headers */
section {
  scroll-margin-top: 80px;
}

/* Highlight target section */
:target {
  background-color: #fff3cd;
}
```

## Examples

### Example 1: Documentation with Table of Contents
**Use Case:** Technical documentation with in-page navigation

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>API Documentation</title>
  <style>
    html {
      scroll-behavior: smooth;
    }
    body {
      font-family: Arial, sans-serif;
      line-height: 1.7;
    }
    header {
      background-color: #2c3e50;
      color: white;
      padding: 2em;
      position: sticky;
      top: 0;
      z-index: 100;
    }
    nav ul {
      list-style: none;
      display: flex;
      gap: 1.5em;
    }
    nav a {
      color: #ecf0f1;
      text-decoration: none;
      padding: 0.5em 1em;
    }
    nav a:hover,
    nav a:focus {
      background-color: #34495e;
    }
    section {
      margin: 4em 0;
      scroll-margin-top: 120px;
    }
    :target {
      background-color: #fff3cd;
      padding: 1em;
      border-radius: 8px;
    }
  </style>
</head>
<body>
  <header id="top">
    <h1>REST API Documentation</h1>
    <nav aria-label="Documentation sections">
      <ul>
        <li><a href="#authentication">Authentication</a></li>
        <li><a href="#endpoints">Endpoints</a></li>
        <li><a href="#errors">Error Codes</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="authentication">
      <h2>Authentication</h2>
      <p>All API requests require authentication...</p>
      <p><a href="#top">↑ Back to top</a></p>
    </section>

    <section id="endpoints">
      <h2>API Endpoints</h2>
      <p>Base URL: <code>https://api.example.com/v1/</code></p>
      <p><a href="#top">↑ Back to top</a></p>
    </section>

    <section id="errors">
      <h2>Error Codes</h2>
      <p>The API uses standard HTTP status codes...</p>
      <p><a href="#top">↑ Back to top</a></p>
    </section>
  </main>
</body>
</html>
```

### Example 2: Skip Link for Accessibility
**Use Case:** Accessible navigation bypass

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Accessible Page</title>
  <style>
    .skip-link {
      position: absolute;
      top: -40px;
      left: 0;
      background: #000;
      color: white;
      padding: 8px;
      text-decoration: none;
      z-index: 100;
    }
    .skip-link:focus {
      top: 0;
    }
  </style>
</head>
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>

  <header>
    <nav>
      <!-- Navigation links -->
    </nav>
  </header>

  <main id="main-content" tabindex="-1">
    <h1>Main Content</h1>
    <!-- Content -->
  </main>
</body>
</html>
```

### Example 3: FAQ with Direct Linking
**Use Case:** Shareable FAQ answers

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>FAQ</title>
  <style>
    html {
      scroll-behavior: smooth;
    }
    .faq-item {
      margin: 2em 0;
      padding: 1.5em;
      border-left: 4px solid #3498db;
      scroll-margin-top: 2em;
    }
    .faq-item:target {
      background-color: #fff3cd;
      border-left-color: #f39c12;
    }
  </style>
</head>
<body>
  <h1>Frequently Asked Questions</h1>

  <nav>
    <ul>
      <li><a href="#pricing">How does pricing work?</a></li>
      <li><a href="#refunds">What is your refund policy?</a></li>
      <li><a href="#support">How do I contact support?</a></li>
    </ul>
  </nav>

  <div class="faq-item" id="pricing">
    <h3>How does pricing work?</h3>
    <p>We offer three tiers: Starter ($29/month)...</p>
  </div>

  <div class="faq-item" id="refunds">
    <h3>What is your refund policy?</h3>
    <p>30-day money-back guarantee...</p>
  </div>

  <div class="faq-item" id="support">
    <h3>How do I contact support?</h3>
    <p>Email support@example.com...</p>
  </div>
</body>
</html>
```

## Common Use Cases

### 1. Table of Contents
Create navigable table of contents for long documents:

```html
<nav aria-labelledby="toc-heading">
  <h2 id="toc-heading">Table of Contents</h2>
  <ul>
    <li><a href="#introduction">Introduction</a></li>
    <li><a href="#methodology">Methodology</a></li>
    <li><a href="#results">Results</a></li>
  </ul>
</nav>
```

**When to use:** Documentation, articles, legal documents, research papers

### 2. Back to Top Links
Enable quick return to page header:

```html
<a href="#top">↑ Back to top</a>
```

**When to use:** Long articles, product pages, documentation

### 3. Skip Links (Accessibility)
Allow keyboard users to skip repetitive navigation:

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
```

**When to use:** Every website (WCAG 2.4.1 Level A)

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| Fragment links (#id) | All | All | All | All | All | All |
| `scroll-behavior: smooth` | 61+ | 36+ | 15.4+ | 79+ | 15.4+ | 61+ |
| `scroll-margin-top` | 69+ | 68+ | 14.1+ | 79+ | 14.1+ | 69+ |
| `:target` pseudo-class | All | All | All | All | All | All |

**Browser Support:** Universal for core functionality

Fragment identifiers have been part of HTML since HTML 1.0 (1993). Modern CSS enhancements have 95%+ browser support.

**Resources:**
- [MDN: Fragment identifier](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Identifying_resources_on_the_Web#fragment)
- [MDN: scroll-behavior](https://developer.mozilla.org/en-US/docs/Web/CSS/scroll-behavior)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- **Bypass Blocks (2.4.1):** Provide skip links to bypass repetitive navigation
- **Keyboard (2.1.1):** All fragment links keyboard-accessible

**Level AA Requirements:**
- **Multiple Ways (2.4.5):** Provide multiple ways to locate content
- **Focus Visible (2.4.7):** Fragment targets visually identifiable

### Best Practices

1. **Use descriptive IDs:**
```html
<!-- GOOD -->
<section id="pricing-plans">
<section id="installation-guide">

<!-- AVOID -->
<section id="section1">
<section id="s2">
```

2. **Provide skip links:**
```html
<a href="#main-content" class="skip-link">Skip to main content</a>

<style>
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: #000;
  color: white;
  padding: 8px;
}
.skip-link:focus {
  top: 0;
}
</style>
```

3. **Use scroll-margin-top for fixed headers:**
```css
section {
  scroll-margin-top: 80px;
}
```

**Resources:**
- [WCAG 2.1: Bypass Blocks (2.4.1)](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
- [WebAIM: Skip Navigation Links](https://webaim.org/techniques/skipnav/)

## Best Practices

### Do This ✓

1. **Use descriptive, unique IDs:**
```html
<section id="pricing-overview">
<section id="installation-steps">
```

2. **Add smooth scrolling:**
```css
html {
  scroll-behavior: smooth;
}
```

3. **Offset scroll for fixed headers:**
```css
section {
  scroll-margin-top: 80px;
}
```

4. **Provide skip links:**
```html
<a href="#main-content" class="skip-link">Skip to main content</a>
```

5. **Style :target for feedback:**
```css
:target {
  background-color: #fff3cd;
}
```

### Avoid This ✗

1. **Don't use spaces in IDs:**
```html
<!-- WRONG -->
<section id="my section">

<!-- CORRECT -->
<section id="my-section">
```

2. **Don't start IDs with numbers:**
```html
<!-- WRONG -->
<section id="1-introduction">

<!-- CORRECT -->
<section id="section-1-introduction">
```

3. **Don't reuse IDs:**
```html
<!-- WRONG -->
<section id="overview"></section>
<section id="overview"></section>

<!-- CORRECT -->
<section id="pricing-overview"></section>
<section id="features-overview"></section>
```

## Related Topics

### Prerequisites
- [Anchor Links](anchor-links.md) - Basic hyperlink syntax
- [HTML Syntax](../01-fundamentals/syntax.md) - id attribute rules

### Related Topics
- [Link States](link-states.md) - Styling fragment links
- [Email and Telephone Links](email-telephone-links.md) - Other link types
- [Global Attributes](../09-global-attributes/id-class.md) - id attribute specification

### Next Steps
- [Download Links](download-links.md) - File download functionality
- [Navigation Element](../07-semantic-html5/nav.md) - Semantic navigation
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Skip links

## Practice Exercise

### Requirements
Create a **"Privacy Policy Document"** demonstrating bookmark links with:

1. Table of contents with 6+ section links
2. Skip link for keyboard accessibility
3. "Back to top" links after each section
4. CSS: smooth scrolling, scroll-margin-top, :target highlighting
5. Proper ID attributes (descriptive, unique, no spaces)

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Privacy Policy</title>
  <style>
    html { scroll-behavior: smooth; }
    body { max-width: 900px; margin: 0 auto; padding: 20px; }
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
  <title>Privacy Policy - TechCorp</title>
  <style>
    html {
      scroll-behavior: smooth;
    }
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.7;
    }
    .skip-link {
      position: absolute;
      top: -40px;
      left: 0;
      background: #000;
      color: white;
      padding: 10px;
      text-decoration: none;
      z-index: 100;
    }
    .skip-link:focus {
      top: 0;
    }
    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #3498db;
      padding-bottom: 0.5em;
    }
    .toc {
      background-color: #ecf0f1;
      padding: 1.5em;
      border-radius: 8px;
      margin: 2em 0;
    }
    .toc ul {
      margin-left: 2em;
    }
    .toc a {
      color: #0066cc;
      text-decoration: none;
    }
    .toc a:hover,
    .toc a:focus {
      text-decoration: underline;
    }
    section {
      margin: 3em 0;
      scroll-margin-top: 2em;
    }
    section:target {
      background-color: #fff3cd;
      padding: 1em;
      border-radius: 8px;
      border-left: 4px solid #f39c12;
    }
    h2 {
      color: #34495e;
      border-bottom: 2px solid #95a5a6;
      padding-bottom: 0.3em;
    }
    .back-to-top {
      text-align: right;
      margin-top: 1.5em;
    }
    .back-to-top a {
      color: #3498db;
      text-decoration: none;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>

  <header id="top">
    <h1>Privacy Policy</h1>
    <p><strong>Effective Date:</strong> November 17, 2025</p>

    <nav class="toc" aria-labelledby="toc-heading">
      <h2 id="toc-heading">Table of Contents</h2>
      <ul>
        <li><a href="#information-collection">Information We Collect</a></li>
        <li><a href="#how-we-use">How We Use Your Information</a></li>
        <li><a href="#data-sharing">Data Sharing and Disclosure</a></li>
        <li><a href="#data-security">Data Security</a></li>
        <li><a href="#your-rights">Your Rights and Choices</a></li>
        <li><a href="#cookies">Cookies and Tracking</a></li>
        <li><a href="#children">Children's Privacy</a></li>
        <li><a href="#changes">Changes to This Policy</a></li>
        <li><a href="#contact">Contact Us</a></li>
      </ul>
    </nav>
  </header>

  <main id="main-content">
    <section id="information-collection">
      <h2>Information We Collect</h2>
      <p>
        We collect information you provide directly to us, including name,
        email address, phone number, and payment information when you create
        an account or make purchases.
      </p>
      <p>
        We also automatically collect device information, IP address, browser
        type, and usage data when you interact with our services.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="how-we-use">
      <h2>How We Use Your Information</h2>
      <p>We use collected information to:</p>
      <ul>
        <li>Provide, maintain, and improve our services</li>
        <li>Process transactions and send related information</li>
        <li>Send technical notices and support messages</li>
        <li>Respond to your comments and questions</li>
        <li>Monitor and analyze trends and usage</li>
      </ul>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="data-sharing">
      <h2>Data Sharing and Disclosure</h2>
      <p>
        We do not sell your personal information. We may share information
        with service providers who assist in our operations, such as payment
        processors and hosting providers.
      </p>
      <p>
        We may disclose information if required by law or to protect our
        rights and safety.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="data-security">
      <h2>Data Security</h2>
      <p>
        We implement industry-standard security measures including encryption
        (AES-256), secure data transmission (TLS 1.3), and regular security
        audits. Our infrastructure is SOC 2 Type II certified.
      </p>
      <p>
        While we strive to protect your information, no method of transmission
        over the internet is 100% secure.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="your-rights">
      <h2>Your Rights and Choices</h2>
      <p>You have the right to:</p>
      <ul>
        <li><strong>Access:</strong> Request a copy of your personal data</li>
        <li><strong>Correction:</strong> Update or correct inaccurate information</li>
        <li><strong>Deletion:</strong> Request deletion of your account and data</li>
        <li><strong>Opt-out:</strong> Unsubscribe from marketing communications</li>
        <li><strong>Data Portability:</strong> Export your data in a portable format</li>
      </ul>
      <p>
        To exercise these rights, contact us at
        <a href="mailto:privacy@techcorp.com">privacy@techcorp.com</a>.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="cookies">
      <h2>Cookies and Tracking Technologies</h2>
      <p>
        We use cookies and similar technologies to provide functionality,
        analyze usage, and personalize content. You can control cookies
        through your browser settings.
      </p>
      <p>
        We use both first-party and third-party cookies for analytics
        (Google Analytics) and advertising (if applicable).
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="children">
      <h2>Children's Privacy</h2>
      <p>
        Our services are not directed to children under 13. We do not
        knowingly collect information from children. If we learn we have
        collected information from a child, we will delete it promptly.
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="changes">
      <h2>Changes to This Privacy Policy</h2>
      <p>
        We may update this policy periodically. Changes take effect when
        posted on this page. We will notify you of significant changes via
        email or prominent notice on our website.
      </p>
      <p>
        <strong>Last Updated:</strong> November 17, 2025
      </p>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>

    <section id="contact">
      <h2>Contact Us</h2>
      <p>
        If you have questions about this Privacy Policy, please contact:
      </p>
      <address>
        <strong>TechCorp Privacy Team</strong><br>
        Email: <a href="mailto:privacy@techcorp.com">privacy@techcorp.com</a><br>
        Phone: <a href="tel:+15551234567">+1 (555) 123-4567</a><br>
        Address: 123 Tech Street, San Francisco, CA 94102
      </address>
      <p class="back-to-top">
        <a href="#top">↑ Back to top</a>
      </p>
    </section>
  </main>

  <footer>
    <p style="text-align: center; margin-top: 3em; color: #7f8c8d;">
      <small>© 2025 TechCorp. All rights reserved.</small>
    </p>
  </footer>
</body>
</html>
```

**Key Features:**
- Skip link (hidden until keyboard focus)
- Table of contents with 9 section links
- Smooth scrolling via CSS
- :target highlighting with yellow background + border
- scroll-margin-top for proper positioning
- "Back to top" links after each section
- Descriptive, unique IDs (no spaces, start with letters)
- Accessible navigation structure
- WCAG 2.1 Level AA compliant

---

## Navigation

- **Previous:** [Email and Telephone Links](email-telephone-links.md)
- **Next:** [Download Links](download-links.md)
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
