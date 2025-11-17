---
title: Date & Time Inputs
category: Forms & Input
order: 4
---

# Date & Time Inputs

> **Quick Summary:** HTML5 date and time input types (`date`, `time`, `datetime-local`, `month`, `week`) provide native date/time pickers, automatic validation, and consistent formatting without third-party JavaScript libraries.

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

Before HTML5, collecting dates and times required text inputs with complex JavaScript date pickers or third-party libraries. HTML5 introduced **five native date/time input types** that provide built-in calendar/time pickers, automatic format validation, and consistent data handling across browsers.

The five types are: `date` (calendar picker for year-month-day), `time` (clock picker for hours:minutes), `datetime-local` (combined date + time), `month` (month picker for year-month), and `week` (week picker for year-week number). Each returns data in ISO 8601 format (e.g., "2025-03-15" for dates), making server-side processing predictable.

These inputs are particularly powerful on mobile devices, where they trigger native date/time pickers optimized for touch input. Desktop browsers show customizable calendar widgets. The browser handles all formatting and validation automatically—no JavaScript required.

**Key Concept:** HTML5 date/time inputs provide free, accessible, mobile-optimized date pickers with automatic validation and ISO 8601 formatting—eliminating the need for heavy JavaScript libraries.

---

## Basic Syntax

```html
<!-- Date picker (calendar) -->
<input type="date" name="birthday" min="1900-01-01" max="2025-12-31">

<!-- Time picker (clock) -->
<input type="time" name="appointment" min="09:00" max="17:00" step="900">

<!-- Date + Time picker -->
<input type="datetime-local" name="event_datetime">

<!-- Month picker -->
<input type="month" name="start_month">

<!-- Week picker -->
<input type="week" name="week_number">
```

### Key Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `type` | `date`, `time`, `datetime-local`, `month`, `week` | Determines picker type |
| `value` | ISO 8601 format | Default value (e.g., "2025-03-15", "14:30") |
| `min` | ISO 8601 format | Earliest allowed date/time |
| `max` | ISO 8601 format | Latest allowed date/time |
| `step` | Number (seconds) | Time increment (e.g., `900` = 15 min intervals) |
| `required` | Boolean | Makes field mandatory |
| `readonly` | Boolean | Prevents editing |
| `disabled` | Boolean | Disables input |

### Date/Time Format Reference

- **`type="date"`:** Value format `YYYY-MM-DD` (e.g., "2025-03-15")
- **`type="time"`:** Value format `HH:MM` or `HH:MM:SS` (e.g., "14:30")
- **`type="datetime-local"`:** Value format `YYYY-MM-DDTHH:MM` (e.g., "2025-03-15T14:30")
- **`type="month"`:** Value format `YYYY-MM` (e.g., "2025-03")
- **`type="week"`:** Value format `YYYY-W##` (e.g., "2025-W11" for week 11)

---

## Examples

### Example 1: Birthday Selector (Date Input)

**Scenario:** User registration form collecting date of birth with age restriction (13+).

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Birthday Input</title>
</head>
<body>
  <form action="/register" method="POST">
    <label for="dob">Date of Birth:</label>
    <input
      type="date"
      id="dob"
      name="birthday"
      min="1900-01-01"
      max="2012-12-31"
      required
      aria-describedby="dob-hint">

    <small id="dob-hint">You must be at least 13 years old to register.</small>

    <button type="submit">Register</button>
  </form>
</body>
</html>
```

**Result:** Browser shows a calendar picker. The `max="2012-12-31"` ensures users are at least 13 years old (assuming current year is 2025). Returns data in "YYYY-MM-DD" format.

---

### Example 2: Appointment Scheduler (Date + Time)

**Scenario:** Medical appointment booking with business hours restriction.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Appointment Scheduler</title>
</head>
<body>
  <h1>Schedule Appointment</h1>
  <form action="/book-appointment" method="POST">
    <label for="appointment-datetime">Appointment Date & Time:</label>
    <input
      type="datetime-local"
      id="appointment-datetime"
      name="appointment"
      min="2025-01-01T09:00"
      max="2025-12-31T17:00"
      step="900"
      required
      aria-describedby="appointment-hint">

    <small id="appointment-hint">
      Business hours: 9:00 AM - 5:00 PM. Appointments in 15-minute intervals.
    </small>

    <button type="submit">Book Appointment</button>
  </form>
</body>
</html>
```

