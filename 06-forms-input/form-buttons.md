---
title: Form Buttons
category: Forms & Input
order: 9
---

# Form Buttons

> **Quick Summary:** Form buttons (`<button>` and `<input type="button/submit/reset">`) trigger form actions—submission, reset, or custom JavaScript functions. Understanding `type` attribute differences is critical for proper form behavior.

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

Form buttons execute actions: **submit** sends form data to the server, **reset** clears all form fields to defaults, and **button** performs custom actions via JavaScript. HTML provides two ways to create buttons: the `<button>` element (preferred, more flexible) and `<input type="button/submit/reset">` (legacy, less flexible).

The `<button>` element supports rich content (icons, images, complex markup) and has explicit `type` attribute control. **Critical:** Inside a `<form>`, `<button>` defaults to `type="submit"` even without the attribute—a common source of bugs when developers expect `type="button"` behavior.

Modern forms typically use: `<button type="submit">` for form submission, `<button type="button">` for JavaScript actions (modals, adding fields), and rarely `<button type="reset">` (poor UX, accidental clicks).

**Key Concept:** Always explicitly set `type` attribute on `<button>` elements inside forms. Without it, they default to `type="submit"`, potentially causing unexpected form submissions.

---

## Basic Syntax

```html
<!-- Submit button (submits form) -->
<button type="submit">Submit Form</button>

<!-- Reset button (clears form) -->
<button type="reset">Clear Form</button>

<!-- Generic button (does nothing unless JS attached) -->
<button type="button" onclick="alert('Clicked!')">Click Me</button>

<!-- Legacy input buttons -->
<input type="submit" value="Submit">
<input type="reset" value="Reset">
<input type="button" value="Click">
```

### Button Types

| Type | Behavior | Use Case |
|------|----------|----------|
| `submit` | Submits the form | Primary action (Save, Send, Login) |
| `reset` | Resets all fields to default values | Rarely used (poor UX) |
| `button` | Does nothing (requires JavaScript) | Custom actions (Add Item, Show Modal) |

### Key Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `type` | `submit`, `reset`, `button` | Determines button behavior (**critical**) |
| `form` | Form ID | Associates button with form outside it |
| `formaction` | URL | Override form's `action` for this button |
| `formmethod` | `GET`, `POST` | Override form's `method` for this button |
| `formnovalidate` | Boolean | Skip validation for this button (e.g., "Save Draft") |
| `disabled` | Boolean | Disables button (grayed out, non-clickable) |
| `name` / `value` | Text | Sends button's value if clicked (for server-side detection) |

---

## Examples

### Example 1: Standard Form with Submit and Reset

**Scenario:** Contact form with submit and clear buttons.

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
    <label for="name">Name: *</label>
    <input type="text" id="name" name="name" required>

    <label for="email">Email: *</label>
    <input type="email" id="email" name="email" required>

    <label for="message">Message: *</label>
    <textarea id="message" name="message" rows="5" required></textarea>

    <!-- Submit button -->
    <button type="submit">Send Message</button>

    <!-- Reset button (clears form) -->
    <button type="reset">Clear Form</button>
  </form>
</body>
</html>
```

**Result:** "Send Message" submits form to `/contact`. "Clear Form" resets all fields to empty (or default values if specified).

---

### Example 2: Multiple Submit Buttons with Different Actions

**Scenario:** Draft/publish system where users can save draft or publish post.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog Post Editor</title>
</head>
<body>
  <form action="/posts" method="POST">
    <label for="title">Post Title: *</label>
    <input type="text" id="title" name="title" required>

    <label for="content">Content: *</label>
    <textarea id="content" name="content" rows="15" required></textarea>

    <!-- Publish button (validates form) -->
    <button type="submit" name="action" value="publish">
      Publish Post
    </button>

    <!-- Save draft button (skips validation) -->
    <button type="submit" name="action" value="draft" formnovalidate>
      Save as Draft
    </button>
  </form>
</body>
</html>
```

**Result:** "Publish Post" validates form (required fields). "Save as Draft" submits without validation (formnovalidate). Server receives `action=publish` or `action=draft` to determine behavior.

