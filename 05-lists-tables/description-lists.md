# Description Lists

## Overview
The `<dl>` (description list) element represents a list of term-description pairs. Commonly used for glossaries, metadata, key-value pairs, FAQs, and definitions. Each term is marked with `<dt>` (description term) and its description with `<dd>` (description details).

## Basic Syntax

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language - the standard markup language for web pages</dd>

  <dt>CSS</dt>
  <dd>Cascading Style Sheets - used for styling HTML documents</dd>

  <dt>JavaScript</dt>
  <dd>Programming language that adds interactivity to websites</dd>
</dl>
```

**Output:**
**HTML**
    HyperText Markup Language - the standard markup language for web pages
**CSS**
    Cascading Style Sheets - used for styling HTML documents
**JavaScript**
    Programming language that adds interactivity to websites

## Elements

### `<dl>` - Description List Container

The parent element containing term-description pairs.

```html
<dl>
  <!-- Terms and descriptions go here -->
</dl>
```

### `<dt>` - Description Term

Represents the term or name in the name-value pair.

```html
<dt>Term</dt>
```

### `<dd>` - Description Details

Provides the description, definition, or value for the preceding term.

```html
<dd>Description of the term</dd>
```

## Patterns

### One Term, One Description

```html
<dl>
  <dt>Coffee</dt>
  <dd>A brewed beverage made from roasted coffee beans</dd>
</dl>
```

### One Term, Multiple Descriptions

```html
<dl>
  <dt>Python</dt>
  <dd>A high-level programming language</dd>
  <dd>Known for its simple syntax and readability</dd>
  <dd>Popular for data science and web development</dd>
</dl>
```

### Multiple Terms, One Description

```html
<dl>
  <dt>HTML</dt>
  <dt>HyperText Markup Language</dt>
  <dd>The standard markup language for creating web pages</dd>
</dl>
```

### Groups with divs (HTML5)

```html
<dl>
  <div>
    <dt>Name</dt>
    <dd>John Doe</dd>
  </div>

  <div>
    <dt>Email</dt>
    <dd>john@example.com</dd>
  </div>

  <div>
    <dt>Phone</dt>
    <dd>+1 (555) 123-4567</dd>
  </div>
</dl>
```

**Note**: HTML5 allows wrapping `<dt>`/`<dd>` pairs in `<div>` for styling purposes.

## Common Use Cases

### Glossary

```html
<h2>Web Development Glossary</h2>
<dl>
  <dt>API</dt>
  <dd>Application Programming Interface - A set of protocols for building software applications</dd>

  <dt>CDN</dt>
  <dd>Content Delivery Network - A distributed network of servers that delivers web content</dd>

  <dt>DOM</dt>
  <dd>Document Object Model - Programming interface for HTML and XML documents</dd>

  <dt>REST</dt>
  <dd>Representational State Transfer - Architectural style for designing networked applications</dd>
</dl>
```

### FAQ Section

```html
<h2>Frequently Asked Questions</h2>
<dl>
  <dt>What is HTML5?</dt>
  <dd>HTML5 is the latest version of HTML, featuring new semantic elements, APIs, and multimedia support without plugins.</dd>

  <dt>Do I need to know CSS?</dt>
  <dd>Yes, CSS is essential for styling HTML content and creating visually appealing web pages.</dd>

  <dt>Is JavaScript difficult to learn?</dt>
  <dd>JavaScript has a moderate learning curve. With consistent practice and good resources, most people can become proficient within a few months.</dd>
</dl>
```

### Product Specifications

```html
<h2>Technical Specifications</h2>
<dl>
  <dt>Display</dt>
  <dd>15.6-inch LED-backlit display</dd>
  <dd>1920 x 1080 resolution (Full HD)</dd>

  <dt>Processor</dt>
  <dd>Intel Core i7-11th Gen</dd>
  <dd>2.8 GHz base frequency</dd>
  <dd>4.7 GHz max turbo frequency</dd>

  <dt>Memory</dt>
  <dd>16 GB DDR4 RAM</dd>

  <dt>Storage</dt>
  <dd>512 GB NVMe SSD</dd>

  <dt>Graphics</dt>
  <dd>NVIDIA GeForce RTX 3050</dd>
  <dd>4 GB GDDR6 dedicated memory</dd>

  <dt>Operating System</dt>
  <dd>Windows 11 Home</dd>
