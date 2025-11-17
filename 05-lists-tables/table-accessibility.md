# Table Accessibility

## Overview
Accessible tables ensure that screen reader users and keyboard-only users can understand and navigate tabular data. Proper semantic markup, scope attributes, captions, and ARIA labels make tables usable for everyone.

## Essential Accessibility Features

### 1. Use `<caption>` Element

Provides a title/description for the table.

```html
<table>
  <caption>Employee Contact Information</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Email</th>
      <th>Phone</th>
    </tr>
  </thead>
  <!-- tbody content -->
</table>
```

**Screen reader announcement:** "Table: Employee Contact Information, 3 columns, 5 rows"

### 2. Use scope Attribute

Specifies whether header applies to rows or columns.

```html
<table>
  <thead>
    <tr>
      <th scope="col">Product</th>
      <th scope="col">Price</th>
      <th scope="col">Stock</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Laptop</th>
      <td>$999</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
```

**scope values:**
- `scope="col"` - Column header (vertical)
- `scope="row"` - Row header (horizontal)
- `scope="colgroup"` - Group of columns
- `scope="rowgroup"` - Group of rows

### 3. Use `<th>` for Headers

Use `<th>` instead of `<td>` for header cells.

```html
<!-- ✅ Good -->
<tr>
  <th scope="col">Name</th>
  <th scope="col">Age</th>
</tr>

<!-- ❌ Bad -->
<tr>
  <td><strong>Name</strong></td>
  <td><strong>Age</strong></td>
</tr>
```

### 4. Use `id` and `headers` for Complex Tables

For tables with multiple header levels.

```html
<table>
  <caption>Quarterly Sales by Region</caption>
  <thead>
    <tr>
      <th id="region" scope="col">Region</th>
      <th id="q1" scope="col">Q1</th>
      <th id="q2" scope="col">Q2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th id="north" scope="row">North</th>
      <td headers="north q1">$50,000</td>
      <td headers="north q2">$55,000</td>
    </tr>
    <tr>
      <th id="south" scope="row">South</th>
      <td headers="south q1">$45,000</td>
      <td headers="south q2">$48,000</td>
    </tr>
  </tbody>
</table>
```

## ARIA Attributes

### aria-label

Provides accessible name when caption is not suitable.

```html
<table aria-label="Student grades for Fall 2024 semester">
  <!-- table content -->
</table>
```

### aria-labelledby

References an element that labels the table.

```html
<h2 id="sales-title">2024 Sales Report</h2>
<table aria-labelledby="sales-title">
  <!-- table content -->
</table>
```

### aria-describedby

Provides additional description.

```html
<p id="table-desc">This table shows monthly revenue and growth percentages</p>
<table aria-describedby="table-desc">
  <caption>Monthly Performance</caption>
  <!-- table content -->
</table>
```

## Sortable Tables

```html
<table>
  <thead>
    <tr>
      <th scope="col">
        <button aria-label="Sort by name">
          Name <span aria-hidden="true">▼</span>
        </button>
      </th>
      <th scope="col">
        <button aria-label="Sort by age">
          Age <span aria-hidden="true">▼</span>
        </button>
      </th>
    </tr>
  </thead>
  <tbody>
    <!-- data rows -->
  </tbody>
</table>
```

## Responsive Accessible Tables

### Scrollable Container

```html
<div role="region" aria-labelledby="table-title" tabindex="0" style="overflow-x: auto;">
  <h3 id="table-title">Product Specifications</h3>
  <table>
    <!-- wide table content -->
  </table>
</div>
```

**Benefits:**
- `role="region"`: Identifies scrollable area
- `aria-labelledby`: Links to table title
- `tabindex="0"`: Makes scrollable with keyboard

## Visual Focus Indicators

```html
<style>
  table {
    border-collapse: collapse;
  }

  th, td {
    padding: 12px;
    border: 1px solid #ddd;
  }

  th:focus,
  td:focus {
    outline: 3px solid #3498db;
    outline-offset: -3px;
  }

  a:focus,
  button:focus {
    outline: 3px solid #e74c3c;
    outline-offset: 2px;
  }
</style>
```

## Complete Accessible Table Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Accessible Data Table</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 1000px;
      margin: 50px auto;
      padding: 20px;
    }

    .table-container {
      overflow-x: auto;
      border: 2px solid #ddd;
      border-radius: 8px;
    }

    .table-container:focus {
      outline: 3px solid #3498db;
      outline-offset: 2px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      background: white;
    }

    caption {
      padding: 20px;
      font-size: 1.3rem;
      font-weight: bold;
      text-align: left;
      background: #ecf0f1;
      color: #2c3e50;
    }

    .sr-only {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0,0,0,0);
      white-space: nowrap;
      border: 0;
    }

    thead {
      background: #3498db;
      color: white;
    }

    th {
      padding: 15px;
      text-align: left;
      font-weight: bold;
    }

    tbody tr:nth-child(even) {
      background: #f8f9fa;
    }

    tbody tr:hover {
      background: #e9ecef;
    }

    tbody tr:focus-within {
      background: #d1ecf1;
      outline: 2px solid #3498db;
    }

    td, tbody th {
      padding: 15px;
      border-bottom: 1px solid #dee2e6;
    }

    /* Focus indicators */
    th:focus,
    td:focus {
      outline: 3px solid #e74c3c;
      outline-offset: -3px;
    }

    a {
      color: #3498db;
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }

    a:focus {
      outline: 3px solid #e74c3c;
      outline-offset: 2px;
      background: #fff3cd;
    }

    button {
      background: transparent;
      border: none;
      cursor: pointer;
      padding: 5px 10px;
      font-size: inherit;
    }

    button:focus {
      outline: 3px solid #e74c3c;
      outline-offset: 2px;
      background: #fff3cd;
    }

    .sort-icon {
      margin-left: 5px;
      color: #95a5a6;
    }

    .sorted-asc .sort-icon::after {
      content: " ▲";
      color: white;
    }

    .sorted-desc .sort-icon::after {
      content: " ▼";
      color: white;
    }
  </style>
