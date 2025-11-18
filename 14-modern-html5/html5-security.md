---
title: HTML5 Security
category: Modern HTML5
order: 4
---

# HTML5 Security

> **Quick Summary:** HTML5 security involves preventing XSS attacks, using Content Security Policy, sanitizing user input, and following secure coding practices.

## Common Security Threats

### 1. Cross-Site Scripting (XSS)

**Attack:** Injecting malicious JavaScript into pages

```html
<!-- ❌ VULNERABLE - User input directly in HTML -->
<div>Welcome, <?php echo $_GET['name']; ?>!</div>

<!-- Attack URL: ?name=<script>steal Cookies()</script> -->
```

**Prevention:**
```html
<!-- ✅ ESCAPED - HTML entities -->
<div>Welcome, <?php echo htmlspecialchars($_GET['name']); ?>!</div>

<!-- Attack becomes: &lt;script&gt;stealCookies()&lt;/script&gt; -->
```

### 2. Injection via innerHTML

```javascript
// ❌ DANGEROUS
userInput = '<img src=x onerror="alert(document.cookie)">';
div.innerHTML = userInput;

// ✅ SAFE - Use textContent
div.textContent = userInput;

// ✅ SAFE - Sanitize HTML
import DOMPurify from 'dompurify';
div.innerHTML = DOMPurify.sanitize(userInput);
```

---

## Content Security Policy (CSP)

Prevents XSS by controlling which resources can load.

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'self'; script-src 'self' https://trusted-cdn.com; style-src 'self' 'unsafe-inline';">
```

**What it does:**
- Scripts: Only from same origin + trusted CDN
- Styles: Same origin + inline styles allowed
- Images/fonts/etc.: Same origin only

---

## Secure Form Handling

### CSRF Protection

```html
<form method="POST" action="/submit">
  <!-- CSRF token -->
  <input type="hidden" name="csrf_token" value="<?php echo generateToken(); ?>">
  <input type="text" name="comment">
  <button>Submit</button>
</form>
```

### Input Validation

```html
<!-- Client-side validation (UX) -->
<input type="email" required pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$">

<!-- ⚠️ Always validate server-side too! Client-side can be bypassed -->
```

---

## Secure Third-Party Content

### Sandbox iframes

```html
<!-- ❌ DANGEROUS - Full access -->
<iframe src="https://untrusted-site.com"></iframe>

<!-- ✅ SAFE - Sandboxed -->
<iframe src="https://untrusted-site.com"
        sandbox="allow-scripts allow-same-origin">
</iframe>
```

**Sandbox Permissions:**
- `allow-scripts` - Allow JavaScript
- `allow-forms` - Allow form submission
- `allow-same-origin` - Treat as same origin (dangerous if combined with allow-scripts)
- `allow-popups` - Allow popups

---

## Clickjacking Prevention

```html
<!-- Prevent embedding in iframes -->
<meta http-equiv="X-Frame-Options" content="DENY">

<!-- Or via CSP -->
<meta http-equiv="Content-Security-Policy" content="frame-ancestors 'none';">
```

---

## Secure Storage

### LocalStorage Security

```javascript
// ❌ NEVER store sensitive data in localStorage
localStorage.setItem('password', userPassword); // BAD!
localStorage.setItem('creditCard', cardNumber); // BAD!

// ✅ Store non-sensitive data only
localStorage.setItem('theme', 'dark'); // OK
localStorage.setItem('language', 'en'); // OK
```

**Why:** localStorage is accessible to all JavaScript on the same origin, including third-party scripts.

---

## Best Practices

### 1. Escape User Input

```javascript
function escapeHTML(str) {
  return str.replace(/[&<>"']/g, (char) => {
    const entities = {
      '&': '&amp;',
      '<': '&lt;',
      '>': '&gt;',
      '"': '&quot;',
      "'": '&#39;'
    };
    return entities[char];
  });
}
```

### 2. Use HTTPS

```html
<!-- ✅ Force HTTPS -->
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
```

### 3. Subresource Integrity (SRI)

```html
<!-- Verify CDN scripts haven't been tampered with -->
<script src="https://cdn.example.com/lib.js"
        integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho1wx4JwY8wC"
        crossorigin="anonymous"></script>
```

---

## Related Topics

- [Form Validation](../06-forms-input/form-validation.md)
- [Content Security Policy (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)

---

**Last Updated:** November 18, 2025
**Category:** Modern HTML5
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
