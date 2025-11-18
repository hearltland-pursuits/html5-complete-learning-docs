---
title: ARIA States and Properties
category: Accessibility
order: 3
---

# ARIA States and Properties

> **Quick Summary:** ARIA states and properties provide additional information about elements' current state, relationships, and behaviors to assistive technologies.

## Introduction

While ARIA roles define what an element is, ARIA states and properties describe its current condition and relationships.

**Key Difference:**
- **States:** Change frequently (aria-expanded, aria-checked)
- **Properties:** Rarely change (aria-label, aria-labelledby)

---

## Widget States

### aria-expanded

Indicates if a collapsible element is expanded or collapsed.

```html
<button aria-expanded="false" aria-controls="menu">
  Menu
</button>

<div id="menu" hidden>
  <a href="/">Home</a>
  <a href="/about">About</a>
</div>

<script>
button.addEventListener('click', () => {
  const isExpanded = button.getAttribute('aria-expanded') === 'true';
  button.setAttribute('aria-expanded', !isExpanded);
  menu.hidden = isExpanded;
});
</script>
```

### aria-checked

For checkboxes and radio buttons (custom).

```html
<div role="checkbox" aria-checked="false" tabindex="0">
  Agree to terms
</div>

<!-- ✅ BETTER - Native checkbox -->
<label>
  <input type="checkbox"> Agree to terms
</label>
```

### aria-selected

For selectable items (tabs, list options).

```html
<div role="tablist">
  <button role="tab" aria-selected="true">Tab 1</button>
  <button role="tab" aria-selected="false">Tab 2</button>
</div>
```

### aria-disabled

```html
<button aria-disabled="true">Submit</button>

<!-- ✅ BETTER - Native disabled -->
<button disabled>Submit</button>
```

---

## Live Region Properties

### aria-live

Announces dynamic content changes.

```html
<!-- Polite: Waits for user to finish -->
<div aria-live="polite">
  Item added to cart
</div>

<!-- Assertive: Interrupts immediately -->
<div aria-live="assertive" role="alert">
  Error: Payment failed
</div>

<!-- Off: No announcement -->
<div aria-live="off">
  Silent update
</div>
```

### aria-atomic

Whether entire region is announced or just changes.

```html
<!-- Announce entire region -->
<div aria-live="polite" aria-atomic="true">
  <span>Items in cart:</span>
  <span id="count">3</span>
</div>
<!-- Announces: "Items in cart: 3" -->

<!-- Announce only changed part -->
<div aria-live="polite" aria-atomic="false">
  <span>Items in cart:</span>
  <span id="count">3</span>
</div>
<!-- Announces only: "3" -->
```

### aria-relevant

What changes should be announced.

```html
<div aria-live="polite" aria-relevant="additions removals">
  <p>Item 1</p>
  <p>Item 2</p>
</div>
```

Values:
- `additions` - New nodes added
- `removals` - Nodes removed
- `text` - Text changes
- `all` - All changes (default)

---

## Labeling Properties

### aria-label

Provides accessible name when visible label doesn't exist.

```html
<button aria-label="Close dialog">×</button>

<nav aria-label="Main navigation">
  <a href="/">Home</a>
</nav>
```

### aria-labelledby

References visible element(s) as label.

```html
<h2 id="dialog-title">Confirm Delete</h2>
<div role="dialog" aria-labelledby="dialog-title">
  <p>Are you sure?</p>
  <button>Delete</button>
</div>
```

### aria-describedby

Provides additional description.

```html
<label for="password">Password:</label>
<input type="password" id="password" aria-describedby="pwd-rules">
<div id="pwd-rules">
  Must be at least 8 characters with 1 number
</div>
```

---

## Relationship Properties

### aria-controls

Identifies elements controlled by this element.

```html
<button aria-expanded="false" aria-controls="dropdown-menu">
  Options
</button>
<ul id="dropdown-menu" hidden>
  <li>Option 1</li>
  <li>Option 2</li>
</ul>
```

### aria-owns

Establishes parent-child relationship when DOM structure doesn't.

```html
<div role="listbox" aria-owns="opt1 opt2">
  <div>Select an option:</div>
</div>

<!-- Options defined elsewhere in DOM -->
<div id="opt1" role="option">Option 1</div>
<div id="opt2" role="option">Option 2</div>
```

---

## Form Properties

### aria-required

Indicates required field.

```html
<label for="email">Email:</label>
<input type="email" id="email" aria-required="true">

<!-- ✅ BETTER - Native required -->
<input type="email" required>
```

### aria-invalid

Marks validation state.

```html
<input type="email" aria-invalid="true" aria-describedby="email-error">
<span id="email-error" role="alert">Invalid email format</span>
```

### aria-errormessage

Points to error message.

```html
<input type="email"
       aria-invalid="true"
       aria-errormessage="email-error">
<span id="email-error" role="alert">
  Please enter a valid email address
</span>
```

---

## Visibility Properties

### aria-hidden

Hides content from assistive tech.

```html
<!-- Decorative icon hidden from screen readers -->
<span aria-hidden="true">🎉</span>
<span class="sr-only">Celebration</span>

<!-- Icon font -->
<i class="icon-home" aria-hidden="true"></i>
<span class="sr-only">Home</span>
```

**Warning:** Never use `aria-hidden="true"` on focusable elements!

```html
<!-- ❌ WRONG - Button hidden but still focusable -->
<button aria-hidden="true">Click</button>

<!-- ✅ CORRECT - Hide and remove from tab order -->
<button hidden>Click</button>
```

---

## Best Practices

### 1. Update States Dynamically

```javascript
// ❌ BAD - Static state
<button aria-expanded="false">Menu</button>

// ✅ GOOD - JavaScript updates state
button.addEventListener('click', () => {
  const expanded = button.getAttribute('aria-expanded') === 'true';
  button.setAttribute('aria-expanded', !expanded);
});
```

### 2. Use aria-label Sparingly

```html
<!-- ❌ REDUNDANT - Label already visible -->
<button aria-label="Submit form">Submit</button>

<!-- ✅ GOOD - Label not visible -->
<button aria-label="Close">×</button>

<!-- ✅ BETTER - Use aria-labelledby when possible -->
<button aria-labelledby="button-text">
  <span id="button-text">Submit</span>
</button>
```

### 3. Prefer Native HTML

```html
<!-- ❌ ARIA overload -->
<div role="button" aria-label="Submit" tabindex="0">Submit</div>

<!-- ✅ Native -->
<button>Submit</button>
```

---

## Related Topics

- [ARIA Roles](aria-roles.md)
- [Form Accessibility](form-accessibility-detailed.md)
- [Screen Readers](screen-readers.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