</head>
<body>
  <h1 id="page-title">Employee Directory</h1>

  <p id="table-instructions">
    Use Tab key to navigate between cells. Press Enter on column headers to sort.
    Table can be scrolled horizontally using arrow keys when focused.
  </p>

  <div class="table-container"
       role="region"
       aria-labelledby="page-title"
       aria-describedby="table-instructions"
       tabindex="0">

    <table>
      <caption>
        Company Employee Contact Information
        <span class="sr-only">
          Contains 5 columns: Name, Department, Email, Phone, and Location.
          5 data rows. Sortable by clicking column headers.
        </span>
      </caption>

      <thead>
        <tr>
          <th scope="col" class="sorted-asc">
            <button aria-label="Sort by name, currently sorted ascending">
              Name<span class="sort-icon" aria-hidden="true"></span>
            </button>
          </th>
          <th scope="col">
            <button aria-label="Sort by department">
              Department<span class="sort-icon" aria-hidden="true"></span>
            </button>
          </th>
          <th scope="col">
            <button aria-label="Sort by email">
              Email<span class="sort-icon" aria-hidden="true"></span>
            </button>
          </th>
          <th scope="col">
            <button aria-label="Sort by phone">
              Phone<span class="sort-icon" aria-hidden="true"></span>
            </button>
          </th>
          <th scope="col">
            <button aria-label="Sort by location">
              Location<span class="sort-icon" aria-hidden="true"></span>
            </button>
          </th>
        </tr>
      </thead>

      <tbody>
        <tr>
          <th scope="row">Alice Johnson</th>
          <td>Engineering</td>
          <td><a href="mailto:alice@company.com">alice@company.com</a></td>
          <td><a href="tel:+15551234567">+1 (555) 123-4567</a></td>
          <td>Seattle, WA</td>
        </tr>

        <tr>
          <th scope="row">Bob Smith</th>
          <td>Marketing</td>
          <td><a href="mailto:bob@company.com">bob@company.com</a></td>
          <td><a href="tel:+15552345678">+1 (555) 234-5678</a></td>
          <td>Austin, TX</td>
        </tr>

        <tr>
          <th scope="row">Carol White</th>
          <td>Design</td>
          <td><a href="mailto:carol@company.com">carol@company.com</a></td>
          <td><a href="tel:+15553456789">+1 (555) 345-6789</a></td>
          <td>San Francisco, CA</td>
        </tr>

        <tr>
          <th scope="row">David Brown</th>
          <td>Sales</td>
          <td><a href="mailto:david@company.com">david@company.com</a></td>
          <td><a href="tel:+15554567890">+1 (555) 456-7890</a></td>
          <td>New York, NY</td>
        </tr>

        <tr>
          <th scope="row">Eve Martinez</th>
          <td>HR</td>
          <td><a href="mailto:eve@company.com">eve@company.com</a></td>
          <td><a href="tel:+15555678901">+1 (555) 567-8901</a></td>
          <td>Chicago, IL</td>
        </tr>
      </tbody>
    </table>
  </div>

  <p style="margin-top: 20px; color: #7f8c8d; font-size: 0.9rem;">
    <strong>Accessibility features:</strong> Keyboard navigation, sortable columns,
    screen reader support, high contrast focus indicators.
  </p>
</body>
</html>
```

## Testing Checklist

### Manual Testing

- [ ] Navigate table with Tab key
- [ ] Test with screen reader (NVDA, JAWS, VoiceOver)
- [ ] Verify caption is announced
- [ ] Check header associations
- [ ] Test sortable columns
- [ ] Verify focus indicators are visible
- [ ] Test in high contrast mode

### Screen Reader Testing

**Expected announcements:**
- "Table: [caption]"
- "3 columns, 5 rows"
- "Column header: Name"
- "Row 1, Name: Alice Johnson"

## Common Accessibility Mistakes

❌ **No caption**
```html
<table>
  <tr><th>Name</th></tr>
</table>
```

✅ **Include caption**
```html
<table>
  <caption>Employee List</caption>
  <tr><th scope="col">Name</th></tr>
</table>
```

---

❌ **Missing scope**
```html
<th>Product</th>
```

✅ **Include scope**
```html
<th scope="col">Product</th>
```

---

❌ **Using td for headers**
```html
<tr>
  <td><strong>Name</strong></td>
</tr>
```

✅ **Use th for headers**
```html
<tr>
  <th scope="col">Name</th>
</tr>
```

## WCAG Guidelines

- **WCAG 2.1 Level A**: Tables must have programmatic structure
- **WCAG 2.1 Level AA**: Sufficient color contrast (4.5:1)
- **WCAG 2.1 Level AAA**: Enhanced contrast (7:1)

## Additional Resources

- **W3C**: [Tables Tutorial](https://www.w3.org/WAI/tutorials/tables/)
- **WebAIM**: [Creating Accessible Tables](https://webaim.org/techniques/tables/)
- **MDN**: [HTML Table Accessibility](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Advanced)

---

**Previous Topic**: [Table Sections](./table-sections.md)
**Next Topic**: [Responsive Tables](./responsive-tables.md)
**Category**: [Lists and Tables](./README.md)
