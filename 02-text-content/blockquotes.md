---
title: Blockquotes
category: Text Content
order: 4
---

# Blockquotes

> **Quick Summary:** The blockquote element represents extended quotations from external sources, with optional citation attribution, ensuring proper semantic markup for quoted content and improving accessibility for assistive technologies.

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

The `<blockquote>` element is designed to mark up extended quotations from external sources—such as books, articles, speeches, or other documents. Unlike the inline `<q>` element (used for short, inline quotations), blockquotes are block-level elements that typically display as indented sections to visually distinguish quoted material from the surrounding content.

Blockquotes provide semantic meaning that helps search engines, screen readers, and other assistive technologies understand that the content is a quotation rather than original material. This distinction is important for attribution, copyright considerations, and accessibility compliance under WCAG 2.1 guidelines.

The HTML5 specification allows blockquotes to contain multiple paragraphs, lists, headings, and other block-level elements, making them suitable for quoting complex passages. The optional `cite` attribute provides a URL reference to the source material, while the `<cite>` element can be used within or adjacent to the blockquote to provide human-readable attribution.

**Key Concept:** Blockquotes separate quoted content from original content, providing semantic meaning for both human readers and assistive technologies. Always attribute sources for clarity and legal compliance.

## Basic Syntax

**Basic blockquote:**
```html
<blockquote>
  <p>Quoted text goes here.</p>
</blockquote>
```

**Blockquote with cite attribute (URL):**
```html
<blockquote cite="https://example.com/source-article">
  <p>The only way to do great work is to love what you do.</p>
</blockquote>
```

**Blockquote with citation element:**
```html
<blockquote cite="https://example.com/source">
  <p>Stay hungry, stay foolish.</p>
  <footer>
    — <cite>Steve Jobs, Stanford Commencement Address, 2005</cite>
  </footer>
</blockquote>
```

**Attributes:**

| Attribute | Purpose | Value | Required |
|-----------|---------|-------|----------|
| `cite` | URL reference to source material | Valid URL | Optional |
| Global attributes | id, class, lang, dir, etc. | Varies | Optional |

**Nested Elements:**
- `<blockquote>` can contain: paragraphs (`<p>`), headings (`<h1>`-`<h6>`), lists (`<ul>`, `<ol>`), other blockquotes (for nested quotes), footer (`<footer>`), and cite (`<cite>`)
- Common pattern: Wrap quoted text in `<p>` elements for proper structure
- Attribution pattern: Use `<footer>` or `<figcaption>` (when wrapped in `<figure>`)

## Examples

### Example 1: Simple Book Quotation
**Use Case:** Blog post quoting a famous passage from literature

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Inspirational Quotes</title>
  <style>
    blockquote {
      margin: 1.5em 0;
      padding: 1em 2em;
      background-color: #f9f9f9;
      border-left: 4px solid #0066cc;
      font-style: italic;
    }
    blockquote p {
      margin: 0.5em 0;
    }
    blockquote footer {
      font-style: normal;
      text-align: right;
      margin-top: 1em;
      font-size: 0.9em;
      color: #555;
    }
  </style>
</head>
<body>
  <article>
    <h1>Leadership Wisdom</h1>

    <p>
      One of my favorite quotes about leadership comes from
      Theodore Roosevelt's famous speech:
    </p>

    <blockquote cite="https://www.theodore-roosevelt.com/tr-citizenship.html">
      <p>
        It is not the critic who counts; not the man who points out how the
        strong man stumbles, or where the doer of deeds could have done them
        better. The credit belongs to the man who is actually in the arena.
      </p>
      <footer>
        — <cite>Theodore Roosevelt, "The Man in the Arena," 1910</cite>
      </footer>
    </blockquote>

    <p>
      This quote reminds us that participation and effort matter more
      than passive criticism.
    </p>
  </article>
