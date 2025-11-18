---
title: Keyboard Navigation
category: Accessibility
order: 5
---

# Keyboard Navigation

> **Quick Summary:** Keyboard accessibility ensures users who can't use a mouse can navigate and interact with websites using Tab, Enter, Arrow keys, and other keyboard controls.

## Why Keyboard Navigation Matters

**Users who rely on keyboards:**
- Motor disabilities (can't use mouse precisely)
- Blind users (screen readers use keyboard)
- Power users (keyboard is faster)

**Legal requirement:** WCAG 2.1 Success Criterion 2.1.1 (Level A) - All functionality must be keyboard accessible.

---

## Essential Keyboard Controls

| Key | Function |
|-----|----------|
| **Tab** | Move focus forward |
| **Shift + Tab** | Move focus backward |
| **Enter** | Activate links and buttons |
| **Space** | Activate buttons, check checkboxes |
| **Arrow keys** | Navigate within components (menus, tabs, radio groups) |
| **Escape** | Close dialogs, cancel actions |
| **Home/End** | Jump to first/last item |

---

## Tab Order

### Natural Tab Order

```html
<!-- Tab order: 1 → 2 → 3 -->
<input type="text" placeholder="Name">
<input type="email" placeholder="Email">
<button>Submit</button>
```

Tab order follows **DOM order**. No `tabindex` needed for standard HTML.

### Controlling Tab Order

```html
<!-- tabindex="0" - Add to tab order -->
<div tabindex="0" role="button">Custom Button</div>

<!-- tabindex="-1" - Remove from tab order but focusable via JS -->
<div tabindex="-1" id="error-message">Error text</div>

<!-- ❌ AVOID - Positive tabindex creates confusing order -->
<input tabindex="3">
<input tabindex="1"> <!-- Focused first! -->
<input tabindex="2">
```

**Best Practice:** Use `tabindex="0"` or `-1` only. Never use positive numbers.

---

## Focus Indicators

### Default Browser Focus

```html
<button>I show a focus ring when tabbed to</button>
```

### Custom Focus Styles

```css
/* ❌ BAD - Removes focus indicator */
button:focus {
  outline: none; /* Never do this without alternative */
}

/* ✅ GOOD - Custom accessible focus */
button:focus {
  outline: 3px solid #4A90E2;
  outline-offset: 2px;
}

/* ✅ BETTER - Use :focus-visible (modern browsers) */
button:focus-visible {
  outline: 3px solid #4A90E2;
  outline-offset: 2px;
}
```

**WCAG Requirement:** Focus indicator must have **3:1 contrast ratio** with background.

---

## Skip Links

Allow keyboard users to skip repetitive content.

```html
<body>
  <!-- Skip link (hidden until focused) -->
  <a href="#main-content" class="skip-link">Skip to main content</a>

  <header>
    <nav>
      <!-- Long navigation... -->
    </nav>
  </header>

  <main id="main-content">
    <h1>Page Content</h1>
  </main>
</body>

<style>
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: #000;
  color: #fff;
  padding: 8px;
  z-index: 100;
}

.skip-link:focus {
  top: 0;
}
</style>
```

---

## Interactive Components

### Buttons

```html
<!-- ✅ Native button - keyboard works automatically -->
<button onclick="submit()">Submit</button>

<!-- ❌ Custom button - needs tabindex + key handlers -->
<div tabindex="0" role="button"
     onclick="submit()"
     onkeydown="if(event.key==='Enter' || event.key===' ')submit()">
  Submit
</div>
```

### Dropdown Menu

```html
<button aria-expanded="false" aria-controls="menu">
  Menu
</button>

<ul id="menu" role="menu" hidden>
  <li role="menuitem"><a href="/">Home</a></li>
  <li role="menuitem"><a href="/about">About</a></li>
</ul>

<script>
// Arrow key navigation
menu.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowDown') {
    // Focus next item
  } else if (e.key === 'ArrowUp') {
    // Focus previous item
  } else if (e.key === 'Escape') {
    // Close menu
  }
});
</script>
```

### Modal Dialogs

```html
<div role="dialog" aria-labelledby="dialog-title" aria-modal="true">
  <h2 id="dialog-title">Confirm</h2>
  <p>Are you sure?</p>
  <button id="confirm">Yes</button>
  <button id="cancel">No</button>
</div>

<script>
// Focus trap - keep focus inside dialog
dialog.addEventListener('keydown', (e) => {
  if (e.key === 'Tab') {
    const focusable = dialog.querySelectorAll('button, [href], input');
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

  if (e.key === 'Escape') {
    closeDialog();
  }
});
</script>
```

---

## Testing Keyboard Accessibility

### Manual Testing Checklist

1. **Unplug your mouse**
2. **Tab through the entire page**
   - Can you reach all interactive elements?
   - Is focus order logical?
   - Are focus indicators visible?
3. **Activate elements with Enter/Space**
   - Do buttons work?
   - Do links navigate?
4. **Test custom widgets**
   - Dropdowns, modals, tabs, carousels
   - Arrow keys, Escape, Home/End
5. **Check focus trapping**
   - Can you exit modals?
   - Can you escape infinite loops?

---

## Common Mistakes

### 1. JavaScript Click Handlers on Divs

```html
<!-- ❌ BAD - Not keyboard accessible -->
<div onclick="doSomething()">Click me</div>

<!-- ✅ GOOD - Use button -->
<button onclick="doSomething()">Click me</button>
```

### 2. CSS `pointer-events: none`

```css
/* ❌ DANGEROUS - Disables keyboard focus -->
.overlay {
  pointer-events: none; /* Breaks keyboard and mouse */
}
```

### 3. Positive Tabindex

```html
<!-- ❌ CONFUSING - Breaks natural tab order -->
<input tabindex="5">
<input tabindex="1"> <!-- Focused first -->
<input tabindex="3">
```

---

## Best Practices

1. **Use semantic HTML** - Buttons, links, forms have built-in keyboard support
2. **Visible focus indicators** - Never remove `:focus` outline without replacement
3. **Logical tab order** - Follow visual flow (left-to-right, top-to-bottom)
4. **Skip links** - For pages with long navigation
5. **Focus management** - Move focus after deleting items, opening modals
6. **Test without mouse** - Actually try using your site with keyboard only

---

## Related Topics

- [Screen Readers](screen-readers.md)
- [ARIA Roles](aria-roles.md)
- [Form Accessibility](form-accessibility-detailed.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
