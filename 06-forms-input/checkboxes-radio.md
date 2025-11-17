---
title: Checkboxes & Radio Buttons
category: Forms & Input
order: 5
---

# Checkboxes & Radio Buttons

> **Quick Summary:** Checkboxes (`type="checkbox"`) allow multiple selections, while radio buttons (`type="radio"`) force single-choice from a group. Both are essential for selection-based form inputs with built-in keyboard navigation and accessibility.

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

Checkboxes and radio buttons are fundamental form controls for selection-based input. **Checkboxes** allow users to select zero, one, or multiple options from a list (e.g., "Select all that apply: Email, SMS, Phone"). **Radio buttons** allow exactly one selection from a group of mutually exclusive options (e.g., "Shipping method: Standard, Express, Overnight").

The key difference: checkbox selections are independent (checking one doesn't uncheck others), while radio buttons within the same `name` group are mutually exclusive (selecting one automatically deselects others). This makes radio buttons perfect for required single-choice questions and checkboxes for optional multi-select scenarios.

Both input types use the `checked` attribute to set default selections and the `value` attribute to specify what data gets submitted to the server. Always wrap labels around checkboxes/radios or use `for`/`id` association to increase click target area and improve accessibility.

**Key Concept:** Use checkboxes for "select all that apply" scenarios. Use radio buttons for "choose exactly one" scenarios. Never use radio buttons alone—always provide at least 2 options in a group.

---

## Basic Syntax

```html
<!-- Checkbox (independent selections) -->
<input type="checkbox" id="agree" name="terms" value="accepted">
<label for="agree">I agree to terms</label>

<!-- Radio buttons (mutually exclusive group) -->
<input type="radio" id="option1" name="choice" value="1">
<label for="option1">Option 1</label>

<input type="radio" id="option2" name="choice" value="2">
<label for="option2">Option 2</label>
```

### Key Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `type` | `checkbox`, `radio` | Determines selection behavior |
| `name` | Text string | Groups radio buttons; identifies checkbox |
| `value` | Text string | Value sent to server when checked/selected |
| `checked` | Boolean | Pre-selects the input (default state) |
| `required` | Boolean | Makes checkbox/radio selection mandatory |
| `disabled` | Boolean | Disables input (not submitted, grayed out) |

### Important Concepts

- **Radio button groups:** All radios with the same `name` belong to one group (only one can be selected)
- **Checkbox independence:** Each checkbox has a unique `name` (or same name for array submission)
- **Value submission:** Only checked inputs send their `value` to the server
- **Label association:** Clicking the label toggles the input (improves UX)

---

## Examples

### Example 1: Newsletter Subscription Checkboxes

**Scenario:** User can subscribe to multiple newsletter types independently.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Newsletter Preferences</title>
</head>
<body>
  <form action="/subscribe" method="POST">
    <fieldset>
      <legend>Newsletter Subscriptions (select all that apply):</legend>

      <label>
        <input type="checkbox" name="newsletters[]" value="weekly" checked>
        Weekly Digest
      </label>

      <label>
        <input type="checkbox" name="newsletters[]" value="promotions">
        Special Offers & Promotions
      </label>

      <label>
        <input type="checkbox" name="newsletters[]" value="updates">
        Product Updates
      </label>
    </fieldset>

    <button type="submit">Save Preferences</button>
  </form>
</body>
</html>
```

**Result:** Users can select zero, one, two, or all three options. "Weekly Digest" is pre-selected (`checked`). Server receives array like `newsletters=[weekly, updates]` if first and third are checked.

---

### Example 2: Shipping Method Radio Buttons

**Scenario:** E-commerce checkout where user must choose exactly one shipping method.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shipping Selection</title>
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

**Result:** Exactly one option must be selected (enforced by `required` on first radio). Selecting "Express" automatically deselects "Standard". Server receives `shipping=express`.

---

### Example 3: Terms Agreement Checkbox (Required)

**Scenario:** User registration requiring agreement to terms and conditions.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registration Form</title>
</head>
<body>
  <form action="/register" method="POST">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>

    <label>
      <input type="checkbox" id="terms" name="agree_terms" value="yes" required>
      I agree to the <a href="/terms" target="_blank">Terms and Conditions</a> *
    </label>

    <label>
      <input type="checkbox" name="newsletter" value="yes">
      Send me occasional updates (optional)
    </label>

    <button type="submit">Create Account</button>
  </form>
</body>
</html>
```

**Result:** Form cannot be submitted unless terms checkbox is checked (`required`). Newsletter checkbox is optional. Server receives `agree_terms=yes&newsletter=yes` if both are checked.

---

## Common Use Cases

### Use Case 1: Survey with Multiple Answers
**When:** Collecting survey responses where multiple answers are allowed.
**How:**
```html
<fieldset>
  <legend>What features do you use? (select all that apply)</legend>
  <label><input type="checkbox" name="features[]" value="search"> Search</label>
  <label><input type="checkbox" name="features[]" value="notifications"> Notifications</label>
  <label><input type="checkbox" name="features[]" value="analytics"> Analytics</label>
</fieldset>
```
**Why:** `name="features[]"` sends an array to server. Users can select any combination.

---

### Use Case 2: Payment Method Selection
**When:** User must choose exactly one payment method.
**How:**
```html
<fieldset>
  <legend>Payment Method *</legend>
  <label><input type="radio" name="payment" value="credit_card" required> Credit Card</label>
  <label><input type="radio" name="payment" value="paypal" required> PayPal</label>
  <label><input type="radio" name="payment" value="bank_transfer" required> Bank Transfer</label>
</fieldset>
```
**Why:** Radio buttons ensure exactly one payment method is selected. `required` prevents form submission without selection.

---

### Use Case 3: Yes/No Question
**When:** Binary choice questions (account settings, preferences).
**How:**
```html
<fieldset>
  <legend>Enable two-factor authentication?</legend>
  <label><input type="radio" name="2fa" value="yes"> Yes</label>
  <label><input type="radio" name="2fa" value="no" checked> No (default)</label>
</fieldset>
```
**Why:** Radio buttons are better than checkboxes for yes/no because they make both options explicit and visible.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | Full support since earliest versions |
| Firefox | All     | Full Support  | Full support since earliest versions |
| Safari  | All     | Full Support  | Full support since earliest versions |
| Edge    | All     | Full Support  | Full support (all versions) |
| IE 11   | All     | Full Support  | Full support (all versions) |

**Fallback Strategy:**
```html
<!-- No fallback needed - checkboxes and radio buttons are universally supported -->
<!-- Always provide labels for better accessibility and UX -->
```

**Can I Use Link:** Not needed - universal support across all browsers

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- All checkboxes/radios must have associated `<label>` elements
- Related checkboxes/radios should be grouped in `<fieldset>` with `<legend>`
- Keyboard navigation must work (Spacebar to toggle, Arrow keys for radios)

**Level AA Requirements:**
- Labels must have sufficient color contrast (4.5:1)
- Required selections must be clearly indicated (visual and programmatic)
- Error messages must be associated with the group

### Screen Reader Support

```html
<!-- Accessible radio button group -->
<fieldset>
  <legend>Preferred Contact Method <span aria-label="required">*</span></legend>

  <label for="contact-email">
    <input type="radio" id="contact-email" name="contact_method" value="email" required aria-required="true">
    Email
  </label>

  <label for="contact-phone">
    <input type="radio" id="contact-phone" name="contact_method" value="phone" required aria-required="true">
    Phone
  </label>
</fieldset>

<!-- Accessible checkbox with description -->
<label for="marketing">
  <input type="checkbox" id="marketing" name="marketing_consent" value="yes" aria-describedby="marketing-hint">
  I consent to marketing communications
</label>
<small id="marketing-hint">You can unsubscribe at any time.</small>
```

**Key Points:**
- `<fieldset>` and `<legend>` group related inputs for screen readers
- `aria-required="true"` announces required selections
- `aria-describedby` links additional context to checkboxes/radios

### Keyboard Navigation

**Checkboxes:**
- **Tab:** Moves focus to next checkbox
- **Spacebar:** Toggles checked/unchecked state
- **Shift + Tab:** Moves focus to previous checkbox

**Radio Buttons:**
- **Tab:** Moves focus into/out of radio group
- **Arrow Keys (↑↓←→):** Cycles through radio options within group
- **Spacebar:** Selects focused radio button

---

## Best Practices

### Do This

1. **Always Use Labels**
   ```html
   <!-- GOOD: Label increases click area -->
   <label>
     <input type="checkbox" name="remember" value="yes">
     Remember me
   </label>

   <!-- GOOD: Alternative with for/id -->
   <input type="checkbox" id="subscribe" name="subscribe" value="yes">
   <label for="subscribe">Subscribe to newsletter</label>
   ```
   **Why:** Labels make inputs easier to click (larger target area) and improve accessibility.

2. **Group Related Radio Buttons with Fieldset**
   ```html
   <fieldset>
     <legend>Shipping Speed</legend>
     <label><input type="radio" name="speed" value="standard"> Standard</label>
     <label><input type="radio" name="speed" value="express"> Express</label>
   </fieldset>
   ```
   **Why:** Screen readers announce the group context, helping users understand the choices.

3. **Provide Default Selection for Radio Buttons**
   ```html
   <label><input type="radio" name="size" value="medium" checked> Medium (recommended)</label>
   <label><input type="radio" name="size" value="large"> Large</label>
   ```
   **Why:** Radio buttons should always have a default selected. Prevents confusing "no selection" state.

---

### Avoid This

1. **Single Radio Button**
   ```html
   <!-- WRONG: Single radio button is confusing -->
   <label><input type="radio" name="agree" value="yes"> I agree</label>
   ```
   **Why Not:** Radio buttons are for groups. User can't deselect once selected.
   **Instead:**
   ```html
   <!-- Use checkbox for single yes/no -->
   <label><input type="checkbox" name="agree" value="yes"> I agree</label>
   ```

2. **Missing name Attribute on Radio Group**
   ```html
   <!-- WRONG: Different names = not a group -->
   <label><input type="radio" name="option1" value="1"> Option 1</label>
   <label><input type="radio" name="option2" value="2"> Option 2</label>
   ```
   **Why Not:** These radios don't form a group, so both can be selected simultaneously.
   **Instead:**
   ```html
   <label><input type="radio" name="choice" value="1"> Option 1</label>
   <label><input type="radio" name="choice" value="2"> Option 2</label>
   ```

3. **Using Checkboxes for Mutually Exclusive Options**
   ```html
   <!-- WRONG: Checkboxes allow multiple selections -->
   <label><input type="checkbox" name="size" value="small"> Small</label>
   <label><input type="checkbox" name="size" value="large"> Large</label>
   ```
   **Why Not:** User can select both sizes, which doesn't make sense.
   **Instead:**
   ```html
   <label><input type="radio" name="size" value="small"> Small</label>
   <label><input type="radio" name="size" value="large"> Large</label>
   ```

---

## Related Topics

**Prerequisites:**
- [Form Element](form-element.md) - Understanding forms
- [Text Inputs](text-inputs.md) - Basic input concepts

**Related Concepts:**
- [Fieldsets](fieldsets.md) - Grouping form elements
- [Form Accessibility](form-accessibility.md) - WCAG-compliant forms
- [Select & Datalist](select-datalist.md) - Alternative selection methods

**Next Steps:**
- [Select & Datalist](select-datalist.md) - Dropdown menus
- [Form Validation](form-validation.md) - Validating selections

**External Resources:**
- [MDN - Checkbox Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)
- [MDN - Radio Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)
- [W3Schools - HTML Input Types](https://www.w3schools.com/html/html_form_input_types.asp)

---

## Practice Exercise

### Challenge: Build a Survey Form

**Objective:** Create a survey with checkbox multi-select questions and radio button single-choice questions.

**Requirements:**
- [ ] Question 1: "What topics interest you?" (checkboxes, 4+ options)
- [ ] Question 2: "Experience level?" (radio buttons, 3 options with default)
- [ ] Question 3: "Agree to share responses?" (required checkbox)
- [ ] Use fieldsets with legends for grouping
- [ ] Bonus: Add "Other (please specify)" text input option

---

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Survey Form</title>
</head>
<body>
  <h1>Developer Survey</h1>
  <form action="/submit-survey" method="POST">
    <!-- Add your questions here -->
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
  <title>Developer Survey</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 2rem auto; padding: 0 1rem; }
    fieldset { margin-bottom: 1.5rem; border: 1px solid #ccc; padding: 1rem; }
    legend { font-weight: bold; }
    label { display: block; margin: 0.5rem 0; }
    input[type="text"] { margin-left: 1.5rem; width: 200px; }
  </style>
</head>
<body>
  <h1>Developer Survey</h1>
  <form action="/submit-survey" method="POST">
    <!-- Question 1: Checkboxes -->
    <fieldset>
      <legend>What topics interest you? (select all that apply)</legend>
      <label><input type="checkbox" name="topics[]" value="frontend"> Frontend Development</label>
      <label><input type="checkbox" name="topics[]" value="backend"> Backend Development</label>
      <label><input type="checkbox" name="topics[]" value="devops"> DevOps & Cloud</label>
      <label><input type="checkbox" name="topics[]" value="ai"> AI & Machine Learning</label>
      <label><input type="checkbox" name="topics[]" value="mobile"> Mobile Development</label>
    </fieldset>

    <!-- Question 2: Radio buttons -->
    <fieldset>
      <legend>Experience Level <span aria-label="required">*</span></legend>
      <label><input type="radio" name="experience" value="beginner" required> Beginner (0-1 years)</label>
      <label><input type="radio" name="experience" value="intermediate" checked required> Intermediate (2-5 years)</label>
      <label><input type="radio" name="experience" value="advanced" required> Advanced (5+ years)</label>
    </fieldset>

    <!-- Question 3: Required agreement -->
    <fieldset>
      <legend>Data Sharing</legend>
      <label>
        <input type="checkbox" name="share_consent" value="yes" required>
        I agree to share my anonymous responses for research purposes *
      </label>
    </fieldset>

    <!-- Bonus: Other option -->
    <fieldset>
      <legend>Additional Comments (optional)</legend>
      <label>
        <input type="checkbox" id="has-other" name="has_other" value="yes">
        I have additional topics to suggest
      </label>
      <input type="text" id="other-text" name="other_topics" placeholder="Please specify..." aria-label="Specify other topics">
    </fieldset>

    <button type="submit">Submit Survey</button>
  </form>
</body>
</html>
```

**Explanation:** This survey uses checkboxes for multi-select (topics), radio buttons for single-choice with default (experience level), and a required checkbox for consent. Fieldsets group related questions. The bonus "other" checkbox enables a text input for additional suggestions.

</details>

---

### Expected Result

A complete survey form with proper grouping, labels, and accessibility. Topics allow multiple selections, experience requires exactly one selection with "Intermediate" pre-selected, and consent checkbox must be checked to submit.

**Key Learnings:**
- When to use checkboxes vs radio buttons
- Grouping related inputs with fieldset/legend
- Making selections required
- Using name="array[]" for checkbox groups

---

## Navigation

**Previous:** [Date & Time Inputs](date-time.md)
**Next:** [Select & Datalist](select-datalist.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
