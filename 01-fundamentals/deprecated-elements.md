---
title: Deprecated HTML4 Elements
category: Fundamentals
order: 8
---

# Deprecated HTML4 Elements

> **Quick Summary:** Deprecated elements are outdated HTML4 tags removed from HTML5. They mixed presentation with content and are replaced by semantic HTML and CSS for better accessibility, maintainability, and standards compliance.

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

HTML5 deprecated dozens of presentational elements that mixed styling with structure. Elements like `<font>`, `<center>`, and `<big>` controlled appearance directly in HTML, violating the separation of concerns principle. Modern web development uses HTML for structure, CSS for presentation, and JavaScript for behavior—keeping each layer independent.

Why were these elements deprecated? They created unmaintainable code where styling was hardcoded in markup. Changing site-wide fonts or colors required editing every HTML file. Screen readers struggled with presentational markup that lacked semantic meaning. Search engines couldn't distinguish important content from decorative styling.

HTML5 replaced deprecated elements with semantic alternatives and CSS. Instead of `<font color="red">`, use `<span class="error">` styled with CSS. Instead of `<center>`, use `text-align: center` in CSS. This separation improves accessibility, SEO, maintainability, and follows modern web standards.

**Key Concept:** Deprecated elements still work in browsers (for backward compatibility) but fail HTML5 validation and should never be used in new projects. Always use semantic HTML5 elements with CSS styling.

---

## Basic Syntax

### Deprecated vs Modern Alternatives

```html
<!-- DEPRECATED: Presentational HTML4 -->
<font color="red" size="5">Important Text</font>
<center>Centered Content</center>
<big>Large Text</big>
<strike>Strikethrough</strike>

<!-- MODERN: Semantic HTML5 + CSS -->
<p class="important">Important Text</p>
<div class="centered">Centered Content</div>
<p class="large">Large Text</p>
<del>Strikethrough (with semantic meaning)</del>

<!-- CSS for styling -->
<style>
  .important { color: red; font-size: 1.5em; }
  .centered { text-align: center; }
  .large { font-size: 1.2em; }
</style>
```

### Complete List of Deprecated Elements

| Deprecated Element | Purpose | Modern Alternative |
|-------------------|---------|-------------------|
| `<acronym>` | Acronyms | `<abbr>` (abbreviation) |
| `<applet>` | Java applets | `<object>` or `<embed>` |
| `<basefont>` | Default font | CSS `font-family` |
| `<big>` | Larger text | CSS `font-size` |
| `<center>` | Centered content | CSS `text-align: center` |
| `<dir>` | Directory list | `<ul>` with CSS |
| `<font>` | Font styling | CSS `font` properties |
| `<frame>` | Framesets | CSS Grid, Flexbox, or `<iframe>` |
| `<frameset>` | Frame container | Modern layout techniques |
| `<noframes>` | Non-frame fallback | Not needed (frames deprecated) |
| `<strike>` | Strikethrough | `<del>` (deletion) or `<s>` (inaccurate) |
| `<tt>` | Teletype text | `<code>` or `<kbd>` |
| `<u>` | Underline | CSS `text-decoration: underline` (or avoid—looks like links) |

### Deprecated Attributes (on valid elements)

| Element | Deprecated Attributes | Modern Alternative |
|---------|----------------------|-------------------|
| `<body>` | `bgcolor`, `text`, `link`, `vlink`, `alink` | CSS color properties |
| `<table>` | `border`, `cellpadding`, `cellspacing`, `bgcolor` | CSS border, padding, background |
| `<img>` | `align`, `border`, `hspace`, `vspace` | CSS float, border, margin |
| `<div>` | `align` | CSS text-align or flexbox |
| `<p>` | `align` | CSS text-align |
| `<h1>`-`<h6>` | `align` | CSS text-align |

---

## Examples

### Example 1: Font and Text Styling Migration

**Scenario:** Updating old HTML4 styling to modern HTML5 + CSS

**HTML4 (deprecated):**
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN">
<html>
<head>
  <title>Old Page</title>
</head>
<body bgcolor="#FFFFFF" text="#000000">
  <center>
    <font face="Arial" size="5" color="red">
      <b>Welcome to Our Site</b>
    </font>
  </center>

  <p>
    <font size="3" color="#333333">
      This is a paragraph with <big>large text</big> and
      <font color="blue">colored text</font>.
    </font>
  </p>

  <center>
    <font size="2">
      <i>Copyright 2025</i>
    </font>
  </center>