</dl>
```

### Contact Information

```html
<h2>Contact Details</h2>
<dl>
  <dt>Name</dt>
  <dd>Acme Corporation</dd>

  <dt>Address</dt>
  <dd>123 Main Street</dd>
  <dd>Suite 500</dd>
  <dd>San Francisco, CA 94105</dd>

  <dt>Phone</dt>
  <dd>+1 (415) 555-0123</dd>

  <dt>Email</dt>
  <dd><a href="mailto:info@acme.com">info@acme.com</a></dd>

  <dt>Hours</dt>
  <dd>Monday - Friday: 9:00 AM - 5:00 PM</dd>
  <dd>Saturday: 10:00 AM - 3:00 PM</dd>
  <dd>Sunday: Closed</dd>
</dl>
```

### Metadata Display

```html
<article>
  <h1>Understanding CSS Grid</h1>

  <dl>
    <dt>Author</dt>
    <dd>Jane Smith</dd>

    <dt>Published</dt>
    <dd><time datetime="2024-01-15">January 15, 2024</time></dd>

    <dt>Category</dt>
    <dd>Web Development</dd>

    <dt>Tags</dt>
    <dd>CSS, Grid, Layout, Responsive Design</dd>

    <dt>Reading Time</dt>
    <dd>8 minutes</dd>
  </dl>

  <p>Article content begins here...</p>
</article>
```

## Styling Description Lists

### Basic Horizontal Layout

```html
<style>
  dl {
    display: grid;
    grid-template-columns: max-content auto;
    gap: 10px 20px;
  }

  dt {
    font-weight: bold;
    color: #2c3e50;
  }

  dd {
    margin: 0;
    color: #555;
  }
</style>

<dl>
  <dt>Name:</dt>
  <dd>John Doe</dd>

  <dt>Email:</dt>
  <dd>john@example.com</dd>

  <dt>Location:</dt>
  <dd>San Francisco, CA</dd>
