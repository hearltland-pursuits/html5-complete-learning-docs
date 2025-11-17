---
title: Number & Range Inputs
category: Forms & Input
order: 3
---

# Number & Range Inputs

> **Quick Summary:** HTML5 introduced `type="number"` and `type="range"` for numeric input, providing built-in validation, increment/decrement controls, mobile numeric keyboards, and accessible slider controls without JavaScript.

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

Before HTML5, collecting numeric input required generic text fields with JavaScript validation. HTML5 introduced two powerful input types for numbers: **`type="number"`** for precise numeric values (e.g., quantity, age, price) and **`type="range"`** for approximate values on a slider (e.g., volume, brightness, rating).

The `number` input provides spinner controls (up/down arrows), validates that the value is a number, and shows a numeric keyboard on mobile devices. The `range` input displays a visual slider that users can drag, making it perfect for settings where the exact number matters less than the relative position (e.g., "loud" vs "73% volume").

Both inputs support `min`, `max`, and `step` attributes for fine-grained control over acceptable values. For example, a price input might allow values from 0.00 to 10,000.00 in increments of 0.01, while a rating slider might allow values from 1 to 5 in whole number steps.

**Key Concept:** Use `type="number"` when the exact numeric value matters (quantity, age, price). Use `type="range"` when approximate values are sufficient and visual feedback improves UX (volume, brightness, ratings).

---

## Basic Syntax

```html
<!-- Number input with spinner controls -->
<input type="number" name="quantity" min="1" max="100" step="1" value="1">

<!-- Range input (slider) -->
<input type="range" name="volume" min="0" max="100" step="1" value="50">
```

### Key Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `type` | `number`, `range` | Determines numeric input style |
| `min` | Number | Minimum allowed value |
| `max` | Number | Maximum allowed value |
| `step` | Number, `any` | Increment value (e.g., `0.01` for decimals, `1` for integers) |
| `value` | Number | Default/initial value |
| `placeholder` | Text | Hint text (number input only) |
| `required` | Boolean | Makes field mandatory |
| `readonly` | Boolean | Prevents editing but shows value |
| `disabled` | Boolean | Disables input (value not submitted) |

### Common Attribute Combinations

- **Integers (whole numbers):** `step="1"` (default)
- **Decimals (two places):** `step="0.01"` (e.g., currency)
- **Any decimal:** `step="any"` (allows any precision)
- **Percentage slider:** `min="0" max="100" step="1"`
- **Star rating:** `min="1" max="5" step="1"`

---

## Examples

### Example 1: Product Quantity Selector (Number Input)

**Scenario:** E-commerce product page where users select quantity to purchase.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quantity Selector</title>
</head>
<body>
  <form action="/add-to-cart" method="POST">
    <label for="product-qty">Quantity:</label>
    <input
      type="number"
      id="product-qty"
      name="quantity"
      min="1"
      max="99"
      step="1"
      value="1"
      required>

    <button type="submit">Add to Cart</button>
  </form>
</body>
</html>
```

**Result:** Users see spinner controls (arrows) to increase/decrease quantity. Mobile shows numeric keyboard. Browser validates that quantity is between 1-99 and is a whole number. Default value is 1.

---

### Example 2: Price Input with Decimal Support

**Scenario:** Form for sellers to enter product prices with cents.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Price Input</title>
</head>
<body>
  <form action="/submit-price" method="POST">
    <label for="item-price">Item Price (USD):</label>
    <input
      type="number"
      id="item-price"
      name="price"
      min="0.01"
      max="10000.00"
      step="0.01"
      placeholder="0.00"
      required
      aria-describedby="price-hint">

    <small id="price-hint">Enter price with cents (e.g., 19.99)</small>

    <button type="submit">Save Price</button>
  </form>
</body>
</html>
```

**Result:** `step="0.01"` allows two decimal places (e.g., 19.99). Browser validates that the price is between $0.01 and $10,000.00 and is a valid decimal number.