</body>
</html>
```

**HTML5 (modern):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Modern Page</title>
  <style>
    body {
      background-color: #FFFFFF;
      color: #000000;
      font-family: Arial, sans-serif;
    }
    .hero {
      text-align: center;
      font-size: 2em;
      color: red;
      font-weight: bold;
    }
    .content {
      font-size: 1em;
      color: #333333;
    }
    .emphasis {
      font-size: 1.2em;
    }
    .highlight {
      color: blue;
    }
    .copyright {
      text-align: center;
      font-size: 0.875em;
      font-style: italic;
    }
  </style>
</head>
<body>
  <header>
    <h1 class="hero">Welcome to Our Site</h1>
  </header>

  <main>
    <p class="content">
      This is a paragraph with <span class="emphasis">large text</span> and
      <span class="highlight">colored text</span>.
    </p>
  </main>

  <footer class="copyright">
    <p>Copyright 2025</p>
  </footer>
</body>
</html>
```

**Result:** Modern code is more maintainable (CSS in one place), semantic (h1, header, footer), and accessible (proper structure for screen readers).

---

### Example 2: Table Attributes Migration

**Scenario:** Removing deprecated table styling attributes

**HTML4 (deprecated):**
```html
<table border="1" cellpadding="10" cellspacing="0" bgcolor="#f0f0f0" width="100%">
  <tr bgcolor="#cccccc">
    <td align="center" width="50%"><font color="red">Column 1</font></td>
    <td align="right"><b>Column 2</b></td>
  </tr>
  <tr>
    <td valign="top">Data 1</td>
    <td>Data 2</td>
  </tr>
</table>
```

**HTML5 (modern):**
```html
<table class="data-table">
  <thead>
    <tr>
      <th>Column 1</th>
      <th>Column 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Data 1</td>
      <td>Data 2</td>
    </tr>
  </tbody>
</table>

<style>
  .data-table {
    width: 100%;
    border-collapse: collapse;
    background-color: #f0f0f0;
  }
  .data-table th,
  .data-table td {
    border: 1px solid #ddd;
    padding: 10px;
  }
  .data-table th {
    background-color: #cccccc;
    text-align: center;
    font-weight: bold;
  }
  .data-table th:first-child {
    color: red;
    width: 50%;
  }
  .data-table th:last-child {
    text-align: right;
  }
  .data-table td:first-child {
    vertical-align: top;
  }
</style>
```

**Result:** Semantic table structure with CSS styling. The `<thead>` and `<tbody>` elements improve accessibility, and CSS provides flexible styling.

---

### Example 3: Frame to Modern Layout Migration

**Scenario:** Replacing deprecated frames with modern layout

**HTML4 (deprecated - frames):**
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN">
<html>
<head>
  <title>Framed Site</title>
</head>
<frameset cols="200,*">
  <frame src="nav.html" name="navigation">
  <frame src="content.html" name="main">
  <noframes>
    <p>Your browser does not support frames.</p>
  </noframes>
</frameset>
</html>
```

**HTML5 (modern - flexbox layout):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Modern Layout</title>
  <style>
    body {
      margin: 0;
      display: flex;
      min-height: 100vh;
    }
    nav {
      width: 200px;
      background-color: #f0f0f0;
      padding: 20px;
    }
    main {
      flex: 1;
      padding: 20px;
    }
  </style>
</head>
<body>
  <nav>
    <h2>Navigation</h2>
    <ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <main>
    <h1>Main Content</h1>
    <p>Content goes here...</p>
  </main>
</body>
</html>
```

**Result:** Modern layout using CSS Flexbox is responsive, accessible, SEO-friendly, and doesn't suffer from frame navigation issues.

**Notes:**
- Frames broke browser back button behavior
- Frames prevented bookmarking specific pages
- Frames created accessibility nightmares for screen readers
- Modern CSS Grid and Flexbox solve all frame use cases better

---

## Common Use Cases

### Use Case 1: Updating Legacy Websites
**When:** Maintaining or modernizing old HTML4 websites
**How:**
```html
<!-- Find and replace patterns -->
<!-- Old: --> <font color="red">Error</font>
<!-- New: --> <span class="error">Error</span>

<!-- Old: --> <center>Content</center>
<!-- New: --> <div class="centered">Content</div>

<!-- Old: --> <big>Important</big>
<!-- New: --> <strong class="large">Important</strong>

<!-- Add CSS -->
<style>
  .error { color: red; }
  .centered { text-align: center; }
  .large { font-size: 1.2em; }
</style>
```
**Why:** Gradual migration from deprecated elements improves code quality and validation while maintaining visual appearance.

