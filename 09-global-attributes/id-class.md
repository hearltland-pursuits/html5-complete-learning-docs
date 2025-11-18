---
title: ID and Class Attributes
category: Global Attributes
order: 17
---

# ID and Class Attributes

> **Quick Summary:** The `id` and `class` attributes are the most commonly used global attributes for identifying and styling HTML elements. `id` must be unique per page (used for single elements, anchors, JavaScript targeting). `class` can be reused (used for styling groups of elements with CSS).

## Table of Contents
- [Introduction](#introduction)
- [ID Attribute](#id-attribute)
- [Class Attribute](#class-attribute)
- [ID vs Class](#id-vs-class)
- [Naming Conventions](#naming-conventions)
- [CSS Selectors](#css-selectors)
- [JavaScript Usage](#javascript-usage)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `id` and `class` attributes are global attributes available on all HTML elements. They serve as identifiers that connect HTML to CSS styling and JavaScript functionality.

**Key differences:**
- **`id`**: Unique identifier (one per page)
- **`class`**: Reusable identifier (many per page)

**Common uses:**
- **CSS styling**: Target elements for visual design
- **JavaScript**: Select and manipulate elements
- **Anchors**: Link to specific page sections (id only)
- **Form labels**: Associate labels with inputs (id only)

**Key Concept:** Think of `id` as a person's social security number (unique), and `class` as their job title (many people can have the same one). Use `id` for unique elements, `class` for groups.

---

## ID Attribute

### Syntax

```html
<element id="unique-identifier">Content</element>
```

### Rules

1. **Must be unique** - Only one element per page can have the same id
2. **Case-sensitive** - `id="Header"` ≠ `id="header"`
3. **No spaces** - Use hyphens or camelCase
4. **Start with letter** - Not a number or special character
5. **Valid characters** - Letters, numbers, hyphens, underscores

### Valid Examples

```html
<!-- GOOD: Valid id names -->
<div id="header">Header</div>
<div id="main-content">Content</div>
<div id="sidebar1">Sidebar</div>
<div id="contact_form">Form</div>
<div id="navBar">Navigation</div>
```

### Invalid Examples

```html
<!-- WRONG: Starts with number -->
<div id="1header">Header</div>

<!-- WRONG: Contains spaces -->
<div id="main content">Content</div>

<!-- WRONG: Contains special characters -->
<div id="header@site">Header</div>

<!-- WRONG: Duplicate id (same page) -->
<div id="content">Content 1</div>
<div id="content">Content 2</div> <!-- ❌ Duplicate! -->
```

### Use Cases

**1. Page Anchors (Jump Links)**
```html
<nav>
  <a href="#introduction">Introduction</a>
  <a href="#features">Features</a>
  <a href="#pricing">Pricing</a>
</nav>

<section id="introduction">
  <h2>Introduction</h2>
  <p>Content...</p>
</section>

<section id="features">
  <h2>Features</h2>
  <p>Content...</p>
</section>

<section id="pricing">
  <h2>Pricing</h2>
  <p>Content...</p>
</section>
```

**2. Form Label Association**
```html
<label for="email">Email:</label>
<input type="email" id="email" name="email">

<label for="password">Password:</label>
<input type="password" id="password" name="password">
```

**3. JavaScript Targeting**
```html
<button id="submit-btn">Submit</button>

<script>
document.getElementById('submit-btn').addEventListener('click', function() {
  alert('Button clicked!');
});
</script>
```

**4. CSS Styling (Unique Elements)**
```html
<header id="main-header">
  <h1>Site Title</h1>
</header>

<style>
#main-header {
  background: #333;
  color: white;
  padding: 20px;
}
</style>
```

---

## Class Attribute

### Syntax

```html
<element class="class-name">Content</element>

<!-- Multiple classes (space-separated) -->
<element class="class1 class2 class3">Content</element>
```

### Rules

1. **Can be reused** - Multiple elements can have the same class
2. **Case-sensitive** - `class="Card"` ≠ `class="card"`
3. **Multiple classes** - Space-separated list
4. **No spaces in names** - Use hyphens or camelCase
5. **Valid characters** - Same as id (letters, numbers, hyphens, underscores)

### Valid Examples

```html
<!-- GOOD: Single class -->
<div class="card">Card</div>

<!-- GOOD: Multiple classes -->
<div class="card featured large">Featured Card</div>

<!-- GOOD: Reusable (same class on multiple elements) -->
<article class="blog-post">Post 1</article>
<article class="blog-post">Post 2</article>
<article class="blog-post">Post 3</article>

<!-- GOOD: Hyphen-case -->
<button class="btn-primary">Click Me</button>

<!-- GOOD: camelCase -->
<button class="btnPrimary">Click Me</button>
```

### Invalid Examples

```html
<!-- WRONG: Spaces in class name (creates two classes) -->
<div class="card featured">...</div>
<!-- This actually has TWO classes: "card" and "featured" (which is valid) -->
<!-- Wrong would be trying to name a single class "card featured" -->

<!-- WRONG: Special characters -->
<div class="card@featured">...</div>
```

### Use Cases

**1. Styling Groups of Elements**
```html
<article class="card">
  <h3>Card Title 1</h3>
  <p>Content...</p>
</article>

<article class="card">
  <h3>Card Title 2</h3>
  <p>Content...</p>
</article>

<article class="card">
  <h3>Card Title 3</h3>
  <p>Content...</p>
</article>

<style>
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
}
</style>
```

**2. Modifier Classes (BEM Pattern)**
```html
<!-- Base button -->
<button class="btn">Default Button</button>

<!-- Button with modifiers -->
<button class="btn btn--primary">Primary Button</button>
<button class="btn btn--secondary">Secondary Button</button>
<button class="btn btn--large">Large Button</button>

<style>
.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn--primary {
  background: #007bff;
  color: white;
}

.btn--secondary {
  background: #6c757d;
  color: white;
}

.btn--large {
  padding: 15px 30px;
  font-size: 18px;
}
</style>
```

**3. State Classes (JavaScript)**
```html
<div class="modal hidden">
  <p>Modal content</p>
</div>

<style>
.modal {
  display: block;
}

.modal.hidden {
  display: none;
}
</style>

<script>
// Toggle modal visibility
const modal = document.querySelector('.modal');
modal.classList.toggle('hidden');
</script>
```

---

## ID vs Class

### When to Use ID

✅ **Use `id` when:**
- Element is unique on the page (e.g., main header, footer)
- Creating page anchors/jump links
- Associating form labels with inputs
- Targeting specific element with JavaScript
- CSS specificity override (rarely needed)

### When to Use Class

✅ **Use `class` when:**
- Styling groups of elements (e.g., all cards, all buttons)
- Element may appear multiple times
- Applying multiple styles to one element
- Following CSS methodologies (BEM, SMACSS)
- General styling and reusability

### Comparison Table

| Feature | ID | Class |
|---------|----|----|
| **Uniqueness** | One per page | Many per page |
| **Reusability** | Not reusable | Fully reusable |
| **Multiple per element** | One id only | Multiple classes (space-separated) |
| **CSS Selector** | `#id-name` | `.class-name` |
| **CSS Specificity** | High (0,1,0,0) | Low (0,0,1,0) |
| **JavaScript** | `getElementById()` | `getElementsByClassName()`, `querySelectorAll()` |
| **Anchors** | ✅ Yes (`href="#id"`) | ❌ No |
| **Form Labels** | ✅ Yes (`for="id"`) | ❌ No |

---

## Naming Conventions

### Common Patterns

**1. Hyphen-case (kebab-case) - Recommended**
```html
<div class="main-content">Content</div>
<div id="user-profile">Profile</div>
<button class="btn-primary">Button</button>
```

**2. camelCase**
```html
<div class="mainContent">Content</div>
<div id="userProfile">Profile</div>
<button class="btnPrimary">Button</button>
```

**3. snake_case**
```html
<div class="main_content">Content</div>
<div id="user_profile">Profile</div>
<button class="btn_primary">Button</button>
```

**4. BEM (Block Element Modifier)**
```html
<!-- Block -->
<div class="card">
  <!-- Element -->
  <h3 class="card__title">Title</h3>
  <p class="card__body">Body</p>

  <!-- Modifier -->
  <div class="card card--featured">
    <h3 class="card__title">Featured</h3>
  </div>
</div>
```

### Semantic Naming

**Good (Describes purpose):**
```html
<button class="btn-submit">Submit</button>
<div class="user-profile">Profile</div>
<article class="blog-post">Post</article>
<section class="pricing-table">Pricing</section>
```

**Bad (Describes appearance):**
```html
<button class="blue-button">Submit</button>
<div class="big-box">Profile</div>
<article class="white-card">Post</article>
<section class="left-column">Pricing</section>
```

**Why?** If design changes (blue → green), semantic names remain valid.

---

## CSS Selectors

### ID Selector

```css
/* ID selector (use #) */
#header {
  background: #333;
  color: white;
}

#main-content {
  max-width: 1200px;
  margin: 0 auto;
}
```

### Class Selector

```css
/* Class selector (use .) */
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
}

.btn {
  padding: 10px 20px;
  border: none;
  cursor: pointer;
}
```

### Combining Selectors

```css
/* Element with specific class */
button.btn-primary {
  background: #007bff;
  color: white;
}

/* Multiple classes (both required) */
.card.featured {
  border: 2px solid gold;
}

/* Element with id and class */
#header.sticky {
  position: fixed;
  top: 0;
}

/* Descendant selector */
.card .title {
  font-size: 24px;
}

#sidebar .nav-link {
  color: #333;
}
```

---

## JavaScript Usage

### Selecting by ID

```javascript
// Get element by ID
const header = document.getElementById('main-header');

// Modify content
header.textContent = 'New Header Text';

// Add event listener
const button = document.getElementById('submit-btn');
button.addEventListener('click', function() {
  console.log('Button clicked!');
});
```

### Selecting by Class

```javascript
// Get all elements with class (HTMLCollection)
const cards = document.getElementsByClassName('card');

// Loop through elements
for (let i = 0; i < cards.length; i++) {
  cards[i].style.border = '1px solid red';
}

// Modern approach (NodeList)
const buttons = document.querySelectorAll('.btn');
buttons.forEach(button => {
  button.addEventListener('click', function() {
    console.log('Button clicked!');
  });
});
```

### Adding/Removing Classes

```javascript
const element = document.getElementById('my-element');

// Add class
element.classList.add('active');

// Remove class
element.classList.remove('hidden');

// Toggle class
element.classList.toggle('open');

// Check if has class
if (element.classList.contains('active')) {
  console.log('Element is active');
}

// Replace class
element.classList.replace('btn-primary', 'btn-secondary');
```

---

## Examples

### Example 1: Blog Post Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Blog Post</title>
  <style>
    /* ID for unique header */
    #site-header {
      background: #333;
      color: white;
      padding: 20px;
      text-align: center;
    }

    /* Class for reusable blog posts */
    .blog-post {
      max-width: 800px;
      margin: 40px auto;
      padding: 20px;
      border: 1px solid #ddd;
      border-radius: 8px;
    }

    .blog-post__title {
      font-size: 32px;
      margin-bottom: 10px;
    }

    .blog-post__meta {
      color: #666;
      font-size: 14px;
      margin-bottom: 20px;
    }

    .blog-post__content {
      line-height: 1.6;
    }

    /* Multiple posts use same class */
    .featured {
      border: 2px solid gold;
      background: #fffbe6;
    }
  </style>
</head>
<body>
  <!-- Unique header (id) -->
  <header id="site-header">
    <h1>Tech Blog</h1>
  </header>

  <main>
    <!-- Featured post (class + modifier) -->
    <article class="blog-post featured">
      <h2 class="blog-post__title">10 SEO Strategies for 2025</h2>
      <p class="blog-post__meta">By John Doe | Nov 17, 2025</p>
      <div class="blog-post__content">
        <p>Content...</p>
      </div>
    </article>

    <!-- Regular posts (reusable class) -->
    <article class="blog-post">
      <h2 class="blog-post__title">Understanding HTML5</h2>
      <p class="blog-post__meta">By Jane Smith | Nov 16, 2025</p>
      <div class="blog-post__content">
        <p>Content...</p>
      </div>
    </article>

    <article class="blog-post">
      <h2 class="blog-post__title">CSS Grid Layout</h2>
      <p class="blog-post__meta">By Bob Johnson | Nov 15, 2025</p>
      <div class="blog-post__content">
        <p>Content...</p>
      </div>
    </article>
  </main>
</body>
</html>
```

### Example 2: Navigation with Anchors

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Single Page Site</title>
  <style>
    /* Unique sticky nav (id) */
    #main-nav {
      position: fixed;
      top: 0;
      width: 100%;
      background: #333;
      padding: 10px 0;
    }

    /* Reusable nav link style (class) */
    .nav-link {
      color: white;
      text-decoration: none;
      margin: 0 15px;
    }

    .nav-link:hover {
      text-decoration: underline;
    }

    /* Sections with unique ids (for anchors) */
    section {
      min-height: 100vh;
      padding: 80px 20px 20px;
    }
  </style>
</head>
<body>
  <!-- Unique navigation (id) -->
  <nav id="main-nav">
    <a href="#about" class="nav-link">About</a>
    <a href="#services" class="nav-link">Services</a>
    <a href="#portfolio" class="nav-link">Portfolio</a>
    <a href="#contact" class="nav-link">Contact</a>
  </nav>

  <!-- Sections with unique ids (anchors) -->
  <section id="about">
    <h2>About Us</h2>
    <p>Content...</p>
  </section>

  <section id="services">
    <h2>Our Services</h2>
    <p>Content...</p>
  </section>

  <section id="portfolio">
    <h2>Portfolio</h2>
    <p>Content...</p>
  </section>

  <section id="contact">
    <h2>Contact</h2>
    <p>Content...</p>
  </section>
</body>
</html>
```

### Example 3: Interactive Component with JavaScript

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Modal Demo</title>
  <style>
    /* Unique modal container (id) */
    #modal-overlay {
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

    /* Show state (class) */
    #modal-overlay.active {
      display: flex;
    }

    /* Modal content (class) */
    .modal-content {
      background: white;
      padding: 40px;
      border-radius: 8px;
      max-width: 500px;
    }

    /* Reusable button styles (class) */
    .btn {
      padding: 10px 20px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }

    .btn-primary {
      background: #007bff;
      color: white;
    }

    .btn-secondary {
      background: #6c757d;
      color: white;
    }
  </style>
</head>
<body>
  <button id="open-modal-btn" class="btn btn-primary">Open Modal</button>

  <div id="modal-overlay">
    <div class="modal-content">
      <h2>Modal Title</h2>
      <p>Modal content goes here...</p>
      <button id="close-modal-btn" class="btn btn-secondary">Close</button>
    </div>
  </div>

  <script>
    const openBtn = document.getElementById('open-modal-btn');
    const closeBtn = document.getElementById('close-modal-btn');
    const modal = document.getElementById('modal-overlay');

    openBtn.addEventListener('click', function() {
      modal.classList.add('active');
    });

    closeBtn.addEventListener('click', function() {
      modal.classList.remove('active');
    });

    // Close modal when clicking outside content
    modal.addEventListener('click', function(e) {
      if (e.target === modal) {
        modal.classList.remove('active');
      }
    });
  </script>
</body>
</html>
```

---

## Best Practices

### Do This

1. **Use Semantic Class Names**
   ```html
   <!-- GOOD: Describes purpose -->
   <button class="submit-button">Submit</button>
   <div class="user-profile">Profile</div>

   <!-- BAD: Describes appearance -->
   <button class="blue-btn">Submit</button>
   <div class="big-box">Profile</div>
   ```

2. **Keep IDs Unique**
   ```html
   <!-- GOOD: One id per page -->
   <header id="main-header">Header</header>
   <footer id="main-footer">Footer</footer>

   <!-- WRONG: Duplicate ids -->
   <div id="content">Content 1</div>
   <div id="content">Content 2</div> <!-- ❌ -->
   ```

3. **Use Classes for Styling, ID for Functionality**
   ```html
   <!-- GOOD: Class for styling, id for JS/anchors -->
   <button id="submit-btn" class="btn btn-primary">Submit</button>
   ```

4. **Use BEM or Consistent Naming**
   ```html
   <!-- BEM pattern -->
   <div class="card">
     <h3 class="card__title">Title</h3>
     <p class="card__body">Body</p>
     <button class="card__button card__button--primary">Click</button>
   </div>
   ```

### Avoid This

1. **Don't Use ID for Styling (When Class Works)**
   ```html
   <!-- AVOID: ID for styling reusable elements -->
   <style>
   #card1 { border: 1px solid #ddd; }
   #card2 { border: 1px solid #ddd; }
   #card3 { border: 1px solid #ddd; }
   </style>

   <!-- BETTER: Class for reusable styling -->
   <style>
   .card { border: 1px solid #ddd; }
   </style>
   ```

2. **Don't Overuse IDs**
   ```html
   <!-- WRONG: Too many unique IDs -->
   <div id="container">
     <div id="row">
       <div id="column1">Content</div>
       <div id="column2">Content</div>
     </div>
   </div>

   <!-- BETTER: Use classes -->
   <div class="container">
     <div class="row">
       <div class="column">Content</div>
       <div class="column">Content</div>
     </div>
   </div>
   ```

3. **Don't Use Non-Semantic Names**
   ```html
   <!-- WRONG: Non-descriptive -->
   <div class="box1">Content</div>
   <div class="thing">Content</div>
   <div class="stuff">Content</div>

   <!-- CORRECT: Descriptive -->
   <div class="sidebar">Content</div>
   <div class="user-card">Content</div>
   <div class="pricing-table">Content</div>
   ```

---

## Quick Reference

### Syntax

```html
<!-- ID (unique) -->
<element id="unique-name"></element>

<!-- Class (reusable) -->
<element class="class-name"></element>

<!-- Multiple classes -->
<element class="class1 class2 class3"></element>

<!-- ID and classes together -->
<element id="unique-id" class="class1 class2"></element>
```

### CSS Selectors

```css
/* ID selector */
#unique-id { }

/* Class selector */
.class-name { }

/* Multiple classes (both required) */
.class1.class2 { }

/* Descendant selector */
#parent .child { }
.parent .child { }
```

### JavaScript Selection

```javascript
// By ID
document.getElementById('id-name');

// By class
document.getElementsByClassName('class-name');
document.querySelectorAll('.class-name');

// Manipulate classes
element.classList.add('class-name');
element.classList.remove('class-name');
element.classList.toggle('class-name');
element.classList.contains('class-name');
```

---

## Browser Support

The `id` and `class` attributes are supported in all browsers:

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| `id` attribute | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `class` attribute | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `classList` API | ✅ 8+ | ✅ 3.6+ | ✅ 5.1+ | ✅ All | ✅ 10+ |

---

## Related Topics
- [Data Attributes](data-attributes.md)
- [Global Attributes](html5-attributes.md)
- [ARIA Attributes](aria-attributes.md)

---

**Last Updated:** November 17, 2025
**Category:** Global Attributes
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
