---
title: HTML Entities & Special Characters
category: Fundamentals
order: 7
---

# HTML Entities & Special Characters

> **Quick Summary:** HTML entities are codes that represent special characters like `<`, `>`, `&`, copyright symbols, and mathematical operators. They prevent parsing conflicts and display characters not on standard keyboards.

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

HTML entities solve two problems: displaying reserved characters and accessing special symbols. Reserved characters like `<`, `>`, and `&` have special meaning in HTML—they mark tags and entities. To display them as actual characters, you need entities. Special symbols like ©, €, and ™ may not be on your keyboard, so entities provide a way to insert them.

Every entity has two formats: a named entity (`&nbsp;` for non-breaking space) and a numeric entity (`&#160;` for the same character). Named entities are easier to remember but limited in number. Numeric entities can represent any Unicode character, making them more flexible but harder to read.

With UTF-8 encoding now standard, many special characters can be typed directly: © instead of `&copy;`, € instead of `&euro;`. However, entities remain essential for reserved characters and maintain compatibility with older systems that don't support full Unicode.

**Key Concept:** Use entities for reserved HTML characters (`<`, `>`, `&`), but with UTF-8 encoding, you can type most special symbols directly. Entities are legacy solutions for many characters but mandatory for a few.

---

## Basic Syntax

```html
<!-- Named entities (easier to remember) -->
&lt;    <!-- Less than: < -->
&gt;    <!-- Greater than: > -->
&amp;   <!-- Ampersand: & -->
&quot;  <!-- Quotation mark: " -->
&copy;  <!-- Copyright: © -->
&nbsp;  <!-- Non-breaking space -->

<!-- Numeric entities (decimal) -->
&#60;   <!-- Less than: < -->
&#62;   <!-- Greater than: > -->
&#38;   <!-- Ampersand: & -->
&#169;  <!-- Copyright: © -->

<!-- Numeric entities (hexadecimal) -->
&#x3C;  <!-- Less than: < -->
&#x3E;  <!-- Greater than: > -->
&#xA9;  <!-- Copyright: © -->
```

### Entity Syntax Rules

| Component | Description | Example |
|-----------|-------------|---------|
| Start | Always begins with `&` | `&copy;` |
| Name/Number | Entity name or number | `copy` or `169` or `xA9` |
| End | Always ends with `;` | `;` |
| Case sensitivity | Named entities are case-sensitive | `&nbsp;` works, `&NBSP;` doesn't |

### Most Common HTML Entities

| Character | Named Entity | Numeric Entity | Description |
|-----------|--------------|----------------|-------------|
| `<` | `&lt;` | `&#60;` | Less than |
| `>` | `&gt;` | `&#62;` | Greater than |
| `&` | `&amp;` | `&#38;` | Ampersand |
| `"` | `&quot;` | `&#34;` | Quotation mark |
| `'` | `&apos;` | `&#39;` | Apostrophe (XML/XHTML) |
| ` ` (space) | `&nbsp;` | `&#160;` | Non-breaking space |
| `©` | `&copy;` | `&#169;` | Copyright |
| `®` | `&reg;` | `&#174;` | Registered trademark |
| `™` | `&trade;` | `&#8482;` | Trademark |
| `€` | `&euro;` | `&#8364;` | Euro currency |

---

## Examples

### Example 1: Displaying HTML Code in a Page

**Scenario:** Showing HTML markup as text (not rendered elements)

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>HTML Tutorial</title>
</head>
<body>
  <h1>How to Create a Paragraph</h1>

  <p>To create a paragraph, use this code:</p>

  <!-- Using entities to display HTML tags as text -->
  <pre><code>&lt;p&gt;This is a paragraph.&lt;/p&gt;</code></pre>

  <p>The paragraph will render like this:</p>
  <p>This is a paragraph.</p>

  <h2>Creating Links</h2>
  <pre><code>&lt;a href="https://example.com"&gt;Click here&lt;/a&gt;</code></pre>
</body>
</html>
```

**Result:** The code examples display as text instead of being parsed as HTML. `&lt;` and `&gt;` prevent browsers from interpreting `<p>` as an actual paragraph tag.

---

### Example 2: Copyright, Trademark, and Legal Symbols

**Scenario:** Adding legal information to a website footer

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Company Website</title>
</head>
<body>
  <header>
    <h1>TechCorp&trade;</h1>
  </header>

  <main>
    <p>Our flagship product: CloudOS&reg;</p>
    <p>Pricing starts at &euro;99 per user/month.</p>
  </main>

  <footer>
    <p>&copy; 2025 TechCorp. All rights reserved.</p>
    <p>Patent pending &ndash; US Patent Application No. 12345</p>
    <p>Terms &amp; Conditions | Privacy Policy</p>
  </footer>
</body>
</html>
```

