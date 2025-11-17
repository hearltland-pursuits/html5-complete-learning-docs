---
title: Select & Datalist
category: Forms & Input
order: 6
---

# Select & Datalist

> **Quick Summary:** The `<select>` element creates dropdown menus for choosing from predefined options, while HTML5's `<datalist>` provides autocomplete suggestions for text inputs—combining the flexibility of free text with the convenience of preset options.

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

The `<select>` element has been part of HTML since the beginning, providing dropdown menus where users choose from a list of options. It's perfect for scenarios with a defined set of choices (countries, states, categories) where free-text input would be error-prone or impractical.

HTML5 introduced `<datalist>`, a hybrid approach that combines a text input with autocomplete suggestions. Users can either type freely OR select from suggestions—ideal for fields like city names, product searches, or skills where you want to suggest common options but allow custom entries.

Both elements improve form usability by reducing typing, preventing typos, and guiding users toward valid choices. The key difference: `<select>` restricts to predefined options only, while `<datalist>` allows any input with optional suggestions.

**Key Concept:** Use `<select>` when choices must be restricted to a specific list. Use `<datalist>` when you want to suggest options but allow custom user input.

---

## Basic Syntax

```html
<!-- Select dropdown (must choose from list) -->
<label for="country">Country:</label>
<select id="country" name="country">
  <option value="">--Please choose--</option>
  <option value="us">United States</option>
  <option value="ca">Canada</option>
  <option value="mx">Mexico</option>
</select>

<!-- Datalist autocomplete (free text + suggestions) -->
<label for="city">City:</label>
<input type="text" id="city" name="city" list="city-suggestions">
<datalist id="city-suggestions">
  <option value="New York">
  <option value="Los Angeles">
  <option value="Chicago">
</datalist>
```

### Key Attributes (Select)

| Attribute | Values | Description |
|-----------|--------|-------------|
| `name` | Text string | Form field name sent to server |
| `id` | Text string | Associates with label |
| `multiple` | Boolean | Allows selecting multiple options (Ctrl+click) |
| `size` | Number | Number of visible options (default 1 = dropdown) |
| `required` | Boolean | Makes selection mandatory |
| `disabled` | Boolean | Disables entire dropdown |

### Key Attributes (Option)

| Attribute | Values | Description |
|-----------|--------|-------------|
| `value` | Text string | Value sent to server when selected |
| `selected` | Boolean | Pre-selects this option |
| `disabled` | Boolean | Disables this specific option (grayed out) |

### Datalist Key Points

- Always pair with `<input>` using the `list` attribute
- Datalist `id` must match input's `list` value
- Provides suggestions but doesn't restrict input
- User can ignore suggestions and type anything

---

## Examples

### Example 1: Country Selector with Optgroups

**Scenario:** Multi-region country selector with grouped continents.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Country Selector</title>
</head>
<body>
  <form action="/submit" method="POST">
    <label for="country-select">Select your country: <span aria-label="required">*</span></label>
    <select id="country-select" name="country" required>
      <option value="">--Please choose--</option>

      <optgroup label="North America">
        <option value="us">United States</option>
        <option value="ca">Canada</option>
        <option value="mx">Mexico</option>
      </optgroup>

      <optgroup label="Europe">
        <option value="uk">United Kingdom</option>
        <option value="de">Germany</option>
        <option value="fr">France</option>
      </optgroup>

      <optgroup label="Asia">
        <option value="jp">Japan</option>
        <option value="cn">China</option>
        <option value="in">India</option>
      </optgroup>
    </select>

    <button type="submit">Continue</button>
  </form>
</body>
</html>
```

**Result:** Dropdown menu with grouped regions (North America, Europe, Asia). Empty option ensures user makes active choice. `required` prevents submission without selection.

---

### Example 2: Programming Language Selector (Multiple Select)

**Scenario:** Developer profile where user can select multiple programming languages.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Multiple Select</title>
</head>
<body>
  <form action="/profile" method="POST">
    <label for="languages">Programming Languages (hold Ctrl/Cmd to select multiple):</label>
    <select id="languages" name="languages[]" multiple size="6" required>
      <option value="javascript">JavaScript</option>
      <option value="python">Python</option>
      <option value="java">Java</option>
      <option value="csharp">C#</option>
      <option value="go">Go</option>
      <option value="rust">Rust</option>
      <option value="php">PHP</option>
    </select>

    <button type="submit">Save Profile</button>
  </form>
</body>
</html>
```

