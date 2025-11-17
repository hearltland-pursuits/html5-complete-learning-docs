# Table Structure

## Overview
The `<table>` element represents tabular data—information organized in rows and columns. Tables are used for data presentation, comparisons, pricing plans, schedules, and any content best displayed in a grid format.

## Basic Syntax

```html
<table>
  <tr>
    <th>Header 1</th>
    <th>Header 2</th>
  </tr>
  <tr>
    <td>Data 1</td>
    <td>Data 2</td>
  </tr>
  <tr>
    <td>Data 3</td>
    <td>Data 4</td>
  </tr>
</table>
```

## Core Elements

### `<table>` - Table Container

The parent element that wraps all table content.

```html
<table>
  <!-- table content -->
</table>
```

### `<tr>` - Table Row

Defines a row in the table.

```html
<tr>
  <td>Cell 1</td>
  <td>Cell 2</td>
</tr>
```

### `<th>` - Table Header

Defines a header cell (bold and centered by default).

```html
<tr>
  <th>Name</th>
  <th>Age</th>
  <th>City</th>
</tr>
```

**Attributes:**
- `scope`: Specifies whether header is for row, column, or group
  - `scope="col"` - Column header (default)
  - `scope="row"` - Row header
  - `scope="colgroup"` - Column group header
  - `scope="rowgroup"` - Row group header

```html
<tr>
  <th scope="col">Product</th>
  <th scope="col">Price</th>
  <th scope="col">Stock</th>
</tr>
```

### `<td>` - Table Data

Defines a standard data cell.

```html
<tr>
  <td>Laptop</td>
  <td>$999</td>
  <td>15</td>
</tr>
```

## Cell Spanning

### colspan - Span Multiple Columns

```html
<table border="1">
  <tr>
    <th colspan="3">Q1 Sales Report</th>
  </tr>
  <tr>
    <th>January</th>
    <th>February</th>
    <th>March</th>
  </tr>
  <tr>
    <td>$10,000</td>
    <td>$12,000</td>
    <td>$15,000</td>
  </tr>
</table>
```

### rowspan - Span Multiple Rows

```html
<table border="1">
  <tr>
    <th rowspan="2">Product</th>
    <th colspan="2">Sales</th>
  </tr>
  <tr>
    <th>Q1</th>
    <th>Q2</th>
  </tr>
  <tr>
    <td>Laptop</td>
    <td>100</td>
    <td>150</td>
  </tr>
</table>
```

## Basic Styling

```html
<style>
  table {
    border-collapse: collapse;
    width: 100%;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 12px;
    text-align: left;
  }

  th {
    background-color: #3498db;
    color: white;
  }

  tr:nth-child(even) {
    background-color: #f2f2f2;
  }

  tr:hover {
    background-color: #e0e0e0;
  }
</style>

<table>
  <tr>
    <th>Name</th>
    <th>Email</th>
    <th>Role</th>
  </tr>
  <tr>
    <td>John Doe</td>
    <td>john@example.com</td>
    <td>Developer</td>
  </tr>
  <tr>
    <td>Jane Smith</td>
    <td>jane@example.com</td>
    <td>Designer</td>
  </tr>
</table>
```

## Common Use Cases

### Employee Directory

```html
<table>
  <caption>Employee Directory</caption>
  <tr>
    <th scope="col">Name</th>
    <th scope="col">Department</th>
    <th scope="col">Email</th>
    <th scope="col">Phone</th>
  </tr>
  <tr>
    <th scope="row">Sarah Johnson</th>
    <td>Engineering</td>
    <td>sarah@company.com</td>
    <td>(555) 123-4567</td>
  </tr>
  <tr>
    <th scope="row">Mike Chen</th>
    <td>Marketing</td>
    <td>mike@company.com</td>
    <td>(555) 234-5678</td>
  </tr>
</table>
```

### Pricing Table

```html
<table style="border-collapse: collapse; width: 100%; text-align: center;">
  <caption>Pricing Plans</caption>
  <tr>
    <th>Feature</th>
    <th>Basic</th>
    <th>Pro</th>
    <th>Enterprise</th>
  </tr>
  <tr>
    <th scope="row">Price</th>
    <td>$9/mo</td>
    <td>$29/mo</td>
    <td>$99/mo</td>
  </tr>
  <tr>
    <th scope="row">Storage</th>
    <td>10 GB</td>
    <td>100 GB</td>
    <td>Unlimited</td>
  </tr>
  <tr>
    <th scope="row">Users</th>
    <td>1</td>
    <td>10</td>
    <td>Unlimited</td>
  </tr>
  <tr>
    <th scope="row">Support</th>
    <td>Email</td>
    <td>Priority</td>
    <td>24/7 Phone</td>
  </tr>
</table>
```

### Schedule Table

```html
<table border="1" style="border-collapse: collapse; width: 100%;">
  <caption>Weekly Schedule</caption>
  <tr>
    <th scope="col">Time</th>
    <th scope="col">Monday</th>
    <th scope="col">Tuesday</th>
    <th scope="col">Wednesday</th>
  </tr>
  <tr>
    <th scope="row">9:00 AM</th>
    <td>Team Meeting</td>
    <td>Project Review</td>
    <td>Client Call</td>
  </tr>
  <tr>
    <th scope="row">11:00 AM</th>
    <td colspan="3">Development Time</td>
  </tr>
  <tr>
    <th scope="row">2:00 PM</th>
    <td>Code Review</td>
    <td>Design Sprint</td>
    <td>Testing</td>
  </tr>
</table>
```