</dl>
```

### Card-Style Specs

```html
<style>
  .specs {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
  }

  .specs dt {
    font-weight: bold;
    color: #3498db;
    margin-top: 15px;
    font-size: 0.9rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .specs dt:first-child {
    margin-top: 0;
  }

  .specs dd {
    margin: 5px 0 0 20px;
    color: #2c3e50;
  }
</style>

<dl class="specs">
  <dt>Processor</dt>
  <dd>Intel Core i7-12700K</dd>
  <dd>12 cores, 20 threads</dd>

  <dt>Memory</dt>
  <dd>32 GB DDR5 RAM</dd>

  <dt>Storage</dt>
  <dd>1 TB NVMe SSD</dd>
</dl>
```

### FAQ Style with Accordion Effect

```html
<style>
  .faq dl {
    max-width: 700px;
    margin: 0 auto;
  }

  .faq dt {
    background: #3498db;
    color: white;
    padding: 15px 20px;
    margin: 10px 0 0 0;
    cursor: pointer;
    border-radius: 5px;
    font-weight: bold;
    transition: background 0.3s;
  }

  .faq dt:hover {
    background: #2980b9;
  }

  .faq dd {
    background: #ecf0f1;
    margin: 0;
    padding: 20px;
    border-radius: 0 0 5px 5px;
    line-height: 1.6;
  }
</style>

<div class="faq">
  <h2>Frequently Asked Questions</h2>
  <dl>
    <dt>What payment methods do you accept?</dt>
    <dd>We accept all major credit cards (Visa, MasterCard, American Express), PayPal, and bank transfers for enterprise accounts.</dd>

    <dt>How long does shipping take?</dt>
    <dd>Standard shipping takes 5-7 business days. Express shipping is available for 2-3 business day delivery. International orders may take 10-15 days.</dd>

    <dt>What is your return policy?</dt>
    <dd>We offer a 30-day money-back guarantee. Items must be returned in original condition with all packaging and accessories.</dd>
  </dl>
</div>
```

### Modern Key-Value Layout

```html
<style>
  .info-card {
    max-width: 500px;
    margin: 20px auto;
    background: white;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    overflow: hidden;
  }

  .info-card h2 {
    margin: 0;
    padding: 20px;
    background: #3498db;
    color: white;
  }

  .info-card dl {
    margin: 0;
    padding: 0;
  }

  .info-card div {
    display: grid;
    grid-template-columns: 150px 1fr;
    border-bottom: 1px solid #ecf0f1;
  }

  .info-card div:last-child {
    border-bottom: none;
  }

  .info-card dt {
    padding: 15px 20px;
    background: #f8f9fa;
    font-weight: bold;
    color: #2c3e50;
  }

  .info-card dd {
    padding: 15px 20px;
    margin: 0;
    color: #555;
  }
</style>

<div class="info-card">
  <h2>User Profile</h2>
  <dl>
    <div>
      <dt>Name</dt>
      <dd>Sarah Johnson</dd>
    </div>
    <div>
      <dt>Role</dt>
      <dd>Senior Developer</dd>
    </div>
    <div>
      <dt>Department</dt>
      <dd>Engineering</dd>
    </div>
    <div>
      <dt>Location</dt>
      <dd>Seattle, WA</dd>
    </div>
    <div>
      <dt>Member Since</dt>
      <dd>January 2022</dd>
    </div>
  </dl>
</div>
```

## Accessibility Considerations

### Proper Semantic Use

```html
<!-- ✅ Good: Term-description pairs -->
<dl>
  <dt>HTML</dt>
  <dd>Markup language for web pages</dd>
</dl>

<!-- ❌ Bad: Should use ul or ol -->
<dl>
  <dt>Step 1</dt>
  <dd>Open the file</dd>
  <dt>Step 2</dt>
  <dd>Edit the content</dd>
</dl>
```

### Clear Associations

```html
<dl>
  <dt id="term-api">API</dt>
  <dd aria-labelledby="term-api">
    Application Programming Interface - a set of protocols and tools
    for building software applications.
  </dd>
</dl>
```

## Complete Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Specifications</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 50px auto;
      padding: 20px;
      background: #f5f5f5;
    }

    .product {
      background: white;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 2px 15px rgba(0,0,0,0.1);
    }

    .product-header {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      padding: 40px;
      text-align: center;
    }

    .product-header h1 {
      margin: 0 0 10px 0;
      font-size: 2.5rem;
    }

    .product-header .price {
      font-size: 2rem;
      font-weight: bold;
    }

    .specs {
      padding: 40px;
    }

    .specs h2 {
      color: #2c3e50;
      margin-top: 0;
      border-bottom: 3px solid #667eea;
      padding-bottom: 10px;
    }

    .specs dl {
      margin: 30px 0;
    }

    .specs div {
      display: grid;
      grid-template-columns: 180px 1fr;
      border-bottom: 1px solid #ecf0f1;
      transition: background 0.2s;
    }

    .specs div:hover {
      background: #f8f9fa;
    }

    .specs dt {
      padding: 15px 20px;
      font-weight: bold;
      color: #667eea;
      background: #f8f9fa;
    }

    .specs dd {
      padding: 15px 20px;
      margin: 0;
      color: #555;
    }

    .specs dd + dd {
      grid-column: 2;
      padding-top: 0;
      border-top: 1px dashed #e0e0e0;
      margin-top: 0;
    }

    .buy-button {
      display: block;
      margin: 30px 40px 40px;
      padding: 15px;
      background: #667eea;
      color: white;
      text-align: center;
      text-decoration: none;
      border-radius: 5px;
      font-size: 1.2rem;
      font-weight: bold;
      transition: background 0.3s;
    }

    .buy-button:hover {
      background: #764ba2;
    }
  </style>
</head>
<body>
  <div class="product">
    <div class="product-header">
      <h1>UltraBook Pro 15</h1>
      <p>Premium Laptop for Professionals</p>
      <div class="price">$1,799</div>
    </div>

    <div class="specs">
      <h2>Technical Specifications</h2>

      <dl>
        <div>
          <dt>Display</dt>
          <dd>15.6-inch OLED display</dd>
          <dd>3840 x 2160 (4K UHD)</dd>
          <dd>100% DCI-P3 color gamut</dd>
        </div>

        <div>
          <dt>Processor</dt>
          <dd>Intel Core i9-13900H</dd>
          <dd>14 cores (6P + 8E), 20 threads</dd>
          <dd>Up to 5.4 GHz Turbo</dd>
        </div>

        <div>
          <dt>Memory</dt>
          <dd>32 GB DDR5 RAM</dd>
          <dd>5600 MHz</dd>
        </div>

        <div>
          <dt>Storage</dt>
          <dd>1 TB PCIe 4.0 NVMe SSD</dd>
          <dd>Up to 7000 MB/s read speed</dd>
        </div>

        <div>
          <dt>Graphics</dt>
          <dd>NVIDIA GeForce RTX 4060</dd>
          <dd>8 GB GDDR6 VRAM</dd>
          <dd>Ray tracing support</dd>
        </div>

        <div>
          <dt>Battery</dt>
          <dd>90Wh lithium-polymer</dd>
          <dd>Up to 12 hours mixed usage</dd>
          <dd>Fast charging (0-80% in 1 hour)</dd>
        </div>

        <div>
          <dt>Connectivity</dt>
          <dd>Wi-Fi 6E (802.11ax)</dd>
          <dd>Bluetooth 5.3</dd>
          <dd>2x Thunderbolt 4 ports</dd>
          <dd>1x USB-A 3.2 port</dd>
          <dd>HDMI 2.1</dd>
          <dd>3.5mm audio jack</dd>
        </div>

        <div>
          <dt>Dimensions</dt>
          <dd>35.6 x 24.0 x 1.8 cm</dd>
        </div>

        <div>
          <dt>Weight</dt>
          <dd>1.9 kg (4.2 lbs)</dd>
        </div>

        <div>
          <dt>Operating System</dt>
          <dd>Windows 11 Pro</dd>
        </div>

        <div>
          <dt>Warranty</dt>
          <dd>3-year manufacturer warranty</dd>
          <dd>1-year accidental damage protection</dd>
        </div>
      </dl>
    </div>

    <a href="#buy" class="buy-button">Add to Cart</a>
  </div>
</body>
</html>
```

## Browser Support

- **`<dl>`, `<dt>`, `<dd>`**: Universal support (all browsers, all versions)
- **`<div>` inside `<dl>`**: HTML5+ (all modern browsers)

## Common Mistakes

❌ **Missing dd or dt**
```html
<dl>
  <dt>Term</dt>
  <!-- Missing dd! -->
</dl>
```

✅ **Always pair dt with dd**
```html
<dl>
  <dt>Term</dt>
  <dd>Description</dd>
</dl>
```

---

❌ **Invalid nesting**
```html
<dl>
  <li>Item</li> <!-- Invalid! -->
</dl>
```

✅ **Only dt/dd as children**
```html
<dl>
  <dt>Term</dt>
  <dd>Description</dd>
</dl>
```

## Practice Exercise

Create a team member profile card with:
1. Name and photo
2. Role and department
3. Contact information
4. Skills list
5. Modern card styling

Solution provided in table-structure.md...

## Additional Resources

- **MDN Web Docs**: [The Description List element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dl)
- **W3Schools**: [HTML Description Lists](https://www.w3schools.com/html/html_lists_other.asp)

---

**Previous Topic**: [Unordered Lists](./unordered-lists.md)
**Next Topic**: [Nested Lists](./nested-lists.md)
**Category**: [Lists and Tables](./README.md)
