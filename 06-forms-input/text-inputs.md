---
title: Text Inputs
category: Forms & Input
order: 2
---

# Text Inputs

> **Quick Summary:** HTML5 introduced specialized text input types (email, tel, url, search) that provide built-in validation, mobile-optimized keyboards, and better user experience compared to the generic text input.

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

Text inputs are the foundation of web forms, allowing users to enter single-line text data. While the classic `<input type="text">` works for any text, HTML5 introduced **semantic input types** that automatically provide validation, mobile keyboard optimization, and better accessibility.

For example, `type="email"` displays an email-specific keyboard on mobile devices (with @ and .com shortcuts), validates email format automatically, and tells screen readers this field expects an email address. This eliminates the need for custom JavaScript validation and improves the user experience across devices.

Modern web developers should choose the most specific input type for their use case: `email` for email addresses, `tel` for phone numbers, `url` for web addresses, `search` for search boxes, and `text` only when none of the specialized types apply.

**Key Concept:** Using semantic HTML5 input types improves accessibility, provides free validation, and optimizes mobile keyboards—all without writing a single line of JavaScript.

---

## Basic Syntax

```html
<!-- Generic text input -->
<input type="text" name="username" id="username">

<!-- HTML5 semantic input types -->
<input type="email" name="email" id="email">
<input type="tel" name="phone" id="phone">
<input type="url" name="website" id="website">
<input type="search" name="query" id="query">
```

### Key Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `type` | `text`, `email`, `tel`, `url`, `search` | Determines input behavior and validation |
| `name` | Text string | Name sent to server (e.g., `name="email"`) |
| `id` | Text string | Unique identifier for label association |
| `value` | Text string | Pre-filled value (initial content) |
| `placeholder` | Text string | Hint text displayed when input is empty |
| `required` | Boolean | Makes field mandatory before submission |
| `maxlength` | Number | Maximum character limit |
| `minlength` | Number | Minimum character requirement (HTML5) |
| `pattern` | Regex | Custom validation pattern |
| `autocomplete` | `on`, `off`, specific values | Controls browser autofill behavior |
| `readonly` | Boolean | Prevents editing (value still submitted) |
| `disabled` | Boolean | Disables input (value NOT submitted) |

### Input Types Explained

