---
title: Text Formatting
category: Text Content
order: 3
---

# Text Formatting

> **Quick Summary:** HTML5 provides semantic text formatting elements to convey meaning and importance, such as strong emphasis, editorial changes, and scientific notation, ensuring accessibility and proper interpretation by assistive technologies.

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

Text formatting elements in HTML5 are designed to add semantic meaning to text rather than just visual styling. Unlike deprecated presentational elements like `<b>` and `<i>`, modern HTML5 formatting elements communicate the purpose and importance of text to both browsers and assistive technologies.

Understanding the difference between semantic and presentational markup is crucial for creating accessible, maintainable web content. Elements like `<strong>` indicate importance, while `<em>` indicates stress emphasis. Elements like `<mark>` highlight relevance, `<del>` and `<ins>` track editorial changes, and `<sub>` and `<sup>` handle scientific notation.

These elements work together with CSS to provide both meaning and presentation. Screen readers interpret semantic elements to convey context to users, making proper element selection essential for accessibility compliance (WCAG 2.1 Level A).

**Key Concept:** Semantic text formatting separates meaning from presentation. Use HTML elements to describe what text means, then use CSS to control how it looks.

## Basic Syntax

| Element | Purpose | Semantic Meaning | Default Styling |
|---------|---------|------------------|-----------------|
| `<strong>` | Strong importance | High importance, seriousness, urgency | Bold |
| `<em>` | Emphasis (stress) | Changes meaning of sentence | Italic |
| `<mark>` | Highlighted relevance | Relevant to current context | Yellow background |
| `<small>` | Side comments, fine print | Less important content | Smaller text |
| `<del>` | Deleted content | Removed from document | Strikethrough |
| `<ins>` | Inserted content | Added to document | Underline |
| `<sub>` | Subscript | Chemical formulas, mathematical notation | Subscript |
| `<sup>` | Superscript | Exponents, footnote references | Superscript |
| `<code>` | Inline code | Programming code or markup | Monospace font |
| `<kbd>` | Keyboard input | User keyboard actions | Monospace font |
| `<samp>` | Sample output | Computer program output | Monospace font |
| `<var>` | Variable | Mathematical/programming variables | Italic |
| `<abbr>` | Abbreviation | Shortened form with expansion | Dotted underline (optional) |
| `<dfn>` | Definition | Term being defined | Italic |
| `<cite>` | Citation | Title of creative work | Italic |
| `<q>` | Short quotation | Inline quoted text | Quotation marks |

**Syntax:**
```html
<strong>Important text</strong>
<em>Emphasized text</em>
<mark>Highlighted text</mark>
<small>Fine print</small>
<del>Deleted text</del>
<ins>Inserted text</ins>
H<sub>2</sub>O  <!-- Subscript -->
E = mc<sup>2</sup>  <!-- Superscript -->
```

**Attributes:**
- `<del>` and `<ins>` support `cite` (URL explaining change) and `datetime` (when change occurred)
- `<abbr>` uses `title` attribute for full expansion
- All elements support global attributes (class, id, style, lang, etc.)

## Examples

### Example 1: Basic Text Emphasis
**Use Case:** Blog post with important warnings and emphasized points

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Security Best Practices</title>
</head>
<body>
  <article>
    <h1>Web Security Best Practices</h1>

    <p>
      <strong>Warning:</strong> Never store passwords in plain text.
      This is <em>critically</em> important for user safety.
    </p>

    <p>
      When implementing authentication, you <em>must</em> use
      industry-standard hashing algorithms. The most commonly
      recommended option is <strong>bcrypt</strong>.
    </p>

    <p>
      <small>Last updated: November 2025 | Security Team</small>
    </p>
  </article>
</body>
</html>
```

### Example 2: Editorial Changes and Highlighting
**Use Case:** Document revision tracking with context highlighting

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Policy Document - Revised</title>
  <style>
    del { background-color: #ffe6e6; }
    ins { background-color: #e6ffe6; }
    mark { background-color: #fff3cd; font-weight: bold; }
  </style>
</head>
<body>
  <article>
    <h1>Remote Work Policy - Version 2.1</h1>

    <p>
      Employees may work remotely up to
      <del datetime="2025-11-01" cite="policy-change-2025-q4.html">2 days</del>
      <ins datetime="2025-11-01" cite="policy-change-2025-q4.html">3 days</ins>
      per week with manager approval.
    </p>

    <p>
      <mark>New requirement:</mark> All remote workers must attend
      the monthly team meeting in person.
    </p>

    <p>
      Office hours remain
      <del>9:00 AM - 5:00 PM</del>
      <ins>flexible core hours between 10:00 AM - 3:00 PM</ins>.
    </p>
  </article>
</body>
</html>
```

