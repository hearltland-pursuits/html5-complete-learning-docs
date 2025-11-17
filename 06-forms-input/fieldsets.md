---
title: Fieldsets & Legends
category: Forms & Input
order: 10
---

# Fieldsets & Legends

> **Quick Summary:** The `<fieldset>` element groups related form controls, while `<legend>` provides a caption for the group. Together they improve form organization, accessibility, and semantic structure—especially for screen readers.

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

The `<fieldset>` and `<legend>` elements provide semantic grouping for related form controls. **`<fieldset>`** acts as a container, visually grouping inputs with a border, while **`<legend>`** serves as the group's title or description.

These elements are particularly important for accessibility. Screen readers announce the legend when users enter a fieldset, providing context for the grouped inputs. For example, a fieldset with legend "Shipping Address" tells screen reader users that the following inputs (street, city, zip) are all for shipping.

Fieldsets also support the `disabled` attribute, which disables all inputs within the group at once—useful for conditional form sections. While often styled away (border removed with CSS), the semantic benefits remain.

**Key Concept:** Use `<fieldset>` + `<legend>` for groups of related inputs (radio buttons, checkboxes, address fields). Essential for accessibility—screen readers announce the legend as context for each input in the group.

---

## Basic Syntax

```html
<fieldset>
  <legend>Personal Information</legend>

  <label for="first-name">First Name:</label>
  <input type="text" id="first-name" name="first_name">

  <label for="last-name">Last Name:</label>
  <input type="text" id="last-name" name="last_name">
</fieldset>
```

### Key Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `disabled` | Boolean | Disables all form controls within the fieldset |
| `form` | Form ID | Associates fieldset with a form outside it (HTML5) |
| `name` | Text string | Names the fieldset (used for form submission grouping) |

### Fieldset Styling

```css
/* Remove default border */
fieldset {
  border: none;
  padding: 0;
  margin: 0;
}

/* Style legend */
legend {
  font-weight: bold;
  font-size: 1.2em;
  margin-bottom: 1rem;
}
```

---

## Examples

### Example 1: Radio Button Group with Fieldset

**Scenario:** Shipping method selection where fieldset groups related radio buttons.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shipping Method</title>
</head>
<body>
  <form action="/checkout" method="POST">
    <fieldset>
      <legend>Shipping Method <span aria-label="required">*</span></legend>

      <label>
        <input type="radio" name="shipping" value="standard" checked required>
        Standard Shipping (5-7 days) - Free
      </label>

      <label>
        <input type="radio" name="shipping" value="express" required>
        Express Shipping (2-3 days) - $9.99
      </label>

      <label>
        <input type="radio" name="shipping" value="overnight" required>
        Overnight Shipping (1 day) - $24.99
      </label>
    </fieldset>

    <button type="submit">Continue to Payment</button>
  </form>
</body>
</html>
```

**Result:** Radio buttons visually grouped with border and "Shipping Method" legend. Screen readers announce "Shipping Method, Standard Shipping" when focus enters the group.

---

### Example 2: Multi-Section Form with Multiple Fieldsets

**Scenario:** Registration form with separate sections for personal info, account info, and preferences.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registration Form</title>
  <style>
    fieldset { border: 1px solid #ccc; padding: 1rem; margin-bottom: 1.5rem; }
    legend { font-weight: bold; font-size: 1.1em; padding: 0 0.5rem; }
    label { display: block; margin-top: 0.75rem; }
    input, select { width: 100%; max-width: 400px; padding: 0.5rem; margin-top: 0.25rem; }
  </style>
</head>
<body>
  <h1>Create Account</h1>
  <form action="/register" method="POST">
    <!-- Personal Information -->
    <fieldset>
      <legend>Personal Information</legend>

      <label for="first-name">First Name: *</label>
      <input type="text" id="first-name" name="first_name" required>

      <label for="last-name">Last Name: *</label>
      <input type="text" id="last-name" name="last_name" required>

      <label for="dob">Date of Birth: *</label>
      <input type="date" id="dob" name="dob" required>
    </fieldset>

    <!-- Account Information -->
    <fieldset>
      <legend>Account Information</legend>

      <label for="email">Email: *</label>
      <input type="email" id="email" name="email" required>

      <label for="username">Username: *</label>
      <input type="text" id="username" name="username" required>

      <label for="password">Password: *</label>
      <input type="password" id="password" name="password" required>
    </fieldset>

    <!-- Preferences -->
    <fieldset>
      <legend>Communication Preferences</legend>

      <label>
        <input type="checkbox" name="newsletter" value="yes">
        Receive newsletter updates
      </label>

      <label>
        <input type="checkbox" name="promotions" value="yes">
        Receive special offers and promotions
      </label>
    </fieldset>

    <button type="submit">Create Account</button>
  </form>
</body>
</html>
```

