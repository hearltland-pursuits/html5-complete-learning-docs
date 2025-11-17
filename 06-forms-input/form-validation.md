---
title: Form Validation
category: Forms & Input
order: 8
---

# Form Validation

> **Quick Summary:** HTML5 provides built-in form validation using attributes like `required`, `pattern`, `min`, `max`, `minlength`, and `maxlength`—reducing the need for JavaScript while improving user experience and security.

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

Before HTML5, form validation required JavaScript or server-side processing. HTML5 introduced **native validation attributes** that browsers enforce automatically before form submission, providing instant feedback to users without custom code.

Key validation attributes include: `required` (field must be filled), `pattern` (regex validation), `min`/`max` (numeric/date ranges), `minlength`/`maxlength` (character limits), and `type`-specific validation (email format, URL format). When validation fails, browsers display built-in error messages and prevent form submission.

Modern forms combine HTML5 validation (client-side, instant feedback) with server-side validation (security, business logic). HTML5 validation improves UX but never replaces server-side validation, as client-side checks can be bypassed.

**Key Concept:** HTML5 validation provides free, accessible, instant user feedback. Always complement with server-side validation for security. Use `novalidate` attribute to disable HTML5 validation when implementing custom JavaScript validation.

---

## Basic Syntax

```html
<!-- Required field -->
<input type="text" name="username" required>

<!-- Pattern validation (regex) -->
<input type="text" name="zip" pattern="[0-9]{5}" title="5-digit ZIP code">

<!-- Min/max for numbers -->
<input type="number" name="age" min="13" max="120">

<!-- Min/max for dates -->
<input type="date" name="event" min="2025-01-01" max="2025-12-31">

<!-- Length validation -->
<input type="text" name="code" minlength="6" maxlength="6">

<!-- Email validation (built-in) -->
<input type="email" name="email" required>
```

### Validation Attributes

