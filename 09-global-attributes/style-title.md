---
title: Style and Title Attributes
category: Global Attributes
order: 19
---

# Style and Title Attributes

> **Quick Summary:** The `style` attribute applies inline CSS directly to elements (use sparingly for dynamic styles). The `title` attribute provides advisory information shown as tooltips on hover—useful for accessibility, extra context, and abbreviation expansions.

## Table of Contents
- [Introduction](#introduction)
- [Style Attribute](#style-attribute)
- [Title Attribute](#title-attribute)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `style` and `title` attributes are global attributes available on all HTML elements:

- **`style`**: Applies inline CSS styling directly to an element
- **`title`**: Provides advisory text displayed as a tooltip on hover

**Key points:**
- Both are global (work on any HTML element)
- `style` should be used sparingly (external CSS preferred)
- `title` improves accessibility and user experience
- Both are inherited by screen readers

**Key Concept:** Think of `style` as quick styling for dynamic content (JavaScript-generated colors, positions), and `title` as helpful "sticky notes" that appear when users hover over elements.

---

## Style Attribute

### Basic Syntax

```html
<element style="property: value; property: value;">Content</element>
```

### Valid Examples

```html
<!-- Single property -->
<p style="color: red;">Red text</p>

<!-- Multiple properties (semicolon-separated) -->
<div style="background: blue; color: white; padding: 20px;">
  Styled div
</div>

<!-- Complex styles -->
<h1 style="font-size: 32px; font-weight: bold; margin-bottom: 10px; text-align: center;">
  Centered Heading
</h1>
```

### CSS Property Syntax

```html
<!-- Background -->
<div style="background-color: #f0f0f0;">Content</div>
<div style="background: url('image.jpg') no-repeat center;">Content</div>

<!-- Text styling -->
<p style="color: #333; font-size: 16px; line-height: 1.5;">Text</p>

<!-- Layout -->
<div style="display: flex; justify-content: center; align-items: center;">
  Flexbox
</div>

<!-- Positioning -->
<div style="position: absolute; top: 10px; left: 20px;">
  Positioned
</div>

<!-- Borders and spacing -->
<div style="border: 1px solid #ddd; margin: 20px; padding: 15px;">
  Box
</div>
```

### When to Use Inline Styles

✅ **Use inline styles for:**

**1. Dynamic Styles from JavaScript**
```javascript
// User-selected color
const element = document.getElementById('box');
element.style.backgroundColor = userSelectedColor;

// Calculated position
element.style.left = (windowWidth / 2) + 'px';
```

**2. Email HTML (External CSS Often Blocked)**
```html
<!-- Email templates need inline styles -->
<table style="width: 600px; margin: 0 auto; font-family: Arial, sans-serif;">
  <tr>
    <td style="background: #007bff; color: white; padding: 20px;">
      Email Header
    </td>
  </tr>
</table>
```

**3. Quick Prototyping/Testing**
```html
<!-- Testing a style before moving to CSS -->
<div style="background: red;">
  Quick test
</div>
```

**4. Overriding Specific Instances**
```html
<!-- Override one card in a list -->
<div class="card">Regular card</div>
<div class="card">Regular card</div>
<div class="card" style="background: yellow;">Highlighted card</div>
```

❌ **Avoid inline styles for:**
- General styling (use external CSS)
- Reusable styles (use classes)
- Responsive design (use media queries in CSS)
- Maintainability (CSS is easier to update)

### Inline Style Specificity

Inline styles have **high specificity** (1,0,0,0):
```html
<style>
  #my-element {
    color: blue; /* Specificity: 0,1,0,0 */
  }

  .my-class {
    color: green; /* Specificity: 0,0,1,0 */
  }
</style>

<!-- Inline style wins (highest specificity) -->
<div id="my-element" class="my-class" style="color: red;">
  This text will be RED
</div>
```

Only `!important` can override inline styles:
```html
<style>
  #my-element {
    color: blue !important; /* Now this wins */
  }
</style>

<div id="my-element" style="color: red;">
  This text will be BLUE (because of !important)
</div>
```

---

## Title Attribute

### Basic Syntax

```html
<element title="Advisory text">Content</element>
```

### Common Use Cases

**1. Providing Additional Context**
```html
<abbr title="World Wide Web Consortium">W3C</abbr>
<abbr title="HyperText Markup Language">HTML</abbr>
<abbr title="Cascading Style Sheets">CSS</abbr>

<p>
  The <abbr title="Application Programming Interface">API</abbr>
  is currently <span title="Currently being updated">under maintenance</span>.
</p>
```

**2. Explaining Icons/Images**
```html
<button title="Save document">
  <img src="save-icon.png" alt="Save">
</button>

<button title="Delete this item">
  <img src="trash-icon.png" alt="Delete">
</button>

<a href="/settings" title="Configure application settings">
  ⚙️ Settings
</a>
```

**3. Showing Full Text for Truncated Content**
```html
<style>
  .truncate {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    max-width: 200px;
  }
</style>

<p class="truncate" title="This is a very long title that will be truncated with ellipsis but the full text is shown on hover">
  This is a very long title that will be truncated...
</p>
```

**4. Link Descriptions**
```html
<a href="/products/wireless-headphones" title="View details about our wireless noise-canceling headphones">
  Wireless Headphones
</a>

<a href="https://example.com" title="Opens in new window" target="_blank">
  External Link
</a>
```

**5. Form Field Help Text**
```html
<label for="username">Username:</label>
<input type="text"
       id="username"
       title="Username must be 3-20 characters, letters and numbers only"
       placeholder="Enter username">

<label for="password">Password:</label>
<input type="password"
       id="password"
       title="Password must be at least 8 characters with uppercase, lowercase, and numbers"
       placeholder="Enter password">
```

**6. Disabled Elements Explanation**
```html
<button disabled title="This feature is only available to premium users">
  Premium Feature
</button>

<input type="text" disabled title="This field is automatically generated">
```

### Title Attribute Behavior

**Desktop browsers:**
- Tooltip appears on hover (after ~1 second delay)
- Varies by browser and OS styling

**Mobile devices:**
- **No hover on touch devices** (title not accessible)
- Use `aria-label` or visible text for mobile accessibility

**Screen readers:**
- May or may not announce title attribute (inconsistent)
- Don't rely on `title` alone for critical accessibility info

---

## Examples

### Example 1: Dynamic Inline Styles with JavaScript

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic Color Picker</title>
  <style>
    .color-box {
      width: 200px;
      height: 200px;
      border: 2px solid #333;
      margin: 20px 0;
      transition: background-color 0.3s;
    }
  </style>
</head>
<body>
  <h1>Color Picker</h1>

  <label for="color-input">Choose a color:</label>
  <input type="color" id="color-input" value="#3498db">

  <div class="color-box" id="color-box"></div>

  <p>
    Selected color: <span id="color-value">#3498db</span>
  </p>

  <script>
    const colorInput = document.getElementById('color-input');
    const colorBox = document.getElementById('color-box');
    const colorValue = document.getElementById('color-value');

    // Set initial color
    colorBox.style.backgroundColor = colorInput.value;

    // Update color on change
    colorInput.addEventListener('input', function() {
      // Dynamic inline style from user input
      colorBox.style.backgroundColor = this.value;
      colorValue.textContent = this.value;
    });
  </script>
</body>
</html>
```

### Example 2: Title Attribute for Accessibility

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Abbreviations Example</title>
  <style>
    abbr {
      text-decoration: underline dotted;
      cursor: help;
    }
  </style>
</head>
<body>
  <article>
    <h1>Web Development Technologies</h1>

    <p>
      Modern web development uses
      <abbr title="HyperText Markup Language 5">HTML5</abbr>,
      <abbr title="Cascading Style Sheets 3">CSS3</abbr>, and
      <abbr title="JavaScript">JS</abbr> to create interactive websites.
    </p>

    <p>
      The <abbr title="World Wide Web Consortium">W3C</abbr> maintains
      web standards, while
      <abbr title="Mozilla Developer Network">MDN</abbr> provides
      comprehensive documentation.
    </p>

    <p>
      Developers often use
      <abbr title="Application Programming Interface">APIs</abbr> to
      integrate with backend services and databases like
      <abbr title="Structured Query Language">SQL</abbr> or
      <abbr title="Not Only SQL">NoSQL</abbr>.
    </p>
  </article>
</body>
</html>
```

### Example 3: Icon Buttons with Titles

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Icon Toolbar</title>
  <style>
    .toolbar {
      display: flex;
      gap: 10px;
      padding: 10px;
      background: #f0f0f0;
      border-radius: 4px;
    }

    .icon-btn {
      width: 40px;
      height: 40px;
      border: none;
      background: white;
      border-radius: 4px;
      cursor: pointer;
      font-size: 20px;
      transition: background 0.2s;
    }

    .icon-btn:hover {
      background: #e0e0e0;
    }

    .icon-btn:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  </style>
</head>
<body>
  <div class="toolbar">
    <button class="icon-btn" title="Save document (Ctrl+S)">💾</button>
    <button class="icon-btn" title="Open file (Ctrl+O)">📂</button>
    <button class="icon-btn" title="Print (Ctrl+P)">🖨️</button>
    <button class="icon-btn" title="Undo (Ctrl+Z)">↶</button>
    <button class="icon-btn" title="Redo (Ctrl+Y)">↷</button>
    <button class="icon-btn" title="Cut (Ctrl+X)">✂️</button>
    <button class="icon-btn" title="Copy (Ctrl+C)">📋</button>
    <button class="icon-btn" title="Paste (Ctrl+V)">📄</button>
    <button class="icon-btn" disabled title="This feature is not available in the free version">⭐</button>
  </div>

  <p>Hover over the icons to see their functions.</p>
</body>
</html>
```

### Example 4: Email Template with Inline Styles

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Email Template</title>
</head>
<body style="margin: 0; padding: 0; font-family: Arial, sans-serif; background-color: #f4f4f4;">
  <!-- Email clients strip external CSS, so inline styles are required -->
  <table style="width: 100%; max-width: 600px; margin: 0 auto; background-color: white;">
    <!-- Header -->
    <tr>
      <td style="background-color: #007bff; color: white; padding: 30px; text-align: center;">
        <h1 style="margin: 0; font-size: 28px;">Welcome to Our Service!</h1>
      </td>
    </tr>

    <!-- Content -->
    <tr>
      <td style="padding: 40px 30px;">
        <p style="font-size: 16px; line-height: 1.6; color: #333; margin-bottom: 20px;">
          Thank you for signing up. We're excited to have you on board!
        </p>

        <p style="font-size: 16px; line-height: 1.6; color: #333; margin-bottom: 30px;">
          Click the button below to get started:
        </p>

        <!-- Button -->
        <table style="width: 100%;">
          <tr>
            <td style="text-align: center;">
              <a href="https://example.com/get-started"
                 style="display: inline-block; background-color: #28a745; color: white; padding: 15px 30px; text-decoration: none; border-radius: 5px; font-size: 16px; font-weight: bold;">
                Get Started
              </a>
            </td>
          </tr>
        </table>
      </td>
    </tr>

    <!-- Footer -->
    <tr>
      <td style="background-color: #f8f9fa; padding: 20px; text-align: center; font-size: 14px; color: #666;">
        <p style="margin: 0;">© 2025 Your Company. All rights reserved.</p>
        <p style="margin: 10px 0 0 0;">
          <a href="https://example.com/unsubscribe" style="color: #007bff; text-decoration: none;">Unsubscribe</a>
        </p>
      </td>
    </tr>
  </table>
</body>
</html>
```

---

## Best Practices

### Style Attribute

**Do This:**

1. **Use for Dynamic JavaScript-Generated Styles**
   ```javascript
   // GOOD: Dynamic positioning
   element.style.left = calculatePosition() + 'px';
   element.style.backgroundColor = userPreferences.color;
   ```

2. **Use for Email Templates**
   ```html
   <!-- Email clients require inline styles -->
   <td style="background: #007bff; padding: 20px; color: white;">
     Content
   </td>
   ```

3. **Use for Quick Testing**
   ```html
   <!-- Test styling before moving to CSS file -->
   <div style="background: red;">Test</div>
   ```

**Avoid This:**

1. **Don't Use for General Styling**
   ```html
   <!-- WRONG: Use CSS instead -->
   <div style="margin: 20px; padding: 10px; background: white;">Content</div>

   <!-- CORRECT: Use class -->
   <div class="card">Content</div>
   ```

2. **Don't Repeat Inline Styles**
   ```html
   <!-- WRONG: Repeated inline styles -->
   <div style="color: blue; font-size: 16px;">Item 1</div>
   <div style="color: blue; font-size: 16px;">Item 2</div>
   <div style="color: blue; font-size: 16px;">Item 3</div>

   <!-- CORRECT: Use class -->
   <div class="item">Item 1</div>
   <div class="item">Item 2</div>
   <div class="item">Item 3</div>
   ```

### Title Attribute

**Do This:**

1. **Use for Abbreviations**
   ```html
   <abbr title="HyperText Markup Language">HTML</abbr>
   ```

2. **Use for Icon Buttons**
   ```html
   <button title="Save document">💾</button>
   ```

3. **Use for Disabled Elements Explanation**
   ```html
   <button disabled title="Available in premium plan">Premium Feature</button>
   ```

**Avoid This:**

1. **Don't Rely on Title for Critical Info (Mobile)**
   ```html
   <!-- WRONG: Mobile users can't hover -->
   <button title="Click to submit form">Submit</button>

   <!-- BETTER: Visible label -->
   <button>Submit Form</button>
   ```

2. **Don't Use for Form Validation Messages**
   ```html
   <!-- WRONG: Title not accessible enough -->
   <input type="text" title="Please enter a valid email">

   <!-- BETTER: Visible error message -->
   <input type="text" aria-describedby="email-error">
   <span id="email-error" class="error">Please enter a valid email</span>
   ```

3. **Don't Duplicate Visible Text**
   ```html
   <!-- WRONG: Redundant -->
   <a href="/about" title="About Us">About Us</a>

   <!-- CORRECT: Add context -->
   <a href="/about" title="Learn more about our company history">About Us</a>
   ```

---

## Quick Reference

### Style Attribute

```html
<!-- Syntax -->
<element style="property: value; property: value;"></element>

<!-- Examples -->
<div style="color: red;">Text</div>
<div style="background: blue; padding: 20px;">Box</div>

<!-- JavaScript -->
element.style.property = 'value';
element.style.backgroundColor = 'red';
```

### Title Attribute

```html
<!-- Syntax -->
<element title="Advisory text"></element>

<!-- Examples -->
<abbr title="World Wide Web">WWW</abbr>
<button title="Save document">💾</button>
<a href="/page" title="Opens in new window" target="_blank">Link</a>
```

---

## Browser Support

| Attribute | Chrome | Firefox | Safari | Edge | IE |
|-----------|--------|---------|--------|------|----|
| `style` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `title` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| Title tooltip | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |

**Mobile support:**
- `style`: ✅ Full support
- `title`: ⚠️ No hover tooltip (touch devices)

---

## Related Topics
- [ID and Class Attributes](id-class.md)
- [Data Attributes](data-attributes.md)
- [Global Attributes](html5-attributes.md)

---

**Last Updated:** November 17, 2025
**Category:** Global Attributes
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
