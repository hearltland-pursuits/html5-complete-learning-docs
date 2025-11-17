# Responsive Tables

## Overview
Responsive tables adapt to different screen sizes, especially mobile devices where traditional table layouts can be difficult to read. Techniques include horizontal scrolling, card layouts, and hiding non-essential columns.

## Strategies for Responsive Tables

### 1. Horizontal Scrolling (Simplest)

Allow table to scroll horizontally on small screens.

```html
<style>
  .table-wrapper {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch; /* Smooth scrolling on iOS */
  }

  table {
    min-width: 600px; /* Prevent excessive shrinking */
  }
</style>

<div class="table-wrapper">
  <table>
    <thead>
      <tr>
        <th>Product</th>
        <th>Description</th>
        <th>Price</th>
        <th>Stock</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Laptop</td>
        <td>15-inch display, 16GB RAM</td>
        <td>$999</td>
        <td>15</td>
        <td><button>Buy</button></td>
      </tr>
    </tbody>
  </table>
</div>
```

### 2. Stack Columns (Mobile-First)

Convert table rows to card-style blocks on mobile.

```html
<style>
  @media (max-width: 768px) {
    table, thead, tbody, th, td, tr {
      display: block;
    }

    thead tr {
      position: absolute;
      top: -9999px;
      left: -9999px;
    }

    tr {
      border: 1px solid #ddd;
      margin-bottom: 15px;
      border-radius: 8px;
      padding: 10px;
    }

    td {
      border: none;
      position: relative;
      padding-left: 50%;
      text-align: right;
    }

    td::before {
      content: attr(data-label);
      position: absolute;
      left: 10px;
      font-weight: bold;
      text-align: left;
    }
  }
</style>

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Email</th>
      <th>Role</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-label="Name">Alice Johnson</td>
      <td data-label="Email">alice@company.com</td>
      <td data-label="Role">Developer</td>
    </tr>
    <tr>
      <td data-label="Name">Bob Smith</td>
      <td data-label="Email">bob@company.com</td>
      <td data-label="Role">Designer</td>
    </tr>
  </tbody>
</table>
```

### 3. Hide Non-Essential Columns

Show only critical columns on mobile.

```html
<style>
  @media (max-width: 768px) {
    .hide-mobile {
      display: none;
    }
  }
</style>

<table>
  <thead>
    <tr>
      <th>Product</th>
      <th>Price</th>
      <th class="hide-mobile">Description</th>
      <th class="hide-mobile">Stock</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Laptop</td>
      <td>$999</td>
      <td class="hide-mobile">15-inch display, 16GB RAM</td>
      <td class="hide-mobile">15</td>
      <td><button>Buy</button></td>
    </tr>
  </tbody>
</table>
```

### 4. Flip Table (Rows become Columns)

Transpose table for better mobile viewing.

```html
<style>
  @media (max-width: 768px) {
    .flip-table {
      display: block;
      overflow-x: auto;
    }

    .flip-table thead {
      float: left;
    }

    .flip-table tbody {
      display: block;
      width: auto;
      overflow-x: auto;
      white-space: nowrap;
    }

    .flip-table tbody tr {
      display: inline-block;
      vertical-align: top;
    }

    .flip-table th,
    .flip-table td {
      display: block;
      text-align: left;
    }
  }
</style>
```

