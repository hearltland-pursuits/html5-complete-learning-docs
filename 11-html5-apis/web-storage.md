---
title: Web Storage API
category: HTML5 APIs
order: 32
---

# Web Storage API

> **Quick Summary:** Web Storage provides `localStorage` (persistent) and `sessionStorage` (tab-scoped) for storing key-value data in the browser. Simple, synchronous API for storing up to 5-10MB of string data. Essential for user preferences, shopping carts, and offline functionality.

## Table of Contents
- [Introduction](#introduction)
- [localStorage vs sessionStorage](#localstorage-vs-sessionstorage)
- [Basic Operations](#basic-operations)
- [Storage Events](#storage-events)
- [JSON Storage](#json-storage)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Web Storage provides two mechanisms for storing data locally:

**localStorage** - Persistent storage (survives browser restarts)
**sessionStorage** - Tab-scoped storage (cleared when tab closes)

**Key characteristics:**
- **Key-value pairs** - Stores strings only
- **Synchronous API** - Blocking operations
- **Storage limit** - 5-10MB per origin
- **Same-origin policy** - Isolated by domain

---

## localStorage vs sessionStorage

| Feature | localStorage | sessionStorage |
|---------|--------------|----------------|
| **Lifetime** | Permanent (until cleared) | Tab session only |
| **Scope** | All tabs/windows | Single tab |
| **Storage** | ~5-10MB | ~5-10MB |
| **Use case** | User preferences, offline data | Form data, temporary state |

---

## Basic Operations

### Set Item

```javascript
// localStorage
localStorage.setItem('username', 'JohnDoe');
localStorage.key = 'value'; // Alternative syntax

// sessionStorage
sessionStorage.setItem('temp', 'data');
```

### Get Item

```javascript
const username = localStorage.getItem('username');
// Returns: "JohnDoe" or null if not found
```

### Remove Item

```javascript
localStorage.removeItem('username');
```

### Clear All

```javascript
localStorage.clear(); // Removes ALL items
```

### Get Key by Index

```javascript
const key = localStorage.key(0); // First key
```

### Check Length

```javascript
const count = localStorage.length;
```

---

## Storage Events

Listen for storage changes from other tabs/windows:

```javascript
window.addEventListener('storage', function(e) {
  console.log('Key:', e.key);
  console.log('Old value:', e.oldValue);
  console.log('New value:', e.newValue);
  console.log('URL:', e.url);
});
```

**Note:** Storage event only fires in OTHER tabs, not the one making the change.

---

## JSON Storage

Storage only accepts strings. Use JSON for objects:

```javascript
// Store object
const user = { name: 'John', age: 30 };
localStorage.setItem('user', JSON.stringify(user));

// Retrieve object
const storedUser = JSON.parse(localStorage.getItem('user'));
console.log(storedUser.name); // "John"
```

---

## Examples

### Example 1: Dark Mode Toggle

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dark Mode</title>
  <style>
    body {
      transition: background 0.3s, color 0.3s;
    }

    body.dark {
      background: #1a1a1a;
      color: white;
    }

    button {
      padding: 10px 20px;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <h1>Dark Mode Demo</h1>
  <button id="toggle">Toggle Dark Mode</button>

  <script>
    const toggle = document.getElementById('toggle');

    // Load saved preference
    if (localStorage.getItem('darkMode') === 'enabled') {
      document.body.classList.add('dark');
    }

    toggle.addEventListener('click', function() {
      document.body.classList.toggle('dark');

      // Save preference
      if (document.body.classList.contains('dark')) {
        localStorage.setItem('darkMode', 'enabled');
      } else {
        localStorage.removeItem('darkMode');
      }
    });
  </script>
</body>
</html>
```

### Example 2: Shopping Cart

```javascript
// Add item to cart
function addToCart(product) {
  let cart = JSON.parse(localStorage.getItem('cart')) || [];
  cart.push(product);
  localStorage.setItem('cart', JSON.stringify(cart));
}

// Get cart
function getCart() {
  return JSON.parse(localStorage.getItem('cart')) || [];
}

// Clear cart
function clearCart() {
  localStorage.removeItem('cart');
}

// Usage
addToCart({ id: 1, name: 'Product A', price: 29.99 });
const cart = getCart();
console.log(cart); // [{ id: 1, name: 'Product A', price: 29.99 }]
```

### Example 3: Form Auto-Save

```html
<form id="myForm">
  <input type="text" name="name" placeholder="Name">
  <textarea name="message" placeholder="Message"></textarea>
  <button type="submit">Submit</button>
</form>

<script>
  const form = document.getElementById('myForm');
  const inputs = form.querySelectorAll('input, textarea');

  // Load saved values
  inputs.forEach(input => {
    const saved = sessionStorage.getItem(`form_${input.name}`);
    if (saved) input.value = saved;
  });

  // Auto-save on input
  inputs.forEach(input => {
    input.addEventListener('input', function() {
      sessionStorage.setItem(`form_${this.name}`, this.value);
    });
  });

  // Clear on submit
  form.addEventListener('submit', function() {
    inputs.forEach(input => {
      sessionStorage.removeItem(`form_${input.name}`);
    });
  });
</script>
```

---

## Best Practices

### Do This

1. **Always check for null**
   ```javascript
   const user = localStorage.getItem('user');
   if (user) {
     const data = JSON.parse(user);
   }
   ```

2. **Use try-catch for JSON.parse**
   ```javascript
   try {
     const data = JSON.parse(localStorage.getItem('data'));
   } catch(e) {
     console.error('Invalid JSON');
   }
   ```

3. **Check storage availability**
   ```javascript
   function storageAvailable() {
     try {
       localStorage.setItem('test', 'test');
       localStorage.removeItem('test');
       return true;
     } catch(e) {
       return false;
     }
   }
   ```

### Avoid This

1. **Don't store sensitive data**
   ```javascript
   // WRONG: Never store passwords/tokens
   localStorage.setItem('password', 'secret123');

   // CORRECT: Use secure HTTP-only cookies
   ```

2. **Don't assume infinite storage**
   ```javascript
   // WRONG: No error handling
   localStorage.setItem('huge', bigData);

   // CORRECT: Catch quota errors
   try {
     localStorage.setItem('huge', bigData);
   } catch(e) {
     if (e.name === 'QuotaExceededError') {
       alert('Storage full');
     }
   }
   ```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| localStorage | ✅ 4+ | ✅ 3.5+ | ✅ 4+ | ✅ All | ✅ 8+ |
| sessionStorage | ✅ 4+ | ✅ 2+ | ✅ 4+ | ✅ All | ✅ 8+ |
| Storage events | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |

---

## Related Topics
- [Geolocation](geolocation.md)
- [Web Workers](web-workers.md)
- [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)

---

**Last Updated:** November 17, 2025
**Category:** HTML5 APIs
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