---

### Example 3: Volume Slider with Live Display (Range Input)

**Scenario:** Audio player with volume control showing current volume percentage.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Volume Slider</title>
  <style>
    .volume-control { margin: 2rem; }
    #volume-slider { width: 300px; }
    #volume-display { font-size: 1.5rem; font-weight: bold; }
  </style>
</head>
<body>
  <div class="volume-control">
    <label for="volume-slider">Volume:</label>
    <input
      type="range"
      id="volume-slider"
      name="volume"
      min="0"
      max="100"
      step="1"
      value="50"
      aria-valuemin="0"
      aria-valuemax="100"
      aria-valuenow="50"
      aria-label="Volume control">

    <output id="volume-display" for="volume-slider">50%</output>
  </div>

  <script>
    const slider = document.getElementById('volume-slider');
    const display = document.getElementById('volume-display');

    slider.addEventListener('input', function() {
      display.textContent = this.value + '%';
      slider.setAttribute('aria-valuenow', this.value);
    });
  </script>
</body>
</html>
```

**Result:** Visual slider that users can drag from 0-100. The `<output>` element displays the current value in real-time. Screen readers announce value changes via `aria-valuenow`.

**Notes:**
- `<output>` is semantic HTML5 element for displaying calculation results
- ARIA attributes make the slider accessible to screen readers
- JavaScript updates display in real-time as user drags slider

---

## Common Use Cases

### Use Case 1: Age Input with Validation
**When:** Collecting user age with realistic min/max constraints.
**How:**
```html
<label for="user-age">Age:</label>
<input
  type="number"
  id="user-age"
  name="age"
  min="13"
  max="120"
  step="1"
  required
  aria-describedby="age-requirement">

<small id="age-requirement">You must be at least 13 years old.</small>
```
**Why:** Validates age is between 13-120 (realistic range), prevents decimals with `step="1"`, shows helpful message about minimum age requirement.

---

### Use Case 2: Star Rating Slider
**When:** Collecting product/service ratings on a 1-5 star scale.
**How:**
```html
<label for="rating">Rate this product:</label>
<input
  type="range"
  id="rating"
  name="rating"
  min="1"
  max="5"
  step="1"
  value="3"
  list="star-labels"
  aria-label="Rate from 1 to 5 stars">

<datalist id="star-labels">
  <option value="1" label="Poor"></option>
  <option value="2" label="Fair"></option>
  <option value="3" label="Good"></option>
  <option value="4" label="Very Good"></option>
  <option value="5" label="Excellent"></option>
</datalist>

<output id="rating-display" for="rating">3 stars</output>
```
**Why:** Range slider provides intuitive visual feedback. `<datalist>` adds labels at each step (browser support varies). Middle value (3) as default avoids bias.

---

### Use Case 3: Donation Amount with Preset Increments
**When:** Charity donation form with suggested amounts.
**How:**
```html
<label for="donation">Donation Amount (USD):</label>
<input
  type="number"
  id="donation"
  name="amount"
  min="1"
  max="100000"
  step="5"
  value="25"
  required>

<small>Suggested amounts: $10, $25, $50, $100</small>
```
**Why:** `step="5"` increments by $5 when using spinner controls, guiding users toward suggested amounts while still allowing custom values.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 7+      | Full Support  | Full support for number and range inputs |
| Firefox | 29+     | Full Support  | Range input supported since Firefox 23+ |
| Safari  | 5+      | Full Support  | Full HTML5 numeric input support |
| Edge    | All     | Full Support  | Full support (all versions) |
| IE 11   | 11      | Partial Support | Number input works; range falls back to text |

**Fallback Strategy:**
```html
<!-- Modern browsers: Number input with validation -->
<!-- IE 10 and older: Falls back to text input -->
<input type="number" name="quantity" min="1" max="99" pattern="[0-9]+" required>

<!-- For range input, provide text fallback with JavaScript polyfill -->
<input type="range" name="volume" min="0" max="100" value="50">
<noscript>
  <input type="number" name="volume" min="0" max="100" value="50">
