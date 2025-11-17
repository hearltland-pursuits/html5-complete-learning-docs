---
title: HTML5 Form Attributes
category: Forms & Input
order: 11
---

# HTML5 Form Attributes

> **Quick Summary:** HTML5 introduced powerful form attributes like `placeholder`, `autofocus`, `autocomplete`, `readonly`, `disabled`, `inputmode`, and more—enhancing user experience without JavaScript while improving accessibility and mobile support.

## Table of Contents
- [Introduction](#introduction)
- [Key Attributes](#key-attributes)
- [Examples](#examples)
- [Common Use Cases](#common-use-cases)
- [Browser Support](#browser-support)
- [Accessibility Considerations](#accessibility-considerations)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)
- [Practice Exercise](#practice-exercise)

---

## Introduction

HTML5 dramatically expanded form capabilities with new attributes that improve user experience, accessibility, and mobile optimization. These attributes handle common scenarios that previously required JavaScript: **autofocus** moves cursor to a field on page load, **placeholder** shows hint text, **autocomplete** controls browser autofill, and **inputmode** displays optimized mobile keyboards.

Understanding these attributes is critical for modern web development. For example, `readonly` vs `disabled` (readonly submits data, disabled doesn't), `autocomplete` values for better autofill (use `autocomplete="email"` not generic `on`), and `inputmode` for mobile UX (`inputmode="numeric"` shows numbers without validation like `type="number"`).

Many attributes work across multiple input types, while some are type-specific. All are designed to work without JavaScript, degrading gracefully in older browsers.

**Key Concept:** HTML5 form attributes provide free UX improvements that would otherwise require JavaScript. Learn the difference between `readonly`/`disabled`, specific `autocomplete` values, and mobile-optimized `inputmode` options.

---

## Key Attributes

### Universal Attributes (Most Inputs)

| Attribute | Values | Description |
|-----------|--------|-------------|
| `autofocus` | Boolean | Automatically focuses this input on page load |
| `autocomplete` | `on`, `off`, specific tokens | Controls browser autofill behavior |
| `readonly` | Boolean | Prevents editing but allows focus and submission |
| `disabled` | Boolean | Disables input (no focus, no submission) |
| `tabindex` | Number | Controls tab order (use sparingly) |
| `spellcheck` | `true`, `false` | Enables/disables spell checking |

### HTML5-Specific Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `placeholder` | Text | Hint text shown when input is empty |
| `inputmode` | `text`, `numeric`, `decimal`, `tel`, `email`, `url`, `search` | Mobile keyboard type (no validation) |
| `list` | Datalist ID | Associates input with datalist suggestions |
| `form` | Form ID | Associates input with form outside it |
| `multiple` | Boolean | Allows multiple values (file, email) |

### Autocomplete Specific Values

| Value | Use Case |
|-------|----------|
| `name` | Full name |
| `email` | Email address |
| `username` | Username for login |
| `current-password` | Current password |
| `new-password` | New password (registration/reset) |
| `tel` | Phone number |
| `street-address` | Street address |
| `postal-code` | ZIP/postal code |
| `cc-number` | Credit card number |

---

## Examples

### Example 1: Login Form with Autofocus and Autocomplete

**Scenario:** Login page where username field automatically gets focus and browser autofills credentials.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Login</title>
</head>
<body>
  <form action="/login" method="POST">
    <h1>Log In</h1>

    <label for="username">Username or Email:</label>
    <input
      type="text"
      id="username"
      name="username"
      autocomplete="username"
      autofocus
      required
      placeholder="Enter your username">

    <label for="password">Password:</label>
    <input
      type="password"
      id="password"
      name="password"
      autocomplete="current-password"
      required
      placeholder="Enter your password">

    <button type="submit">Log In</button>
  </form>
</body>
</html>
```

**Result:** Page loads with cursor in username field (`autofocus`). Browser offers to autofill saved credentials (`autocomplete="username"` and `autocomplete="current-password"`).

---

### Example 2: Mobile-Optimized Phone Number Input

**Scenario:** Contact form optimized for mobile with numeric keyboard but allowing formatting.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Form</title>
</head>
<body>
  <form action="/contact" method="POST">
    <label for="phone">Phone Number:</label>
    <input
      type="text"
      id="phone"
      name="phone"
      inputmode="tel"
      autocomplete="tel"
      placeholder="(555) 123-4567"
      pattern="[\d\s\(\)\-\+]+"
      required
      aria-describedby="phone-hint">

    <small id="phone-hint">Any format accepted. Mobile shows number keyboard.</small>

    <button type="submit">Submit</button>
  </form>
</body>
</html>
```

**Result:** Mobile devices show tel keypad (`inputmode="tel"`) but input allows any characters (unlike `type="tel"`). Browser offers phone number autofill. Pattern validates format server-side.

**Why not `type="tel"`?** `type="tel"` provides no validation and some desktop browsers show spinners. `inputmode="tel"` provides mobile keyboard without side effects.

---

### Example 3: Code Input with No Autocorrect/Spellcheck

**Scenario:** Developer form where users paste code snippets—autocorrect would be harmful.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Code Submission</title>
</head>
<body>
  <form action="/submit-code" method="POST">
    <label for="code-snippet">Code Snippet:</label>
    <textarea
      id="code-snippet"
      name="code"
      rows="15"
      cols="70"
      spellcheck="false"
      autocomplete="off"
      autocorrect="off"
      autocapitalize="off"
      wrap="off"
      placeholder="Paste your code here..."
      required></textarea>

    <button type="submit">Submit Code</button>
  </form>
</body>
</html>
```

**Result:** No spell check red underlines, no autocorrect changing variable names, no auto-capitalization of keywords, no line wrapping. Perfect for code input.

---

## Common Use Cases

### Use Case 1: Search Box with Autofocus
**When:** Search page where users immediately start typing.
**How:**
```html
<form action="/search" method="GET" role="search">
  <label for="q">Search:</label>
  <input
    type="search"
    id="q"
    name="q"
    autofocus
    autocomplete="off"
    placeholder="Search products...">
  <button type="submit">Search</button>
</form>
```
**Why:** `autofocus` puts cursor in search box. `autocomplete="off"` prevents showing old searches (user wants fresh search).

---

### Use Case 2: Readonly Order Summary
**When:** Checkout page showing order total (calculated, not editable).
**How:**
```html
<label for="subtotal">Subtotal:</label>
<input type="text" id="subtotal" name="subtotal" value="$99.99" readonly>

<label for="tax">Tax:</label>
<input type="text" id="tax" name="tax" value="$8.50" readonly>

<label for="total">Total:</label>
<input type="text" id="total" name="total" value="$108.49" readonly>
```
**Why:** `readonly` displays values in input format (for consistency) but prevents editing. Values still submit with form.

---

### Use Case 3: Numeric Input on Mobile (No Spinner)
**When:** Quantity input on mobile where you want number keyboard but no desktop spinners.
**How:**
```html
<label for="quantity">Quantity:</label>
<input
  type="text"
  id="quantity"
  name="quantity"
  inputmode="numeric"
  pattern="[0-9]+"
  maxlength="3"
  placeholder="1"
  required>
```
**Why:** `inputmode="numeric"` shows number keyboard on mobile. `type="text"` avoids desktop spinners. `pattern` validates numbers only.

---

## Browser Support

| Attribute | Chrome | Firefox | Safari | Edge | IE 11 |
|-----------|--------|---------|--------|------|-------|
| `autofocus` | 5+ | 4+ | 5+ | All | 10+ |
| `placeholder` | 4+ | 4+ | 5+ | All | 10+ |
| `autocomplete` | All | All | All | All | All |
| `readonly`/`disabled` | All | All | All | All | All |
| `inputmode` | 66+ | 95+ | 12.2+ | 79+ | ✗ |
| `spellcheck` | All | All | All | All | All |

**Fallback Strategy:**
```html
<!-- Graceful degradation - attributes ignored in unsupported browsers -->
<!-- No JavaScript polyfill needed - forms still work -->
<input type="text" inputmode="numeric" placeholder="Enter number">
<!-- Old browsers: Shows text keyboard, no placeholder, form still works -->
```

**Can I Use Links:**
- [Autofocus](https://caniuse.com/autofocus)
- [Placeholder](https://caniuse.com/input-placeholder)
- [Inputmode](https://caniuse.com/input-inputmode)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- `autofocus` should not disorient keyboard users
- `placeholder` must not replace `<label>` (placeholders disappear)
- `readonly`/`disabled` fields must be clearly indicated

**Level AA Requirements:**
- Placeholder text must have sufficient contrast (WCAG 2.1: minimum 4.5:1)
- Readonly fields should indicate why they're readonly
- Autofocus should not move focus unexpectedly mid-task

### Screen Reader Support

```html
<!-- Accessible placeholder (does NOT replace label) -->
<label for="email">Email Address: *</label>
<input
  type="email"
  id="email"
  name="email"
  placeholder="you@example.com"
  autocomplete="email"
  required
  aria-required="true">

<!-- Accessible readonly field with explanation -->
<label for="order-id">Order ID:</label>
<input
  type="text"
  id="order-id"
  name="order_id"
  value="#12345"
  readonly
  aria-readonly="true"
  aria-describedby="order-id-hint">
<small id="order-id-hint">This value cannot be changed.</small>

<!-- Accessible disabled field -->
<label for="premium-feature">Premium Analytics:</label>
<input
  type="checkbox"
  id="premium-feature"
  disabled
  aria-disabled="true">
<small>Upgrade to access this feature</small>
```

**Key Points:**
- Always use `<label>` even with `placeholder`
- `aria-readonly="true"` announces readonly state
- `aria-disabled="true"` announces disabled state
- Provide context for why fields are readonly/disabled

---

## Best Practices

### Do This

1. **Use Specific Autocomplete Values**
   ```html
   <!-- GOOD: Specific autocomplete tokens -->
   <input type="email" autocomplete="email">
   <input type="text" autocomplete="street-address">
   <input type="text" autocomplete="postal-code">
   ```
   **Why:** Browsers autofill accurately. Generic `autocomplete="on"` is less effective.

2. **Use inputmode for Mobile Keyboards**
   ```html
   <!-- GOOD: Optimized mobile keyboard without type validation -->
   <input type="text" inputmode="decimal" placeholder="0.00">
   ```
   **Why:** Shows decimal keyboard on mobile but avoids `type="number"` spinner issues and validation quirks.

3. **Placeholder as Hint, Not Label**
   ```html
   <!-- GOOD: Label + placeholder as example -->
   <label for="username">Username:</label>
   <input type="text" id="username" placeholder="e.g., john_doe123">
   ```
   **Why:** Placeholder disappears when typing. Always use label for field identification.

---

### Avoid This

1. **Multiple Autofocus Attributes**
   ```html
   <!-- WRONG: Multiple autofocus (only last one works) -->
   <input type="text" autofocus>
   <input type="email" autofocus>
   ```
   **Why Not:** Only one element can have focus. Last autofocus wins, behavior unpredictable.
   **Instead:** Use autofocus on the most important field only.

2. **Placeholder as Label Replacement**
   ```html
   <!-- WRONG: No label, only placeholder -->
   <input type="text" placeholder="Enter your name">
   ```
   **Why Not:** Placeholder disappears when typing. Screen readers may not announce it. Fails WCAG.
   **Instead:**
   ```html
   <label for="name">Name:</label>
   <input type="text" id="name" placeholder="e.g., John Doe">
   ```

3. **Disabling Submit Button Unnecessarily**
   ```html
   <!-- WRONG: Disabled until all fields valid (frustrating UX) -->
   <button type="submit" disabled id="submit-btn">Submit</button>
   <script>
     // Enable only when form is 100% valid
   </script>
   ```
   **Why Not:** Users can't submit to see validation errors. HTML5 validation shows errors on submit attempt.
   **Instead:** Let HTML5 validation handle it. Enable submit button always.

---

## Related Topics

**Prerequisites:**
- [Form Element](form-element.md) - Form structure
- [Text Inputs](text-inputs.md) - Input basics

**Related Concepts:**
- [Form Validation](form-validation.md) - Validation attributes
- [Form Accessibility](form-accessibility.md) - Accessible attributes

**Next Steps:**
- [Form Accessibility](form-accessibility.md) - Complete accessibility guide

**External Resources:**
- [MDN - HTML Attribute Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes)
- [HTML Spec - Autofill](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill)
- [W3Schools - HTML Input Attributes](https://www.w3schools.com/html/html_form_attributes_form.asp)

---

## Practice Exercise

### Challenge: Build an Optimized Contact Form

**Objective:** Create a mobile-optimized contact form using HTML5 attributes for better UX.

**Requirements:**
- [ ] Name input with autofocus
- [ ] Email with autocomplete and placeholder
- [ ] Phone with inputmode for mobile keyboard (numeric)
- [ ] Message textarea with spellcheck enabled
- [ ] Order ID field (readonly, pre-filled with #12345)
- [ ] Bonus: Add autocomplete values for all fields

---

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Form</title>
</head>
<body>
  <h1>Contact Support</h1>
  <form action="/support" method="POST">
    <!-- Add your optimized inputs here -->
    <button type="submit">Send Message</button>
  </form>
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Form</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 2rem auto; padding: 0 1rem; }
    label { display: block; margin-top: 1.5rem; font-weight: bold; }
    input, textarea { width: 100%; padding: 0.5rem; margin-top: 0.5rem; }
    input:read-only { background: #f0f0f0; cursor: not-allowed; }
    small { display: block; color: #666; margin-top: 0.25rem; }
    button { margin-top: 2rem; padding: 0.75rem 1.5rem; width: 100%; }
  </style>
</head>
<body>
  <h1>Contact Support</h1>
  <form action="/support" method="POST">
    <!-- Name with autofocus -->
    <label for="name">Full Name: <span aria-label="required">*</span></label>
    <input
      type="text"
      id="name"
      name="name"
      autofocus
      autocomplete="name"
      placeholder="John Doe"
      required
      aria-required="true">

    <!-- Email with autocomplete -->
    <label for="email">Email Address: <span aria-label="required">*</span></label>
    <input
      type="email"
      id="email"
      name="email"
      autocomplete="email"
      placeholder="you@example.com"
      required
      aria-required="true">

    <!-- Phone with inputmode for mobile -->
    <label for="phone">Phone Number:</label>
    <input
      type="text"
      id="phone"
      name="phone"
      inputmode="tel"
      autocomplete="tel"
      placeholder="(555) 123-4567"
      aria-describedby="phone-hint">
    <small id="phone-hint">Mobile shows number keyboard for easier input</small>

    <!-- Order ID (readonly) -->
    <label for="order-id">Order ID (if applicable):</label>
    <input
      type="text"
      id="order-id"
      name="order_id"
      value="#12345"
      readonly
      aria-readonly="true"
      aria-describedby="order-id-hint">
    <small id="order-id-hint">This is your current order. Cannot be changed.</small>

    <!-- Message with spellcheck -->
    <label for="message">Message: <span aria-label="required">*</span></label>
    <textarea
      id="message"
      name="message"
      rows="8"
      spellcheck="true"
      autocomplete="off"
      placeholder="Describe your issue or question..."
      required
      aria-required="true"
      aria-describedby="message-hint"></textarea>
    <small id="message-hint">Spellcheck enabled to help catch typos</small>

    <button type="submit">Send Message</button>
  </form>
</body>
</html>
```

**Explanation:** This contact form leverages HTML5 attributes for optimal UX: `autofocus` on name field (cursor ready), `autocomplete` with specific tokens (name, email, tel) for accurate browser autofill, `inputmode="tel"` for mobile number keyboard without validation side effects, `readonly` on order ID with visual indication (gray background), and `spellcheck="true"` on message to catch typos. All fields have proper labels, placeholders as hints (not replacements), and ARIA attributes for accessibility.

</details>

---

### Expected Result

A mobile-optimized contact form where cursor starts in name field, browser autofills saved contact info, phone field shows numeric keyboard on mobile, order ID is visible but uneditable (grayed out), and message textarea enables spellcheck.

**Key Learnings:**
- Using `autofocus` appropriately (one field only)
- Specific `autocomplete` values improve autofill accuracy
- `inputmode` provides mobile keyboard optimization without validation
- Difference between `readonly` (submits) and `disabled` (doesn't submit)
- `placeholder` as hint, never as label replacement
- Combining attributes for optimal UX

---

## Navigation

**Previous:** [Fieldsets & Legends](fieldsets.md)
**Next:** [Form Accessibility](form-accessibility.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
