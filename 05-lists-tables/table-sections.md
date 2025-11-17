# Table Sections

## Overview
HTML tables can be divided into logical sections using `<thead>` (header), `<tbody>` (body), and `<tfoot>` (footer) elements. These sections improve accessibility, allow independent styling, and enable features like fixed headers in scrollable tables.

## Table Section Elements

### `<thead>` - Table Header Section

Contains header rows with column labels.

```html
<table>
  <thead>
    <tr>
      <th>Product</th>
      <th>Price</th>
      <th>Stock</th>
    </tr>
  </thead>
  <!-- tbody content -->
</table>
```

**Benefits:**
- Can be styled independently
- Allows fixed headers while scrolling body
- Improves screen reader navigation
- Repeats on printed pages

### `<tbody>` - Table Body Section

Contains the main data rows.

```html
<table>
  <thead><!-- headers --></thead>
  <tbody>
    <tr>
      <td>Laptop</td>
      <td>$999</td>
      <td>15</td>
    </tr>
    <tr>
      <td>Mouse</td>
      <td>$29</td>
      <td>150</td>
    </tr>
  </tbody>
</table>
```

**Notes:**
- Can have multiple `<tbody>` elements in one table
- Useful for grouping related rows

### `<tfoot>` - Table Footer Section

Contains summary or total rows.

```html
<table>
  <thead><!-- headers --></thead>
  <tbody><!-- data rows --></tbody>
  <tfoot>
    <tr>
      <th>Total</th>
      <td>$1,028</td>
      <td>165 units</td>
    </tr>
  </tfoot>
</table>
```

**Notes:**
- Placed before `<tbody>` in HTML4 (deprecated order)
- Now placed after `<tbody>` in HTML5
- Displays at bottom regardless of source order

## Complete Structure

```html
<table>
  <caption>Sales Report - Q4 2024</caption>
  <thead>
    <tr>
      <th scope="col">Month</th>
      <th scope="col">Revenue</th>
      <th scope="col">Units Sold</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">October</th>
      <td>$45,000</td>
      <td>320</td>
    </tr>
    <tr>
      <th scope="row">November</th>
      <td>$52,000</td>
      <td>385</td>
    </tr>
    <tr>
      <th scope="row">December</th>
      <td>$68,000</td>
      <td>475</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row">Quarter Total</th>
      <td><strong>$165,000</strong></td>
      <td><strong>1,180</strong></td>
    </tr>
  </tfoot>
</table>
```

## Multiple tbody Elements

Group related rows for better organization and styling.

```html
<table>
  <caption>Team Structure</caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Role</th>
      <th>Email</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <th colspan="3" style="background: #ecf0f1;">Engineering Team</th>
    </tr>
    <tr>
      <td>Alice Johnson</td>
      <td>Senior Developer</td>
      <td>alice@company.com</td>
    </tr>
    <tr>
      <td>Bob Smith</td>
      <td>Frontend Developer</td>
      <td>bob@company.com</td>
    </tr>
  </tbody>

  <tbody>
    <tr>
      <th colspan="3" style="background: #ecf0f1;">Design Team</th>
    </tr>
    <tr>
      <td>Carol White</td>
      <td>UX Designer</td>
      <td>carol@company.com</td>
    </tr>
    <tr>
      <td>David Brown</td>
      <td>UI Designer</td>
      <td>david@company.com</td>
    </tr>
  </tbody>
</table>
```

## Styling Sections

### Basic Section Styling

```html
<style>
  thead {
    background: #3498db;
    color: white;
    font-weight: bold;
  }

  tbody tr:nth-child(even) {
    background: #f8f9fa;
  }

  tbody tr:hover {
    background: #e9ecef;
  }

  tfoot {
    background: #2c3e50;
    color: white;
    font-weight: bold;
  }

  tfoot td {
    font-size: 1.1rem;
  }
</style>
```

### Fixed Header (Scrollable Body)