</noscript>
```

**Can I Use Links:**
- [Number Input](https://caniuse.com/input-number)
- [Range Input](https://caniuse.com/input-range)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- All inputs must have associated `<label>` elements
- Inputs must be keyboard-accessible (Tab, arrow keys for range)
- Required fields must be clearly indicated

**Level AA Requirements:**
- Labels must have sufficient color contrast (4.5:1)
- Range sliders must announce current value to screen readers
- Error messages for invalid numbers must be programmatically associated

### Screen Reader Support

```html
<!-- Accessible number input -->
<label for="quantity-input">
  Quantity <span aria-label="required">*</span>
</label>
<input
  type="number"
  id="quantity-input"
  name="quantity"
  min="1"
  max="100"
  required
  aria-required="true"
  aria-describedby="quantity-hint">

<small id="quantity-hint">Enter a number between 1 and 100</small>

<!-- Accessible range slider -->
<label for="brightness-slider">Screen Brightness:</label>
<input
  type="range"
  id="brightness-slider"
  name="brightness"
  min="0"
  max="100"
  value="75"
  aria-valuemin="0"
  aria-valuemax="100"
  aria-valuenow="75"
  aria-label="Adjust screen brightness from 0 to 100 percent">

<output id="brightness-value" for="brightness-slider">75%</output>
```

**Key Points:**
- `aria-required="true"` announces required numeric fields
- Range sliders need `aria-valuemin`, `aria-valuemax`, `aria-valuenow` for screen reader support
- Use `<output>` element to display current range value visually

### Keyboard Navigation

**Number Input:**
- **Tab:** Moves focus to/from input
- **Up Arrow:** Increases value by `step` amount
- **Down Arrow:** Decreases value by `step` amount
- **Page Up:** Large increase (10× step in some browsers)
- **Page Down:** Large decrease (10× step in some browsers)

**Range Input:**
- **Tab:** Moves focus to/from slider
- **Left/Down Arrow:** Decreases value by `step` amount
- **Right/Up Arrow:** Increases value by `step` amount
- **Home:** Jumps to minimum value
- **End:** Jumps to maximum value

---

## Best Practices

### Do This

1. **Set Realistic Min, Max, and Step**
   ```html
   <!-- GOOD: Realistic age constraints -->
   <input type="number" name="age" min="13" max="120" step="1">

   <!-- GOOD: Price with cents -->
   <input type="number" name="price" min="0.01" step="0.01">
   ```
   **Why:** Prevents invalid input (negative ages, prices with more than 2 decimals) and guides user input with appropriate increments.

2. **Use Range for Approximate Values, Number for Exact Values**
   ```html
   <!-- GOOD: Range for volume (approximate) -->
   <input type="range" name="volume" min="0" max="100">

   <!-- GOOD: Number for quantity (exact) -->
   <input type="number" name="quantity" min="1" max="99">
   ```
   **Why:** Range sliders work best when users don't need to know the exact number (volume at "75" vs "loud"). Number inputs work best when precision matters (ordering exactly 3 items).

3. **Display Current Value for Range Sliders**
   ```html
   <label for="zoom-slider">Zoom Level:</label>
   <input type="range" id="zoom-slider" min="50" max="200" value="100">
   <output id="zoom-value" for="zoom-slider">100%</output>

   <script>
     const slider = document.getElementById('zoom-slider');
     const output = document.getElementById('zoom-value');
     slider.addEventListener('input', () => {
       output.textContent = slider.value + '%';
     });
   </script>
   ```
   **Why:** Range sliders don't show the current value by default. Displaying it improves UX and accessibility.

---

### Avoid This

1. **Using Number Input for Non-Numeric Data**
   ```html
   <!-- WRONG: Credit card numbers aren't mathematical values -->
   <input type="number" name="credit_card">
   ```
   **Why Not:** Number inputs can strip leading zeros (0123 becomes 123), don't support formatting (spaces/hyphens), and encourage mathematical operations on non-math data.
   **Instead:**
   ```html
   <input type="text" name="credit_card" inputmode="numeric" pattern="[0-9]{13,19}">
   ```

2. **Forgetting Step for Decimal Values**
   ```html
   <!-- WRONG: Default step="1" prevents decimals -->
   <input type="number" name="price" min="0" max="1000">
   ```
   **Why Not:** User can't enter 19.99 because default `step="1"` only allows whole numbers. Browser shows validation error for decimal input.
   **Instead:**
   ```html
   <input type="number" name="price" min="0" max="1000" step="0.01">
   ```

3. **Using Range Without Accessible Labels**
   ```html
   <!-- WRONG: Screen readers can't announce current value -->
   <input type="range" name="volume" min="0" max="100">
   ```
   **Why Not:** Screen reader users hear "slider" but don't know current value or purpose.
   **Instead:**
   ```html
   <label for="volume">Volume:</label>
   <input type="range" id="volume" name="volume" min="0" max="100"
          aria-valuemin="0" aria-valuemax="100" aria-valuenow="50">
   <output for="volume">50%</output>
   ```

---

## Related Topics

**Prerequisites (Learn These First):**
- [Form Element](form-element.md) - Understanding form structure
- [Text Inputs](text-inputs.md) - Basic input concepts

**Related Concepts:**
- [Form Validation](form-validation.md) - How min/max/step affect validation
- [Form Attributes](form-attributes.md) - Additional HTML5 input attributes
- [Date & Time Inputs](date-time.md) - Other specialized HTML5 inputs

**Next Steps (Learn These Next):**
- [Date & Time Inputs](date-time.md) - HTML5 date and time pickers
- [Checkboxes & Radio Buttons](checkboxes-radio.md) - Selection inputs

**External Resources:**
- [MDN Web Docs - Number Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number)
- [MDN Web Docs - Range Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range)
- [W3Schools - HTML Input Types](https://www.w3schools.com/html/html_form_input_types.asp)

---

## Practice Exercise

### Challenge: Build a Product Customization Form

**Objective:** Create a form for customizing a product order with quantity selector, price calculator, and quality slider.

**Requirements:**
- [ ] Quantity selector (1-50, whole numbers only)
- [ ] Price per unit input ($0.01 - $999.99 with cents)
- [ ] Quality slider (1-5, where 1=Basic, 5=Premium) with live display
- [ ] Calculate and display total price (quantity × price) using JavaScript
- [ ] Bonus: Add delivery time estimate slider (1-30 days)

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Customization</title>
</head>
<body>
  <h1>Customize Your Order</h1>
  <form action="/submit-order" method="POST">
    <!-- Add your numeric inputs here -->
    <button type="submit">Place Order</button>
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
  <title>Product Customization</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 2rem auto; padding: 0 1rem; }
    label { display: block; margin-top: 1.5rem; font-weight: bold; }
    input[type="number"], input[type="range"] { width: 100%; max-width: 400px; margin-top: 0.5rem; }
    input[type="range"] { width: 300px; }
    output { display: inline-block; margin-left: 1rem; font-weight: bold; color: #0066cc; }
    #total-price { font-size: 1.5rem; color: #006600; margin-top: 1rem; }
    button { margin-top: 2rem; padding: 0.75rem 1.5rem; font-size: 1rem; }
  </style>
</head>
<body>
  <h1>Customize Your Order</h1>
  <form action="/submit-order" method="POST">
    <!-- Quantity selector -->
    <label for="quantity">Quantity:</label>
    <input
      type="number"
      id="quantity"
      name="quantity"
      min="1"
      max="50"
      step="1"
      value="1"
      required
      aria-describedby="quantity-hint">
    <small id="quantity-hint">How many units? (1-50)</small>

    <!-- Price per unit -->
    <label for="unit-price">Price per Unit ($):</label>
    <input
      type="number"
      id="unit-price"
      name="price"
      min="0.01"
      max="999.99"
      step="0.01"
      value="10.00"
      required
      aria-describedby="price-hint">
    <small id="price-hint">Enter price with cents (e.g., 10.00)</small>

    <!-- Quality slider -->
    <label for="quality-slider">Quality Level:</label>
    <input
      type="range"
      id="quality-slider"
      name="quality"
      min="1"
      max="5"
      step="1"
      value="3"
      aria-valuemin="1"
      aria-valuemax="5"
      aria-valuenow="3"
      aria-label="Select quality from 1 (Basic) to 5 (Premium)">
    <output id="quality-display" for="quality-slider">Good (3)</output>

    <!-- Delivery time slider (bonus) -->
    <label for="delivery-slider">Delivery Time (days):</label>
    <input
      type="range"
      id="delivery-slider"
      name="delivery_days"
      min="1"
      max="30"
      step="1"
      value="7"
      aria-valuemin="1"
      aria-valuemax="30"
      aria-valuenow="7"
      aria-label="Select delivery time from 1 to 30 days">
    <output id="delivery-display" for="delivery-slider">7 days</output>

    <!-- Total price calculation -->
    <div id="total-price">Total: $10.00</div>

    <button type="submit">Place Order</button>
  </form>

  <script>
    // Get elements
    const quantityInput = document.getElementById('quantity');
    const priceInput = document.getElementById('unit-price');
    const qualitySlider = document.getElementById('quality-slider');
    const qualityDisplay = document.getElementById('quality-display');
    const deliverySlider = document.getElementById('delivery-slider');
    const deliveryDisplay = document.getElementById('delivery-display');
    const totalPriceDisplay = document.getElementById('total-price');

    // Quality level labels
    const qualityLabels = ['', 'Basic', 'Fair', 'Good', 'Very Good', 'Premium'];

    // Update total price
    function updateTotal() {
      const quantity = parseFloat(quantityInput.value) || 1;
      const price = parseFloat(priceInput.value) || 0;
      const total = (quantity * price).toFixed(2);
      totalPriceDisplay.textContent = `Total: $${total}`;
    }

    // Update quality display
    qualitySlider.addEventListener('input', function() {
      const value = this.value;
      qualityDisplay.textContent = `${qualityLabels[value]} (${value})`;
      qualitySlider.setAttribute('aria-valuenow', value);
    });

    // Update delivery display
    deliverySlider.addEventListener('input', function() {
      const value = this.value;
      deliveryDisplay.textContent = `${value} day${value > 1 ? 's' : ''}`;
      deliverySlider.setAttribute('aria-valuenow', value);
    });

    // Update total on quantity/price change
    quantityInput.addEventListener('input', updateTotal);
    priceInput.addEventListener('input', updateTotal);

    // Initialize displays
    updateTotal();
  </script>
</body>
</html>
```

**Explanation:**
This form combines `type="number"` for precise values (quantity, price) and `type="range"` for approximate values (quality, delivery time). JavaScript calculates total price in real-time, displays quality labels ("Basic" through "Premium"), and shows delivery time. ARIA attributes ensure screen reader accessibility for sliders. The `step="0.01"` on price allows cents input, while `step="1"` on quantity/sliders enforces whole numbers.

</details>

---

### Expected Result

**Visual Outcome:** A functional product customization form with two number inputs (with spinner controls), two range sliders (visual sliders), and real-time total price calculation. Quality slider shows text labels like "Good (3)" and delivery slider shows "7 days".

**Key Learnings:**
- When to use `type="number"` vs `type="range"`
- How `min`, `max`, and `step` control input validation
- Using `<output>` element to display calculated values
- Combining JavaScript with HTML5 inputs for dynamic UX
- Making range sliders accessible with ARIA attributes

---

## Navigation

**Previous:** [Text Inputs](text-inputs.md)
**Next:** [Date & Time Inputs](date-time.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
