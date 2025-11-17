# Unordered Lists

## Overview
The `<ul>` (unordered list) element represents a list of items where the order doesn't matter. Items are typically displayed with bullet points. Unordered lists are used for collections of items, feature lists, navigation menus, and any content where sequence is not important.

## Basic Syntax

```html
<ul>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ul>
```

**Output:**
• First item
• Second item
• Third item

## Common Use Cases

### Feature Lists

```html
<h2>Product Features</h2>
<ul>
  <li>Wireless connectivity</li>
  <li>30-hour battery life</li>
  <li>Noise cancellation</li>
  <li>Comfortable fit</li>
  <li>Premium sound quality</li>
</ul>
```

### Navigation Menus

```html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/services">Services</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

### Bullet Point Content

```html
<h2>Benefits of Exercise</h2>
<ul>
  <li>Improves cardiovascular health</li>
  <li>Strengthens muscles and bones</li>
  <li>Reduces stress and anxiety</li>
  <li>Boosts energy levels</li>
  <li>Enhances mood and mental health</li>
</ul>
```

### Checklist

```html
<h2>Morning Routine</h2>
<ul>
  <li>Make bed</li>
  <li>Brush teeth</li>
  <li>Exercise for 30 minutes</li>
  <li>Eat healthy breakfast</li>
  <li>Review daily goals</li>
</ul>
```

### Tags or Categories

```html
<h3>Blog Topics</h3>
<ul>
  <li>Web Development</li>
  <li>JavaScript</li>
  <li>React</li>
  <li>Node.js</li>
  <li>CSS</li>
</ul>
```

## Styling Unordered Lists

### Basic CSS Styling

```html
<style>
  .custom-list {
    list-style-type: square;
    padding-left: 30px;
    color: #333;
  }

  .custom-list li {
    margin: 8px 0;
    padding: 5px;
  }
</style>

<ul class="custom-list">
  <li>Square bullets</li>
  <li>Custom spacing</li>
  <li>Styled list items</li>
</ul>
```

### Bullet Styles with list-style-type

```css
ul { list-style-type: disc; }      /* ● Filled circle (default) */
ul { list-style-type: circle; }    /* ○ Empty circle */
ul { list-style-type: square; }    /* ■ Square */
ul { list-style-type: none; }      /* No bullet */
```

### Custom Bullet with Unicode

```html
<style>
  .checkmark-list {
    list-style: none;
    padding-left: 0;
  }

  .checkmark-list li::before {
    content: "✓ ";
    color: #27ae60;
    font-weight: bold;
    margin-right: 10px;
  }
</style>

<ul class="checkmark-list">
  <li>Completed task one</li>
  <li>Completed task two</li>
  <li>Completed task three</li>
</ul>
```

### Icon-based Bullets

```html
<style>
  .icon-list {
    list-style: none;
    padding-left: 0;
  }

  .icon-list li {
    padding-left: 35px;
    margin: 15px 0;
    position: relative;
  }

  .icon-list li::before {
    content: "🎯";
    position: absolute;
    left: 0;
    font-size: 1.2rem;
  }
</style>

<ul class="icon-list">
  <li>Goal number one</li>
  <li>Goal number two</li>
  <li>Goal number three</li>
</ul>
```

### Modern Card-Style List

```html
<style>
  .card-list {
    list-style: none;
    padding: 0;
  }

  .card-list li {
    background: #f8f9fa;
    margin: 15px 0;
    padding: 20px;
    border-left: 4px solid #3498db;
    border-radius: 4px;
    transition: transform 0.2s, box-shadow 0.2s;
  }

  .card-list li:hover {
    transform: translateX(5px);
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  }

  .card-list li::before {
    content: "▸";
    color: #3498db;
    font-weight: bold;
    margin-right: 10px;
    font-size: 1.2rem;
  }
</style>

<ul class="card-list">
  <li>Advanced feature description with hover effect</li>
  <li>Another feature with smooth animation</li>
  <li>Third feature with custom styling</li>
</ul>
```

## Accessibility

### Semantic Use

```html
<!-- ✅ Good: Non-sequential items -->
<h2>Available Colors</h2>
<ul>
  <li>Red</li>
  <li>Blue</li>
  <li>Green</li>
</ul>