```html
<style>
  .scrollable-table {
    max-height: 400px;
    overflow-y: auto;
    display: block;
  }

  .scrollable-table thead {
    position: sticky;
    top: 0;
    background: #3498db;
    z-index: 10;
  }

  .scrollable-table thead th {
    position: sticky;
    top: 0;
  }

  .scrollable-table tbody {
    display: block;
  }

  .scrollable-table tr {
    display: table;
    width: 100%;
    table-layout: fixed;
  }
</style>

<table class="scrollable-table">
  <thead>
    <tr>
      <th>Product</th>
      <th>Price</th>
      <th>Stock</th>
    </tr>
  </thead>
  <tbody>
    <!-- 50+ rows of data -->
    <tr><td>Product 1</td><td>$99</td><td>100</td></tr>
    <!-- ... more rows ... -->
  </tbody>
</table>
```

## Complete Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Financial Report Table</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
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
      padding: 20px;
      font-size: 1.5rem;
      font-weight: bold;
      color: #2c3e50;
      text-align: left;
      background: #ecf0f1;
    }

    thead {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
    }

    thead th {
      padding: 15px;
      text-align: left;
      font-weight: bold;
      text-transform: uppercase;
      font-size: 0.9rem;
      letter-spacing: 0.5px;
    }

    tbody tr {
      border-bottom: 1px solid #ecf0f1;
    }

    tbody tr:nth-child(even) {
      background: #f8f9fa;
    }

    tbody tr:hover {
      background: #e3f2fd;
      transition: background 0.2s;
    }

    tbody th {
      padding: 15px;
      text-align: left;
      font-weight: 600;
      color: #2c3e50;
    }

    tbody td {
      padding: 15px;
      color: #555;
    }

    tbody td.positive {
      color: #27ae60;
      font-weight: bold;
    }

    tbody td.negative {
      color: #e74c3c;
      font-weight: bold;
    }

    tfoot {
      background: #2c3e50;
      color: white;
      font-weight: bold;
    }

    tfoot th,
    tfoot td {
      padding: 20px 15px;
      font-size: 1.1rem;
    }

    tfoot td {
      text-align: left;
    }
  </style>
</head>
<body>
  <h1>Annual Financial Report</h1>

  <table>
    <caption>Company Performance - Fiscal Year 2024</caption>

    <thead>
      <tr>
        <th scope="col">Quarter</th>
        <th scope="col">Revenue</th>
        <th scope="col">Expenses</th>
        <th scope="col">Profit</th>
        <th scope="col">Growth</th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <th scope="row">Q1 2024</th>
        <td>$250,000</td>
        <td>$180,000</td>
        <td>$70,000</td>
        <td class="positive">+12%</td>
      </tr>
      <tr>
        <th scope="row">Q2 2024</th>
        <td>$285,000</td>
        <td>$195,000</td>
        <td>$90,000</td>
        <td class="positive">+14%</td>
      </tr>
      <tr>
        <th scope="row">Q3 2024</th>
        <td>$310,000</td>
        <td>$220,000</td>
        <td>$90,000</td>
        <td class="positive">+9%</td>
      </tr>
      <tr>
        <th scope="row">Q4 2024</th>
        <td>$345,000</td>
        <td>$235,000</td>
        <td>$110,000</td>
        <td class="positive">+11%</td>
      </tr>
    </tbody>

    <tfoot>
      <tr>
        <th scope="row">Annual Total</th>
        <td>$1,190,000</td>
        <td>$830,000</td>
        <td>$360,000</td>
        <td>+11.5% Avg</td>
      </tr>
    </tfoot>
  </table>

  <p style="text-align: center; margin-top: 30px; color: #7f8c8d;">
    Report generated: January 15, 2025
  </p>
</body>
</html>
```

## Print Optimization

### Repeat Headers on Each Page

```html
<style>
  @media print {
    thead {
      display: table-header-group;
    }

    tfoot {
      display: table-footer-group;
    }

    tbody {
      display: table-row-group;
    }

    tr {
      page-break-inside: avoid;
    }
  }
</style>
```

## Browser Support

- **`<thead>`, `<tbody>`, `<tfoot>`**: Universal support (all browsers)
- **Sticky headers**: Modern browsers (Chrome 56+, Firefox 59+, Safari 13+)

## Additional Resources

- **MDN Web Docs**: [Table Sections](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Advanced)
- **W3Schools**: [HTML Table Headers](https://www.w3schools.com/html/html_table_headers.asp)

---

**Previous Topic**: [Table Structure](./table-structure.md)
**Next Topic**: [Table Accessibility](./table-accessibility.md)
**Category**: [Lists and Tables](./README.md)