---

### Use Case 2: Code Review and Validation
**When:** Ensuring codebase doesn't use deprecated elements
**How:**
```bash
# Search for deprecated elements in project
grep -r "<font" .
grep -r "<center" .
grep -r "<big" .
grep -r "<strike" .

# Use W3C Validator to catch deprecated attributes
# https://validator.w3.org/
```
**Why:** Automated checks catch deprecated elements before they reach production.

---

### Use Case 3: Teaching Web Development
**When:** Explaining why certain approaches are outdated
**How:**
```html
<!-- Teaching example: Why <font> is bad -->

<!-- WRONG (deprecated): -->
<p>
  Welcome to <font color="red" size="5">Our Store</font>!
  Save <font color="green">20%</font> today.
</p>

<!-- RIGHT (semantic + CSS): -->
<p>
  Welcome to <span class="brand">Our Store</span>!
  Save <span class="discount">20%</span> today.
</p>

<style>
  .brand {
    color: red;
    font-size: 1.5em;
    font-weight: bold;
  }
  .discount {
    color: green;
    font-weight: bold;
  }
</style>

<!-- Benefits explained:
  1. Separation of concerns (HTML = structure, CSS = style)
  2. Reusable classes (.discount can be used anywhere)
  3. Easy to change (edit CSS once, affects all .brand elements)
  4. Semantic meaning (.discount tells what it is, not just how it looks)
-->
```
**Why:** Understanding deprecated elements helps developers appreciate modern web standards and avoid old patterns.

---

## Browser Support

| Browser | Deprecated Elements | Notes |
|---------|-------------------|-------|
| Chrome  | Still render (backward compatibility) | Validation fails, not recommended |
| Firefox | Still render | Renders but deprecated |
| Safari  | Still render | Legacy support only |
| Edge    | Still render | Works but invalid HTML5 |
| IE 11   | Full support | Old browser, deprecated elements work |

**Fallback Strategy:**
Deprecated elements still work in all browsers for backward compatibility. However, they fail HTML5 validation and should be replaced with modern alternatives.