**Result:** Combined date + time picker. `step="900"` (900 seconds = 15 minutes) restricts selections to 15-minute intervals (9:00, 9:15, 9:30, etc.). Returns format "2025-03-15T14:30".

---

### Example 3: Monthly Report Selector (Month Input)

**Scenario:** Financial dashboard where users select a month to view reports.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Monthly Report</title>
</head>
<body>
  <form action="/reports" method="GET">
    <label for="report-month">Select Report Month:</label>
    <input
      type="month"
      id="report-month"
      name="month"
      min="2020-01"
      max="2025-12"
      value="2025-11"
      required>

    <button type="submit">View Report</button>
  </form>
</body>
</html>
```

**Result:** Month picker showing only year and month (no day selection). Value returned as "YYYY-MM" (e.g., "2025-11" for November 2025).

---

## Common Use Cases

### Use Case 1: Event Registration with Future Dates Only
**When:** Collecting event attendance dates where past dates are invalid.
**How:**
```html
<label for="event-date">Event Date:</label>
<input
  type="date"
  id="event-date"
  name="event_date"
  min="2025-11-18"
  required
  aria-describedby="event-hint">

<small id="event-hint">Select a future date for your event.</small>

<script>
  // Dynamically set min to today's date
  document.getElementById('event-date').min = new Date().toISOString().split('T')[0];
</script>
```
**Why:** JavaScript sets `min` to today's date dynamically, preventing users from selecting past dates.

---

### Use Case 2: Business Hours Time Picker
**When:** Restaurant reservation system with operating hours 11 AM - 10 PM.
**How:**
```html
<label for="reservation-time">Reservation Time:</label>
<input
  type="time"
  id="reservation-time"
  name="time"
  min="11:00"
  max="22:00"
  step="1800"
  required>

<small>Available: 11:00 AM - 10:00 PM (30-minute intervals)</small>
```
**Why:** `step="1800"` (30 minutes) restricts selections to 11:00, 11:30, 12:00, etc. `min/max` enforces business hours.

---

### Use Case 3: Timesheet Week Selector
**When:** Employee timesheet system where employees select work week.
**How:**
```html
<label for="work-week">Select Work Week:</label>
<input
  type="week"
  id="work-week"
  name="week"
  min="2025-W01"
  max="2025-W52"
  value="2025-W47"
  required>

<button type="submit">Load Timesheet</button>
```
**Why:** `type="week"` allows selecting by week number, perfect for payroll/timesheet systems. Returns "YYYY-W##" format.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 20+     | Full Support  | All date/time types fully supported |
| Firefox | 57+     | Full Support  | Full support since Firefox 57 |
| Safari  | 14.1+   | Full Support  | Earlier versions have partial support |
| Edge    | 12+     | Full Support  | Full support (all modern versions) |
| IE 11   | -       | No Support    | Falls back to text input |

**Fallback Strategy:**
```html
<!-- Modern browsers: Date picker -->
<!-- Older browsers: Text input with pattern validation -->
<input
  type="date"
  name="birthday"
  pattern="\d{4}-\d{2}-\d{2}"
  placeholder="YYYY-MM-DD"
  title="Enter date in format YYYY-MM-DD">

<!-- For production, use JavaScript polyfill for older browsers -->
<script>
  // Detect if browser supports date input
  const input = document.createElement('input');
  input.type = 'date';
  if (input.type === 'text') {
    // Load polyfill (e.g., flatpickr, date-fns) for unsupported browsers
  }
</script>
```

**Can I Use Links:**
- [Date Input](https://caniuse.com/input-datetime)
- [Time Input](https://caniuse.com/input-datetime)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- All date/time inputs must have associated `<label>` elements
- Inputs must be keyboard-accessible
- Required fields must be clearly indicated

**Level AA Requirements:**
- Labels and hints must have sufficient color contrast
- Error messages must be programmatically associated with inputs
- Date format instructions must be provided

### Screen Reader Support

```html
<!-- Accessible date input -->
<label for="start-date">
  Start Date <span aria-label="required">*</span>
