---
title: ARIA Roles
category: Accessibility
order: 2
---

# ARIA Roles

> **Quick Summary:** ARIA roles define what an element is or does, helping assistive technologies understand non-semantic elements like custom widgets and dynamic content.

## Introduction

ARIA (Accessible Rich Internet Applications) roles communicate the purpose of elements to assistive technologies when semantic HTML isn't sufficient.

**Key Concept:** Semantic HTML is preferred. Only use ARIA when native HTML elements can't achieve the needed semantics.

---

## Landmark Roles

Landmark roles identify regions of a page for screen reader navigation.

### Common Landmarks

```html
<header role="banner">Site Header</header>
<nav role="navigation">Main Navigation</nav>
<main role="main">Main Content</main>
<aside role="complementary">Sidebar</aside>
<footer role="contentinfo">Site Footer</footer>

<!-- Search landmark -->
<div role="search">
  <input type="search" aria-label="Search site">
</div>
```

**Note:** HTML5 semantic elements have implicit roles. Use explicit `role` only when needed for older browser support.

---

## Widget Roles

For custom interactive components.

### Button

```html
<div role="button" tabindex="0"
     onclick="handleClick()"
     onkeydown="if(event.key==='Enter')handleClick()">
  Click Me
</div>

<!-- ✅ BETTER - Use native button -->
<button onclick="handleClick()">Click Me</button>
```

### Tab Interface

```html
<div role="tablist" aria-label="Product Information">
  <button role="tab" aria-selected="true" aria-controls="panel1" id="tab1">
    Overview
  </button>
  <button role="tab" aria-selected="false" aria-controls="panel2" id="tab2">
    Specs
  </button>
</div>

<div role="tabpanel" id="panel1" aria-labelledby="tab1">
  <p>Product overview content...</p>
</div>

<div role="tabpanel" id="panel2" aria-labelledby="tab2" hidden>
  <p>Technical specifications...</p>
</div>
```

### Dialog (Modal)

```html
<div role="dialog" aria-labelledby="dialog-title" aria-modal="true">
  <h2 id="dialog-title">Confirm Action</h2>
  <p>Are you sure you want to delete this item?</p>
  <button>Confirm</button>
  <button>Cancel</button>
</div>
```

---

## Document Structure Roles

```html
<!-- Article -->
<div role="article">
  <h2>Blog Post Title</h2>
  <p>Content...</p>
</div>

<!-- Feed (social media style) -->
<div role="feed" aria-label="News Feed">
  <article role="article">Post 1</article>
  <article role="article">Post 2</article>
</div>

<!-- Region (generic landmark) -->
<section role="region" aria-labelledby="region-title">
  <h2 id="region-title">Related Articles</h2>
</section>
```

---

## Live Region Roles

For dynamic content updates.

```html
<!-- Alert (important message) -->
<div role="alert">
  Form submitted successfully!
</div>

<!-- Status (non-critical update) -->
<div role="status" aria-live="polite" aria-atomic="true">
  3 items in cart
</div>

<!-- Log (chat, console) -->
<div role="log" aria-live="polite" aria-atomic="false">
  <p>User joined: John</p>
  <p>User joined: Jane</p>
</div>

<!-- Timer -->
<div role="timer" aria-live="off" aria-atomic="true">
  <span>Time remaining: 5:00</span>
</div>
```

---

## Best Practices

### 1. Prefer Semantic HTML

```html
<!-- ❌ BAD -->
<div role="button">Submit</div>

<!-- ✅ GOOD -->
<button>Submit</button>
```

### 2. Don't Override Native Semantics

```html
<!-- ❌ WRONG - Contradicts native semantics -->
<button role="heading">Not a Button</button>

<!-- ✅ CORRECT -->
<button>Submit</button>
<h1>Heading</h1>
```

### 3. Use Roles with Required Attributes

```html
<!-- ❌ INCOMPLETE - tab needs aria-controls -->
<div role="tab">Tab</div>

<!-- ✅ COMPLETE -->
<div role="tab" aria-controls="panel1" aria-selected="true">Tab</div>
```

---

## Related Topics

- [ARIA States](aria-states.md)
- [Keyboard Navigation](keyboard-navigation.md)
- [Semantic HTML](semantic-accessibility.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