---

### Example 3: Button Outside Form (using form attribute)

**Scenario:** Submit button located outside the form (e.g., sticky footer).

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>External Button</title>
  <style>
    .sticky-footer { position: fixed; bottom: 0; width: 100%; background: #f0f0f0; padding: 1rem; }
  </style>
</head>
<body>
  <form id="checkout-form" action="/checkout" method="POST">
    <h1>Checkout</h1>

    <label for="card-name">Name on Card: *</label>
    <input type="text" id="card-name" name="name" required>

    <label for="card-number">Card Number: *</label>
    <input type="text" id="card-number" name="card" pattern="[0-9]{13,19}" required>

    <!-- Form fields... -->
  </form>

  <!-- Button outside form but associated via form="checkout-form" -->
  <div class="sticky-footer">
    <button type="submit" form="checkout-form">Complete Purchase</button>
  </div>
</body>
</html>
```

**Result:** Button in sticky footer submits the form even though it's not a child of `<form>`. The `form` attribute links it to the form by ID.

---

## Common Use Cases

### Use Case 1: Icon Button with Text
**When:** Modern UI with icon + text submit buttons.
**How:**
```html
<button type="submit">
  <svg width="16" height="16"><!-- Send icon SVG --></svg>
  Send Message
</button>
```
**Why:** `<button>` allows rich content (icons, images). `<input type="submit">` only allows text.

---

### Use Case 2: Loading State (Disabled During Submission)
**When:** Prevent duplicate submissions while processing.
**How:**
```html
<form id="payment-form">
  <!-- Form fields -->
  <button type="submit" id="submit-btn">Complete Payment</button>
</form>

<script>
  const form = document.getElementById('payment-form');
  const btn = document.getElementById('submit-btn');

  form.addEventListener('submit', function(e) {
    btn.disabled = true;
    btn.textContent = 'Processing...';
    // Form submits normally after this
  });
</script>
```
**Why:** Disables button on submit to prevent double-clicking. Provides visual feedback.

---

### Use Case 3: Dynamic Form (Add/Remove Fields)
**When:** Form where users can add/remove input fields (e.g., multiple phone numbers).
**How:**
```html
<form>
  <div id="phone-fields">
    <label>Phone: <input type="tel" name="phones[]"></label>
  </div>

  <!-- Button type="button" to avoid submitting form -->
  <button type="button" onclick="addPhone()">Add Another Phone</button>

  <button type="submit">Save Contact</button>
</form>

<script>
  function addPhone() {
    const container = document.getElementById('phone-fields');
    const newField = document.createElement('div');
    newField.innerHTML = '<label>Phone: <input type="tel" name="phones[]"></label>';
    container.appendChild(newField);
  }
</script>
```
**Why:** `type="button"` prevents form submission. Only used for JavaScript actions.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | Full support for all button types and attributes |
| Firefox | All     | Full Support  | Full support since earliest versions |
| Safari  | All     | Full Support  | Full support (all versions) |
| Edge    | All     | Full Support  | Full support (all versions) |
| IE 11   | 11      | Partial Support | `form` attribute not supported in IE 9 and older |

**Fallback Strategy:**
```html
<!-- No fallback needed - universal support -->
<!-- For 'form' attribute in old IE, place button inside form -->
```

**Can I Use Link:** [Button Element](https://caniuse.com/button) (universal support)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Buttons must be keyboard-accessible (Spacebar/Enter to activate)
- Button text must clearly describe the action
- Disabled buttons should not be in tab order

**Level AA Requirements:**
- Button text must have sufficient color contrast (4.5:1 for normal, 3:1 for large)
- Icon-only buttons must have accessible labels
- Loading states should be announced to screen readers

### Screen Reader Support

```html
<!-- Accessible submit button -->
<button type="submit" aria-label="Submit contact form">
  Send Message
</button>

<!-- Accessible icon button -->
<button type="button" aria-label="Add new item">
  <svg aria-hidden="true"><!-- Plus icon --></svg>
  Add Item
</button>

<!-- Accessible loading state -->
<button type="submit" id="login-btn" aria-live="polite">
  Log In
</button>

<script>
  const btn = document.getElementById('login-btn');
  form.addEventListener('submit', function() {
    btn.textContent = 'Logging in...';
    btn.setAttribute('aria-busy', 'true');
    btn.disabled = true;
  });
</script>
```

**Key Points:**
- `aria-label` provides accessible name for icon-only buttons
- `aria-busy="true"` announces processing state to screen readers
- `aria-hidden="true"` on icons prevents redundant announcements

### Keyboard Navigation

- **Tab:** Moves focus to button
- **Shift + Tab:** Moves focus to previous element
- **Spacebar:** Activates button
- **Enter:** Activates button (also submits form if focus is on submit button)

---

## Best Practices

### Do This

1. **Always Specify type Attribute**
   ```html
   <!-- GOOD: Explicit type prevents bugs -->
   <button type="button" onclick="showModal()">Open Modal</button>
   <button type="submit">Submit Form</button>
   ```
   **Why:** Inside forms, `<button>` defaults to `type="submit"` without explicit type, causing unexpected submissions.

2. **Use button Element Over input**
   ```html
   <!-- GOOD: Flexible, supports rich content -->
   <button type="submit">
     <img src="icon.svg" alt=""> Send Message
   </button>
   ```
   **Why:** `<button>` allows icons, images, complex markup. `<input type="submit">` only allows text.

3. **Disable Submit During Processing**
   ```html
   <form onsubmit="disableButton()">
     <button type="submit" id="submit">Submit</button>
   </form>

   <script>
     function disableButton() {
       const btn = document.getElementById('submit');
       btn.disabled = true;
       btn.textContent = 'Submitting...';
     }
   </script>
   ```
   **Why:** Prevents double-submissions from impatient users clicking multiple times.

---

### Avoid This

1. **Missing type Attribute Inside Forms**
   ```html
   <!-- WRONG: Will submit form unexpectedly -->
   <form>
     <button onclick="showModal()">Options</button>
   </form>
   ```
   **Why Not:** Without `type="button"`, this submits the form when clicked.
   **Instead:**
   ```html
   <button type="button" onclick="showModal()">Options</button>
   ```

2. **Using Reset Buttons**
   ```html
   <!-- WRONG: Easy to accidentally click, frustrating users -->
   <button type="submit">Submit</button>
   <button type="reset">Reset</button>
   ```
   **Why Not:** Users accidentally click reset, losing all their work. Very poor UX.
   **Instead:** Remove reset buttons. If needed, use confirmation dialog.

3. **Generic Button Text**
   ```html
   <!-- WRONG: Screen readers announce "button" with no context -->
   <button type="submit">Click Here</button>
   <button type="button" aria-label="Button">
     <svg><!-- Icon --></svg>
   </button>
   ```
   **Why Not:** "Click Here" doesn't describe action. Generic labels confuse screen reader users.
   **Instead:**
   ```html
   <button type="submit">Submit Application</button>
   <button type="button" aria-label="Add to cart">
     <svg><!-- Icon --></svg>
   </button>
   ```

---

## Related Topics

**Prerequisites:**
- [Form Element](form-element.md) - Understanding form structure
- [Form Validation](form-validation.md) - Validation and formnovalidate

**Related Concepts:**
- [Form Attributes](form-attributes.md) - Form-related button attributes
- [Form Accessibility](form-accessibility.md) - Accessible buttons

**Next Steps:**
- [Fieldsets](fieldsets.md) - Grouping form elements
- [Form Accessibility](form-accessibility.md) - WCAG-compliant forms

**External Resources:**
- [MDN - Button Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)
- [W3Schools - HTML Button Tag](https://www.w3schools.com/tags/tag_button.asp)
- [WCAG - Button Accessibility](https://www.w3.org/WAI/ARIA/apg/patterns/button/)

---

## Practice Exercise

### Challenge: Build a Multi-Action Form

**Objective:** Create a post editor with publish, draft, and preview buttons using different button types and attributes.

**Requirements:**
- [ ] Publish button (validates form, name/value for server detection)
- [ ] Save draft button (skips validation using formnovalidate)
- [ ] Preview button (type="button", opens new window with preview)
- [ ] Cancel button (type="button", redirects to dashboard)
- [ ] Bonus: Disable publish during submission with loading text

---

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Post Editor</title>
</head>
<body>
  <h1>Create New Post</h1>
  <form id="post-form" action="/posts" method="POST">
    <label for="title">Title: *</label>
    <input type="text" id="title" name="title" required>

    <label for="content">Content: *</label>
    <textarea id="content" name="content" rows="15" required></textarea>

    <!-- Add your buttons here -->
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
  <title>Post Editor</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 800px; margin: 2rem auto; padding: 0 1rem; }
    label { display: block; margin-top: 1rem; font-weight: bold; }
    input, textarea { width: 100%; padding: 0.5rem; margin-top: 0.5rem; }
    .button-group { margin-top: 2rem; display: flex; gap: 1rem; }
    button { padding: 0.75rem 1.5rem; }
    button[type="submit"] { background: #0066cc; color: white; border: none; }
    button[type="button"] { background: #f0f0f0; border: 1px solid #ccc; }
  </style>
</head>
<body>
  <h1>Create New Post</h1>
  <form id="post-form" action="/posts" method="POST">
    <label for="title">Title: <span aria-label="required">*</span></label>
    <input type="text" id="title" name="title" required>

    <label for="content">Content: <span aria-label="required">*</span></label>
    <textarea id="content" name="content" rows="15" required></textarea>

    <div class="button-group">
      <!-- Publish button (validates, sends action=publish) -->
      <button type="submit" name="action" value="publish" id="publish-btn">
        Publish Post
      </button>

      <!-- Save draft (no validation, sends action=draft) -->
      <button type="submit" name="action" value="draft" formnovalidate>
        Save as Draft
      </button>

      <!-- Preview button (type="button", JavaScript action) -->
      <button type="button" onclick="previewPost()">
        Preview
      </button>

      <!-- Cancel button (type="button", redirect) -->
      <button type="button" onclick="window.location.href='/dashboard'">
        Cancel
      </button>
    </div>
  </form>

  <script>
    // Preview function (opens in new window)
    function previewPost() {
      const title = document.getElementById('title').value;
      const content = document.getElementById('content').value;

      const previewWindow = window.open('', 'Preview', 'width=800,height=600');
      previewWindow.document.write(`
        <html>
        <head><title>Preview: ${title}</title></head>
        <body>
          <h1>${title}</h1>
          <div>${content}</div>
        </body>
        </html>
      `);
    }

    // Bonus: Disable publish during submission
    const form = document.getElementById('post-form');
    const publishBtn = document.getElementById('publish-btn');

    form.addEventListener('submit', function(e) {
      if (e.submitter === publishBtn) {
        publishBtn.disabled = true;
        publishBtn.textContent = 'Publishing...';
        publishBtn.setAttribute('aria-busy', 'true');
      }
    });
  </script>
</body>
</html>
```

**Explanation:** This form uses multiple button types: `type="submit"` for publish/draft (with `name="action"` and different `value`s so server knows which was clicked), `formnovalidate` on draft button to skip validation, `type="button"` for preview (JavaScript opens new window) and cancel (redirects). Bonus: publish button disables during submission with "Publishing..." text and `aria-busy="true"` for screen readers.

</details>

---

### Expected Result

A post editor with 4 buttons: Publish (validates + submits), Save Draft (submits without validation), Preview (opens new window with preview, doesn't submit), Cancel (redirects to dashboard). Publish button shows "Publishing..." and disables when clicked.

**Key Learnings:**
- Difference between `type="submit"` and `type="button"`
- Using `formnovalidate` for draft/save buttons
- Multiple submit buttons with `name`/`value` for server detection
- Disabling buttons during submission for better UX
- Using `form` attribute to associate external buttons

---

## Navigation

**Previous:** [Form Validation](form-validation.md)
**Next:** [Fieldsets & Legends](fieldsets.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
