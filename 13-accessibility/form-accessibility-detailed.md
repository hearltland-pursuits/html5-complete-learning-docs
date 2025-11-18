---
title: Advanced Form Accessibility
category: Accessibility
order: 8
---

# Advanced Form Accessibility

> **Quick Summary:** Accessible forms use proper labels, error handling, keyboard navigation, and ARIA attributes to ensure all users can complete forms successfully.

## Essential Form Accessibility

### 1. Label Every Input

```html
<!-- ✅ GOOD - Explicit label -->
<label for="email">Email:</label>
<input type="email" id="email" required>

<!-- ✅ ALSO GOOD - Implicit label -->
<label>
  Email:
  <input type="email" required>
</label>

<!-- ❌ BAD - No label -->
<input type="email" placeholder="Email">
```

**Why:** Placeholders disappear; labels persist. Screen readers announce labels.

### 2. Group Related Fields

```html
<fieldset>
  <legend>Shipping Address</legend>
  <label for="street">Street:</label>
  <input type="text" id="street">

  <label for="city">City:</label>
  <input type="text" id="city">
</fieldset>
```

**Screen reader announces:** "Shipping Address, group. Street, edit text."

### 3. Required Field Indicators

```html
<label for="name">
  Name <span aria-label="required">*</span>
</label>
<input type="text" id="name" required aria-required="true">
```

---

## Error Handling

### Inline Errors

```html
<label for="email">Email:</label>
<input type="email" id="email"
       aria-invalid="true"
       aria-describedby="email-error">
<span id="email-error" role="alert">
  Please enter a valid email address
</span>
```

### Error Summary

```html
<div role="alert" aria-labelledby="error-title">
  <h2 id="error-title">Please fix the following errors:</h2>
  <ul>
    <li><a href="#email">Email is invalid</a></li>
    <li><a href="#password">Password too short</a></li>
  </ul>
</div>
```

### Live Validation

```html
<label for="username">Username:</label>
<input type="text" id="username" aria-describedby="username-status">
<span id="username-status" aria-live="polite" role="status">
  <!-- Dynamically updated: "Available" or "Already taken" -->
</span>
```

---

## Complex Form Patterns

### Radio Groups

```html
<fieldset>
  <legend>Subscription Plan</legend>
  <label>
    <input type="radio" name="plan" value="free" checked>
    Free
  </label>
  <label>
    <input type="radio" name="plan" value="pro">
    Pro ($9.99/month)
  </label>
</fieldset>
```

### Checkbox Groups

```html
<fieldset>
  <legend>Interests (select all that apply)</legend>
  <label><input type="checkbox" name="interest" value="web"> Web Development</label>
  <label><input type="checkbox" name="interest" value="mobile"> Mobile Apps</label>
  <label><input type="checkbox" name="interest" value="data"> Data Science</label>
</fieldset>
```

### Custom Select (Combobox)

```html
<label for="country">Country:</label>
<div role="combobox" aria-expanded="false" aria-owns="country-list" aria-haspopup="listbox">
  <input type="text" id="country" aria-autocomplete="list" aria-controls="country-list">
</div>
<ul id="country-list" role="listbox" hidden>
  <li role="option">United States</li>
  <li role="option">Canada</li>
  <li role="option">Mexico</li>
</ul>
```

---

## Form Instructions

### Field-Level Help

```html
<label for="password">Password:</label>
<input type="password" id="password" aria-describedby="password-help">
<div id="password-help">
  Must be at least 8 characters with 1 number and 1 special character
</div>
```

### Conditional Fields

```html
<label>
  <input type="checkbox" id="shipping" onchange="toggleAddress()">
  Ship to different address
</label>

<div id="shipping-address" hidden aria-hidden="true">
  <h3>Shipping Address</h3>
  <!-- Address fields -->
</div>

<script>
function toggleAddress() {
  const visible = document.getElementById('shipping').checked;
  const address = document.getElementById('shipping-address');
  address.hidden = !visible;
  address.setAttribute('aria-hidden', !visible);
}
</script>
```

---

## Multi-Step Forms

```html
<div role="region" aria-label="Step 2 of 4: Payment Information">
  <h2>Payment Information</h2>

  <nav aria-label="Form progress">
    <ol>
      <li aria-current="false">Account</li>
      <li aria-current="step">Payment</li>
      <li aria-current="false">Review</li>
      <li aria-current="false">Complete</li>
    </ol>
  </nav>

  <form>
    <!-- Payment fields -->
    <button type="button">Back</button>
    <button type="submit">Next</button>
  </form>
</div>
```

---

## Best Practices

### 1. Autocomplete Attributes

```html
<input type="text" name="name" autocomplete="name">
<input type="email" name="email" autocomplete="email">
<input type="tel" name="phone" autocomplete="tel">
<input type="text" name="address" autocomplete="street-address">
```

**Why:** Helps autofill and assistive tech predict field purpose.

### 2. Input Types

```html
<!-- ✅ Specific types -->
<input type="email"> <!-- Shows @ keyboard on mobile -->
<input type="tel"> <!-- Shows number pad -->
<input type="url"> <!-- Shows .com keyboard -->
<input type="date"> <!-- Shows date picker -->

<!-- ❌ Generic type -->
<input type="text"> <!-- Less helpful -->
```

### 3. Clear Button Labels

```html
<!-- ❌ VAGUE -->
<button>Submit</button>

<!-- ✅ SPECIFIC -->
<button type="submit">Create Account</button>
<button type="button">Add Another Address</button>
```

---

## Testing Checklist

- [ ] All inputs have labels
- [ ] Tab order is logical
- [ ] Error messages are clear and associated with fields
- [ ] Required fields are marked
- [ ] Form can be completed with keyboard only
- [ ] Screen reader announces all labels and errors
- [ ] Focus visible on all fields

---

## Related Topics

- [Form Elements](../06-forms-input/form-element.md)
- [Form Validation](../06-forms-input/form-validation.md)
- [Keyboard Navigation](keyboard-navigation.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