- **`type="text"`:** Generic single-line text (default, use when no semantic type fits)
- **`type="email"`:** Email addresses (validates format, mobile shows @ key)
- **`type="tel"`:** Phone numbers (mobile shows numeric keyboard, no validation)
- **`type="url"`:** Web addresses (validates http://, mobile shows .com key)
- **`type="search"`:** Search queries (shows X clear button in some browsers)

---

## Examples

### Example 1: Email Input with Validation

**Scenario:** Creating an email subscription form that automatically validates email format.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Email Input Example</title>
</head>
<body>
  <form action="/subscribe" method="POST">
    <label for="subscriber-email">Email Address:</label>
    <input
      type="email"
      id="subscriber-email"
      name="email"
      placeholder="you@example.com"
      required
      autocomplete="email">

    <button type="submit">Subscribe</button>
  </form>
</body>
</html>
```

**Result:** The browser automatically validates email format (must contain @, valid domain). On mobile devices, the keyboard shows @ and .com shortcuts. If the user enters invalid text, the browser displays an error message before submission.

---

### Example 2: Phone Number Input (International)

**Scenario:** Collecting phone numbers with a specific format pattern for validation.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Phone Input Example</title>
</head>
<body>
  <form action="/contact" method="POST">
    <label for="phone-number">Phone Number:</label>
    <input
      type="tel"
      id="phone-number"
      name="phone"
      placeholder="+1 (555) 123-4567"
      pattern="[+]?[0-9]{1,4}?[-.\s]?[(]?[0-9]{1,3}?[)]?[-.\s]?[0-9]{1,4}[-.\s]?[0-9]{1,4}[-.\s]?[0-9]{1,9}"
      title="Please enter a valid phone number"
      required
      autocomplete="tel">

    <button type="submit">Call Me</button>
  </form>
</body>
</html>
```

**Result:** Mobile devices display a numeric keypad. The `pattern` attribute validates the format, and `title` provides helpful error text. `type="tel"` doesn't validate format by itself (phone formats vary globally), so the pattern is needed.

---

### Example 3: Complete Contact Form with All Text Input Types

**Scenario:** Building a comprehensive contact form using all semantic input types.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Form</title>
  <style>
    label { display: block; margin-top: 1rem; }
    input { width: 100%; max-width: 400px; padding: 0.5rem; }
    button { margin-top: 1rem; padding: 0.5rem 1rem; }
  </style>
</head>
<body>
  <h1>Contact Information</h1>
  <form action="/submit-contact" method="POST">
    <!-- Text input -->
    <label for="full-name">Full Name:</label>
    <input
      type="text"
      id="full-name"
      name="name"
      placeholder="John Doe"
      required
      minlength="2"
      maxlength="100"
      autocomplete="name">

    <!-- Email input -->
    <label for="email-address">Email:</label>
    <input
      type="email"
      id="email-address"
      name="email"
      placeholder="john@example.com"
      required
      autocomplete="email">

    <!-- Telephone input -->
    <label for="phone-contact">Phone:</label>
    <input
      type="tel"
      id="phone-contact"
      name="phone"
      placeholder="+1-555-123-4567"
      autocomplete="tel">

    <!-- URL input -->
    <label for="website-url">Website:</label>
    <input
      type="url"
      id="website-url"
      name="website"
      placeholder="https://example.com"
      autocomplete="url">

    <!-- Search input -->
    <label for="search-query">How did you find us?</label>
    <input
      type="search"
      id="search-query"
      name="referral"
      placeholder="Google, friend referral, etc.">

    <button type="submit">Submit Contact Info</button>
  </form>
</body>
</html>
```

**Result:** A fully functional contact form with optimized mobile keyboards for each field type. Email and URL fields validate automatically. Search input shows a clear (X) button in some browsers.

**Notes:**
- `autocomplete` values follow [HTML spec](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill) for better browser autofill
- `minlength` and `maxlength` control character count
- Only email, phone, and name are required; website and search are optional

---

## Common Use Cases

### Use Case 1: Login Form with Username/Email
**When:** Users can log in with either username or email.
**How:**
```html
<form action="/login" method="POST">
  <label for="login-id">Username or Email:</label>
  <input
    type="text"
    id="login-id"
    name="login"
    placeholder="Username or email"
    required
    autocomplete="username">

  <label for="password">Password:</label>
  <input type="password" id="password" name="password" required autocomplete="current-password">

  <button type="submit">Log In</button>
</form>
```
**Why:** Use `type="text"` (not email) when accepting both username and email. The `autocomplete="username"` tells password managers to save this field.

---

### Use Case 2: Search Box in Navigation
**When:** Adding a search feature in website header/navigation.
**How:**
```html
<form action="/search" method="GET" role="search">
  <label for="site-search" class="visually-hidden">Search this site:</label>
  <input
    type="search"
    id="site-search"
    name="q"
    placeholder="Search..."
    autocomplete="off"
    aria-label="Search through site content">

  <button type="submit">🔍</button>
</form>
```
**Why:** `type="search"` provides a clear (X) button on many browsers. `autocomplete="off"` prevents showing old searches. `role="search"` improves accessibility.

---

### Use Case 3: Newsletter Signup with Email Validation
**When:** Simple newsletter subscription form.
**How:**
```html
<form action="/api/newsletter" method="POST">
  <label for="newsletter-email">Get updates via email:</label>
  <input
    type="email"
    id="newsletter-email"
    name="email"
    placeholder="your.email@example.com"
    required
    autocomplete="email"
    pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$"
    title="Please enter a valid email address">

  <button type="submit">Subscribe</button>
</form>
```
**Why:** `type="email"` provides built-in validation, but adding a `pattern` makes validation stricter (e.g., preventing spaces or invalid characters).

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 10+     | Full Support  | All HTML5 input types fully supported |
| Firefox | 4+      | Full Support  | Full support for email, url, tel, search |
| Safari  | 5+      | Full Support  | iOS Safari shows optimized keyboards |
| Edge    | All     | Full Support  | Full HTML5 input type support |
| IE 11   | 11      | Partial Support | Falls back to `type="text"` for unsupported types |

**Fallback Strategy:**
```html
<!-- Modern browsers: email validation + mobile keyboard -->
<!-- Older browsers (IE): Gracefully degrades to type="text" -->
<input type="email" name="email" required>

<!-- For older browser support, add pattern as backup validation -->
<input type="email" name="email" pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$" required>
```

**Can I Use Links:**
- [Email Input](https://caniuse.com/input-email-tel-url)
- [Search Input](https://caniuse.com/input-search)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- All inputs must have associated `<label>` elements with matching `for` and `id`
- Inputs must be keyboard-accessible (Tab to navigate, Enter to submit)

**Level AA Requirements:**
- Labels must have sufficient color contrast (4.5:1 for normal text)
- Error messages must be programmatically associated with inputs
- `placeholder` should not replace `<label>` (placeholders disappear on input)

### Screen Reader Support

```html
<!-- Accessible text input with label, hint, and error handling -->
<label for="user-email">
  Email Address <span aria-label="required">*</span>
</label>
<input
  type="email"
  id="user-email"
  name="email"
  required
  aria-required="true"
  aria-describedby="email-hint email-error">

<small id="email-hint">We'll never share your email with anyone.</small>
<span id="email-error" role="alert" aria-live="polite"></span>
```

**Key Points:**
- `aria-required="true"` announces required fields to screen readers
- `aria-describedby` links helpful hints and error messages to the input
- `role="alert"` makes error messages announce immediately when they appear

### Keyboard Navigation

- **Tab:** Moves focus to next input field
- **Shift + Tab:** Moves focus to previous input
- **Enter:** Submits form when focus is on any text input
- **Esc:** Clears search input in some browsers (type="search")

---

## Best Practices

### Do This

1. **Use Semantic Input Types**
   ```html
   <!-- GOOD: Semantic type provides validation + mobile keyboard -->
   <input type="email" name="email" required>
   ```
   **Why:** `type="email"` validates format automatically and shows @ key on mobile keyboards. No JavaScript needed.

2. **Always Pair Inputs with Labels**
   ```html
   <!-- GOOD: Label explicitly associated via for/id -->
   <label for="user-name">Your Name:</label>
   <input type="text" id="user-name" name="name">
   ```
   **Why:** Labels improve accessibility, increase click target area, and are required for screen reader users.

3. **Use Autocomplete Attributes**
   ```html
   <!-- GOOD: Browser can autofill from saved data -->
   <input type="email" name="email" autocomplete="email">
   <input type="tel" name="phone" autocomplete="tel">
   ```
   **Why:** Reduces user effort, especially on mobile. Improves conversion rates on forms.

---

### Avoid This

1. **Using Placeholder as Label Replacement**
   ```html
   <!-- WRONG: No label, only placeholder -->
   <input type="text" name="name" placeholder="Your Name">
   ```
   **Why Not:** Placeholders disappear when typing, confusing users. Screen readers may not announce placeholders. Fails WCAG.
   **Instead:**
   ```html
   <label for="user-name">Your Name:</label>
   <input type="text" id="user-name" name="name" placeholder="e.g., John Doe">
   ```

2. **Using type="text" for Email/Phone/URL**
   ```html
   <!-- WRONG: Generic text input for email -->
   <input type="text" name="email">
   ```
   **Why Not:** No validation, generic keyboard on mobile, poor accessibility.
   **Instead:**
   ```html
   <input type="email" name="email" autocomplete="email">
   ```

3. **Forgetting Name Attribute**
   ```html
   <!-- WRONG: No name attribute means data won't be submitted -->
   <input type="email" id="email">
   ```
   **Why Not:** The `name` attribute is what gets sent to the server. Without it, the form submission won't include this field's data.
   **Instead:**
   ```html
   <input type="email" id="email" name="email">
   ```

---

## Related Topics

**Prerequisites (Learn These First):**
- [Form Element](form-element.md) - Understanding form structure and submission
- [HTML5 Syntax](../01-fundamentals/syntax.md) - HTML element and attribute basics

**Related Concepts:**
- [Form Validation](form-validation.md) - HTML5 validation (required, pattern, etc.)
- [Form Attributes](form-attributes.md) - Additional HTML5 input attributes
- [Form Accessibility](form-accessibility.md) - WCAG-compliant form design
- [Number & Range Inputs](number-range.md) - Numeric input types

**Next Steps (Learn These Next):**
- [Number & Range Inputs](number-range.md) - HTML5 numeric inputs
- [Date & Time Inputs](date-time.md) - Date and time pickers

**External Resources:**
- [MDN Web Docs - Input Types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)
- [W3Schools - HTML Input Types](https://www.w3schools.com/html/html_form_input_types.asp)
- [HTML Spec - Autofill Values](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#autofill)

---

## Practice Exercise

### Challenge: Build a User Profile Form

**Objective:** Create a profile update form that collects name, email, phone, and website using appropriate input types with validation.

**Requirements:**
- [ ] Name field (text) with 2-50 character limit
- [ ] Email field with validation and autocomplete
- [ ] Phone field with international format pattern
- [ ] Website field (optional) that accepts http/https URLs
- [ ] All required fields must have proper labels and validation
- [ ] Bonus: Add a search field for "How did you hear about us?"

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Profile Form Exercise</title>
</head>
<body>
  <h1>Update Your Profile</h1>
  <form action="/profile" method="POST">
    <!-- Add your form fields here -->
    <button type="submit">Save Profile</button>
  </form>
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Profile Form Exercise</title>
  <style>
    label { display: block; margin-top: 1rem; font-weight: bold; }
    input { width: 100%; max-width: 400px; padding: 0.5rem; margin-top: 0.25rem; }
    small { display: block; color: #666; margin-top: 0.25rem; }
    button { margin-top: 1.5rem; padding: 0.75rem 1.5rem; }
  </style>
</head>
<body>
  <h1>Update Your Profile</h1>
  <form action="/profile" method="POST">
    <!-- Name field (text) -->
    <label for="full-name">Full Name: <span aria-label="required">*</span></label>
    <input
      type="text"
      id="full-name"
      name="name"
      minlength="2"
      maxlength="50"
      required
      autocomplete="name"
      placeholder="John Doe">
    <small>2-50 characters</small>

    <!-- Email field -->
    <label for="email-address">Email Address: <span aria-label="required">*</span></label>
    <input
      type="email"
      id="email-address"
      name="email"
      required
      autocomplete="email"
      placeholder="you@example.com">

    <!-- Phone field with pattern -->
    <label for="phone-number">Phone Number: <span aria-label="required">*</span></label>
    <input
      type="tel"
      id="phone-number"
      name="phone"
      pattern="[+]?[0-9]{1,4}?[-.\s]?[(]?[0-9]{1,3}?[)]?[-.\s]?[0-9]{1,4}[-.\s]?[0-9]{1,4}"
      title="Enter a valid phone number (e.g., +1-555-123-4567)"
      required
      autocomplete="tel"
      placeholder="+1-555-123-4567">
    <small>International format accepted</small>

    <!-- Website field (optional) -->
    <label for="website-url">Website (optional):</label>
    <input
      type="url"
      id="website-url"
      name="website"
      autocomplete="url"
      placeholder="https://yoursite.com">

    <!-- Referral source (bonus) -->
    <label for="referral-source">How did you hear about us? (optional)</label>
    <input
      type="search"
      id="referral-source"
      name="referral"
      placeholder="Google, friend, advertisement, etc.">

    <button type="submit">Save Profile</button>
  </form>
</body>
</html>
```

**Explanation:**
This form uses semantic HTML5 input types for each field: `text` for names (generic), `email` for email validation, `tel` for phone with custom pattern, `url` for website validation, and `search` for the referral field. The `required` attribute ensures critical fields are filled, while `minlength`, `maxlength`, and `pattern` provide specific validation. Autocomplete attributes enable browser autofill for better UX.

</details>

---

### Expected Result

**Visual Outcome:** A complete profile form with 5 input fields, each using the appropriate HTML5 input type. Mobile users see optimized keyboards (email keyboard for email field, number pad for phone, etc.). Browser validates email/URL format automatically.

**Key Learnings:**
- When to use each HTML5 text input type (text vs email vs tel vs url vs search)
- How to combine validation attributes (`required`, `minlength`, `maxlength`, `pattern`)
- The importance of `autocomplete` for user convenience
- How semantic input types improve mobile UX and accessibility

---

## Navigation

**Previous:** [Form Element](form-element.md)
**Next:** [Number & Range Inputs](number-range.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