**Result:** Legal symbols display correctly: ™, ®, ©, €, –, and &. These ensure proper legal attribution and professional presentation.

**UTF-8 Alternative:**
```html
<!-- Modern approach with UTF-8 (works in all modern browsers) -->
<footer>
  <p>© 2025 TechCorp. All rights reserved.</p>
  <p>Our flagship product: CloudOS®</p>
  <p>TechCorp™</p>
  <p>Terms & Conditions | Privacy Policy</p>
</footer>
```

---

### Example 3: Mathematical and Scientific Notation

**Scenario:** Displaying equations and scientific formulas

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Math Formulas</title>
</head>
<body>
  <h1>Mathematical Symbols</h1>

  <h2>Algebra</h2>
  <p>x &times; y = z</p>
  <p>a &divide; b = c</p>
  <p>x &ne; y (not equal)</p>
  <p>x &le; 10 (less than or equal)</p>
  <p>y &ge; 5 (greater than or equal)</p>

  <h2>Greek Letters (Physics/Math)</h2>
  <p>&alpha; (alpha), &beta; (beta), &gamma; (gamma)</p>
  <p>&pi; = 3.14159...</p>
  <p>&Delta; = change in value</p>
  <p>&sum; (summation), &int; (integral)</p>

  <h2>Set Theory</h2>
  <p>A &cap; B (intersection)</p>
  <p>A &cup; B (union)</p>
  <p>x &isin; S (element of)</p>
  <p>&empty; (empty set)</p>

  <h2>Logic</h2>
  <p>&and; (logical AND)</p>
  <p>&or; (logical OR)</p>
  <p>&not; (logical NOT)</p>
  <p>&rArr; (implies)</p>

  <h2>Arrows</h2>
  <p>&larr; &uarr; &rarr; &darr;</p>
  <p>&lArr; &uArr; &rArr; &dArr;</p>
</body>
</html>
```

**Result:** Complex mathematical and scientific notation displays correctly using HTML entities for symbols not on standard keyboards.

---

## Common Use Cases

### Use Case 1: Escaping User-Generated Content
**When:** Displaying user input that might contain HTML/JavaScript
**How:**
```html
<!-- User input: <script>alert('XSS')</script> -->

<!-- GOOD: Escaped with entities (safe) -->
<p>User said: &lt;script&gt;alert('XSS')&lt;/script&gt;</p>
<!-- Displays as text: <script>alert('XSS')</script> -->

<!-- BAD: Not escaped (dangerous!) -->
<p>User said: <script>alert('XSS')</script></p>
<!-- Executes malicious script! -->
```
**Why:** Entities prevent cross-site scripting (XSS) attacks by treating user input as text, not code. Always escape `<`, `>`, and `&` in user-generated content.

---

### Use Case 2: Formatting Prices and Currency
**When:** Displaying international prices
**How:**
```html
<ul>
  <li>USA: &#36;29.99 (or simply: $29.99)</li>
  <li>Europe: &euro;24.99</li>
  <li>UK: &pound;21.99</li>
  <li>Japan: &yen;3,299</li>
  <li>India: &#8377;2,199 (₹)</li>
</ul>
```
**Why:** Currency symbols ensure proper pricing display across regions. With UTF-8, you can type these directly, but entities provide fallback compatibility.

---

### Use Case 3: Non-Breaking Spaces in Formatting
**When:** Preventing awkward line breaks
**How:**
```html
<!-- Prevent line break between number and unit -->
<p>The file size is 2.5&nbsp;MB.</p>
<p>Temperature: 25&nbsp;&deg;C</p>
<p>Distance: 100&nbsp;km</p>

<!-- Keep names together -->
<p>Dr.&nbsp;Jane&nbsp;Smith spoke at the conference.</p>