**Can I Use Link:** N/A (deprecated = don't use, even though browsers support them)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Semantic HTML improves structure for assistive technologies
- Presentational elements (`<font>`, `<center>`) provide no semantic meaning
- Screen readers benefit from proper heading hierarchy, not font sizes

**Level AA Requirements:**
- Separation of content and presentation improves maintainability
- CSS provides better control over contrast ratios than inline styling
- Semantic elements create clear document structure

### Screen Reader Support

```html
<!-- BAD: Presentational markup (no semantic meaning) -->
<font size="5">Important Heading</font>
<!-- Screen reader announces: "Important Heading" (no indication it's a heading) -->

<!-- GOOD: Semantic markup -->
<h2>Important Heading</h2>
<!-- Screen reader announces: "Heading level 2, Important Heading" -->

<!-- BAD: Visual emphasis only -->
<big>This is important</big>
<!-- Screen reader: No emphasis conveyed -->

<!-- GOOD: Semantic emphasis -->
<strong>This is important</strong>
<!-- Screen reader: Emphasis conveyed through intonation or announcement -->
```

**Key Points:**
- Deprecated elements lack semantic meaning
- Screen readers rely on semantic HTML to convey structure
- CSS visual styling doesn't communicate importance to assistive technologies
- Use semantic elements (`<strong>`, `<em>`, `<h1>`-`<h6>`) for meaningful content

### Keyboard Navigation

Deprecated elements don't directly affect keyboard navigation, but poor structure from presentational markup can create confusing navigation order.

---

## Best Practices

### Do This

1. **Use Semantic HTML5 Elements**
   ```html
   <!-- GOOD: Semantic structure -->
   <article>
     <header>
       <h1>Article Title</h1>
     </header>
     <p class="intro">Introduction text...</p>
     <p>Main content...</p>
   </article>
   ```
   **Why:** Semantic elements convey meaning to browsers, search engines, and assistive technologies.

2. **Separate Content from Presentation**
   ```html
   <!-- GOOD: HTML for structure, CSS for style -->
   <p class="warning">This action cannot be undone.</p>

   <style>
     .warning {
       color: red;
       font-weight: bold;
       border-left: 4px solid red;
       padding-left: 10px;
     }
   </style>
   ```
   **Why:** Changing visual style doesn't require editing HTML. Styles can be reused site-wide.

3. **Validate HTML5 Compliance**
   ```bash
   # Use W3C Validator to catch deprecated elements
   # https://validator.w3.org/

   # Output will show:
   # Error: The font element is obsolete. Use CSS instead.
   # Error: The center element is obsolete. Use CSS instead.
   ```
   **Why:** Validation catches deprecated elements and ensures standards compliance.

---

### Avoid This

1. **Don't Use Deprecated Elements (Even Though They Work)**
   ```html
   <!-- BAD: Works but fails validation -->
   <font color="red">Error message</font>
   <center>Centered content</center>
   ```
   **Why Not:** Deprecated elements fail HTML5 validation, hurt SEO, and demonstrate outdated coding practices.
   **Instead:** Use semantic HTML + CSS.

2. **Don't Mix Inline Styles Excessively**
   ```html
   <!-- BAD: Inline styles (hard to maintain) -->
   <p style="color: red; font-size: 20px; font-weight: bold;">Text</p>
   ```
   **Why Not:** Inline styles are only slightly better than deprecated elements. They still mix presentation with content.
   **Instead:** Use CSS classes for reusable, maintainable styling.

3. **Don't Use `<u>` for Non-Link Underlines**
   ```html
   <!-- BAD: Underline looks like a link -->
   <p>This is <u>underlined text</u>.</p>
   ```
   **Why Not:** Users expect underlined text to be clickable links. This creates confusion.
   **Instead:** Use `<strong>` or `<em>` for emphasis, or CSS `border-bottom` if you need visual underlines that aren't links.

---

## Related Topics

**Prerequisites (Learn These First):**
- [HTML5 Introduction](introduction.md) - Why HTML5 deprecated these elements
- [HTML5 Syntax](syntax.md) - Valid HTML5 structure

**Related Concepts:**
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Modern semantic elements
- [Text Formatting](../02-text-content/text-formatting.md) - Proper text styling
- [Validation](validation.md) - Detecting deprecated elements

**Next Steps (Learn These Next):**
- [Semantic HTML5 Overview](../07-semantic-html5/semantic-overview.md) - Modern semantic markup
- [CSS Fundamentals](../../{atlas}Education_css/01-fundamentals/introduction.md) - Styling with CSS
- [Accessibility](../13-accessibility/accessibility-overview.md) - Accessible markup

**External Resources:**
- [MDN - Deprecated HTML Features](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#deprecated_and_obsolete_elements)
- [W3C - HTML5 Differences from HTML4](https://www.w3.org/TR/html5-diff/)
- [HTML5 Doctor - Element Index](http://html5doctor.com/element-index/)

---

## Practice Exercise

### Challenge: Modernize a Legacy HTML4 Page

**Objective:** Convert an old HTML4 page using deprecated elements to valid, semantic HTML5 with CSS styling.

**Requirements:**
- [ ] Remove all deprecated elements (`<font>`, `<center>`, `<big>`, etc.)
- [ ] Replace with semantic HTML5 elements
- [ ] Create external CSS for all styling
- [ ] Ensure page validates at validator.w3.org
- [ ] Maintain visual appearance while modernizing code
- [ ] Bonus: Improve accessibility with semantic structure

---

### Starter Code

**HTML4 (legacy code to modernize):**
```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
  <title>Legacy Website</title>
</head>
<body bgcolor="#F0F0F0" text="#000000">
  <center>
    <font face="Arial" size="6" color="#CC0000">
      <b>Welcome to TechStore</b>
    </font>
  </center>

  <hr>

  <font face="Verdana" size="3">
    <center>
      <b>Featured Products</b>
    </center>

    <p align="left">
      Check out our <big><font color="blue">amazing deals</font></big>!
    </p>

    <table border="1" cellpadding="5" cellspacing="0" width="80%" align="center" bgcolor="#FFFFFF">
      <tr bgcolor="#CCCCCC">
        <td align="center"><font color="red"><b>Product</b></font></td>
        <td align="center"><b>Price</b></td>
      </tr>
      <tr>
        <td>Laptop</td>
        <td align="right"><font color="green">$999</font></td>
      </tr>
      <tr>
        <td>Monitor</td>
        <td align="right"><font color="green">$299</font></td>
      </tr>
    </table>
  </font>

  <br><br>

  <center>
    <font size="2">
      <i>&copy; 2025 TechStore. All rights reserved.</i>
    </font>
  </center>
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**HTML5 (modernized):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TechStore - Modern Website</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1 class="site-title">Welcome to TechStore</h1>
  </header>

  <main>
    <section class="featured-products">
      <h2 class="section-title">Featured Products</h2>
      <p class="intro">Check out our <span class="highlight">amazing deals</span>!</p>

      <table class="product-table">
        <thead>
          <tr>
            <th>Product</th>
            <th>Price</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Laptop</td>
            <td class="price">$999</td>
          </tr>
          <tr>
            <td>Monitor</td>
            <td class="price">$299</td>
          </tr>
        </tbody>
      </table>
    </section>
  </main>

  <footer>
    <p class="copyright">&copy; 2025 TechStore. All rights reserved.</p>
  </footer>
</body>
</html>
```

**CSS (styles.css):**
```css
/* Global Styles */
body {
  background-color: #F0F0F0;
  color: #000000;
  font-family: Verdana, Arial, sans-serif;
  margin: 0;
  padding: 20px;
  line-height: 1.6;
}

/* Header */
header {
  text-align: center;
  margin-bottom: 30px;
}

.site-title {
  font-family: Arial, sans-serif;
  font-size: 2.5em;
  color: #CC0000;
  font-weight: bold;
  margin: 0;
  padding-bottom: 20px;
  border-bottom: 2px solid #999;
}

/* Main Content */
main {
  max-width: 1200px;
  margin: 0 auto;
}

.section-title {
  text-align: center;
  font-weight: bold;
  font-size: 1.3em;
  margin-top: 30px;
  margin-bottom: 15px;
}

.intro {
  text-align: left;
  margin-bottom: 20px;
}

.highlight {
  font-size: 1.2em;
  color: blue;
  font-weight: bold;
}

/* Product Table */
.product-table {
  width: 80%;
  margin: 20px auto;
  border-collapse: collapse;
  background-color: #FFFFFF;
}

.product-table th,
.product-table td {
  border: 1px solid #999;
  padding: 10px;
}

.product-table thead tr {
  background-color: #CCCCCC;
}

.product-table th {
  text-align: center;
  font-weight: bold;
}

.product-table th:first-child {
  color: red;
}

.product-table td.price {
  text-align: right;
  color: green;
  font-weight: bold;
}

/* Footer */
footer {
  text-align: center;
  margin-top: 40px;
  padding-top: 20px;
  border-top: 1px solid #999;
}

.copyright {
  font-size: 0.875em;
  font-style: italic;
}
```

**Changes Made:**
1. **Replaced `<font>`** with CSS font properties
2. **Replaced `<center>`** with `text-align: center` in CSS
3. **Replaced `<big>`** with `<span class="highlight">` + CSS `font-size`
4. **Replaced table attributes** (`border`, `cellpadding`, `bgcolor`) with CSS
5. **Added semantic HTML5** (`<header>`, `<main>`, `<section>`, `<footer>`)
6. **Used proper headings** (`<h1>`, `<h2>`) instead of styled text
7. **Created reusable CSS classes** for consistent styling
8. **Separated all presentation** into external CSS file

**Validation Results:**
- W3C Validator: ✓ No errors
- Accessibility: Improved with semantic structure
- Maintainability: CSS changes don't require HTML edits

**Explanation:**
Modern HTML5 separates structure (HTML) from presentation (CSS). This makes the code more maintainable (change one CSS rule to update site-wide styling), more accessible (semantic elements help screen readers), and standards-compliant (passes validation). The visual appearance remains the same, but the underlying code follows modern best practices.

</details>

---

### Expected Result

**Visual Outcome:** The modernized page looks identical to the original but uses valid HTML5 with semantic structure and CSS styling.

**Key Learnings:**
- Deprecated elements can always be replaced with semantic HTML + CSS
- Separation of concerns improves maintainability and accessibility
- HTML5 validation catches deprecated elements
- Modern code is more professional and follows web standards

---

## Navigation

**Previous:** [HTML Entities](entities.md)
**Next:** [Text Content Elements](../02-text-content/headings.md)
**Up:** [Fundamentals](../README.md#1-fundamentals-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Fundamentals
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