| Attribute | Applies To | Description |
|-----------|-----------|-------------|
| `required` | Most inputs | Field must have a value |
| `pattern` | Text inputs | Value must match regex pattern |
| `min` | number, date, time | Minimum value |
| `max` | number, date, time | Maximum value |
| `minlength` | text, textarea | Minimum character count |
| `maxlength` | text, textarea | Maximum character count |
| `step` | number, date, time | Increment value for validation |
| `type="email"` | input | Validates email format (contains @) |
| `type="url"` | input | Validates URL format (http://) |

### Validation Control

- **`novalidate`** (on `<form>`): Disables all HTML5 validation for the form
- **`formnovalidate`** (on `<button>`): Submit button that bypasses validation (e.g., "Save Draft")

---

## Examples

### Example 1: Registration Form with Multiple Validations

**Scenario:** User registration requiring username, email, password with strength rules.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registration Validation</title>
</head>
<body>
  <form action="/register" method="POST">
    <h1>Create Account</h1>

    <!-- Username: 3-20 characters, alphanumeric only -->
    <label for="username">Username: *</label>
    <input
      type="text"
      id="username"
      name="username"
      pattern="[A-Za-z0-9]{3,20}"
      title="3-20 characters, letters and numbers only"
      required
      aria-describedby="username-hint">
    <small id="username-hint">3-20 characters, letters and numbers only</small>

    <!-- Email: built-in validation -->
    <label for="email">Email: *</label>
    <input
      type="email"
      id="email"
      name="email"
      required>

    <!-- Password: minimum 8 chars, must include number -->
    <label for="password">Password: *</label>
    <input
      type="password"
      id="password"
      name="password"
      pattern="(?=.*\d).{8,}"
      title="Minimum 8 characters, must include at least one number"
      required
      aria-describedby="password-hint">
    <small id="password-hint">Minimum 8 characters, must include at least one number</small>

    <!-- Age: 13-120 -->
    <label for="age">Age: *</label>
    <input
      type="number"
      id="age"
      name="age"
      min="13"
      max="120"
      required>

    <button type="submit">Create Account</button>
  </form>
</body>
</html>
```

**Result:** Browser validates username format (alphanumeric, 3-20 chars), email format, password strength (8+ chars with number), and age range (13-120) before allowing submission.

---

### Example 2: Event Booking with Date Range Validation

**Scenario:** Event booking form restricting dates to next 6 months.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Event Booking</title>
</head>
<body>
  <form action="/book-event" method="POST">
    <h1>Book Your Event</h1>

    <!-- Event date: Future dates only, max 6 months ahead -->
    <label for="event-date">Event Date: *</label>
    <input
      type="date"
      id="event-date"
      name="date"
      required
      aria-describedby="date-hint">
    <small id="date-hint">Select a date within the next 6 months</small>

    <!-- Number of guests: 1-100 -->
    <label for="guests">Number of Guests: *</label>
    <input
      type="number"
      id="guests"
      name="num_guests"
      min="1"
      max="100"
      step="1"
      value="10"
      required>

    <button type="submit">Book Event</button>
  </form>

  <script>
    // Dynamically set min to today, max to 6 months from now
    const today = new Date();
    const sixMonths = new Date(today);
    sixMonths.setMonth(today.getMonth() + 6);

    document.getElementById('event-date').min = today.toISOString().split('T')[0];
    document.getElementById('event-date').max = sixMonths.toISOString().split('T')[0];
  </script>
</body>
</html>
```

**Result:** JavaScript dynamically sets date constraints. Browser prevents selecting past dates or dates more than 6 months ahead. Guests must be 1-100.

---

### Example 3: Custom Validation Messages with JavaScript

**Scenario:** Form with custom error messages instead of browser defaults.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Custom Validation</title>
</head>
<body>
  <form id="custom-form" action="/submit" method="POST">
    <label for="email-custom">Email: *</label>
    <input
      type="email"
      id="email-custom"
      name="email"
      required>

    <label for="zip-code">ZIP Code: *</label>
    <input
      type="text"
      id="zip-code"
      name="zip"
      pattern="[0-9]{5}"
      required>

    <button type="submit">Submit</button>
  </form>

  <script>
    const emailInput = document.getElementById('email-custom');
    const zipInput = document.getElementById('zip-code');

    // Custom email error message
    emailInput.addEventListener('invalid', function() {
      if (this.validity.valueMissing) {
        this.setCustomValidity('Please enter your email address');
      } else if (this.validity.typeMismatch) {
        this.setCustomValidity('Please enter a valid email (e.g., you@example.com)');
      }
    });

    emailInput.addEventListener('input', function() {
      this.setCustomValidity(''); // Clear custom message on input
    });

    // Custom ZIP code error message
    zipInput.addEventListener('invalid', function() {
      if (this.validity.valueMissing) {
        this.setCustomValidity('Please enter your ZIP code');
      } else if (this.validity.patternMismatch) {
        this.setCustomValidity('ZIP code must be exactly 5 digits');
      }
    });

    zipInput.addEventListener('input', function() {
      this.setCustomValidity('');
    });
  </script>
</body>
</html>
```

**Result:** Browser shows custom error messages ("Please enter your email address") instead of generic "Please fill out this field". Messages are more user-friendly.

---

## Common Use Cases

### Use Case 1: Credit Card Number Format
**When:** Payment form requiring exact credit card format.
**How:**
```html
<label for="cc">Credit Card Number: *</label>
<input
  type="text"
  id="cc"
  name="credit_card"
  pattern="[0-9]{13,19}"
  inputmode="numeric"
  title="13-19 digits"
  maxlength="19"
  required>
```
**Why:** Pattern validates 13-19 digits (AMEX=15, Visa/MC=16). `inputmode="numeric"` shows number keyboard on mobile.

---

### Use Case 2: Phone Number Validation
**When:** Contact form with specific phone format.
**How:**
```html
<label for="phone">Phone (US format): *</label>
<input
  type="tel"
  id="phone"
  name="phone"
  pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
  placeholder="555-123-4567"
  title="Format: 555-123-4567"
  required>
```
**Why:** Pattern enforces XXX-XXX-XXXX format. `title` shows expected format in error message.

---

### Use Case 3: Password Confirmation Match
**When:** Registration requiring password confirmation.
**How:**
```html
<label for="password">Password: *</label>
<input type="password" id="password" name="password" required>

<label for="confirm">Confirm Password: *</label>
<input type="password" id="confirm" name="confirm_password" required>

<script>
  const password = document.getElementById('password');
  const confirm = document.getElementById('confirm');

  confirm.addEventListener('input', function() {
    if (this.value !== password.value) {
      this.setCustomValidity('Passwords do not match');
    } else {
      this.setCustomValidity('');
    }
  });
</script>
```
**Why:** HTML5 can't compare fields natively. JavaScript adds custom validation for password matching.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 10+     | Full Support  | All HTML5 validation attributes supported |
| Firefox | 4+      | Full Support  | Full support since Firefox 4 |
| Safari  | 10+     | Full Support  | Earlier versions have partial support |
| Edge    | All     | Full Support  | Full support (all versions) |
| IE 11   | 11      | Partial Support | `pattern`, `required` work; custom messages require JS |

**Fallback Strategy:**
```html
<!-- HTML5 validation works in modern browsers -->
<!-- For older browsers, JavaScript polyfill or server-side only -->
<input type="email" name="email" required>

<!-- Always validate on server regardless of client-side validation -->
```

**Can I Use Link:** [HTML5 Form Validation](https://caniuse.com/form-validation)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Error messages must be clearly announced to screen readers
- Validation errors must not rely on color alone
- Required fields must be indicated both visually and programmatically

**Level AA Requirements:**
- Error messages must have sufficient color contrast
- Error messages must be programmatically associated with inputs
- Users must understand what caused the error and how to fix it

### Screen Reader Support

```html
<!-- Accessible validated input -->
<label for="username-input">
  Username <span aria-label="required">*</span>
</label>
<input
  type="text"
  id="username-input"
  name="username"
  pattern="[A-Za-z0-9]{3,20}"
  title="3-20 characters, letters and numbers only"
  required
  aria-required="true"
  aria-invalid="false"
  aria-describedby="username-hint username-error">

<small id="username-hint">3-20 characters, letters and numbers only</small>
<span id="username-error" role="alert" aria-live="polite"></span>

<script>
  const input = document.getElementById('username-input');
  const errorSpan = document.getElementById('username-error');

  input.addEventListener('invalid', function() {
    this.setAttribute('aria-invalid', 'true');
    errorSpan.textContent = 'Error: ' + this.validationMessage;
  });

  input.addEventListener('input', function() {
    if (this.validity.valid) {
      this.setAttribute('aria-invalid', 'false');
      errorSpan.textContent = '';
    }
  });
</script>
```

**Key Points:**
- `aria-invalid="true"` announces validation errors
- `role="alert"` and `aria-live="polite"` announce error messages immediately
- `aria-describedby` links hints and error messages to input

### Keyboard Navigation

All validation works seamlessly with keyboard navigation. No special considerations needed beyond standard form navigation (Tab, Enter to submit).

---

## Best Practices

### Do This

1. **Combine Multiple Validation Types**
   ```html
   <!-- GOOD: Multiple layers of validation -->
   <input
     type="email"
     name="email"
     required
     minlength="5"
     maxlength="100"
     pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,}$">
   ```
   **Why:** Type validation (email), required, length limits, and pattern create robust validation.

2. **Always Provide title Attribute for Pattern**
   ```html
   <!-- GOOD: Explains what pattern expects -->
   <input
     type="text"
     pattern="[A-Z]{2}[0-9]{4}"
     title="Format: Two uppercase letters followed by 4 digits (e.g., AB1234)">
   ```
   **Why:** Browser includes `title` in error message, helping users understand the requirement.

3. **Validate Server-Side Always**
   ```html
   <!-- GOOD: Client validation for UX, server validation for security -->
   <input type="email" name="email" required>
   <!-- Backend: Validate email format, check if exists in DB, etc. -->
   ```
   **Why:** Client-side validation can be bypassed (disable JavaScript, edit HTML). Server validation is mandatory for security.

---

### Avoid This

1. **Using Validation for UX Without Explanation**
   ```html
   <!-- WRONG: Pattern error but no guidance -->
   <input type="text" name="code" pattern="[0-9]{6}" required>
   ```
   **Why Not:** User sees "Please match the requested format" but doesn't know what format is expected.
   **Instead:**
   ```html
   <input type="text" name="code" pattern="[0-9]{6}"
          title="6-digit code" placeholder="123456" required>
   <small>Enter the 6-digit code from your email</small>
   ```

2. **Relying Only on Client-Side Validation**
   ```html
   <!-- WRONG: No server-side validation -->
   <form action="/submit" method="POST">
     <input type="email" name="email" required>
   </form>
   <!-- Server accepts any data without validation -->
   ```
   **Why Not:** Attackers can bypass HTML5 validation. SQL injection, XSS, and invalid data can reach your database.
   **Instead:** Always validate on both client (UX) and server (security).

3. **Complex Regex Without Explanation**
   ```html
   <!-- WRONG: Cryptic pattern, no title -->
   <input type="text" pattern="^(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$">
   ```
   **Why Not:** User has no idea what's required. Error message is unhelpful.
   **Instead:**
   ```html
   <input
     type="text"
     pattern="^(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$"
     title="Minimum 8 characters, at least one uppercase letter, one number, one special character">
   <small>Password must contain: uppercase, number, special character (minimum 8 chars)</small>
   ```

---

## Related Topics

**Prerequisites:**
- [Form Element](form-element.md) - Understanding forms
- [Text Inputs](text-inputs.md) - Input types and attributes

**Related Concepts:**
- [Form Attributes](form-attributes.md) - Additional HTML5 attributes
- [Form Accessibility](form-accessibility.md) - Accessible error handling

**Next Steps:**
- [Form Buttons](form-buttons.md) - Submit and reset buttons
- [Form Accessibility](form-accessibility.md) - WCAG-compliant forms

**External Resources:**
- [MDN - Form Validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- [W3Schools - HTML Input Attributes](https://www.w3schools.com/html/html_form_attributes.asp)
- [HTML Spec - Constraint Validation](https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#constraints)

---

## Practice Exercise

### Challenge: Build a Validated Signup Form

**Objective:** Create a signup form with comprehensive HTML5 validation for all fields.

**Requirements:**
- [ ] Username (3-15 chars, alphanumeric, required)
- [ ] Email (valid email format, required)
- [ ] Password (8+ chars, must include number, required)
- [ ] Age (13-100, required)
- [ ] Phone (optional, US format XXX-XXX-XXXX if provided)
- [ ] Show helpful error messages with `title` attributes
- [ ] Bonus: Add custom JavaScript validation messages

---

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Validated Signup</title>
</head>
<body>
  <h1>Create Account</h1>
  <form action="/signup" method="POST">
    <!-- Add your validated inputs here -->
    <button type="submit">Sign Up</button>
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
  <title>Validated Signup</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 500px; margin: 2rem auto; padding: 0 1rem; }
    label { display: block; margin-top: 1.5rem; font-weight: bold; }
    input { width: 100%; padding: 0.5rem; margin-top: 0.5rem; }
    small { display: block; color: #666; margin-top: 0.25rem; }
    input:invalid { border-color: #cc0000; }
    input:valid { border-color: #006600; }
    button { margin-top: 2rem; padding: 0.75rem 1.5rem; width: 100%; }
  </style>
</head>
<body>
  <h1>Create Account</h1>
  <form action="/signup" method="POST">
    <!-- Username -->
    <label for="username">Username: <span aria-label="required">*</span></label>
    <input
      type="text"
      id="username"
      name="username"
      pattern="[A-Za-z0-9]{3,15}"
      title="3-15 characters, letters and numbers only"
      required
      aria-required="true"
      aria-describedby="username-hint">
    <small id="username-hint">3-15 characters, letters and numbers only</small>

    <!-- Email -->
    <label for="email">Email: <span aria-label="required">*</span></label>
    <input
      type="email"
      id="email"
      name="email"
      required
      aria-required="true"
      placeholder="you@example.com">

    <!-- Password -->
    <label for="password">Password: <span aria-label="required">*</span></label>
    <input
      type="password"
      id="password"
      name="password"
      pattern="(?=.*\d).{8,}"
      title="Minimum 8 characters, must include at least one number"
      required
      aria-required="true"
      aria-describedby="password-hint">
    <small id="password-hint">Minimum 8 characters, must include at least one number</small>

    <!-- Age -->
    <label for="age">Age: <span aria-label="required">*</span></label>
    <input
      type="number"
      id="age"
      name="age"
      min="13"
      max="100"
      required
      aria-required="true"
      aria-describedby="age-hint">
    <small id="age-hint">You must be between 13 and 100 years old</small>

    <!-- Phone (optional) -->
    <label for="phone">Phone (optional):</label>
    <input
      type="tel"
      id="phone"
      name="phone"
      pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
      title="Format: 555-123-4567 (optional)"
      placeholder="555-123-4567"
      aria-describedby="phone-hint">
    <small id="phone-hint">US format: XXX-XXX-XXXX (leave blank if outside US)</small>

    <button type="submit">Sign Up</button>
  </form>

  <script>
    // Bonus: Custom validation messages
    const username = document.getElementById('username');
    const password = document.getElementById('password');
    const age = document.getElementById('age');

    username.addEventListener('invalid', function() {
      if (this.validity.valueMissing) {
        this.setCustomValidity('Please choose a username');
      } else if (this.validity.patternMismatch) {
        this.setCustomValidity('Username must be 3-15 characters (letters and numbers only)');
      }
    });

    username.addEventListener('input', function() {
      this.setCustomValidity('');
    });

    password.addEventListener('invalid', function() {
      if (this.validity.valueMissing) {
        this.setCustomValidity('Please create a password');
      } else if (this.validity.patternMismatch) {
        this.setCustomValidity('Password must be at least 8 characters and include a number');
      }
    });

    password.addEventListener('input', function() {
      this.setCustomValidity('');
    });

    age.addEventListener('invalid', function() {
      if (this.validity.valueMissing) {
        this.setCustomValidity('Please enter your age');
      } else if (this.validity.rangeUnderflow) {
        this.setCustomValidity('You must be at least 13 years old to sign up');
      } else if (this.validity.rangeOverflow) {
        this.setCustomValidity('Please enter a valid age (maximum 100)');
      }
    });

    age.addEventListener('input', function() {
      this.setCustomValidity('');
    });
  </script>
</body>
</html>
```

**Explanation:** This signup form uses comprehensive HTML5 validation: `pattern` for username format, `type="email"` for email validation, `pattern` with lookahead regex for password strength, `min`/`max` for age range, and optional phone with pattern. CSS provides visual feedback (red border for invalid, green for valid). Bonus JavaScript adds custom, user-friendly error messages.

</details>

---

### Expected Result

A fully validated signup form where all fields show validation errors before submission. Username must be 3-15 alphanumeric chars, email must be valid format, password needs 8+ chars with number, age 13-100, phone optional but must match XXX-XXX-XXXX if provided. Custom error messages are friendly and helpful.

**Key Learnings:**
- Combining `required`, `pattern`, `min`/`max` for comprehensive validation
- Using `title` to explain validation requirements
- Adding custom validation messages with JavaScript
- Visual feedback with CSS (`:valid` and `:invalid` pseudo-classes)
- Understanding that client validation is UX, not security

---

## Navigation

**Previous:** [Textarea & File Inputs](textarea-file.md)
**Next:** [Form Buttons](form-buttons.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