### Example 3: Scientific and Technical Content
**Use Case:** Educational content with formulas, code, and citations

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Chemistry Lab Report</title>
  <style>
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
    }
    kbd {
      background-color: #333;
      color: white;
      padding: 2px 6px;
      border-radius: 3px;
      font-size: 0.9em;
    }
    var { color: #d63384; }
  </style>
</head>
<body>
  <article>
    <h1>Water Molecule Analysis</h1>

    <section>
      <h2>Chemical Composition</h2>
      <p>
        Water is composed of hydrogen and oxygen with the molecular
        formula H<sub>2</sub>O. Each molecule contains two hydrogen
        atoms bonded to one oxygen atom.
      </p>

      <p>
        The ionization of water can be expressed as:
        H<sub>2</sub>O ⇌ H<sup>+</sup> + OH<sup>-</sup>
      </p>
    </section>

    <section>
      <h2>Calculation Example</h2>
      <p>
        Einstein's mass-energy equivalence is given by
        <var>E</var> = <var>m</var><var>c</var><sup>2</sup>,
        where <var>c</var> represents the speed of light.
      </p>

      <p>
        To calculate this in Python, use:
        <code>energy = mass * (speed_of_light ** 2)</code>
      </p>

      <p>
        <strong>Note:</strong> Run the calculation by pressing
        <kbd>Ctrl</kbd> + <kbd>Enter</kbd> in Jupyter Notebook.
      </p>
    </section>

    <section>
      <h2>References</h2>
      <p>
        For more information, consult
        <cite>Chemistry: The Central Science</cite> by Brown et al.
        The <abbr title="International Union of Pure and Applied Chemistry">IUPAC</abbr>
        provides standardized nomenclature guidelines.
      </p>
    </section>
  </article>
</body>
</html>
```

## Common Use Cases

### 1. Content Warnings and Critical Information
Use `<strong>` for warnings, errors, or critical notices that require immediate attention:

```html
<p>
  <strong>Security Alert:</strong> Your password will expire in 3 days.
  Please update it to maintain account access.
</p>
```

**When to use:** Error messages, security warnings, required field labels, critical deadlines

### 2. Document Version Control
Use `<del>` and `<ins>` to track changes in legal documents, policies, or collaborative writing:

```html
<p>
  The deadline for submissions is
  <del datetime="2025-11-15T10:00:00Z">November 30</del>
  <ins datetime="2025-11-15T10:00:00Z">December 15</ins>, 2025.
</p>
```

**When to use:** Contract revisions, meeting minutes, collaborative editing, changelog documentation

### 3. Search Results and Context Highlighting
Use `<mark>` to highlight search terms or relevant content in search results:

```html
<article>
  <h3>Search Results for "HTML5"</h3>
  <p>
    Learn about <mark>HTML5</mark> semantic elements and how
    <mark>HTML5</mark> improves accessibility...
  </p>
</article>
```

**When to use:** Search result highlighting, in-page text search, relevant passage emphasis, quiz answers

## Browser Support

| Element | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| `<strong>` | All | All | All | All | All | All |
| `<em>` | All | All | All | All | All | All |
| `<mark>` | 6+ | 4+ | 5+ | 12+ | 5+ | 18+ |
| `<small>` | All | All | All | All | All | All |
| `<del>` | All | All | All | All | All | All |
| `<ins>` | All | All | All | All | All | All |
| `<sub>` | All | All | All | All | All | All |
| `<sup>` | All | All | All | All | All | All |
| `<code>` | All | All | All | All | All | All |
| `<kbd>` | All | All | All | All | All | All |
| `<samp>` | All | All | All | All | All | All |
| `<var>` | All | All | All | All | All | All |
| `<abbr>` | All | All | All | All | All | All |
| `<cite>` | All | All | All | All | All | All |
| `<q>` | All | All | All | All | All | All |

**Browser Support:** Universal (100%)

All text formatting elements are supported across all modern browsers and have been part of HTML standards since HTML 4.01. The `<mark>` element is the newest addition (HTML5), but has full support in browsers released after 2011.

**Fallback:** No fallbacks needed. Even in ancient browsers, unsupported elements render as inline text without styling.

**Resources:**
- [MDN: Text-level semantics](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#text_content)
- [WHATWG HTML Living Standard](https://html.spec.whatwg.org/multipage/text-level-semantics.html)
- [Can I Use: mark element](https://caniuse.com/mdn-html_elements_mark)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- Use semantic elements (`<strong>`, `<em>`) instead of presentational styling (`<b>`, `<i>`)
- Ensure text formatting does not rely solely on color (use text decoration or icons)
- Provide text alternatives when formatting conveys critical information visually

**Level AA Requirements:**
- Maintain sufficient color contrast for highlighted text (`<mark>` backgrounds)
- Ensure `<del>` and `<ins>` changes are understandable without color alone
- Provide context for abbreviations using `<abbr title="expansion">`

### Screen Reader Behavior

| Element | Screen Reader Announcement | Impact |
|---------|---------------------------|--------|
| `<strong>` | Announces with increased emphasis | High |
| `<em>` | Announces with stress intonation | High |
| `<mark>` | May announce as "highlighted" (varies by SR) | Medium |
| `<del>` | May announce as "deleted" or ignore | Low |
| `<ins>` | May announce as "inserted" or ignore | Low |
| `<sub>/<sup>` | Reads content normally without context | Low |
| `<abbr>` | Announces title attribute on first encounter | High |

**Best Practices for Screen Readers:**

1. **Don't rely on formatting alone for critical information:**
```html
<!-- BAD: Relies on visual strikethrough -->
<p>Price: <del>$99</del> $79</p>

<!-- GOOD: Provides context -->
<p>Price: <del>Was $99</del> <ins>Now $79</ins> (20% off)</p>
```

2. **Provide context for subscript/superscript:**
```html
<!-- BAD: Screen reader says "H 2 O" without context -->
<p>Formula: H<sub>2</sub>O</p>

<!-- GOOD: Provides chemical context -->
<p>Chemical formula for water: H<sub>2</sub>O (two hydrogen, one oxygen)</p>
```

3. **Use ARIA labels when semantic meaning is insufficient:**
```html
<p>
  <del aria-label="Original price">$99</del>
  <ins aria-label="Sale price">$79</ins>
</p>
```

### Keyboard Navigation

- All text formatting elements are non-interactive and do not require keyboard support
- `<abbr>` with `title` attributes may show tooltips on hover, but should also be understandable without hover
- Use `<kbd>` to represent keyboard shortcuts visually, but provide text alternatives for screen reader users

**Resources:**
- [WCAG 2.1: Sensory Characteristics (1.3.3)](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
- [WebAIM: Semantic Structure](https://webaim.org/techniques/semanticstructure/)

## Best Practices

### Do This ✓

1. **Use semantic elements for meaning, not styling:**
```html
<!-- Correct: Strong importance -->
<p><strong>Warning:</strong> System will restart in 5 minutes.</p>

<!-- Correct: Emphasis changes meaning -->
<p>I <em>love</em> HTML5. (vs. I love <em>HTML5</em>.)</p>
```

2. **Provide datetime and cite attributes for editorial changes:**
```html
<p>
  Meeting time:
  <del datetime="2025-11-17T09:00:00Z" cite="schedule-change.html">2:00 PM</del>
  <ins datetime="2025-11-17T09:00:00Z" cite="schedule-change.html">3:30 PM</ins>
</p>
```

3. **Use CSS to style semantic elements consistently:**
```css
strong { color: #d9534f; font-weight: bold; }
mark { background-color: #fff3cd; padding: 2px 4px; }
del { text-decoration: line-through; opacity: 0.7; }
ins { text-decoration: underline; background-color: #d4edda; }
```

4. **Combine elements for complex semantics:**
```html
<!-- Correct: Combining strong + mark for critical highlights -->
<p>
  <strong><mark>Action required:</mark></strong> Submit report by Friday.
</p>
```

5. **Use abbr with title for first occurrence:**
```html
<p>
  The <abbr title="World Health Organization">WHO</abbr>
  recommends daily exercise. The WHO also emphasizes nutrition...
</p>
```

### Avoid This ✗

1. **Don't use presentational elements instead of semantic ones:**
```html
<!-- WRONG: <b> has no semantic meaning -->
<p><b>Warning:</b> This is important.</p>

<!-- CORRECT: <strong> indicates importance -->
<p><strong>Warning:</strong> This is important.</p>
```

2. **Don't use formatting for visual styling alone:**
```html
<!-- WRONG: Using <em> just to make text italic -->
<p><em>Company Name</em> - <em>Tagline</em></p>

<!-- CORRECT: Use CSS for brand styling -->
<p class="brand-name">Company Name</p>
<style>.brand-name { font-style: italic; }</style>
```

3. **Don't nest emphasis elements excessively:**
```html
<!-- WRONG: Confusing and redundant -->
<p><strong><em><mark>Important!</mark></em></strong></p>

<!-- CORRECT: Use one appropriate element + CSS -->
<p><strong class="critical-alert">Important!</strong></p>
```

4. **Don't use mark without sufficient contrast:**
```html
<!-- WRONG: Low contrast (WCAG violation) -->
<mark style="background-color: #ffffcc; color: #ffffee;">Text</mark>

<!-- CORRECT: High contrast -->
<mark style="background-color: #fff3cd; color: #000;">Text</mark>
```

5. **Don't use del/ins for non-editorial purposes:**
```html
<!-- WRONG: Using <del> for crossed-out pricing (not editorial change) -->
<p><del>$99</del> $79</p>

<!-- CORRECT: Use CSS for visual strikethrough -->
<p><span class="original-price">$99</span> <span class="sale-price">$79</span></p>
<style>.original-price { text-decoration: line-through; }</style>
```

## Related Topics

### Prerequisites
- [HTML Syntax](../01-fundamentals/syntax.md) - Element and attribute syntax rules
- [Paragraphs](paragraphs.md) - Block-level text containers
- [Headings](headings.md) - Document structure and hierarchy

### Related Topics
- [Code and Preformatted Text](code-preformatted.md) - Displaying code blocks and preserving formatting
- [Blockquotes](blockquotes.md) - Quotation elements and citations
- [Abbreviations](abbreviations.md) - Expanding acronyms and abbreviations
- [Links](../03-links-navigation/anchor-links.md) - Hyperlinks and navigation
- [Global Attributes](../09-global-attributes/id-class.md) - Universal HTML attributes

### Next Steps
- [Blockquotes](blockquotes.md) - Learn about quotation and citation elements
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Comprehensive accessibility strategies
- [CSS Text Styling](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text) - Visual text formatting with CSS

## Practice Exercise

### Requirements
Create a **blog post about web development** that demonstrates proper use of text formatting elements. Your HTML document should include:

1. A main heading and at least 2 subheadings
2. At least 3 paragraphs with proper semantic formatting:
   - Use `<strong>` for at least one important warning or key point
   - Use `<em>` for stress emphasis that changes meaning
   - Use `<mark>` to highlight a key term or concept
3. A section showing code examples with:
   - `<code>` for inline code snippets
   - `<kbd>` for keyboard shortcuts
   - `<var>` for a variable name
4. A revised paragraph showing editorial changes:
   - Use `<del>` with `datetime` attribute for removed content
   - Use `<ins>` with `datetime` attribute for added content
5. A scientific or technical example using:
   - `<sub>` for subscript
   - `<sup>` for superscript
6. An abbreviation using `<abbr>` with `title` attribute
7. A citation using `<cite>`

**Accessibility Requirements:**
- Ensure all `<mark>` elements have sufficient color contrast (test with browser DevTools)
- Provide context for all editorial changes (don't rely on strikethrough alone)
- Use semantic elements appropriately (not just for visual styling)

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Web Development Best Practices</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    mark {
      background-color: #fff3cd;
      padding: 2px 4px;
    }
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Courier New', monospace;
    }
    kbd {
      background-color: #333;
      color: white;
      padding: 2px 6px;
      border-radius: 3px;
      font-size: 0.9em;
    }
    del {
      background-color: #f8d7da;
      text-decoration: line-through;
    }
    ins {
      background-color: #d4edda;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <!-- Add your blog post content here -->

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
  <title>Web Development Best Practices</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    mark {
      background-color: #fff3cd;
      padding: 2px 4px;
      font-weight: bold;
    }
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Courier New', monospace;
    }
    kbd {
      background-color: #333;
      color: white;
      padding: 2px 6px;
      border-radius: 3px;
      font-size: 0.9em;
    }
    del {
      background-color: #f8d7da;
      text-decoration: line-through;
    }
    ins {
      background-color: #d4edda;
      text-decoration: none;
    }
    var {
      color: #d63384;
      font-style: italic;
    }
    abbr {
      cursor: help;
      text-decoration: underline dotted;
    }
  </style>
</head>
<body>
  <article>
    <h1>Modern Web Development: HTML5 Semantic Elements</h1>

    <section>
      <h2>Introduction to Semantic HTML</h2>

      <p>
        <strong>Critical principle:</strong> Always use semantic HTML elements
        to describe the <em>meaning</em> of your content, not just its appearance.
        This approach is fundamental to creating accessible, maintainable websites
        that work well with assistive technologies and search engines.
      </p>

      <p>
        The <mark>semantic markup revolution</mark> in HTML5 transformed how we
        build web pages. Instead of relying on generic <code>&lt;div&gt;</code>
        elements everywhere, we now have purpose-built elements like
        <code>&lt;article&gt;</code>, <code>&lt;section&gt;</code>, and
        <code>&lt;nav&gt;</code> that communicate structure and intent.
      </p>

      <p>
        According to <cite>Designing with Web Standards</cite> by Jeffrey Zeldman,
        semantic HTML improves <abbr title="Search Engine Optimization">SEO</abbr>,
        accessibility, and long-term maintainability. When you <em>structure</em>
        your content correctly, styling becomes easier and more flexible.
      </p>
    </section>

    <section>
      <h2>Coding Best Practices</h2>

      <p>
        When writing HTML, use the <kbd>Tab</kbd> key to properly indent nested
        elements. Most modern editors like VS Code support automatic formatting
        when you press <kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>F</kbd>
        (or <kbd>Shift</kbd> + <kbd>Option</kbd> + <kbd>F</kbd> on Mac).
      </p>

      <p>
        Always validate your HTML using the
        <abbr title="World Wide Web Consortium">W3C</abbr> validator.
        A simple validation check can be triggered with the command
        <code>npm run validate</code> in your project, where the
        <var>validate</var> script runs automated checks.
      </p>
    </section>

    <section>
      <h2>Policy Updates (Revised November 2025)</h2>

      <p>
        Our team's code review policy has been updated. All pull requests must now
        receive approval from
        <del datetime="2025-11-01T14:30:00Z">at least one senior developer</del>
        <ins datetime="2025-11-01T14:30:00Z">at least two team members, including one senior developer</ins>
        before merging to the main branch.
      </p>

      <p>
        The maximum file size for uploaded assets has changed from
        <del datetime="2025-11-15T10:00:00Z">5 MB</del>
        <ins datetime="2025-11-15T10:00:00Z">10 MB</ins>
        to accommodate higher-resolution images for responsive design.
      </p>
    </section>

    <section>
      <h2>Technical Examples</h2>

      <p>
        In chemistry notation, water is represented as H<sub>2</sub>O,
        indicating two hydrogen atoms bonded to one oxygen atom.
        Carbon dioxide is CO<sub>2</sub>.
      </p>

      <p>
        Mathematical expressions use superscript for exponents:
        The formula for area of a circle is A = πr<sup>2</sup>,
        and Einstein's famous equation is E = mc<sup>2</sup>.
      </p>

      <p>
        In footnotes, references appear as superscript numbers:
        According to recent studies<sup>1</sup>, semantic HTML improves
        accessibility by 40%<sup>2</sup>.
      </p>
    </section>

    <footer>
      <p><small>Last updated: November 17, 2025 | Web Development Team</small></p>
    </footer>
  </article>
</body>
</html>
```

**Key Features of Solution:**
- Uses `<strong>` for critical principle (high importance)
- Uses `<em>` for stress emphasis ("meaning" vs "structure")
- Highlights key concept with `<mark>`
- Demonstrates `<code>` for HTML elements and commands
- Shows `<kbd>` for keyboard shortcuts
- Uses `<var>` for script variable name
- Includes `<del>` and `<ins>` with `datetime` attributes for policy changes
- Demonstrates `<sub>` for chemical formulas
- Demonstrates `<sup>` for exponents and footnotes
- Uses `<abbr>` with `title` for acronym expansion
- Includes `<cite>` for book reference
- Provides context for all editorial changes (accessible without visual styling)
- Maintains WCAG AA color contrast for `<mark>` element

---

## Navigation

- **Previous:** [Paragraphs](paragraphs.md)
- **Next:** [Blockquotes](blockquotes.md)
- **Up:** [Text Content](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Text Content
- **Difficulty:** Beginner to Intermediate
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