**Result:** List box showing 6 options at once. Users hold Ctrl (Windows) or Cmd (Mac) while clicking to select multiple. Server receives `languages[]=javascript&languages[]=python`.

---

### Example 3: City Input with Datalist Autocomplete

**Scenario:** Address form where users can type any city but get suggestions for common cities.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>City Autocomplete</title>
</head>
<body>
  <form action="/address" method="POST">
    <label for="city-input">City:</label>
    <input
      type="text"
      id="city-input"
      name="city"
      list="us-cities"
      placeholder="Start typing..."
      required>

    <datalist id="us-cities">
      <option value="New York">
      <option value="Los Angeles">
      <option value="Chicago">
      <option value="Houston">
      <option value="Phoenix">
      <option value="Philadelphia">
      <option value="San Antonio">
      <option value="San Diego">
      <option value="Dallas">
      <option value="San Jose">
    </datalist>

    <button type="submit">Save Address</button>
  </form>
</body>
</html>
```

**Result:** Text input with dropdown suggestions as user types. User can select "Chicago" from list OR type "Springfield" (not in list). Browser filters suggestions based on typed characters.

---

## Common Use Cases

### Use Case 1: Time Zone Selector
**When:** User account settings requiring time zone selection.
**How:**
```html
<label for="timezone">Time Zone:</label>
<select id="timezone" name="timezone" required>
  <option value="">--Select timezone--</option>
  <option value="America/New_York">Eastern Time (ET)</option>
  <option value="America/Chicago">Central Time (CT)</option>
  <option value="America/Denver">Mountain Time (MT)</option>
  <option value="America/Los_Angeles">Pacific Time (PT)</option>
</select>
```
**Why:** Time zones must be exact values (no free text). `<select>` ensures valid selection.

---

### Use Case 2: Browser/Search Autocomplete
**When:** Search box that suggests popular searches but allows any query.
**How:**
```html
<label for="search-query">Search:</label>
<input type="search" id="search-query" name="q" list="popular-searches">

<datalist id="popular-searches">
  <option value="HTML5 forms">
  <option value="CSS Grid layout">
  <option value="JavaScript promises">
  <option value="React hooks">
</datalist>
```
**Why:** Users can type anything (custom search) but see popular suggestions for convenience.

---

### Use Case 3: Quantity Dropdown (Small Fixed Set)
**When:** Product quantity selector with limited stock (1-10 items).
**How:**
```html
<label for="quantity">Quantity:</label>
<select id="quantity" name="quantity">
  <option value="1" selected>1</option>
  <option value="2">2</option>
  <option value="3">3</option>
  <option value="4">4</option>
  <option value="5">5</option>
  <option value="6">6</option>
  <option value="7">7</option>
  <option value="8">8</option>
  <option value="9">9</option>
  <option value="10">10</option>
</select>
```
**Why:** `<select>` is cleaner than `<input type="number">` for small, fixed ranges. Prevents typing errors.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | Datalist supported since Chrome 20+ |
| Firefox | All     | Full Support  | Datalist supported since Firefox 4+ |
| Safari  | 12.1+   | Full Support  | Earlier versions have partial datalist support |
| Edge    | All     | Full Support  | Full support (all versions) |
| IE 11   | 11      | Partial Support | Select works; datalist not supported |

**Fallback Strategy:**
```html
<!-- Select: No fallback needed (universal support) -->

<!-- Datalist: Gracefully degrades to regular text input in old browsers -->
<input type="text" name="city" list="cities">
<datalist id="cities">
  <option value="New York">
  <!-- Old browsers ignore <datalist>, input works as plain text field -->
</datalist>
```

**Can I Use Links:**
- [Select Element](https://caniuse.com/select) (universal support)
- [Datalist Element](https://caniuse.com/datalist)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- All `<select>` and `<input>` elements must have associated `<label>` elements
- Keyboard navigation must work (Arrow keys, Enter to select)
- Required fields must be clearly indicated

**Level AA Requirements:**
- Labels and options must have sufficient color contrast
- Error messages must be programmatically associated
- Multi-select instructions should be provided

### Screen Reader Support

```html
<!-- Accessible select dropdown -->
<label for="country-select">
  Country <span aria-label="required">*</span>
</label>
<select id="country-select" name="country" required aria-required="true">
  <option value="">--Please choose--</option>
  <option value="us">United States</option>
  <option value="ca">Canada</option>