**Result:** Three visually distinct sections (Personal, Account, Preferences) each with clear legends. Screen readers announce section context as users navigate through inputs.

---

### Example 3: Disabled Fieldset for Conditional Fields

**Scenario:** Billing address fieldset that's disabled when "Same as shipping" is checked.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Conditional Fieldset</title>
  <style>
    fieldset { border: 1px solid #ccc; padding: 1rem; margin: 1rem 0; }
    fieldset:disabled { opacity: 0.6; }
    legend { font-weight: bold; }
    label { display: block; margin-top: 0.5rem; }
    input[type="text"] { width: 100%; max-width: 300px; padding: 0.5rem; }
  </style>
</head>
<body>
  <form action="/checkout" method="POST">
    <!-- Shipping Address -->
    <fieldset id="shipping-address">
      <legend>Shipping Address</legend>

      <label for="ship-street">Street: *</label>
      <input type="text" id="ship-street" name="ship_street" required>

      <label for="ship-city">City: *</label>
      <input type="text" id="ship-city" name="ship_city" required>

      <label for="ship-zip">ZIP Code: *</label>
      <input type="text" id="ship-zip" name="ship_zip" pattern="[0-9]{5}" required>
    </fieldset>

    <!-- Same as shipping checkbox -->
    <label>
      <input type="checkbox" id="same-address" onchange="toggleBilling()">
      Billing address same as shipping
    </label>

    <!-- Billing Address (disabled when same as shipping) -->
    <fieldset id="billing-address">
      <legend>Billing Address</legend>

      <label for="bill-street">Street: *</label>
      <input type="text" id="bill-street" name="bill_street" required>

      <label for="bill-city">City: *</label>
      <input type="text" id="bill-city" name="bill_city" required>

      <label for="bill-zip">ZIP Code: *</label>
      <input type="text" id="bill-zip" name="bill_zip" pattern="[0-9]{5}" required>
    </fieldset>

    <button type="submit">Complete Order</button>
  </form>

  <script>
    function toggleBilling() {
      const checkbox = document.getElementById('same-address');
      const billingFieldset = document.getElementById('billing-address');

      if (checkbox.checked) {
        billingFieldset.disabled = true;
        // Remove required from disabled fields
        billingFieldset.querySelectorAll('input').forEach(input => {
          input.required = false;
        });
      } else {
        billingFieldset.disabled = false;
        // Re-add required to billing fields
        billingFieldset.querySelectorAll('input').forEach(input => {
          input.required = true;
        });
      }
    }
  </script>
</body>
</html>
```

**Result:** When "Same as shipping" is checked, entire billing fieldset becomes disabled (grayed out, all inputs non-interactive). Unchecking re-enables the fieldset.

---

## Common Use Cases

### Use Case 1: Contact Method Selection
**When:** Grouping radio buttons for contact preference.
**How:**
```html
<fieldset>
  <legend>Preferred Contact Method *</legend>
  <label><input type="radio" name="contact" value="email" required> Email</label>
  <label><input type="radio" name="contact" value="phone" required> Phone</label>
  <label><input type="radio" name="contact" value="sms" required> SMS</label>
</fieldset>
```
**Why:** Fieldset groups related radios. Screen readers announce "Preferred Contact Method, Email" for first option.

---

### Use Case 2: Multi-Checkbox Feature Selection
**When:** Survey or settings with multiple independent checkboxes.
**How:**
```html
<fieldset>
  <legend>Which features do you use? (select all that apply)</legend>
  <label><input type="checkbox" name="features[]" value="search"> Search</label>
  <label><input type="checkbox" name="features[]" value="filters"> Filters</label>
  <label><input type="checkbox" name="features[]" value="export"> Export</label>
</fieldset>
```
**Why:** Groups related checkboxes. Legend clarifies "select all that apply" instruction.

---

### Use Case 3: Address Input Group
**When:** Collecting street address with multiple related fields.
**How:**
```html
<fieldset>
  <legend>Mailing Address</legend>
  <label for="street">Street: *</label>
  <input type="text" id="street" name="street" required>

  <label for="city">City: *</label>
  <input type="text" id="city" name="city" required>

  <label for="state">State: *</label>
  <select id="state" name="state" required>
    <option value="">--Select--</option>
    <option value="CA">California</option>
    <option value="NY">New York</option>
  </select>

  <label for="zip">ZIP: *</label>
  <input type="text" id="zip" name="zip" pattern="[0-9]{5}" required>
</fieldset>
```
**Why:** Semantically groups related address fields. Screen readers announce "Mailing Address" context for all inputs.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | Full support since earliest versions |
| Firefox | All     | Full Support  | Full support since earliest versions |
| Safari  | All     | Full Support  | Full support (all versions) |
| Edge    | All     | Full Support  | Full support (all versions) |
| IE 11   | All     | Full Support  | Full support (all versions) |

**Fallback Strategy:**
```html
<!-- No fallback needed - universal support -->
<!-- Fieldset and legend are part of original HTML spec -->
```

**Can I Use Link:** Not needed - universal support across all browsers

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Use `<fieldset>` and `<legend>` for groups of related form controls
- Legend must be the first child of fieldset
- Legend text must be clear and descriptive

**Level AA Requirements:**
- Legend must have sufficient color contrast
- Disabled fieldsets should be clearly indicated (visual and programmatic)
- Complex forms should be divided into logical fieldsets

### Screen Reader Support

```html
<!-- Accessible fieldset with proper structure -->
<fieldset>
  <legend>
    Payment Method <span aria-label="required">*</span>
  </legend>

  <label>
    <input type="radio" name="payment" value="credit_card" required aria-required="true">
    Credit Card
  </label>

  <label>
    <input type="radio" name="payment" value="paypal" required aria-required="true">
    PayPal
  </label>
</fieldset>

<!-- Accessible disabled fieldset -->
<fieldset disabled aria-disabled="true">
  <legend>Premium Features (Upgrade Required)</legend>
  <label><input type="checkbox" name="feature1"> Advanced Analytics</label>
  <label><input type="checkbox" name="feature2"> Priority Support</label>
</fieldset>
```

**Key Points:**
- Screen readers announce legend text when entering fieldset
- Nested inputs inherit context: "Payment Method, Credit Card" (legend + label)
- `aria-disabled="true"` on fieldset announces disabled state
- Legend should be concise but descriptive

### Keyboard Navigation

- **Tab:** Moves through inputs within fieldset normally
- **Arrow Keys:** Navigate radio buttons within fieldset
- Fieldset structure doesn't change keyboard navigation behavior

---

## Best Practices

### Do This

1. **Group Related Radio Buttons**
   ```html
   <!-- GOOD: Radio buttons grouped by fieldset -->
   <fieldset>
     <legend>T-Shirt Size</legend>
     <label><input type="radio" name="size" value="s"> Small</label>
     <label><input type="radio" name="size" value="m"> Medium</label>
     <label><input type="radio" name="size" value="l"> Large</label>
   </fieldset>
   ```
   **Why:** Screen readers announce "T-Shirt Size" for each radio, providing context.

2. **Use Fieldset for Multi-Section Forms**
   ```html
   <!-- GOOD: Logical sections with fieldsets -->
   <form>
     <fieldset>
       <legend>Contact Information</legend>
       <!-- Name, email, phone -->
     </fieldset>

     <fieldset>
       <legend>Shipping Address</legend>
       <!-- Street, city, state, zip -->
     </fieldset>
   </form>
   ```
   **Why:** Breaks long forms into manageable sections. Improves both visual organization and accessibility.

3. **Keep Legend Concise**
   ```html
   <!-- GOOD: Short, clear legend -->
   <fieldset>
     <legend>Shipping Speed</legend>
     <label><input type="radio" name="speed" value="standard"> Standard (5-7 days)</label>
   </fieldset>
   ```
   **Why:** Screen readers repeat legend for each input. Long legends are annoying for screen reader users.

---

### Avoid This

1. **Fieldset Without Legend**
   ```html
   <!-- WRONG: Fieldset without legend -->
   <fieldset>
     <label><input type="radio" name="choice" value="1"> Option 1</label>
     <label><input type="radio" name="choice" value="2"> Option 2</label>
   </fieldset>
   ```
   **Why Not:** Legend is required for accessibility. Screen readers need context for the group.
   **Instead:**
   ```html
   <fieldset>
     <legend>Choose an option</legend>
     <label><input type="radio" name="choice" value="1"> Option 1</label>
   </fieldset>
   ```

2. **Nested Fieldsets (Usually)**
   ```html
   <!-- WRONG: Unnecessary nesting -->
   <fieldset>
     <legend>Payment</legend>
     <fieldset>
       <legend>Card Details</legend>
       <!-- Inputs -->
     </fieldset>
   </fieldset>
   ```
   **Why Not:** Confusing for screen readers. Rarely necessary. Creates overly complex structure.
   **Instead:** Use single-level fieldsets for each logical group.

3. **Using Div Instead of Fieldset**
   ```html
   <!-- WRONG: Div with class instead of fieldset -->
   <div class="form-group">
     <h3>Shipping Method</h3>
     <label><input type="radio" name="shipping" value="standard"> Standard</label>
   </div>
   ```
   **Why Not:** No semantic grouping. Screen readers don't associate heading with inputs.
   **Instead:**
   ```html
   <fieldset>
     <legend>Shipping Method</legend>
     <label><input type="radio" name="shipping" value="standard"> Standard</label>
   </fieldset>
   ```

---

## Related Topics

**Prerequisites:**
- [Form Element](form-element.md) - Understanding form structure
- [Checkboxes & Radio Buttons](checkboxes-radio.md) - Common fieldset use cases

**Related Concepts:**
- [Form Accessibility](form-accessibility.md) - WCAG-compliant forms
- [Form Buttons](form-buttons.md) - Submit buttons in fieldsets

**Next Steps:**
- [Form Attributes](form-attributes.md) - HTML5 form attributes
- [Form Accessibility](form-accessibility.md) - Complete accessibility guide

**External Resources:**
- [MDN - Fieldset Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)
- [MDN - Legend Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend)
- [W3C - Grouping Controls](https://www.w3.org/WAI/tutorials/forms/grouping/)

---

## Practice Exercise

### Challenge: Build a Survey Form with Multiple Fieldsets

**Objective:** Create a customer satisfaction survey with properly grouped questions using fieldsets and legends.

**Requirements:**
- [ ] Demographic info fieldset (age range radio buttons)
- [ ] Product experience fieldset (rating radio buttons 1-5)
- [ ] Features used fieldset (checkboxes for multiple features)
- [ ] Contact preference fieldset (email/phone/sms radios)
- [ ] All fieldsets must have descriptive legends
- [ ] Bonus: Add disabled fieldset for "Premium Features" survey

---

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Customer Survey</title>
</head>
<body>
  <h1>Customer Satisfaction Survey</h1>
  <form action="/survey" method="POST">
    <!-- Add your fieldsets here -->
    <button type="submit">Submit Survey</button>
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
  <title>Customer Survey</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 700px; margin: 2rem auto; padding: 0 1rem; }
    fieldset { border: 1px solid #ccc; padding: 1rem; margin-bottom: 1.5rem; }
    fieldset:disabled { opacity: 0.6; background: #f9f9f9; }
    legend { font-weight: bold; font-size: 1.1em; padding: 0 0.5rem; }
    label { display: block; margin: 0.5rem 0; }
    button { margin-top: 1rem; padding: 0.75rem 1.5rem; }
  </style>
</head>
<body>
  <h1>Customer Satisfaction Survey</h1>
  <form action="/survey" method="POST">
    <!-- Demographics -->
    <fieldset>
      <legend>Age Range <span aria-label="required">*</span></legend>
      <label><input type="radio" name="age" value="18-24" required> 18-24</label>
      <label><input type="radio" name="age" value="25-34" required> 25-34</label>
      <label><input type="radio" name="age" value="35-44" required> 35-44</label>
      <label><input type="radio" name="age" value="45-54" required> 45-54</label>
      <label><input type="radio" name="age" value="55+" required> 55+</label>
    </fieldset>

    <!-- Product Experience Rating -->
    <fieldset>
      <legend>How would you rate our product? <span aria-label="required">*</span></legend>
      <label><input type="radio" name="rating" value="1" required> 1 - Very Dissatisfied</label>
      <label><input type="radio" name="rating" value="2" required> 2 - Dissatisfied</label>
      <label><input type="radio" name="rating" value="3" required> 3 - Neutral</label>
      <label><input type="radio" name="rating" value="4" required> 4 - Satisfied</label>
      <label><input type="radio" name="rating" value="5" required> 5 - Very Satisfied</label>
    </fieldset>

    <!-- Features Used -->
    <fieldset>
      <legend>Which features have you used? (select all that apply)</legend>
      <label><input type="checkbox" name="features[]" value="search"> Search</label>
      <label><input type="checkbox" name="features[]" value="filters"> Advanced Filters</label>
      <label><input type="checkbox" name="features[]" value="export"> Data Export</label>
      <label><input type="checkbox" name="features[]" value="api"> API Integration</label>
      <label><input type="checkbox" name="features[]" value="mobile"> Mobile App</label>
    </fieldset>

    <!-- Contact Preference -->
    <fieldset>
      <legend>Preferred Contact Method <span aria-label="required">*</span></legend>
      <label><input type="radio" name="contact" value="email" required> Email</label>
      <label><input type="radio" name="contact" value="phone" required> Phone</label>
      <label><input type="radio" name="contact" value="sms" required> SMS</label>
      <label><input type="radio" name="contact" value="none" required> Do not contact me</label>
    </fieldset>

    <!-- Bonus: Disabled premium features fieldset -->
    <fieldset disabled aria-disabled="true">
      <legend>Premium Features Survey (Available for Premium Users Only)</legend>
      <label><input type="checkbox" name="premium_features[]" value="analytics"> Advanced Analytics</label>
      <label><input type="checkbox" name="premium_features[]" value="priority_support"> Priority Support</label>
      <label><input type="checkbox" name="premium_features[]" value="white_label"> White Label Options</label>
    </fieldset>

    <button type="submit">Submit Survey</button>
  </form>
</body>
</html>
```

**Explanation:** This survey uses four main fieldsets: age range (radio buttons for demographics), product rating (1-5 scale radios), features used (checkboxes for multi-select), and contact preference (radio buttons). Each has a descriptive legend. Bonus: disabled "Premium Features" fieldset shows how to visually and programmatically disable an entire section (all inputs become non-interactive).

</details>

---

### Expected Result

A complete survey form with 5 fieldsets, each visually grouped with borders and clear legends. Screen readers announce legend context for each input. Demographic, rating, and contact sections require selection. Features section allows multiple selections. Premium section is disabled (grayed out).

**Key Learnings:**
- When and how to use fieldsets for grouping
- Writing clear, concise legends
- Accessibility benefits of fieldset/legend for screen readers
- Using `disabled` attribute on fieldsets
- Organizing complex forms into logical sections

---

## Navigation

**Previous:** [Form Buttons](form-buttons.md)
**Next:** [Form Attributes](form-attributes.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