</body>
</html>
```

### Example 2: Multi-Paragraph Technical Documentation Quote
**Use Case:** Technical article referencing official documentation

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>HTML5 Semantic Elements</title>
  <style>
    blockquote {
      margin: 2em 0;
      padding: 1.5em;
      background-color: #e8f4f8;
      border-left: 5px solid #0277bd;
    }
    blockquote p:first-child {
      margin-top: 0;
    }
    blockquote p:last-child {
      margin-bottom: 0;
    }
    cite {
      font-style: italic;
      color: #0277bd;
    }
  </style>
</head>
<body>
  <article>
    <h1>Understanding the Blockquote Element</h1>

    <p>
      According to the official HTML Living Standard published by WHATWG:
    </p>

    <blockquote cite="https://html.spec.whatwg.org/multipage/grouping-content.html#the-blockquote-element">
      <p>
        The blockquote element represents a section that is quoted from
        another source.
      </p>
      <p>
        Content inside a blockquote must be quoted from another source,
        whose address, if it has one, may be cited in the cite attribute.
      </p>
      <p>
        If the cite attribute is present, it must be a valid URL potentially
        surrounded by spaces. To obtain the corresponding citation link,
        the value of the attribute must be parsed relative to the element's
        node document.
      </p>
    </blockquote>

    <p>
      Source: <cite><a href="https://html.spec.whatwg.org/multipage/grouping-content.html#the-blockquote-element">
      WHATWG HTML Living Standard - The blockquote element</a></cite>
    </p>

    <p>
      This specification clarifies that the cite attribute should contain
      a URL, not a person's name. For author attribution, use the
      <code>&lt;cite&gt;</code> element within a footer.
    </p>
  </article>
</body>
</html>
```

