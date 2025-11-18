---
title: Data Attributes
category: Global Attributes
order: 18
---

# Data Attributes

> **Quick Summary:** Data attributes (`data-*`) allow you to store custom data directly on HTML elements without using non-standard attributes or JavaScript variables. They're perfect for passing data from HTML to JavaScript, storing configuration, state management, and creating clean, semantic markup.

## Table of Contents
- [Introduction](#introduction)
- [Basic Syntax](#basic-syntax)
- [Accessing Data Attributes](#accessing-data-attributes)
- [Use Cases](#use-cases)
- [Dataset API](#dataset-api)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Data attributes (introduced in HTML5) let you attach custom data to HTML elements using the `data-*` prefix. They provide a standardized way to store extra information without cluttering your HTML with non-semantic attributes or global JavaScript variables.

**Key points:**
- Must start with `data-` prefix
- Can contain any lowercase alphanumeric characters and hyphens
- Accessible via JavaScript `dataset` property
- Invisible to users (not displayed on page)
- Valid HTML5 (unlike custom attributes)

**Key Concept:** Data attributes are like sticky notes on your HTML elements—they store extra information that JavaScript can read later, without affecting how the page looks or using non-standard attributes.

---

## Basic Syntax

### HTML Syntax

```html
<element data-attribute-name="value">Content</element>
```

**Rules:**
- Must start with `data-`
- Followed by at least one character
- Lowercase letters only (hyphens allowed)
- No uppercase letters or underscores in HTML
- Value can be any string

### Valid Examples

```html
<!-- GOOD: Valid data attributes -->
<div data-user-id="12345">User Card</div>
<button data-action="delete">Delete</button>
<article data-category="technology" data-author="john-doe">Article</article>
<img data-src-large="image-large.jpg" src="image-small.jpg" alt="Image">
```

### Invalid Examples

```html
<!-- WRONG: No 'data-' prefix -->
<div user-id="12345">User Card</div>

<!-- WRONG: Uppercase letters -->
<div data-userId="12345">User Card</div>

<!-- WRONG: Starts with number after 'data-' -->
<div data-123="value">Content</div>

<!-- WRONG: Contains underscore in HTML (use hyphens) -->
<div data-user_id="12345">User Card</div>
```

---

## Accessing Data Attributes

### JavaScript: dataset API (Recommended)

```javascript
const element = document.getElementById('my-element');

// Read data attribute
const userId = element.dataset.userId;  // Reads data-user-id

// Set data attribute
element.dataset.userId = '67890';  // Sets data-user-id="67890"

// Delete data attribute
delete element.dataset.userId;  // Removes data-user-id
```

**Note:** Hyphen-case in HTML becomes camelCase in JavaScript:
- HTML: `data-user-id` → JavaScript: `dataset.userId`
- HTML: `data-product-name` → JavaScript: `dataset.productName`

### JavaScript: getAttribute() (Legacy)

```javascript
const element = document.getElementById('my-element');

// Read data attribute
const userId = element.getAttribute('data-user-id');

// Set data attribute
element.setAttribute('data-user-id', '67890');

// Remove data attribute
element.removeAttribute('data-user-id');
```

### CSS: attr() Function

```html
<div class="tooltip" data-tooltip-text="This is a tooltip">
  Hover me
</div>

<style>
.tooltip::after {
  content: attr(data-tooltip-text);
  position: absolute;
  background: black;
  color: white;
  padding: 5px;
  border-radius: 4px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip:hover::after {
  opacity: 1;
}
</style>
```

---

## Use Cases

### 1. Passing Data from Server to JavaScript

```html
<!-- Server renders user data -->
<div id="user-profile"
     data-user-id="12345"
     data-username="johndoe"
     data-email="john@example.com"
     data-role="admin">
  <h2>User Profile</h2>
</div>

<script>
const profile = document.getElementById('user-profile');

// Access user data
const userData = {
  id: profile.dataset.userId,
  username: profile.dataset.username,
  email: profile.dataset.email,
  role: profile.dataset.role
};

console.log(userData);
// { id: "12345", username: "johndoe", email: "john@example.com", role: "admin" }
</script>
```

### 2. Component Configuration

```html
<div class="carousel"
     data-auto-play="true"
     data-interval="3000"
     data-transition="fade">
  <div class="carousel-item">Slide 1</div>
  <div class="carousel-item">Slide 2</div>
  <div class="carousel-item">Slide 3</div>
</div>

<script>
function initCarousel(element) {
  const config = {
    autoPlay: element.dataset.autoPlay === 'true',
    interval: parseInt(element.dataset.interval),
    transition: element.dataset.transition
  };

  console.log(config);
  // { autoPlay: true, interval: 3000, transition: "fade" }

  // Initialize carousel with config...
}

const carousel = document.querySelector('.carousel');
initCarousel(carousel);
</script>
```

### 3. State Management

```html
<button class="toggle-btn" data-state="off">
  Toggle
</button>

<script>
const button = document.querySelector('.toggle-btn');

button.addEventListener('click', function() {
  // Toggle state
  const currentState = this.dataset.state;
  const newState = currentState === 'off' ? 'on' : 'off';

  this.dataset.state = newState;
  this.textContent = `State: ${newState}`;
});
</script>

<style>
/* Style based on state */
.toggle-btn[data-state="on"] {
  background: green;
  color: white;
}

.toggle-btn[data-state="off"] {
  background: red;
  color: white;
}
</style>
```

### 4. Storing Metadata for Event Handlers

```html
<div class="product-grid">
  <button class="add-to-cart"
          data-product-id="101"
          data-product-name="Wireless Headphones"
          data-price="99.99">
    Add to Cart
  </button>

  <button class="add-to-cart"
          data-product-id="102"
          data-product-name="Smart Watch"
          data-price="199.99">
    Add to Cart
  </button>

  <button class="add-to-cart"
          data-product-id="103"
          data-product-name="Laptop Stand"
          data-price="49.99">
    Add to Cart
  </button>
</div>

<script>
const buttons = document.querySelectorAll('.add-to-cart');

buttons.forEach(button => {
  button.addEventListener('click', function() {
    const product = {
      id: this.dataset.productId,
      name: this.dataset.productName,
      price: parseFloat(this.dataset.price)
    };

    console.log('Adding to cart:', product);
    // { id: "101", name: "Wireless Headphones", price: 99.99 }
  });
});
</script>
```

### 5. Lazy Loading Images

```html
<img class="lazy"
     data-src="image-full.jpg"
     src="placeholder.jpg"
     alt="Product Image">

<script>
const lazyImages = document.querySelectorAll('.lazy');

const imageObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;

      // Replace src with data-src when visible
      img.src = img.dataset.src;
      img.classList.remove('lazy');

      observer.unobserve(img);
    }
  });
});

lazyImages.forEach(img => imageObserver.observe(img));
</script>
```

### 6. Form Validation Rules

```html
<form>
  <input type="text"
         name="username"
         data-required="true"
         data-min-length="3"
         data-max-length="20">

  <input type="email"
         name="email"
         data-required="true"
         data-validation="email">

  <input type="password"
         name="password"
         data-required="true"
         data-min-length="8"
         data-pattern="^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)">
</form>

<script>
function validateInput(input) {
  const rules = {
    required: input.dataset.required === 'true',
    minLength: parseInt(input.dataset.minLength) || 0,
    maxLength: parseInt(input.dataset.maxLength) || Infinity,
    pattern: input.dataset.pattern,
    validation: input.dataset.validation
  };

  // Validate based on rules...
  console.log('Validation rules for', input.name, ':', rules);
}
</script>
```

---

## Dataset API

### Reading Data

```javascript
const element = document.getElementById('my-element');

// Single attribute
const value = element.dataset.userId;  // data-user-id

// Multiple attributes
const { userId, userName, userEmail } = element.dataset;
```

### Writing Data

```javascript
const element = document.getElementById('my-element');

// Set single attribute
element.dataset.userId = '12345';  // Sets data-user-id="12345"

// Set multiple attributes
element.dataset.userName = 'John Doe';
element.dataset.userEmail = 'john@example.com';
```

### Checking if Attribute Exists

```javascript
const element = document.getElementById('my-element');

// Check if data attribute exists
if ('userId' in element.dataset) {
  console.log('User ID exists');
}

// Alternative
if (element.dataset.userId !== undefined) {
  console.log('User ID exists');
}
```

### Deleting Data

```javascript
const element = document.getElementById('my-element');

// Delete data attribute
delete element.dataset.userId;  // Removes data-user-id
```

### Iterating Over All Data Attributes

```javascript
const element = document.getElementById('my-element');

// Loop through all data attributes
for (let key in element.dataset) {
  console.log(key, '=', element.dataset[key]);
}

// Using Object.entries()
Object.entries(element.dataset).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

---

## Examples

### Example 1: Interactive Tabs

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tabs with Data Attributes</title>
  <style>
    .tabs {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }

    .tab-button {
      padding: 10px 20px;
      border: 1px solid #ddd;
      background: white;
      cursor: pointer;
    }

    .tab-button[data-active="true"] {
      background: #007bff;
      color: white;
      border-color: #007bff;
    }

    .tab-content {
      display: none;
      padding: 20px;
      border: 1px solid #ddd;
    }

    .tab-content[data-active="true"] {
      display: block;
    }
  </style>
</head>
<body>
  <div class="tabs">
    <button class="tab-button" data-tab="home" data-active="true">Home</button>
    <button class="tab-button" data-tab="about">About</button>
    <button class="tab-button" data-tab="contact">Contact</button>
  </div>

  <div class="tab-content" data-tab="home" data-active="true">
    <h2>Home</h2>
    <p>Welcome to the home page.</p>
  </div>

  <div class="tab-content" data-tab="about">
    <h2>About</h2>
    <p>Learn more about us.</p>
  </div>

  <div class="tab-content" data-tab="contact">
    <h2>Contact</h2>
    <p>Get in touch with us.</p>
  </div>

  <script>
    const buttons = document.querySelectorAll('.tab-button');
    const contents = document.querySelectorAll('.tab-content');

    buttons.forEach(button => {
      button.addEventListener('click', function() {
        const targetTab = this.dataset.tab;

        // Deactivate all tabs
        buttons.forEach(btn => btn.dataset.active = 'false');
        contents.forEach(content => content.dataset.active = 'false');

        // Activate clicked tab
        this.dataset.active = 'true';

        // Show corresponding content
        const targetContent = document.querySelector(`.tab-content[data-tab="${targetTab}"]`);
        targetContent.dataset.active = 'true';
      });
    });
  </script>
</body>
</html>
```

### Example 2: Sortable Table

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Sortable Table</title>
  <style>
    table {
      border-collapse: collapse;
      width: 100%;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 12px;
      text-align: left;
    }

    th {
      background: #f2f2f2;
      cursor: pointer;
      user-select: none;
    }

    th:hover {
      background: #e0e0e0;
    }

    th[data-sort-order="asc"]::after {
      content: " ▲";
    }

    th[data-sort-order="desc"]::after {
      content: " ▼";
    }
  </style>
</head>
<body>
  <table>
    <thead>
      <tr>
        <th data-sort="name">Name</th>
        <th data-sort="age" data-type="number">Age</th>
        <th data-sort="email">Email</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>John Doe</td>
        <td>32</td>
        <td>john@example.com</td>
      </tr>
      <tr>
        <td>Jane Smith</td>
        <td>28</td>
        <td>jane@example.com</td>
      </tr>
      <tr>
        <td>Bob Johnson</td>
        <td>45</td>
        <td>bob@example.com</td>
      </tr>
    </tbody>
  </table>

  <script>
    const headers = document.querySelectorAll('th[data-sort]');

    headers.forEach(header => {
      header.addEventListener('click', function() {
        const column = this.dataset.sort;
        const type = this.dataset.type || 'string';
        const currentOrder = this.dataset.sortOrder || 'none';
        const newOrder = currentOrder === 'asc' ? 'desc' : 'asc';

        // Clear all sort indicators
        headers.forEach(h => delete h.dataset.sortOrder);

        // Set new sort order
        this.dataset.sortOrder = newOrder;

        // Sort table rows
        sortTable(column, newOrder, type);
      });
    });

    function sortTable(column, order, type) {
      const tbody = document.querySelector('tbody');
      const rows = Array.from(tbody.querySelectorAll('tr'));
      const columnIndex = Array.from(document.querySelectorAll('th')).findIndex(
        th => th.dataset.sort === column
      );

      rows.sort((a, b) => {
        let aValue = a.cells[columnIndex].textContent;
        let bValue = b.cells[columnIndex].textContent;

        if (type === 'number') {
          aValue = parseFloat(aValue);
          bValue = parseFloat(bValue);
        }

        if (order === 'asc') {
          return aValue > bValue ? 1 : -1;
        } else {
          return aValue < bValue ? 1 : -1;
        }
      });

      // Re-append sorted rows
      rows.forEach(row => tbody.appendChild(row));
    }
  </script>
</body>
</html>
```

### Example 3: Modal with Data Attributes

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Modal with Data Attributes</title>
  <style>
    .modal {
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

    .modal[data-visible="true"] {
      display: flex;
    }

    .modal-content {
      background: white;
      padding: 40px;
      border-radius: 8px;
      max-width: 500px;
    }
  </style>
</head>
<body>
  <button data-modal-trigger="modal1">Open Modal 1</button>
  <button data-modal-trigger="modal2">Open Modal 2</button>

  <div class="modal" data-modal-id="modal1">
    <div class="modal-content">
      <h2>Modal 1</h2>
      <p>This is the first modal.</p>
      <button data-modal-close="modal1">Close</button>
    </div>
  </div>

  <div class="modal" data-modal-id="modal2">
    <div class="modal-content">
      <h2>Modal 2</h2>
      <p>This is the second modal.</p>
      <button data-modal-close="modal2">Close</button>
    </div>
  </div>

  <script>
    // Open modal
    const triggers = document.querySelectorAll('[data-modal-trigger]');
    triggers.forEach(trigger => {
      trigger.addEventListener('click', function() {
        const modalId = this.dataset.modalTrigger;
        const modal = document.querySelector(`[data-modal-id="${modalId}"]`);
        modal.dataset.visible = 'true';
      });
    });

    // Close modal
    const closeButtons = document.querySelectorAll('[data-modal-close]');
    closeButtons.forEach(button => {
      button.addEventListener('click', function() {
        const modalId = this.dataset.modalClose;
        const modal = document.querySelector(`[data-modal-id="${modalId}"]`);
        modal.dataset.visible = 'false';
      });
    });

    // Close modal on background click
    const modals = document.querySelectorAll('.modal');
    modals.forEach(modal => {
      modal.addEventListener('click', function(e) {
        if (e.target === this) {
          this.dataset.visible = 'false';
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

1. **Use for Configuration and Metadata**
   ```html
   <!-- GOOD: Store component config -->
   <div class="slider" data-speed="500" data-auto-play="true">
     Slider content
   </div>
   ```

2. **Use Semantic Names**
   ```html
   <!-- GOOD: Descriptive names -->
   <button data-product-id="123" data-action="add-to-cart">Add to Cart</button>

   <!-- BAD: Generic names -->
   <button data-id="123" data-type="1">Add to Cart</button>
   ```

3. **Use dataset API in JavaScript**
   ```javascript
   // GOOD: dataset API (cleaner)
   const userId = element.dataset.userId;

   // OK: getAttribute (legacy)
   const userId = element.getAttribute('data-user-id');
   ```

4. **Store Simple Values, Not Complex Objects**
   ```html
   <!-- GOOD: Simple values -->
   <div data-user-id="123" data-username="john">User</div>

   <!-- AVOID: JSON in data attributes (use script tag instead) -->
   <div data-user='{"id":123,"name":"john","email":"..."}'>User</div>
   ```

### Avoid This

1. **Don't Store Sensitive Data**
   ```html
   <!-- WRONG: Sensitive data visible in HTML -->
   <div data-password="secret123" data-credit-card="1234-5678">User</div>

   <!-- CORRECT: Don't expose sensitive data -->
   <div data-user-id="123">User</div>
   ```

2. **Don't Use for Large Data**
   ```html
   <!-- WRONG: Large dataset in HTML -->
   <div data-products="[{...100 products...}]">Products</div>

   <!-- CORRECT: Use script tag or fetch from API -->
   <script type="application/json" id="products-data">
     [...products...]
   </script>
   ```

3. **Don't Use Instead of Semantic HTML**
   ```html
   <!-- WRONG: Using data attributes to fake semantics -->
   <div data-heading="true">This is a heading</div>

   <!-- CORRECT: Use proper semantic element -->
   <h2>This is a heading</h2>
   ```

---

## Quick Reference

### Syntax

```html
<!-- Single data attribute -->
<element data-attribute-name="value"></element>

<!-- Multiple data attributes -->
<element data-id="123" data-name="John" data-active="true"></element>
```

### JavaScript Access

```javascript
// Read
const value = element.dataset.attributeName;

// Write
element.dataset.attributeName = 'value';

// Delete
delete element.dataset.attributeName;

// Check existence
if ('attributeName' in element.dataset) { }
```

### CSS Access

```css
/* Attribute selector */
[data-status="active"] {
  background: green;
}

/* Content from attribute */
.element::before {
  content: attr(data-label);
}
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|----|
| `data-*` attributes | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `dataset` API | ✅ 8+ | ✅ 6+ | ✅ 5.1+ | ✅ All | ✅ 11+ |

---

## Related Topics
- [ID and Class Attributes](id-class.md)
- [Global Attributes](html5-attributes.md)
- [ARIA Attributes](aria-attributes.md)

---

**Last Updated:** November 17, 2025
**Category:** Global Attributes
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