<!-- ❌ Bad: Sequential process (should use ol) -->
<h2>Assembly Steps</h2>
<ul> <!-- Should be <ol> -->
  <li>Connect part A</li>
  <li>Secure with screws</li>
  <li>Test connection</li>
</ul>
```

### ARIA for Navigation

```html
<nav aria-label="Main navigation">
  <ul>
    <li><a href="/" aria-current="page">Home</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/services">Services</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

## Complete Examples

### Feature Comparison

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Product Features</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 50px auto;
      padding: 20px;
      background: #f5f5f5;
    }

    .pricing-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
    }

    .plan {
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    .plan h2 {
      color: #2c3e50;
      margin-top: 0;
    }

    .price {
      font-size: 2.5rem;
      color: #3498db;
      margin: 20px 0;
    }

    .plan ul {
      list-style: none;
      padding: 0;
    }

    .plan li {
      padding: 12px 0;
      border-bottom: 1px solid #ecf0f1;
    }

    .plan li::before {
      content: "✓";
      color: #27ae60;
      font-weight: bold;
      margin-right: 10px;
    }

    .plan.featured {
      border: 3px solid #3498db;
      transform: scale(1.05);
    }

    .plan.featured h2 {
      color: #3498db;
    }
  </style>
</head>
<body>
  <h1 style="text-align: center;">Choose Your Plan</h1>

  <div class="pricing-grid">
    <div class="plan">
      <h2>Basic</h2>
      <div class="price">$9<small>/mo</small></div>
      <ul>
        <li>10 GB Storage</li>
        <li>Basic Support</li>
        <li>2 Users</li>
        <li>Email Integration</li>
      </ul>
    </div>

    <div class="plan featured">
      <h2>Pro</h2>
      <div class="price">$29<small>/mo</small></div>
      <ul>
        <li>100 GB Storage</li>
        <li>Priority Support</li>
        <li>10 Users</li>
        <li>Email Integration</li>
        <li>Advanced Analytics</li>
        <li>Custom Domain</li>
      </ul>
    </div>

    <div class="plan">
      <h2>Enterprise</h2>
      <div class="price">$99<small>/mo</small></div>
      <ul>
        <li>Unlimited Storage</li>
        <li>24/7 Support</li>
        <li>Unlimited Users</li>
        <li>Email Integration</li>
        <li>Advanced Analytics</li>
        <li>Custom Domain</li>
        <li>API Access</li>
        <li>White Label</li>
      </ul>
    </div>
  </div>
</body>
</html>
```

### Navigation Menu

```html
<style>
  .main-nav {
    background: #2c3e50;
    padding: 0;
  }

  .main-nav ul {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
  }

  .main-nav li {
    margin: 0;
  }

  .main-nav a {
    display: block;
    padding: 20px 30px;
    color: white;
    text-decoration: none;
    transition: background 0.3s;
  }

  .main-nav a:hover,
  .main-nav a[aria-current="page"] {
    background: #34495e;
  }
</style>

<nav class="main-nav" aria-label="Main navigation">
  <ul>
    <li><a href="/" aria-current="page">Home</a></li>
    <li><a href="/products">Products</a></li>
    <li><a href="/about">About</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

## Browser Support

- **`<ul>` and `<li>`**: Universal support (all browsers, all versions)
- **CSS list-style properties**: Universal support

## Common Mistakes

❌ **Direct text in ul**
```html
<ul>
  Item one
  Item two
</ul>
```

✅ **Wrap in li elements**
```html
<ul>
  <li>Item one</li>
  <li>Item two</li>
</ul>
```

---

❌ **Invalid child elements**
```html
<ul>
  <div>Item</div> <!-- Invalid! -->
</ul>
```

✅ **Only li as direct children**
```html
<ul>
  <li>
    <div>Item content can contain divs</div>
  </li>
</ul>
```

## Practice Exercise

Create a product landing page with:
1. Hero section with product name
2. Feature list with icons
3. Benefits list
4. Pricing with included features
5. Custom styling

### Solution in next topic...

## Additional Resources

- **MDN Web Docs**: [The Unordered List element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul)
- **W3Schools**: [HTML Unordered Lists](https://www.w3schools.com/html/html_lists_unordered.asp)

---

**Previous Topic**: [Ordered Lists](./ordered-lists.md)
**Next Topic**: [Description Lists](./description-lists.md)
**Category**: [Lists and Tables](./README.md)