## Complete Responsive Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Product Table</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
      background: #f5f5f5;
    }

    h1 {
      text-align: center;
      color: #2c3e50;
    }

    .table-container {
      background: white;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      overflow: hidden;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    caption {
      padding: 20px;
      font-size: 1.3rem;
      font-weight: bold;
      text-align: left;
      background: #ecf0f1;
      color: #2c3e50;
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

    tbody tr {
      border-bottom: 1px solid #ecf0f1;
    }

    tbody tr:hover {
      background: #f8f9fa;
    }

    td {
      padding: 15px;
    }

    .price {
      font-weight: bold;
      color: #27ae60;
    }

    .stock {
      color: #e74c3c;
    }

    button {
      padding: 8px 16px;
      background: #3498db;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.3s;
    }

    button:hover {
      background: #2980b9;
    }

    /* Responsive: Horizontal scroll for tablets */
    @media (max-width: 1024px) {
      .table-container {
        overflow-x: auto;
        -webkit-overflow-scrolling: touch;
      }

      table {
        min-width: 800px;
      }
    }

    /* Responsive: Card layout for mobile */
    @media (max-width: 768px) {
      .table-container {
        overflow-x: visible;
      }

      table {
        min-width: unset;
      }

      table, thead, tbody, th, td, tr {
        display: block;
      }

      thead tr {
        position: absolute;
        top: -9999px;
        left: -9999px;
      }

      tr {
        background: white;
        border: 1px solid #ddd;
        border-radius: 8px;
        margin-bottom: 15px;
        padding: 15px;
        box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      }

      td {
        border: none;
        position: relative;
        padding: 12px 12px 12px 50%;
        text-align: right;
      }

      td::before {
        content: attr(data-label);
        position: absolute;
        left: 15px;
        font-weight: bold;
        text-align: left;
        color: #7f8c8d;
        font-size: 0.9rem;
      }

      button {
        width: 100%;
        margin-top: 10px;
      }
    }

    /* Responsive: Extra small screens */
    @media (max-width: 480px) {
      body {
        padding: 10px;
      }

      caption {
        font-size: 1.1rem;
        padding: 15px;
      }

      td {
        padding: 10px 10px 10px 45%;
        font-size: 0.9rem;
      }

      td::before {
        font-size: 0.85rem;
      }
    }
  </style>
</head>
<body>
  <h1>Product Catalog</h1>

  <div class="table-container">
    <table>
      <caption>Available Products - All Prices in USD</caption>
      <thead>
        <tr>
          <th scope="col">Product</th>
          <th scope="col">Category</th>
          <th scope="col">Price</th>
          <th scope="col">Stock</th>
          <th scope="col">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td data-label="Product">UltraBook Pro 15</td>
          <td data-label="Category">Laptops</td>
          <td data-label="Price" class="price">$1,799</td>
          <td data-label="Stock" class="stock">5 left</td>
          <td data-label="Actions"><button>Add to Cart</button></td>
        </tr>
        <tr>
          <td data-label="Product">Wireless Mouse X1</td>
          <td data-label="Category">Accessories</td>
          <td data-label="Price" class="price">$29</td>
          <td data-label="Stock">In Stock</td>
          <td data-label="Actions"><button>Add to Cart</button></td>
        </tr>
        <tr>
          <td data-label="Product">4K Monitor 27"</td>
          <td data-label="Category">Monitors</td>
          <td data-label="Price" class="price">$549</td>
          <td data-label="Stock">In Stock</td>
          <td data-label="Actions"><button>Add to Cart</button></td>
        </tr>
        <tr>
          <td data-label="Product">Mechanical Keyboard RGB</td>
          <td data-label="Category">Accessories</td>
          <td data-label="Price" class="price">$149</td>
          <td data-label="Stock" class="stock">2 left</td>
          <td data-label="Actions"><button>Add to Cart</button></td>
        </tr>
        <tr>
          <td data-label="Product">USB-C Hub 7-in-1</td>
          <td data-label="Category">Accessories</td>
          <td data-label="Price" class="price">$69</td>
          <td data-label="Stock">In Stock</td>
          <td data-label="Actions"><button>Add to Cart</button></td>
        </tr>
      </tbody>
    </table>
  </div>

  <p style="text-align: center; margin-top: 20px; color: #7f8c8d; font-size: 0.9rem;">
    <strong>Note:</strong> Table layout adapts to your screen size.
    On mobile, items display as cards for easier reading.
  </p>
</body>
</html>
```

## JavaScript-Enhanced Responsiveness

### Toggle Column Visibility

```html
<div>
  <label>
    <input type="checkbox" class="toggle-col" data-column="description" checked>
    Show Description
  </label>
  <label>
    <input type="checkbox" class="toggle-col" data-column="stock" checked>
    Show Stock
  </label>
</div>

<table id="responsive-table">
  <!-- table content -->
</table>

<script>
document.querySelectorAll('.toggle-col').forEach(checkbox => {
  checkbox.addEventListener('change', function() {
    const column = this.dataset.column;
    const cells = document.querySelectorAll(`[data-column="${column}"]`);

    cells.forEach(cell => {
      cell.style.display = this.checked ? '' : 'none';
    });
  });
});
</script>
```

## Best Practices

### 1. Test on Real Devices

- Test on actual phones and tablets
- Use browser DevTools device emulation
- Check landscape and portrait orientations

### 2. Prioritize Content

Show most important columns first on mobile:
- Product name
- Price
- Action button

Hide on mobile:
- Detailed descriptions
- Secondary metadata
- Extra columns

### 3. Maintain Accessibility

```html
<div class="table-wrapper" role="region" aria-labelledby="table-title" tabindex="0">
  <h2 id="table-title">Products</h2>
  <table>
    <!-- table content -->
  </table>
</div>
```

### 4. Performance Considerations

- Use CSS transforms over layout properties
- Minimize reflows and repaints
- Lazy load table data for large datasets
- Consider virtualization for 100+ rows

## Browser Support

- **CSS Media Queries**: Universal support
- **Flexbox**: IE 11+ (with prefixes), all modern browsers
- **Grid**: IE 11 (limited), all modern browsers
- **overflow-x**: Universal support

## Common Mistakes

❌ **No min-width on scrollable tables**
```html
<div style="overflow-x: auto;">
  <table> <!-- Will shrink too much -->
</table>
```

✅ **Set min-width**
```html
<div style="overflow-x: auto;">
  <table style="min-width: 600px;">
</table>
```

---

❌ **Forgetting data-label attributes**
```html
<td>$99</td> <!-- Won't show label on mobile -->
```

✅ **Include data-label**
```html
<td data-label="Price">$99</td>
```

## Additional Resources

- **CSS-Tricks**: [Responsive Data Tables](https://css-tricks.com/responsive-data-tables/)
- **Smashing Magazine**: [Responsive Table Techniques](https://www.smashingmagazine.com/2011/08/responsive-data-tables/)
- **A11y Project**: [Accessible Tables](https://www.a11yproject.com/posts/accessible-tables/)

---

**Previous Topic**: [Table Accessibility](./table-accessibility.md)
**Next Topic**: [Form Element](../06-forms-input/form-element.md)
**Category**: [Lists and Tables](./README.md)