## Complete Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Comparison Table</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 1000px;
      margin: 50px auto;
      padding: 20px;
      background: #f5f5f5;
    }

    h1 {
      text-align: center;
      color: #2c3e50;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      background: white;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      border-radius: 8px;
      overflow: hidden;
    }

    caption {
      caption-side: top;
      padding: 15px;
      font-size: 1.3rem;
      font-weight: bold;
      color: #2c3e50;
      background: #ecf0f1;
    }

    th {
      background: #3498db;
      color: white;
      padding: 15px;
      text-align: left;
      font-weight: bold;
    }

    td {
      padding: 15px;
      border-bottom: 1px solid #ecf0f1;
    }

    tr:hover {
      background: #f8f9fa;
    }

    .checkmark {
      color: #27ae60;
      font-weight: bold;
      font-size: 1.2rem;
    }

    .cross {
      color: #e74c3c;
      font-weight: bold;
      font-size: 1.2rem;
    }

    tfoot {
      background: #ecf0f1;
      font-weight: bold;
    }

    tfoot td {
      padding: 20px 15px;
      border-bottom: none;
    }
  </style>
</head>
<body>
  <h1>Smartphone Comparison</h1>

  <table>
    <caption>Compare Top 2024 Models</caption>
    <thead>
      <tr>
        <th scope="col">Feature</th>
        <th scope="col">Model A</th>
        <th scope="col">Model B</th>
        <th scope="col">Model C</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Price</th>
        <td>$799</td>
        <td>$999</td>
        <td>$1,199</td>
      </tr>
      <tr>
        <th scope="row">Display</th>
        <td>6.1" OLED</td>
        <td>6.5" AMOLED</td>
        <td>6.7" LTPO</td>
      </tr>
      <tr>
        <th scope="row">Processor</th>
        <td>A16 Bionic</td>
        <td>Snapdragon 8 Gen 2</td>
        <td>A17 Pro</td>
      </tr>
      <tr>
        <th scope="row">RAM</th>
        <td>6 GB</td>
        <td>8 GB</td>
        <td>12 GB</td>
      </tr>
      <tr>
        <th scope="row">Storage</th>
        <td>128 GB</td>
        <td>256 GB</td>
        <td>512 GB</td>
      </tr>
      <tr>
        <th scope="row">Main Camera</th>
        <td>48 MP</td>
        <td>50 MP</td>
        <td>64 MP</td>
      </tr>
      <tr>
        <th scope="row">Battery</th>
        <td>3,200 mAh</td>
        <td>4,500 mAh</td>
        <td>5,000 mAh</td>
      </tr>
      <tr>
        <th scope="row">5G Support</th>
        <td><span class="checkmark">✓</span></td>
        <td><span class="checkmark">✓</span></td>
        <td><span class="checkmark">✓</span></td>
      </tr>
      <tr>
        <th scope="row">Wireless Charging</th>
        <td><span class="checkmark">✓</span></td>
        <td><span class="checkmark">✓</span></td>
        <td><span class="checkmark">✓</span></td>
      </tr>
      <tr>
        <th scope="row">Expandable Storage</th>
        <td><span class="cross">✗</span></td>
        <td><span class="checkmark">✓</span></td>
        <td><span class="cross">✗</span></td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td>Overall Rating</td>
        <td>⭐⭐⭐⭐☆ (4.2/5)</td>
        <td>⭐⭐⭐⭐⭐ (4.7/5)</td>
        <td>⭐⭐⭐⭐⭐ (4.9/5)</td>
      </tr>
    </tfoot>
  </table>
</body>
</html>
```

## Accessibility

### Always Use scope Attribute

```html
<table>
  <tr>
    <th scope="col">Product</th>
    <th scope="col">Price</th>
  </tr>
  <tr>
    <th scope="row">Laptop</th>
    <td>$999</td>
  </tr>
</table>
```

### Add Caption

```html
<table>
  <caption>Employee Contact Information</caption>
  <!-- table content -->
</table>
```

### Summary (Deprecated, use caption instead)

```html
<!-- ❌ Old HTML4 -->
<table summary="Employee contacts with names and emails">

<!-- ✅ HTML5 -->
<table>
  <caption>Employee contacts with names and emails</caption>
</table>
```

## Browser Support

- **`<table>`, `<tr>`, `<td>`, `<th>`**: Universal support (all browsers)
- **colspan/rowspan**: Universal support
- **scope attribute**: All modern browsers

## Common Mistakes

❌ **Using tables for layout**
```html
<table>
  <tr>
    <td>Sidebar</td>
    <td>Main content</td>
  </tr>
</table>
```

✅ **Use CSS Grid or Flexbox for layout**

---

❌ **Missing table structure**
```html
<table>
  <td>Data</td> <!-- Missing tr! -->
</table>
```

✅ **Proper nesting**
```html
<table>
  <tr>
    <td>Data</td>
  </tr>
</table>
```

## Additional Resources

- **MDN Web Docs**: [The Table element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)
- **W3Schools**: [HTML Tables](https://www.w3schools.com/html/html_tables.asp)

---

**Previous Topic**: [Nested Lists](./nested-lists.md)
**Next Topic**: [Table Sections](./table-sections.md)
**Category**: [Lists and Tables](./README.md)