</select>

<!-- Accessible datalist -->
<label for="skill-input">Skills:</label>
<input
  type="text"
  id="skill-input"
  name="skills"
  list="skill-suggestions"
  aria-describedby="skill-hint"
  autocomplete="off">

<small id="skill-hint">Start typing to see suggestions, or enter your own.</small>

<datalist id="skill-suggestions">
  <option value="JavaScript">
  <option value="Python">
  <option value="Java">
</datalist>
```

**Key Points:**
- `aria-required="true"` announces required selects
- `aria-describedby` links helpful instructions
- Datalists announce available suggestions to screen readers

### Keyboard Navigation

**Select Dropdown:**
- **Tab:** Moves focus to select element
- **Spacebar/Enter:** Opens dropdown
- **Arrow Keys (↑↓):** Navigate options
- **Enter:** Selects highlighted option
- **Escape:** Closes dropdown

**Datalist Input:**
- **Tab:** Moves focus to input
- **Type:** Filters suggestions dynamically
- **Arrow Keys (↑↓):** Navigate suggestions
- **Enter:** Selects suggestion or submits typed value

---

## Best Practices

### Do This

1. **Always Provide a Default Empty Option**
   ```html
   <!-- GOOD: Forces user to make active selection -->
   <select name="country" required>
     <option value="">--Please choose--</option>
     <option value="us">United States</option>
   </select>
   ```
   **Why:** Without empty option, first option is pre-selected, causing users to miss the field if it's already "selected".

2. **Use Meaningful Values for Options**
   ```html
   <!-- GOOD: Server receives clear, database-friendly values -->
   <option value="free_shipping">Free Shipping (5-7 days)</option>
   <option value="express">Express (2-3 days) - $9.99</option>
   ```
   **Why:** Value attribute should be machine-readable (database ID, code), while display text is human-readable.

3. **Group Related Options with Optgroup**
   ```html
   <select name="region">
     <optgroup label="North America">
       <option value="us">USA</option>
       <option value="ca">Canada</option>
     </optgroup>
     <optgroup label="Europe">
       <option value="uk">UK</option>
       <option value="de">Germany</option>
     </optgroup>
   </select>
   ```
   **Why:** Improves usability for long lists. Screen readers announce group context.

---

### Avoid This

1. **Hiding the First Option with CSS**
   ```html
   <!-- WRONG: Trying to hide default option -->
   <select>
     <option value="" style="display:none;">Choose...</option>
     <option value="1">Option 1</option>
   </select>
   ```
   **Why Not:** Breaks keyboard navigation in some browsers. Confuses screen readers.
   **Instead:**
   ```html
   <select>
     <option value="" disabled selected>Choose...</option>
     <option value="1">Option 1</option>
   </select>
   ```

2. **Using Multiple Select Without Instructions**
   ```html
   <!-- WRONG: Users don't know how to select multiple -->
   <select multiple>
     <option>Option 1</option>
     <option>Option 2</option>
   </select>
   ```
   **Why Not:** Many users don't know Ctrl/Cmd+click is required for multiple selections.
   **Instead:**
   ```html
   <label for="langs">Languages (hold Ctrl/Cmd to select multiple):</label>
   <select id="langs" multiple size="5">
     <!-- options -->
   </select>
   ```

3. **Datalist Without Fallback Hint**
   ```html
   <!-- WRONG: No indication that suggestions are available -->
   <input type="text" name="city" list="cities">
   <datalist id="cities">...</datalist>
   ```
   **Why Not:** Users may not realize suggestions exist. Some browsers don't show clear UI.
   **Instead:**
   ```html
   <input type="text" name="city" list="cities" placeholder="Start typing for suggestions...">
   <datalist id="cities">...</datalist>
   ```

---

## Related Topics

**Prerequisites:**
- [Form Element](form-element.md) - Understanding forms
- [Text Inputs](text-inputs.md) - Input basics

**Related Concepts:**
- [Checkboxes & Radio Buttons](checkboxes-radio.md) - Alternative selection methods
- [Form Validation](form-validation.md) - Validating selections
- [Form Accessibility](form-accessibility.md) - Accessible form design

**Next Steps:**
- [Textarea & File Inputs](textarea-file.md) - Multi-line text and file uploads
- [Form Buttons](form-buttons.md) - Submit and reset buttons

**External Resources:**
- [MDN - Select Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select)
- [MDN - Datalist Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist)
- [W3Schools - HTML Select](https://www.w3schools.com/tags/tag_select.asp)

---

## Practice Exercise

### Challenge: Build a Travel Booking Form

**Objective:** Create a travel form using select dropdowns and datalist autocomplete for destinations.

**Requirements:**
- [ ] Country selector with grouped regions (use `<optgroup>`)
- [ ] Departure city (datalist with 5+ suggestions, allows custom input)
- [ ] Number of travelers (select dropdown, 1-10)
- [ ] Travel class (select: Economy, Business, First)
- [ ] Bonus: Add month selector for travel date

---

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Travel Booking</title>
</head>
<body>
  <h1>Book Your Trip</h1>
  <form action="/book" method="POST">
    <!-- Add your select and datalist elements here -->
    <button type="submit">Search Flights</button>
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
  <title>Travel Booking</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 2rem auto; }
    label { display: block; margin-top: 1rem; font-weight: bold; }
    select, input { width: 100%; max-width: 400px; padding: 0.5rem; margin-top: 0.5rem; }
    button { margin-top: 1.5rem; padding: 0.75rem 1.5rem; }
  </style>
</head>
<body>
  <h1>Book Your Trip</h1>
  <form action="/book" method="POST">
    <!-- Country selector with regions -->
    <label for="destination-country">Destination Country: *</label>
    <select id="destination-country" name="country" required>
      <option value="">--Select destination--</option>

      <optgroup label="North America">
        <option value="us">United States</option>
        <option value="ca">Canada</option>
        <option value="mx">Mexico</option>
      </optgroup>

      <optgroup label="Europe">
        <option value="uk">United Kingdom</option>
        <option value="fr">France</option>
        <option value="it">Italy</option>
        <option value="de">Germany</option>
      </optgroup>

      <optgroup label="Asia">
        <option value="jp">Japan</option>
        <option value="th">Thailand</option>
        <option value="cn">China</option>
      </optgroup>
    </select>

    <!-- Departure city with datalist -->
    <label for="departure-city">Departure City: *</label>
    <input
      type="text"
      id="departure-city"
      name="departure"
      list="major-cities"
      placeholder="Start typing..."
      required>

    <datalist id="major-cities">
      <option value="New York, NY">
      <option value="Los Angeles, CA">
      <option value="Chicago, IL">
      <option value="Houston, TX">
      <option value="Miami, FL">
      <option value="Seattle, WA">
      <option value="Boston, MA">
    </datalist>

    <!-- Number of travelers -->
    <label for="travelers">Number of Travelers: *</label>
    <select id="travelers" name="num_travelers" required>
      <option value="1" selected>1 person</option>
      <option value="2">2 people</option>
      <option value="3">3 people</option>
      <option value="4">4 people</option>
      <option value="5">5 people</option>
      <option value="6">6 people</option>
      <option value="7">7 people</option>
      <option value="8">8 people</option>
      <option value="9">9 people</option>
      <option value="10">10 people</option>
    </select>

    <!-- Travel class -->
    <label for="travel-class">Travel Class: *</label>
    <select id="travel-class" name="class" required>
      <option value="">--Select class--</option>
      <option value="economy" selected>Economy</option>
      <option value="premium_economy">Premium Economy</option>
      <option value="business">Business</option>
      <option value="first">First Class</option>
    </select>

    <!-- Bonus: Travel month -->
    <label for="travel-month">Preferred Travel Month:</label>
    <input type="month" id="travel-month" name="travel_month" min="2025-01">

    <button type="submit">Search Flights</button>
  </form>
</body>
</html>
```

**Explanation:** This form combines `<select>` dropdowns for restricted choices (country with regions, travelers, class) and `<datalist>` for departure city (allows any city but suggests major ones). The country selector uses `<optgroup>` to organize regions. Travelers defaults to 1, and class defaults to Economy. Bonus month picker restricts to future months.

</details>

---

### Expected Result

A functional travel booking form with grouped country dropdown, autocomplete city input, traveler quantity selector, and class selector. Datalist provides suggestions while allowing custom city names.

**Key Learnings:**
- When to use `<select>` vs `<datalist>`
- Using `<optgroup>` to organize long dropdown lists
- Combining different selection methods in one form
- Providing default selections for better UX

---

## Navigation

**Previous:** [Checkboxes & Radio Buttons](checkboxes-radio.md)
**Next:** [Textarea & File Inputs](textarea-file.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