### Example 3: Testimonials with Figure and Figcaption
**Use Case:** Customer testimonials on a company website

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Customer Testimonials</title>
  <style>
    .testimonial {
      max-width: 600px;
      margin: 2em auto;
      padding: 2em;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
    .testimonial blockquote {
      margin: 0;
      padding: 0;
      font-size: 1.2em;
      line-height: 1.6;
      font-style: italic;
    }
    .testimonial blockquote p {
      margin: 0 0 1em 0;
    }
    .testimonial blockquote p:last-child {
      margin-bottom: 0;
    }
    .testimonial figcaption {
      margin-top: 1.5em;
      font-style: normal;
      display: flex;
      align-items: center;
      gap: 1em;
    }
    .testimonial figcaption img {
      width: 60px;
      height: 60px;
      border-radius: 50%;
      border: 3px solid white;
    }
    .testimonial cite {
      font-style: normal;
      font-weight: bold;
      display: block;
    }
    .testimonial .role {
      font-size: 0.9em;
      opacity: 0.9;
    }
  </style>
</head>
<body>
  <section>
    <h1>What Our Customers Say</h1>

    <figure class="testimonial">
      <blockquote>
        <p>
          This product transformed how our team collaborates. We've seen a
          40% increase in productivity and our client satisfaction scores
          have never been higher.
        </p>
        <p>
          The customer support is outstanding—they respond within minutes
          and actually solve problems, not just deflect them.
        </p>
      </blockquote>
      <figcaption>
        <img src="sarah-avatar.jpg" alt="Sarah Chen">
        <div>
          <cite>Sarah Chen</cite>
          <p class="role">Director of Operations, TechCorp</p>
        </div>
      </figcaption>
    </figure>

    <figure class="testimonial">
      <blockquote>
        <p>
          I was skeptical at first, but after using this for three months,
          I can't imagine going back to our old workflow. The learning curve
          was minimal and the ROI was immediate.
        </p>
      </blockquote>
      <figcaption>
        <img src="marcus-avatar.jpg" alt="Marcus Rodriguez">
        <div>
          <cite>Marcus Rodriguez</cite>
          <p class="role">Founder, StartupXYZ</p>
        </div>
      </figcaption>
    </figure>
  </section>
</body>
</html>
```

## Common Use Cases

### 1. Blog and Article Quotations
Quoting experts, research, or other publications to support arguments or provide context:

```html
<article>
  <h2>The Importance of Semantic HTML</h2>
  <p>As web standards expert Jeffrey Zeldman explains:</p>

  <blockquote cite="https://example.com/zeldman-article">
    <p>
      Semantic markup is the foundation of accessible, maintainable,
      and future-proof web design.
    </p>
    <footer>
      — <cite>Jeffrey Zeldman, "Designing with Web Standards"</cite>
    </footer>
  </blockquote>
</article>
```

**When to use:** Supporting evidence in articles, academic citations, expert opinions, literary analysis

### 2. Customer Testimonials and Reviews
Displaying customer feedback, product reviews, or case study quotes:

```html
<section class="testimonials">
  <h2>Customer Success Stories</h2>

  <figure>
    <blockquote>
      <p>
        This service saved our company $50,000 in the first year alone.
        The ROI was undeniable.
      </p>
    </blockquote>
    <figcaption>
      <cite>Jane Doe</cite>, CEO of Example Corp
    </figcaption>
  </figure>
</section>
```

**When to use:** Marketing pages, case studies, product landing pages, review sections

### 3. Legal and Compliance Documentation
Quoting laws, regulations, policies, or terms of service:

```html
<section>
  <h2>GDPR Compliance Notice</h2>
  <p>Under the European Union's General Data Protection Regulation:</p>

  <blockquote cite="https://gdpr-info.eu/art-17-gdpr/">
    <p>
      The data subject shall have the right to obtain from the controller
      the erasure of personal data concerning him or her without undue delay.
    </p>
    <footer>
      — <cite>GDPR Article 17: Right to Erasure</cite>
    </footer>
  </blockquote>
</section>
```

**When to use:** Privacy policies, terms of service, compliance documentation, legal notices

## Browser Support

| Element | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| `<blockquote>` | All | All | All | All | All | All |
| `<cite>` element | All | All | All | All | All | All |
| `cite` attribute | All | All | All | All | All | All |

**Browser Support:** Universal (100%)

The `<blockquote>` element has been part of HTML since HTML 2.0 (1995) and is supported by all browsers, including legacy versions. The `cite` attribute is recognized by all modern browsers, though its value (URL) is not displayed by default—it's primarily for semantic purposes and developer tools.

**Default Styling:**
- Most browsers apply left and right margins (typically 40px)
- No special font styling (inherit from parent)
- Block-level display (starts on new line)

**Resources:**
- [MDN: blockquote element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote)
- [WHATWG HTML Living Standard: blockquote](https://html.spec.whatwg.org/multipage/grouping-content.html#the-blockquote-element)
- [W3Schools: HTML blockquote Tag](https://www.w3schools.com/tags/tag_blockquote.asp)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- Use `<blockquote>` only for actual quotations (don't misuse for visual indentation)
- Ensure quoted content is understandable without visual styling alone
- Provide context for quotations (introduce with surrounding text)

**Level AA Requirements:**
- Maintain sufficient color contrast if styling blockquotes with colored backgrounds
- Ensure attribution is accessible (not hidden or overly styled)
- Use semantic elements (`<cite>`, `<footer>`) for attribution, not just visual styling

### Screen Reader Behavior

**How screen readers handle blockquotes:**

| Screen Reader | Behavior | Announcement |
|---------------|----------|--------------|
| NVDA | Announces start and end | "blockquote" / "out of blockquote" |
| JAWS | Announces start and end | "quote" / "end of quote" |
| VoiceOver | Announces start | "blockquote" (may not announce end) |
| TalkBack | Announces start | "quote" |

**Best Practices for Screen Readers:**

1. **Always introduce quotations with context:**
```html
<!-- GOOD: Context before quotation -->
<p>As Albert Einstein said:</p>
<blockquote>
  <p>Imagination is more important than knowledge.</p>
</blockquote>

<!-- BAD: Quotation with no context -->
<blockquote>
  <p>Imagination is more important than knowledge.</p>
</blockquote>
```

2. **Use proper attribution structure:**
```html
<!-- GOOD: Semantic attribution -->
<blockquote>
  <p>Quote text here.</p>
  <footer>— <cite>Author Name, Source</cite></footer>
</blockquote>

<!-- BAD: No semantic attribution -->
<blockquote>
  <p>Quote text here.</p>
  <p style="text-align: right;">- Author Name</p>
</blockquote>
```

3. **Don't misuse blockquote for visual indentation:**
```html
<!-- WRONG: Using blockquote for styling -->
<blockquote>
  <p>This is not a quotation, just indented text.</p>
</blockquote>

<!-- CORRECT: Use CSS for indentation -->
<p class="indented">This is not a quotation.</p>
<style>.indented { margin-left: 2em; }</style>
```

### Language and Direction

- Use `lang` attribute if quoted text is in a different language:
```html
<blockquote lang="es">
  <p>La vida es bella.</p>
  <footer>— <cite>Roberto Benigni</cite></footer>
</blockquote>
```

- Use `dir` attribute for right-to-left languages:
```html
<blockquote lang="ar" dir="rtl">
  <p>النص العربي هنا</p>
</blockquote>
```

**Resources:**
- [WCAG 2.1: Meaningful Sequence (1.3.2)](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
- [WebAIM: Semantic Structure - Quotes](https://webaim.org/techniques/semanticstructure/#quotes)

## Best Practices

### Do This ✓

1. **Use blockquote only for actual quotations:**
```html
<!-- Correct: Actual quotation from external source -->
<blockquote cite="https://example.com/article">
  <p>This is a quote from another source.</p>
</blockquote>
```

2. **Provide both machine-readable and human-readable citations:**
```html
<!-- Correct: cite attribute (URL) + <cite> element (human-readable) -->
<blockquote cite="https://www.w3.org/standards/webdesign/accessibility">
  <p>The power of the Web is in its universality.</p>
  <footer>
    — <cite>Tim Berners-Lee, W3C Director</cite>
  </footer>
</blockquote>
```

3. **Wrap quoted text in paragraph elements:**
```html
<!-- Correct: Text wrapped in <p> -->
<blockquote>
  <p>First paragraph of quote.</p>
  <p>Second paragraph of quote.</p>
</blockquote>

<!-- AVOID: Plain text without <p> -->
<blockquote>
  First paragraph of quote.

  Second paragraph of quote.
</blockquote>
```

4. **Use semantic footer for attribution:**
```html
<!-- Correct: <footer> for attribution -->
<blockquote>
  <p>Quote text.</p>
  <footer>— <cite>Author, Source Title</cite></footer>
</blockquote>
```

5. **Style blockquotes with CSS, not inline styles:**
```css
blockquote {
  margin: 1.5em 0;
  padding: 1em 2em;
  border-left: 4px solid #0066cc;
  background-color: #f4f4f4;
  font-style: italic;
}
blockquote footer {
  font-style: normal;
  text-align: right;
  margin-top: 1em;
}
```

### Avoid This ✗

1. **Don't use blockquote for visual indentation:**
```html
<!-- WRONG: Not a quotation, just indented for looks -->
<blockquote>
  <p>This disclaimer is not a quote from anyone.</p>
</blockquote>

<!-- CORRECT: Use CSS -->
<p class="disclaimer">This disclaimer is not a quote from anyone.</p>
<style>.disclaimer { margin-left: 2em; }</style>
```

2. **Don't put author names in cite attribute:**
```html
<!-- WRONG: cite attribute should be URL, not author name -->
<blockquote cite="Albert Einstein">
  <p>Quote text.</p>
</blockquote>

<!-- CORRECT: URL in cite attribute, author in <cite> element -->
<blockquote cite="https://example.com/einstein-quotes">
  <p>Quote text.</p>
  <footer>— <cite>Albert Einstein</cite></footer>
</blockquote>
```

3. **Don't use quotation marks inside blockquote:**
```html
<!-- WRONG: Redundant quotation marks -->
<blockquote>
  <p>"This is already marked as a quote."</p>
</blockquote>

<!-- CORRECT: No quotation marks needed -->
<blockquote>
  <p>This is already marked as a quote.</p>
</blockquote>
```

4. **Don't nest blockquotes for indentation levels:**
```html
<!-- WRONG: Nested blockquotes for visual hierarchy -->
<blockquote>
  <blockquote>
    <blockquote>
      <p>Deeply indented text</p>
    </blockquote>
  </blockquote>
</blockquote>

<!-- CORRECT: Nest only for actual nested quotations -->
<blockquote>
  <p>Main quote starts here.</p>
  <blockquote>
    <p>This is a quote within the main quote.</p>
  </blockquote>
  <p>Main quote continues.</p>
</blockquote>
```

5. **Don't forget to provide context:**
```html
<!-- WRONG: Quotation appears with no introduction -->
<blockquote>
  <p>To be or not to be, that is the question.</p>
</blockquote>

<!-- CORRECT: Context introduces the quotation -->
<p>Shakespeare's most famous soliloquy from Hamlet begins:</p>
<blockquote cite="https://example.com/hamlet">
  <p>To be or not to be, that is the question.</p>
  <footer>— <cite>William Shakespeare, Hamlet, Act 3, Scene 1</cite></footer>
</blockquote>
```

## Related Topics

### Prerequisites
- [Paragraphs](paragraphs.md) - Block-level text containers
- [Text Formatting](text-formatting.md) - Inline semantic elements like `<cite>`
- [HTML Syntax](../01-fundamentals/syntax.md) - Nesting and structure rules

### Related Topics
- [Code and Preformatted Text](code-preformatted.md) - Displaying code quotations
- [Abbreviations](abbreviations.md) - Expanding acronyms within quotations
- [Links](../03-links-navigation/anchor-links.md) - Linking to source material
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Document structure elements

### Next Steps
- [Code and Preformatted Text](code-preformatted.md) - Learn about displaying code blocks
- [Figure and Figcaption](../04-media-elements/figure-figcaption.md) - Wrapping blockquotes with figure elements
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Comprehensive accessibility strategies

## Practice Exercise

### Requirements
Create an **"Inspirational Quotes" web page** that demonstrates proper use of blockquote elements. Your HTML document should include:

1. A main heading and introduction paragraph
2. At least 3 blockquote elements with:
   - `cite` attribute containing a valid URL (use placeholder URLs like `https://example.com/source-1`)
   - Properly wrapped text in `<p>` elements
   - Attribution using `<footer>` and `<cite>` elements
3. At least one multi-paragraph blockquote
4. At least one blockquote wrapped in a `<figure>` element with `<figcaption>`
5. CSS styling for blockquotes that includes:
   - Custom border or background color
   - Proper spacing (margin/padding)
   - Typography styling (font-size, font-style)
   - Sufficient color contrast (WCAG AA compliant)

**Accessibility Requirements:**
- Introduce each quotation with context (don't drop quotes in randomly)
- Ensure blockquotes are used only for actual quotations, not visual styling
- Maintain minimum 4.5:1 color contrast ratio for text
- Use semantic attribution (<cite>, <footer>)

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Inspirational Quotes</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    /* Add your blockquote styles here */
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
  <title>Inspirational Quotes on Innovation</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
      background-color: #f5f5f5;
    }
    h1 {
      color: #2c3e50;
      text-align: center;
      margin-bottom: 1em;
    }
    .intro {
      text-align: center;
      color: #555;
      margin-bottom: 2em;
    }
    blockquote {
      margin: 2em 0;
      padding: 1.5em 2em;
      background-color: white;
      border-left: 5px solid #3498db;
      font-size: 1.1em;
      font-style: italic;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    blockquote p {
      margin: 0.75em 0;
    }
    blockquote p:first-child {
      margin-top: 0;
    }
    blockquote p:last-of-type {
      margin-bottom: 0;
    }
    blockquote footer {
      font-style: normal;
      text-align: right;
      margin-top: 1em;
      color: #555;
      font-size: 0.95em;
    }
    blockquote cite {
      font-weight: bold;
      color: #3498db;
    }
    figure {
      margin: 2em 0;
    }
    figure blockquote {
      margin: 0;
      border-left-color: #e74c3c;
    }
    figcaption {
      text-align: center;
      margin-top: 1em;
      color: #555;
      font-style: italic;
    }
    .context {
      color: #333;
      margin-top: 2em;
    }
  </style>
</head>
<body>
  <article>
    <h1>Inspirational Quotes on Innovation</h1>

    <p class="intro">
      Throughout history, great thinkers have shared wisdom about creativity,
      innovation, and progress. Here are some of the most powerful quotes
      that continue to inspire us today.
    </p>

    <section>
      <h2>On Creativity and Imagination</h2>

      <p class="context">
        Albert Einstein, one of the greatest minds in physics, understood
        that creativity transcends mere knowledge:
      </p>

      <blockquote cite="https://example.com/einstein-quotes-creativity">
        <p>
          Imagination is more important than knowledge. For knowledge is
          limited, whereas imagination embraces the entire world,
          stimulating progress, giving birth to evolution.
        </p>
        <footer>
          — <cite>Albert Einstein, "What Life Means to Einstein" (1929)</cite>
        </footer>
      </blockquote>
    </section>

    <section>
      <h2>On Perseverance and Failure</h2>

      <p class="context">
        Steve Jobs, co-founder of Apple, delivered one of the most memorable
        commencement speeches at Stanford University in 2005:
      </p>

      <blockquote cite="https://example.com/jobs-stanford-speech">
        <p>
          Your work is going to fill a large part of your life, and the only
          way to be truly satisfied is to do what you believe is great work.
        </p>
        <p>
          And the only way to do great work is to love what you do. If you
          haven't found it yet, keep looking. Don't settle.
        </p>
        <footer>
          — <cite>Steve Jobs, Stanford Commencement Address (2005)</cite>
        </footer>
      </blockquote>

      <p class="context">
        Thomas Edison's perspective on failure revolutionized how we think
        about setbacks in innovation:
      </p>

      <blockquote cite="https://example.com/edison-failure-quotes">
        <p>
          I have not failed. I've just found 10,000 ways that won't work.
        </p>
        <footer>
          — <cite>Thomas Edison, American Inventor</cite>
        </footer>
      </blockquote>
    </section>

    <section>
      <h2>On Taking Action</h2>

      <p class="context">
        Theodore Roosevelt's famous "Man in the Arena" speech from 1910
        remains one of the most powerful calls to action:
      </p>

      <figure>
        <blockquote cite="https://example.com/roosevelt-man-in-arena">
          <p>
            It is not the critic who counts; not the man who points out how
            the strong man stumbles, or where the doer of deeds could have
            done them better.
          </p>
          <p>
            The credit belongs to the man who is actually in the arena,
            whose face is marred by dust and sweat and blood; who strives
            valiantly; who errs, who comes short again and again, because
            there is no effort without error and shortcoming.
          </p>
        </blockquote>
        <figcaption>
          Theodore Roosevelt, "Citizenship in a Republic" speech
          at the Sorbonne, Paris, April 23, 1910
        </figcaption>
      </figure>
    </section>
  </article>
</body>
</html>
```

**Key Features of Solution:**
- Uses `<blockquote>` only for actual quotations (not styling)
- Includes `cite` attribute with placeholder URLs for all blockquotes
- Properly wraps all quoted text in `<p>` elements
- Uses semantic `<footer>` and `<cite>` elements for attribution
- Includes one multi-paragraph quote (Steve Jobs)
- Includes one `<figure>` wrapped blockquote (Roosevelt)
- Provides context for every quotation (introduces with surrounding text)
- CSS styling with border-left accent, background color, proper spacing
- Maintains WCAG AA color contrast (text: #333/#555 on white background = 9.7:1 ratio)
- Different styling for figure-wrapped blockquote (red accent vs. blue)
- Responsive typography with proper line-height (1.6)

---

## Navigation

- **Previous:** [Text Formatting](text-formatting.md)
- **Next:** [Code and Preformatted Text](code-preformatted.md)
- **Up:** [Text Content](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Text Content
- **Difficulty:** Beginner
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
