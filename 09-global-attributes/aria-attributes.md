---
title: ARIA Attributes
category: Global Attributes
order: 22
---

# ARIA Attributes

> **Quick Summary:** ARIA (Accessible Rich Internet Applications) attributes improve accessibility for users with disabilities. They add semantic meaning to elements for screen readers, define roles, states, and properties that make dynamic web apps accessible. Critical for WCAG compliance and modern web development.

## Table of Contents
- [Introduction](#introduction)
- [ARIA Roles](#aria-roles)
- [ARIA States](#aria-states)
- [ARIA Properties](#aria-properties)
- [Common Patterns](#common-patterns)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

ARIA (Accessible Rich Internet Applications) is a W3C specification that makes web content and applications more accessible to people with disabilities. ARIA attributes provide additional semantic information to assistive technologies like screen readers.

**Three categories:**
1. **Roles** - What an element is (`role="button"`, `role="navigation"`)
2. **States** - Dynamic conditions (`aria-expanded`, `aria-checked`)
3. **Properties** - Characteristics (`aria-label`, `aria-describedby`)

**Key points:**
- Use semantic HTML first (ARIA is a supplement, not replacement)
- ARIA doesn't change behavior (only semantics)
- Screen readers announce ARIA information
- Critical for accessibility compliance (WCAG 2.1)

**Key Concept:** ARIA is like adding subtitles for screen readers—it describes what elements do and how they change, making dynamic web apps accessible to users who can't see visual cues.

---

## ARIA Roles

### What Are Roles?

Roles define what an element is or does. Use semantic HTML when possible; use ARIA roles when semantic elements don't exist.

### Common Roles

#### Landmark Roles

```html
<!-- Navigation landmark -->
<div role="navigation">
  <a href="/">Home</a>
  <a href="/about">About</a>
</div>

<!-- Better: Use semantic HTML -->
<nav>
  <a href="/">Home</a>
  <a href="/about">About</a>
</nav>

<!-- Main content landmark -->
<div role="main">Main content</div>

<!-- Better: Semantic HTML -->
<main>Main content</main>

<!-- Complementary content -->
<div role="complementary">Sidebar</div>

<!-- Better: Semantic HTML -->
<aside>Sidebar</aside>
```

#### Widget Roles

```html
<!-- Button (when div used instead of button) -->
<div role="button" tabindex="0">Click me</div>

<!-- Better: Use <button> -->
<button>Click me</button>

<!-- Checkbox -->
<div role="checkbox" aria-checked="false" tabindex="0">
  Accept terms
</div>

<!-- Better: Use <input type="checkbox"> -->
<input type="checkbox" id="terms">
<label for="terms">Accept terms</label>

<!-- Tab interface -->
<div role="tablist">
  <button role="tab" aria-selected="true">Tab 1</button>
  <button role="tab" aria-selected="false">Tab 2</button>
</div>
<div role="tabpanel">Tab 1 content</div>
```

#### Document Roles

```html
<!-- Article -->
<div role="article">Article content</div>

<!-- Better: Semantic HTML -->
<article>Article content</article>

<!-- Alert (important message) -->
<div role="alert">
  Error: Please fill in all required fields.
</div>

<!-- Live region (updates announced to screen readers) -->
<div role="status" aria-live="polite">
  Loading...
</div>
```

---

## ARIA States

### What Are States?

States describe dynamic conditions that change during interaction (expanded/collapsed, checked/unchecked, etc.).

### Common States

#### aria-expanded

```html
<!-- Collapsible menu -->
<button aria-expanded="false" aria-controls="menu">
  Menu
</button>
<ul id="menu" hidden>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<script>
const button = document.querySelector('[aria-expanded]');
const menu = document.getElementById('menu');

button.addEventListener('click', function() {
  const isExpanded = this.getAttribute('aria-expanded') === 'true';
  this.setAttribute('aria-expanded', !isExpanded);
  menu.hidden = isExpanded;
});
</script>
```

#### aria-checked

```html
<!-- Custom checkbox -->
<div role="checkbox"
     aria-checked="false"
     tabindex="0"
     id="custom-checkbox">
  Accept terms
</div>

<script>
const checkbox = document.getElementById('custom-checkbox');

checkbox.addEventListener('click', function() {
  const isChecked = this.getAttribute('aria-checked') === 'true';
  this.setAttribute('aria-checked', !isChecked);
});

checkbox.addEventListener('keypress', function(e) {
  if (e.key === ' ' || e.key === 'Enter') {
    e.preventDefault();
    this.click();
  }
});
</script>
```

#### aria-hidden

```html
<!-- Hide decorative icons from screen readers -->
<button>
  <span aria-hidden="true">🔍</span>
  Search
</button>

<!-- Hide until visible -->
<div aria-hidden="true" id="modal" style="display:none;">
  Modal content
</div>
```

#### aria-disabled

```html
<!-- Disabled button (when using div) -->
<div role="button" aria-disabled="true" tabindex="-1">
  Can't click me
</div>

<!-- Better: Use disabled attribute on button -->
<button disabled>Can't click me</button>
```

#### aria-selected

```html
<!-- Tab interface -->
<div role="tablist">
  <button role="tab" aria-selected="true" aria-controls="panel1">
    Tab 1
  </button>
  <button role="tab" aria-selected="false" aria-controls="panel2">
    Tab 2
  </button>
</div>

<div role="tabpanel" id="panel1">Tab 1 content</div>
<div role="tabpanel" id="panel2" hidden>Tab 2 content</div>
```

---

## ARIA Properties

### What Are Properties?

Properties define characteristics that don't typically change (labels, descriptions, relationships).

### Common Properties

#### aria-label

```html
<!-- Add accessible label when no visible text -->
<button aria-label="Close dialog">
  ✕
</button>

<!-- Icon-only button -->
<button aria-label="Search">
  🔍
</button>

<!-- Navigation -->
<nav aria-label="Main navigation">
  <a href="/">Home</a>
  <a href="/about">About</a>
</nav>
```

#### aria-labelledby

```html
<!-- Label element by referencing another element's ID -->
<h2 id="dialog-title">Confirm Action</h2>
<div role="dialog" aria-labelledby="dialog-title">
  <p>Are you sure you want to delete this item?</p>
  <button>Yes</button>
  <button>No</button>
</div>
```

#### aria-describedby

```html
<!-- Add description for context -->
<label for="password">Password:</label>
<input type="password"
       id="password"
       aria-describedby="password-hint password-error">
<small id="password-hint">Must be at least 8 characters</small>
<span id="password-error" role="alert"></span>
```

#### aria-live

```html
<!-- Announce updates to screen readers -->
<div aria-live="polite" aria-atomic="true">
  <!-- Updates announced when content changes -->
  <p id="status">Loading...</p>
</div>

<script>
// Update status (screen reader announces change)
document.getElementById('status').textContent = 'Loading complete!';
</script>
```

**aria-live values:**
- `off` - No announcements (default)
- `polite` - Announce when user is idle
- `assertive` - Interrupt and announce immediately

#### aria-controls

```html
<!-- Indicate which element is controlled -->
<button aria-expanded="false" aria-controls="menu">
  Menu
</button>
<ul id="menu" hidden>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

#### aria-required

```html
<!-- Mark field as required -->
<label for="email">Email:</label>
<input type="email"
       id="email"
       aria-required="true">

<!-- Better: Use required attribute -->
<input type="email" id="email" required>
```

#### aria-invalid

```html
<!-- Mark field as invalid -->
<label for="email">Email:</label>
<input type="email"
       id="email"
       aria-invalid="true"
       aria-describedby="email-error">
<span id="email-error" role="alert">
  Please enter a valid email address
</span>
```

---

## Common Patterns

### Modal Dialog

```html
<div role="dialog"
     aria-labelledby="dialog-title"
     aria-describedby="dialog-desc"
     aria-modal="true">

  <h2 id="dialog-title">Confirm Delete</h2>
  <p id="dialog-desc">
    Are you sure you want to delete this item? This action cannot be undone.
  </p>

  <button>Delete</button>
  <button>Cancel</button>
</div>
```

### Accordion

```html
<div class="accordion">
  <h3>
    <button aria-expanded="false" aria-controls="section1">
      Section 1
    </button>
  </h3>
  <div id="section1" hidden>
    <p>Section 1 content...</p>
  </div>

  <h3>
    <button aria-expanded="false" aria-controls="section2">
      Section 2
    </button>
  </h3>
  <div id="section2" hidden>
    <p>Section 2 content...</p>
  </div>
</div>
```

### Tabs

```html
<div role="tablist" aria-label="Product Information">
  <button role="tab"
          aria-selected="true"
          aria-controls="desc-panel"
          id="desc-tab">
    Description
  </button>
  <button role="tab"
          aria-selected="false"
          aria-controls="specs-panel"
          id="specs-tab">
    Specifications
  </button>
</div>

<div role="tabpanel"
     id="desc-panel"
     aria-labelledby="desc-tab">
  Product description...
</div>

<div role="tabpanel"
     id="specs-panel"
     aria-labelledby="specs-tab"
     hidden>
  Product specifications...
</div>
```

### Alert/Notification

```html
<!-- Alert (interrupts user) -->
<div role="alert">
  <strong>Error:</strong> Your session has expired.
</div>

<!-- Status (less urgent) -->
<div role="status" aria-live="polite">
  Changes saved successfully.
</div>
```

### Form with Validation

```html
<form>
  <div>
    <label for="username">Username: <span aria-label="required">*</span></label>
    <input type="text"
           id="username"
           aria-required="true"
           aria-invalid="false"
           aria-describedby="username-hint username-error">
    <small id="username-hint">3-20 characters</small>
    <span id="username-error" role="alert" aria-live="polite"></span>
  </div>

  <div>
    <label for="email">Email: <span aria-label="required">*</span></label>
    <input type="email"
           id="email"
           aria-required="true"
           aria-invalid="false"
           aria-describedby="email-error">
    <span id="email-error" role="alert" aria-live="polite"></span>
  </div>

  <button type="submit">Submit</button>
</form>
```

---

## Examples

### Example 1: Accessible Modal

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Accessible Modal</title>
  <style>
    .modal-overlay {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.7);
      justify-content: center;
      align-items: center;
    }

    .modal-overlay[aria-hidden="false"] {
      display: flex;
    }

    .modal-content {
      background: white;
      padding: 40px;
      border-radius: 8px;
      max-width: 500px;
    }

    .close-btn {
      float: right;
      background: none;
      border: none;
      font-size: 24px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <button id="open-modal-btn">Open Modal</button>

  <div class="modal-overlay"
       id="modal"
       role="dialog"
       aria-modal="true"
       aria-labelledby="modal-title"
       aria-describedby="modal-desc"
       aria-hidden="true">

    <div class="modal-content">
      <button class="close-btn"
              aria-label="Close dialog"
              id="close-modal-btn">
        ×
      </button>

      <h2 id="modal-title">Important Message</h2>
      <p id="modal-desc">
        This is an accessible modal dialog. It has proper ARIA attributes
        for screen readers and keyboard navigation.
      </p>

      <button>Confirm</button>
      <button id="cancel-btn">Cancel</button>
    </div>
  </div>

  <script>
    const openBtn = document.getElementById('open-modal-btn');
    const closeBtn = document.getElementById('close-modal-btn');
    const cancelBtn = document.getElementById('cancel-btn');
    const modal = document.getElementById('modal');

    function openModal() {
      modal.setAttribute('aria-hidden', 'false');
      closeBtn.focus(); // Move focus to modal
    }

    function closeModal() {
      modal.setAttribute('aria-hidden', 'true');
      openBtn.focus(); // Return focus to trigger button
    }

    openBtn.addEventListener('click', openModal);
    closeBtn.addEventListener('click', closeModal);
    cancelBtn.addEventListener('click', closeModal);

    // Close on Escape key
    document.addEventListener('keydown', function(e) {
      if (e.key === 'Escape' && modal.getAttribute('aria-hidden') === 'false') {
        closeModal();
      }
    });

    // Trap focus inside modal
    modal.addEventListener('keydown', function(e) {
      if (e.key === 'Tab') {
        const focusable = modal.querySelectorAll('button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])');
        const first = focusable[0];
        const last = focusable[focusable.length - 1];

        if (e.shiftKey && document.activeElement === first) {
          e.preventDefault();
          last.focus();
        } else if (!e.shiftKey && document.activeElement === last) {
          e.preventDefault();
          first.focus();
        }
      }
    });
  </script>
</body>
</html>
```

### Example 2: Accessible Tabs

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Accessible Tabs</title>
  <style>
    [role="tablist"] {
      display: flex;
      border-bottom: 2px solid #ddd;
      gap: 5px;
    }

    [role="tab"] {
      padding: 10px 20px;
      border: none;
      background: white;
      cursor: pointer;
      border-bottom: 3px solid transparent;
    }

    [role="tab"][aria-selected="true"] {
      border-bottom-color: #007bff;
      font-weight: bold;
    }

    [role="tabpanel"] {
      padding: 20px;
      border: 1px solid #ddd;
      border-top: none;
    }
  </style>
</head>
<body>
  <div role="tablist" aria-label="Product Information">
    <button role="tab"
            aria-selected="true"
            aria-controls="panel-desc"
            id="tab-desc"
            tabindex="0">
      Description
    </button>
    <button role="tab"
            aria-selected="false"
            aria-controls="panel-specs"
            id="tab-specs"
            tabindex="-1">
      Specifications
    </button>
    <button role="tab"
            aria-selected="false"
            aria-controls="panel-reviews"
            id="tab-reviews"
            tabindex="-1">
      Reviews
    </button>
  </div>

  <div role="tabpanel"
       id="panel-desc"
       aria-labelledby="tab-desc">
    <h2>Product Description</h2>
    <p>Detailed product description goes here...</p>
  </div>

  <div role="tabpanel"
       id="panel-specs"
       aria-labelledby="tab-specs"
       hidden>
    <h2>Specifications</h2>
    <ul>
      <li>Weight: 500g</li>
      <li>Dimensions: 20x15x5cm</li>
    </ul>
  </div>

  <div role="tabpanel"
       id="panel-reviews"
       aria-labelledby="tab-reviews"
       hidden>
    <h2>Customer Reviews</h2>
    <p>Reviews content goes here...</p>
  </div>

  <script>
    const tabs = document.querySelectorAll('[role="tab"]');
    const panels = document.querySelectorAll('[role="tabpanel"]');

    tabs.forEach((tab, index) => {
      tab.addEventListener('click', function() {
        // Deactivate all tabs
        tabs.forEach(t => {
          t.setAttribute('aria-selected', 'false');
          t.setAttribute('tabindex', '-1');
        });

        // Hide all panels
        panels.forEach(p => p.hidden = true);

        // Activate clicked tab
        this.setAttribute('aria-selected', 'true');
        this.setAttribute('tabindex', '0');

        // Show corresponding panel
        const panelId = this.getAttribute('aria-controls');
        document.getElementById(panelId).hidden = false;
      });

      // Keyboard navigation (Arrow keys)
      tab.addEventListener('keydown', function(e) {
        let targetTab;

        if (e.key === 'ArrowRight') {
          targetTab = tabs[(index + 1) % tabs.length];
        } else if (e.key === 'ArrowLeft') {
          targetTab = tabs[(index - 1 + tabs.length) % tabs.length];
        }

        if (targetTab) {
          targetTab.click();
          targetTab.focus();
        }
      });
    });
  </script>
</body>
</html>
```

---

## Best Practices

### Do This

1. **Use Semantic HTML First**
   ```html
   <!-- GOOD: Semantic HTML (ARIA not needed) -->
   <button>Click me</button>
   <nav>Navigation</nav>
   <main>Content</main>

   <!-- AVOID: Non-semantic + ARIA -->
   <div role="button">Click me</div>
   <div role="navigation">Navigation</div>
   <div role="main">Content</div>
   ```

2. **Provide Text Alternatives**
   ```html
   <!-- GOOD: Screen reader can announce button purpose -->
   <button aria-label="Close dialog">×</button>

   <!-- BAD: No accessible name -->
   <button>×</button>
   ```

3. **Use aria-live for Dynamic Updates**
   ```html
   <!-- GOOD: Screen reader announces changes -->
   <div role="status" aria-live="polite" id="status">
     Loading...
   </div>

   <script>
   document.getElementById('status').textContent = 'Loading complete!';
   </script>
   ```

4. **Associate Labels with Inputs**
   ```html
   <!-- GOOD: Multiple ways to associate -->
   <label for="email">Email:</label>
   <input type="email"
          id="email"
          aria-describedby="email-hint">
   <small id="email-hint">We'll never share your email</small>
   ```

### Avoid This

1. **Don't Overuse ARIA**
   ```html
   <!-- WRONG: Redundant ARIA on semantic HTML -->
   <button role="button" aria-label="Submit">Submit</button>

   <!-- CORRECT: Button element is self-explanatory -->
   <button>Submit</button>
   ```

2. **Don't Forget Keyboard Accessibility**
   ```html
   <!-- WRONG: Div not keyboard accessible -->
   <div role="button" onclick="handleClick()">Click</div>

   <!-- CORRECT: Keyboard accessible -->
   <div role="button" tabindex="0" onclick="handleClick()" onkeypress="handleClick()">
     Click
   </div>

   <!-- BEST: Use actual button -->
   <button onclick="handleClick()">Click</button>
   ```

3. **Don't Use ARIA Without States/Properties**
   ```html
   <!-- WRONG: role="checkbox" without aria-checked -->
   <div role="checkbox">Accept terms</div>

   <!-- CORRECT: Include required states -->
   <div role="checkbox" aria-checked="false" tabindex="0">
     Accept terms
   </div>
   ```

---

## Quick Reference

### Essential ARIA Attributes

| Attribute | Purpose | Example |
|-----------|---------|---------|
| `aria-label` | Add accessible label | `<button aria-label="Close">×</button>` |
| `aria-labelledby` | Reference label element | `<div aria-labelledby="heading">` |
| `aria-describedby` | Reference description | `<input aria-describedby="hint">` |
| `aria-expanded` | Collapsed/expanded state | `<button aria-expanded="false">` |
| `aria-hidden` | Hide from screen readers | `<span aria-hidden="true">🔍</span>` |
| `aria-live` | Announce updates | `<div aria-live="polite">` |
| `aria-required` | Mark field required | `<input aria-required="true">` |
| `aria-invalid` | Mark field invalid | `<input aria-invalid="true">` |

---

## Browser Support

ARIA is supported in all modern browsers and screen readers:

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| ARIA 1.0 | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 8+ |
| ARIA 1.1 | ✅ 50+ | ✅ 48+ | ✅ 10+ | ✅ All | ❌ No |
| ARIA 1.2 | ✅ 81+ | ✅ 72+ | ✅ 13+ | ✅ 81+ | ❌ No |

---

## Related Topics
- [Accessibility Overview](../13-accessibility/accessibility-overview.md)
- [Semantic HTML](../07-semantic-html5/semantic-overview.md)
- [Form Accessibility](../06-forms-input/form-accessibility.md)

---

**Last Updated:** November 17, 2025
**Category:** Global Attributes
**Difficulty:** Advanced
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