</label>
<input
  type="date"
  id="start-date"
  name="start_date"
  required
  aria-required="true"
  aria-describedby="date-format-hint">

<small id="date-format-hint">
  Format: Year-Month-Day (e.g., 2025-03-15). Use calendar picker or type date.
</small>
```

**Key Points:**
- `aria-required="true"` announces required date fields
- `aria-describedby` links format instructions to the input
- Provide format hints for users who can't see the visual picker

### Keyboard Navigation

**Date Picker:**
- **Tab:** Moves focus to/from date input
- **Spacebar/Enter:** Opens calendar picker
- **Arrow Keys:** Navigate calendar (day/month/year)
- **Escape:** Closes calendar picker

**Time Picker:**
- **Tab:** Moves focus to hour/minute fields
- **Up/Down Arrows:** Increment/decrement values
- **Typing:** Direct number entry

---

## Best Practices

### Do This

1. **Set Realistic Min/Max Constraints**
   ```html
   <!-- GOOD: Prevents invalid future birthdates -->
   <input type="date" name="dob" min="1900-01-01" max="2012-12-31">
   ```
   **Why:** Validates age requirements (e.g., 13+ for registration) and prevents accidental selection of invalid dates.

2. **Use Step for Time Intervals**
   ```html
   <!-- GOOD: 30-minute appointment slots -->
   <input type="time" name="appointment" step="1800">
   ```
   **Why:** `step="1800"` (seconds) = 30-minute intervals. Aligns with business scheduling practices.

3. **Provide Format Hints**
   ```html
   <label for="deadline">Deadline:</label>
   <input type="date" id="deadline" name="deadline" required>
   <small>Format: Year-Month-Day (YYYY-MM-DD)</small>
   ```
   **Why:** Even with pickers, some users type dates manually. Format hints reduce errors.

---

### Avoid This

1. **Using Date Inputs for Age Instead of Birthday**
   ```html
   <!-- WRONG: Asking for age (which changes) instead of birthday -->
   <label for="age">Age:</label>
   <input type="number" name="age">
   ```
   **Why Not:** Age changes every year. Birthday is permanent and can be used to calculate current age.
   **Instead:**
   ```html
   <label for="dob">Date of Birth:</label>
   <input type="date" name="birthday" max="2012-12-31">
   ```

2. **Forgetting Min/Max on Appointment Schedulers**
   ```html
   <!-- WRONG: Allows booking appointments in the past -->
   <input type="datetime-local" name="appointment">
   ```
   **Why Not:** Users can select past dates or dates outside business hours.
   **Instead:**
   ```html
   <input type="datetime-local" name="appointment"
          min="2025-01-01T09:00" max="2025-12-31T17:00">
   ```

3. **Using datetime Instead of datetime-local**
   ```html
   <!-- WRONG: type="datetime" is obsolete -->
   <input type="datetime" name="event">
   ```
   **Why Not:** `type="datetime"` (with timezone) was removed from HTML spec. No browser support.
   **Instead:**
   ```html
   <input type="datetime-local" name="event">
   <!-- Handle timezone on server-side -->
   ```

---

## Related Topics

**Prerequisites (Learn These First):**
- [Form Element](form-element.md) - Understanding form structure
- [Number Inputs](number-range.md) - Understanding min/max/step concepts

**Related Concepts:**
- [Form Validation](form-validation.md) - How date/time inputs validate
- [Form Attributes](form-attributes.md) - Additional HTML5 input attributes

**Next Steps (Learn These Next):**
- [Checkboxes & Radio Buttons](checkboxes-radio.md) - Selection inputs
- [Select & Datalist](select-datalist.md) - Dropdown menus

**External Resources:**
- [MDN Web Docs - Date Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date)
- [MDN Web Docs - Time Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/time)
- [W3Schools - HTML Input Types](https://www.w3schools.com/html/html_form_input_types.asp)

---

## Practice Exercise

### Challenge: Build an Event Registration Form

**Objective:** Create an event registration form with date, time, and datetime-local inputs for an upcoming conference.

**Requirements:**
- [ ] Event date selector (future dates only, next 6 months)
- [ ] Session time picker (9:00 AM - 5:00 PM, 1-hour intervals)
- [ ] Full registration datetime (date + time combined)
- [ ] Validate that event date is in the future
- [ ] Bonus: Add month picker for "Which month did you hear about this event?"

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Event Registration</title>
</head>
<body>
  <h1>Conference Registration</h1>
  <form action="/register-event" method="POST">
    <!-- Add your date/time inputs here -->
    <button type="submit">Register for Event</button>
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
  <title>Event Registration</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 600px; margin: 2rem auto; padding: 0 1rem; }
    label { display: block; margin-top: 1.5rem; font-weight: bold; }
    input { width: 100%; max-width: 400px; padding: 0.5rem; margin-top: 0.5rem; }
    small { display: block; color: #666; margin-top: 0.25rem; }
    button { margin-top: 2rem; padding: 0.75rem 1.5rem; }
  </style>
</head>
<body>
  <h1>Conference Registration</h1>
  <form action="/register-event" method="POST">
    <!-- Event date (future only) -->
    <label for="event-date">Event Date: <span aria-label="required">*</span></label>
    <input
      type="date"
      id="event-date"
      name="event_date"
      required
      aria-required="true"
      aria-describedby="date-hint">
    <small id="date-hint">Select a date within the next 6 months.</small>

    <!-- Session time (business hours, 1-hour intervals) -->
    <label for="session-time">Preferred Session Time: <span aria-label="required">*</span></label>
    <input
      type="time"
      id="session-time"
      name="session_time"
      min="09:00"
      max="17:00"
      step="3600"
      required
      aria-required="true"
      aria-describedby="time-hint">
    <small id="time-hint">Sessions run 9:00 AM - 5:00 PM (hourly).</small>

    <!-- Full registration datetime -->
    <label for="registration-datetime">Registration Deadline: <span aria-label="required">*</span></label>
    <input
      type="datetime-local"
      id="registration-datetime"
      name="registration_deadline"
      required
      aria-required="true"
      aria-describedby="datetime-hint">
    <small id="datetime-hint">Last date and time to register.</small>

    <!-- Month heard about event (bonus) -->
    <label for="heard-month">Which month did you hear about this event?</label>
    <input
      type="month"
      id="heard-month"
      name="heard_month"
      min="2024-01"
      max="2025-12"
      aria-describedby="month-hint">
    <small id="month-hint">Optional: Help us track our marketing reach.</small>

    <button type="submit">Register for Event</button>
  </form>

  <script>
    // Set min date to today, max date to 6 months from now
    const eventDateInput = document.getElementById('event-date');
    const regDatetimeInput = document.getElementById('registration-datetime');

    const today = new Date();
    const sixMonthsLater = new Date(today);
    sixMonthsLater.setMonth(today.getMonth() + 6);

    // Format dates as YYYY-MM-DD
    const todayStr = today.toISOString().split('T')[0];
    const maxDateStr = sixMonthsLater.toISOString().split('T')[0];

    eventDateInput.min = todayStr;
    eventDateInput.max = maxDateStr;

    // Set min for registration deadline to right now
    const nowStr = new Date().toISOString().slice(0, 16); // YYYY-MM-DDTHH:MM
    regDatetimeInput.min = nowStr;
  </script>
</body>
</html>
```

**Explanation:**
This form uses three HTML5 date/time inputs: `type="date"` for event date with future-only validation, `type="time"` for session selection with 1-hour intervals (`step="3600"` seconds), and `type="datetime-local"` for combined date+time registration deadline. JavaScript dynamically sets `min` to today's date and `max` to 6 months ahead, preventing past date selection. The bonus `type="month"` input tracks marketing effectiveness.

</details>

---

### Expected Result

**Visual Outcome:** A complete event registration form with native date/time pickers. Event date restricted to next 6 months (future only), session time shows hourly slots (9 AM - 5 PM), and registration deadline combines date + time. Month picker optional for tracking.

**Key Learnings:**
- Using JavaScript to dynamically set min/max dates (e.g., "today" as minimum)
- How `step` attribute controls time intervals (3600 seconds = 1 hour)
- Difference between `type="date"`, `type="time"`, and `type="datetime-local"`
- Combining HTML5 validation with JavaScript for dynamic constraints

---

## Navigation

**Previous:** [Number & Range Inputs](number-range.md)
**Next:** [Checkboxes & Radio Buttons](checkboxes-radio.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