<!-- Time/date formatting -->
<p>Meeting at 3:00&nbsp;PM EST</p>
```
**Why:** `&nbsp;` prevents browsers from breaking lines at inopportune places, maintaining readability and professional formatting.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | All HTML5 entities supported |
| Firefox | All     | Full Support  | Excellent entity support |
| Safari  | All     | Full Support  | Full Unicode and entity support |
| Edge    | All     | Full Support  | Chromium-based, perfect compatibility |
| IE 11   | 11      | Full Support  | Most entities supported |

**Fallback Strategy:**
HTML entities have been supported since HTML 2.0 (1995). No fallback needed—universal support.

**Can I Use Link:** N/A (core HTML standard)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Text alternatives must use proper encoding (entities ensure special characters display)
- Content must be parseable (malformed entities break parsing)

**Level AA Requirements:**
- No specific entity-related requirements
- Entities don't affect accessibility if used correctly

### Screen Reader Support

```html
<!-- Screen readers handle entities correctly -->
<p>&copy; 2025 Company Name</p>
<!-- Announced as: "Copyright 2025 Company Name" -->

<p>Price: &euro;50</p>
<!-- Announced as: "Price: 50 euros" -->

<p>x &times; y = z</p>
<!-- Announced as: "x times y equals z" -->

<!-- CAUTION: Some entities may not announce clearly -->
<p>&nbsp;</p>
<!-- Non-breaking space is silent (may cause confusion) -->
```

**Key Points:**
- Most entities are announced correctly by screen readers
- Mathematical symbols usually have proper pronunciations
- Decorative symbols (like bullet points) might not announce meaningfully
- Non-breaking spaces are invisible to screen readers

### Keyboard Navigation

Entities don't affect keyboard navigation. They're purely presentational.

---

## Best Practices

### Do This

1. **Always Escape Reserved Characters**
   ```html
   <!-- GOOD: Reserved characters escaped -->
   <p>Use &lt;p&gt; for paragraphs.</p>
   <p>AT&amp;T is a telecom company.</p>
   <p>Price range: $5 &ndash; $10</p>
   ```
   **Why:** Reserved characters (`<`, `>`, `&`) must be escaped to display as text instead of being parsed as HTML.

2. **Use Entities for User-Generated Content (Security)**
   ```php
   // Server-side (PHP example)
   $userInput = $_POST['comment'];
   $safe = htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');
   echo "<p>User said: $safe</p>";
   ```
   **Why:** Escaping user input prevents XSS attacks. Always escape untrusted content.

3. **Use UTF-8 for Common Symbols (Modern Approach)**
   ```html
   <!-- GOOD: UTF-8 characters (simpler) -->
   <p>© 2025 Company. All rights reserved.</p>
   <p>Price: €99</p>

   <!-- ACCEPTABLE: Entities (legacy compatibility) -->
   <p>&copy; 2025 Company. All rights reserved.</p>
   <p>Price: &euro;99</p>
   ```
   **Why:** UTF-8 is simpler and more readable. Use entities only when necessary (reserved chars, legacy systems).

---

### Avoid This

1. **Don't Overuse Entities When UTF-8 Works**
   ```html
   <!-- Bad: Unnecessary entities with UTF-8 -->
   <p>&quot;Hello,&quot; he said.</p>

   <!-- Good: Direct UTF-8 characters -->
   <p>"Hello," he said.</p>
   ```
   **Why Not:** Entities make code harder to read when UTF-8 encoding supports the characters directly.
   **Instead:** Use UTF-8 for most special characters; reserve entities for reserved HTML chars.

2. **Don't Forget Semicolons**
   ```html
   <!-- Bad: Missing semicolon -->
   <p>&copy 2025</p>
   <!-- May render as: ©2025 or &copy2025 -->

   <!-- Good: Proper entity -->
   <p>&copy; 2025</p>
   ```
   **Why Not:** Missing semicolons cause unpredictable rendering. Some browsers auto-correct, others don't.
   **Instead:** Always end entities with semicolons.

3. **Don't Use Entities for Accessibility**
   ```html
   <!-- Bad: Using entities to hide content -->
   <p>&#8203;<!-- Zero-width space to "hide" text --></p>

   <!-- Bad: Excessive non-breaking spaces for layout -->
   <p>Name:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;John</p>
   ```
   **Why Not:** Entities aren't for layout or hiding content. Use CSS for spacing.
   **Instead:** Use proper HTML/CSS for layout and visibility control.

---

## Related Topics

**Prerequisites (Learn These First):**
- [Character Encoding](character-encoding.md) - UTF-8 vs entities
- [HTML5 Syntax](syntax.md) - Understanding element structure

**Related Concepts:**
- [Text Formatting](../02-text-content/text-formatting.md) - Displaying text
- [Comments](comments.md) - Code documentation
- [Validation](validation.md) - Checking entity syntax

**Next Steps (Learn These Next):**
- [Deprecated Elements](deprecated-elements.md) - Old HTML to avoid
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Meaningful markup
- [Accessibility](../13-accessibility/accessibility-overview.md) - Screen reader considerations

**External Resources:**
- [HTML Entity Reference (W3Schools)](https://www.w3schools.com/charsets/ref_html_entities_4.asp)
- [MDN - Entity Reference](https://developer.mozilla.org/en-US/docs/Glossary/Entity)
- [Unicode Character Table](https://unicode-table.com/)
- [HTML5 Entity Lookup](https://dev.w3.org/html5/html-author/charref)

---

## Practice Exercise

### Challenge: Create an HTML Entity Reference Page

**Objective:** Build a quick-reference page showing common HTML entities, their codes, and rendered results.

**Requirements:**
- [ ] Create table with: Symbol, Named Entity, Numeric Entity, Description
- [ ] Include at least 20 common entities
- [ ] Group by category (symbols, math, currency, Greek letters)
- [ ] Demonstrate reserved character escaping
- [ ] Show both entity code and rendered result
- [ ] Bonus: Add search/filter functionality with JavaScript

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>HTML Entity Reference</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
    code { background-color: #f4f4f4; padding: 2px 4px; }
  </style>
</head>
<body>
  <h1>HTML Entity Quick Reference</h1>

  <!-- Add your entity tables here -->

</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>HTML Entity Reference</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 1000px;
      margin: 0 auto;
      padding: 20px;
    }
    table {
      border-collapse: collapse;
      width: 100%;
      margin-bottom: 30px;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 12px;
      text-align: left;
    }
    th {
      background-color: #4CAF50;
      color: white;
    }
    tr:nth-child(even) {
      background-color: #f2f2f2;
    }
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Courier New', monospace;
    }
    .symbol {
      font-size: 1.5em;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>HTML Entity Quick Reference</h1>
  <p>Common HTML entities for special characters and symbols.</p>

  <h2>Reserved Characters (Required Entities)</h2>
  <table>
    <thead>
      <tr>
        <th>Symbol</th>
        <th>Named Entity</th>
        <th>Numeric Entity</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="symbol">&lt;</td>
        <td><code>&amp;lt;</code></td>
        <td><code>&amp;#60;</code></td>
        <td>Less than</td>
      </tr>
      <tr>
        <td class="symbol">&gt;</td>
        <td><code>&amp;gt;</code></td>
        <td><code>&amp;#62;</code></td>
        <td>Greater than</td>
      </tr>
      <tr>
        <td class="symbol">&amp;</td>
        <td><code>&amp;amp;</code></td>
        <td><code>&amp;#38;</code></td>
        <td>Ampersand</td>
      </tr>
      <tr>
        <td class="symbol">"</td>
        <td><code>&amp;quot;</code></td>
        <td><code>&amp;#34;</code></td>
        <td>Quotation mark</td>
      </tr>
    </tbody>
  </table>

  <h2>Legal & Copyright</h2>
  <table>
    <thead>
      <tr>
        <th>Symbol</th>
        <th>Named Entity</th>
        <th>Numeric Entity</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="symbol">&copy;</td>
        <td><code>&amp;copy;</code></td>
        <td><code>&amp;#169;</code></td>
        <td>Copyright</td>
      </tr>
      <tr>
        <td class="symbol">&reg;</td>
        <td><code>&amp;reg;</code></td>
        <td><code>&amp;#174;</code></td>
        <td>Registered trademark</td>
      </tr>
      <tr>
        <td class="symbol">&trade;</td>
        <td><code>&amp;trade;</code></td>
        <td><code>&amp;#8482;</code></td>
        <td>Trademark</td>
      </tr>
    </tbody>
  </table>

  <h2>Currency Symbols</h2>
  <table>
    <thead>
      <tr>
        <th>Symbol</th>
        <th>Named Entity</th>
        <th>Numeric Entity</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="symbol">&euro;</td>
        <td><code>&amp;euro;</code></td>
        <td><code>&amp;#8364;</code></td>
        <td>Euro</td>
      </tr>
      <tr>
        <td class="symbol">&pound;</td>
        <td><code>&amp;pound;</code></td>
        <td><code>&amp;#163;</code></td>
        <td>Pound sterling</td>
      </tr>
      <tr>
        <td class="symbol">&yen;</td>
        <td><code>&amp;yen;</code></td>
        <td><code>&amp;#165;</code></td>
        <td>Yen / Yuan</td>
      </tr>
      <tr>
        <td class="symbol">&cent;</td>
        <td><code>&amp;cent;</code></td>
        <td><code>&amp;#162;</code></td>
        <td>Cent</td>
      </tr>
    </tbody>
  </table>

  <h2>Mathematical Symbols</h2>
  <table>
    <thead>
      <tr>
        <th>Symbol</th>
        <th>Named Entity</th>
        <th>Numeric Entity</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="symbol">&times;</td>
        <td><code>&amp;times;</code></td>
        <td><code>&amp;#215;</code></td>
        <td>Multiplication</td>
      </tr>
      <tr>
        <td class="symbol">&divide;</td>
        <td><code>&amp;divide;</code></td>
        <td><code>&amp;#247;</code></td>
        <td>Division</td>
      </tr>
      <tr>
        <td class="symbol">&plusmn;</td>
        <td><code>&amp;plusmn;</code></td>
        <td><code>&amp;#177;</code></td>
        <td>Plus/minus</td>
      </tr>
      <tr>
        <td class="symbol">&ne;</td>
        <td><code>&amp;ne;</code></td>
        <td><code>&amp;#8800;</code></td>
        <td>Not equal</td>
      </tr>
      <tr>
        <td class="symbol">&le;</td>
        <td><code>&amp;le;</code></td>
        <td><code>&amp;#8804;</code></td>
        <td>Less than or equal</td>
      </tr>
      <tr>
        <td class="symbol">&ge;</td>
        <td><code>&amp;ge;</code></td>
        <td><code>&amp;#8805;</code></td>
        <td>Greater than or equal</td>
      </tr>
    </tbody>
  </table>

  <h2>Greek Letters</h2>
  <table>
    <thead>
      <tr>
        <th>Symbol</th>
        <th>Named Entity</th>
        <th>Numeric Entity</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td class="symbol">&alpha;</td>
        <td><code>&amp;alpha;</code></td>
        <td><code>&amp;#945;</code></td>
        <td>Alpha</td>
      </tr>
      <tr>
        <td class="symbol">&beta;</td>
        <td><code>&amp;beta;</code></td>
        <td><code>&amp;#946;</code></td>
        <td>Beta</td>
      </tr>
      <tr>
        <td class="symbol">&gamma;</td>
        <td><code>&amp;gamma;</code></td>
        <td><code>&amp;#947;</code></td>
        <td>Gamma</td>
      </tr>
      <tr>
        <td class="symbol">&pi;</td>
        <td><code>&amp;pi;</code></td>
        <td><code>&amp;#960;</code></td>
        <td>Pi</td>
      </tr>
      <tr>
        <td class="symbol">&sum;</td>
        <td><code>&amp;sum;</code></td>
        <td><code>&amp;#8721;</code></td>
        <td>Summation</td>
      </tr>
    </tbody>
  </table>

  <footer>
    <p><small>&copy; 2025 Joshua P. Hickman | Created with assistance from Claude Code</small></p>
  </footer>
</body>
</html>
```

**Explanation:**
This reference page demonstrates proper entity usage in tables. Notice how entity codes are shown using `&amp;` to display the ampersand itself (e.g., `&amp;copy;` displays as `&copy;` in the code column). The page organizes entities by category for easy lookup. With UTF-8 encoding, many of these characters can be typed directly, but entities ensure compatibility and are required for reserved characters.

</details>

---

### Expected Result

**Visual Outcome:** A comprehensive reference table showing symbols, their entity codes (both named and numeric), and descriptions. Users can quickly look up how to display any special character.

**Key Learnings:**
- Entities have both named (`&copy;`) and numeric (`&#169;`) forms
- Reserved characters (`<`, `>`, `&`) must always use entities
- UTF-8 encoding makes many entities optional (but they remain valid)
- Entities are essential for security (escaping user-generated content)

---

## Navigation

**Previous:** [Character Encoding](character-encoding.md)
**Next:** [Deprecated Elements](deprecated-elements.md)
**Up:** [Fundamentals](../README.md#1-fundamentals-8-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Fundamentals
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
