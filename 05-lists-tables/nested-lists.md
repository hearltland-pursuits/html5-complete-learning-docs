# Nested Lists

## Overview
Nested lists allow you to create hierarchical structures by placing one list inside another. This is useful for outlining content, creating multi-level menus, showing parent-child relationships, and organizing complex information.

## Basic Syntax

### Nested Unordered Lists

```html
<ul>
  <li>Parent Item 1
    <ul>
      <li>Child Item 1.1</li>
      <li>Child Item 1.2</li>
    </ul>
  </li>
  <li>Parent Item 2
    <ul>
      <li>Child Item 2.1</li>
      <li>Child Item 2.2</li>
    </ul>
  </li>
</ul>
```

### Nested Ordered Lists

```html
<ol>
  <li>Chapter 1
    <ol>
      <li>Section 1.1</li>
      <li>Section 1.2</li>
      <li>Section 1.3</li>
    </ol>
  </li>
  <li>Chapter 2
    <ol>
      <li>Section 2.1</li>
      <li>Section 2.2</li>
    </ol>
  </li>
</ol>
```

### Mixed Lists (ul inside ol)

```html
<ol>
  <li>Prepare ingredients:
    <ul>
      <li>Flour</li>
      <li>Sugar</li>
      <li>Eggs</li>
    </ul>
  </li>
  <li>Mix dry ingredients</li>
  <li>Add wet ingredients</li>
</ol>
```

## Common Use Cases

### Document Outline

```html
<h1>Research Paper</h1>
<ol>
  <li>Introduction
    <ol>
      <li>Background</li>
      <li>Problem Statement</li>
      <li>Objectives</li>
    </ol>
  </li>
  <li>Literature Review
    <ol>
      <li>Previous Studies</li>
      <li>Theoretical Framework</li>
    </ol>
  </li>
  <li>Methodology
    <ol>
      <li>Research Design</li>
      <li>Data Collection</li>
      <li>Analysis Methods</li>
    </ol>
  </li>
  <li>Results</li>
  <li>Discussion</li>
  <li>Conclusion</li>
</ol>
```

### Multi-Level Navigation

```html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li>Products
      <ul>
        <li>Electronics
          <ul>
            <li><a href="/phones">Phones</a></li>
            <li><a href="/laptops">Laptops</a></li>
            <li><a href="/tablets">Tablets</a></li>
          </ul>
        </li>
        <li>Clothing
          <ul>
            <li><a href="/mens">Men's</a></li>
            <li><a href="/womens">Women's</a></li>
            <li><a href="/kids">Kids</a></li>
          </ul>
        </li>
      </ul>
    </li>
    <li><a href="/about">About</a></li>
    <li><a href="/contact">Contact</a></li>
  </ul>
</nav>
```

### File System Structure

```html
<h2>Project Directory</h2>
<ul>
  <li>project-root/
    <ul>
      <li>src/
        <ul>
          <li>components/
            <ul>
              <li>Header.js</li>
              <li>Footer.js</li>
              <li>Sidebar.js</li>
            </ul>
          </li>
          <li>styles/
            <ul>
              <li>main.css</li>
              <li>variables.css</li>
            </ul>
          </li>
          <li>index.js</li>
        </ul>
      </li>
      <li>public/
        <ul>
          <li>images/</li>
          <li>index.html</li>
        </ul>
      </li>
      <li>package.json</li>
      <li>README.md</li>
    </ul>
  </li>
</ul>
```

### Course Curriculum

```html
<h2>Web Development Bootcamp</h2>
<ol>
  <li>Fundamentals (4 weeks)
    <ol>
      <li>Week 1: HTML & CSS Basics
        <ul>
          <li>HTML5 elements</li>
          <li>CSS selectors</li>
          <li>Box model</li>
        </ul>
      </li>
      <li>Week 2: Responsive Design
        <ul>
          <li>Flexbox</li>
          <li>CSS Grid</li>
          <li>Media queries</li>
        </ul>
      </li>
      <li>Week 3: JavaScript Basics</li>
      <li>Week 4: DOM Manipulation</li>
    </ol>
  </li>
  <li>Frontend Frameworks (6 weeks)
    <ol>
      <li>React Fundamentals</li>
      <li>State Management</li>
      <li>Routing</li>
      <li>Hooks</li>
    </ol>
  </li>
  <li>Backend Development (6 weeks)</li>
  <li>Final Project (4 weeks)</li>
</ol>
```

## Styling Nested Lists

### Basic Styling

```html
<style>
  ul {
    line-height: 1.8;
  }

  ul ul {
    margin-top: 10px;
    list-style-type: circle;
  }

  ul ul ul {
    list-style-type: square;
  }
</style>

<ul>
  <li>Level 1 (disc)
    <ul>
      <li>Level 2 (circle)
        <ul>
          <li>Level 3 (square)</li>
        </ul>
      </li>
    </ul>
  </li>
</ul>
```

### Indented Outline

```html
<style>
  .outline {
    font-family: Arial, sans-serif;
  }

  .outline ol {
    counter-reset: item;
    list-style: none;
    padding-left: 30px;
  }

  .outline li {
    counter-increment: item;
    margin: 10px 0;
  }

  .outline li::before {
    content: counters(item, ".") ". ";
    font-weight: bold;
    color: #3498db;
  }
</style>

<div class="outline">
  <ol>
    <li>Introduction
      <ol>
        <li>Background</li>
        <li>Objectives</li>
      </ol>
    </li>
    <li>Main Content
      <ol>
        <li>Section One</li>
        <li>Section Two</li>
      </ol>
    </li>
  </ol>
</div>
```

**Output:**
1. Introduction
   1.1. Background
   1.2. Objectives
2. Main Content
   2.1. Section One
   2.2. Section Two

### Dropdown Navigation Menu

```html
<style>
  .nav-menu {
    list-style: none;
    padding: 0;
    background: #2c3e50;
  }

  .nav-menu > li {
    display: inline-block;
    position: relative;
  }

  .nav-menu a {
    display: block;
    padding: 15px 20px;
    color: white;
    text-decoration: none;
  }

  .nav-menu a:hover {
    background: #34495e;
  }

  .nav-menu ul {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    background: #34495e;
    min-width: 200px;
    list-style: none;
    padding: 0;
    box-shadow: 0 2px 10px rgba(0,0,0,0.3);
  }

  .nav-menu li:hover > ul {
    display: block;
  }

  .nav-menu ul li {
    display: block;
  }
</style>

<ul class="nav-menu">
  <li><a href="/">Home</a></li>
  <li><a href="/products">Products</a>
    <ul>
      <li><a href="/electronics">Electronics</a></li>
      <li><a href="/clothing">Clothing</a></li>
      <li><a href="/books">Books</a></li>
    </ul>
  </li>
  <li><a href="/about">About</a></li>
  <li><a href="/contact">Contact</a></li>
</ul>
```

## Complete Example: Legal Document Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Terms and Conditions</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 900px;
      margin: 50px auto;
      padding: 20px;
      line-height: 1.8;
      color: #333;
    }

    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #3498db;
      padding-bottom: 10px;
    }

    .legal-doc {
      counter-reset: section;
    }

    .legal-doc > ol {
      list-style: none;
      counter-reset: item;
      padding-left: 0;
    }

    .legal-doc > ol > li {
      counter-increment: item;
      margin: 30px 0;
    }

    .legal-doc > ol > li::before {
      content: counter(item) ". ";
      font-weight: bold;
      font-size: 1.3rem;
      color: #3498db;
    }

    .legal-doc > ol > li > strong {
      font-size: 1.2rem;
      color: #2c3e50;
    }

    .legal-doc ol ol {
      counter-reset: subitem;
      list-style: none;
      padding-left: 30px;
      margin-top: 15px;
    }

    .legal-doc ol ol li {
      counter-increment: subitem;
      margin: 10px 0;
    }

    .legal-doc ol ol li::before {
      content: counter(item) "." counter(subitem) " ";
      font-weight: bold;
      color: #555;
    }
  </style>
</head>
<body>
  <h1>Terms and Conditions</h1>
  <p><strong>Effective Date:</strong> January 1, 2024</p>
  <p>Please read these terms carefully before using our service.</p>

  <div class="legal-doc">
    <ol>
      <li><strong>Acceptance of Terms</strong>
        <p>By accessing and using this service, you accept and agree to be bound by the terms and provision of this agreement.</p>
        <ol>
          <li>You must be at least 18 years old to use this service</li>
          <li>You agree to provide accurate and complete information</li>
          <li>You are responsible for maintaining account security</li>
        </ol>
      </li>

      <li><strong>User Obligations</strong>
        <p>As a user of this service, you agree to comply with all applicable laws and regulations.</p>
        <ol>
          <li>Prohibited Activities
            <ol>
              <li>Violating any laws or regulations</li>
              <li>Infringing on intellectual property rights</li>
              <li>Transmitting viruses or malicious code</li>
            </ol>
          </li>
          <li>Account Responsibilities
            <ol>
              <li>Maintain confidentiality of login credentials</li>
              <li>Notify us immediately of unauthorized access</li>
              <li>Accept responsibility for all account activity</li>
            </ol>
          </li>
        </ol>
      </li>

      <li><strong>Privacy Policy</strong>
        <p>We are committed to protecting your privacy and personal information.</p>
        <ol>
          <li>We collect only necessary information</li>
          <li>Data is stored securely and encrypted</li>
          <li>We never sell personal information to third parties</li>
        </ol>
      </li>

      <li><strong>Intellectual Property</strong>
        <p>All content on this platform is protected by copyright and trademark laws.</p>
        <ol>
          <li>You retain ownership of content you create</li>
          <li>You grant us a license to display your content</li>
          <li>You may not reproduce our proprietary content</li>
        </ol>
      </li>

      <li><strong>Limitation of Liability</strong>
        <p>We provide this service "as is" without warranties of any kind.</p>
        <ol>
          <li>We are not liable for any indirect or consequential damages</li>
          <li>Our total liability shall not exceed fees paid by you</li>
          <li>Some jurisdictions do not allow liability limitations</li>
        </ol>
      </li>

      <li><strong>Termination</strong>
        <p>We reserve the right to terminate or suspend access to our service.</p>
        <ol>
          <li>We may terminate for violation of these terms</li>
          <li>You may terminate your account at any time</li>
          <li>Certain provisions survive termination</li>
        </ol>
      </li>
    </ol>
  </div>

  <p style="margin-top: 50px; font-style: italic; color: #7f8c8d;">
    Last updated: January 1, 2024
  </p>
</body>
</html>
```

## Accessibility

### Proper Nesting

```html
<!-- ✅ Correct: Nested list inside li element -->
<ul>
  <li>Parent
    <ul>
      <li>Child</li>
    </ul>
  </li>
</ul>

<!-- ❌ Incorrect: Nested list as sibling -->
<ul>
  <li>Parent</li>
  <ul> <!-- Wrong! Should be inside li -->
    <li>Child</li>
  </ul>
</ul>
```

### ARIA for Complex Menus

```html
<nav aria-label="Main navigation">
  <ul role="menubar">
    <li role="none">
      <a href="/" role="menuitem">Home</a>
    </li>
    <li role="none">
      <a href="/products" role="menuitem" aria-haspopup="true" aria-expanded="false">
        Products
      </a>
      <ul role="menu">
        <li role="none">
          <a href="/electronics" role="menuitem">Electronics</a>
        </li>
      </ul>
    </li>
  </ul>
</nav>
```

## Browser Support

- **Nested lists**: Universal support (all browsers, all versions)
- **Unlimited nesting depth**: Supported, but 3-4 levels recommended for usability

## Common Mistakes

❌ **Nested list outside li**
```html
<ul>
  <li>Item 1</li>
  <ul> <!-- Wrong placement! -->
    <li>Subitem</li>
  </ul>
</ul>
```

✅ **Nested list inside li**
```html
<ul>
  <li>Item 1
    <ul>
      <li>Subitem</li>
    </ul>
  </li>
</ul>
```

---

❌ **Too many nesting levels**
```html
<ul>
  <li>Level 1
    <ul>
      <li>Level 2
        <ul>
          <li>Level 3
            <ul>
              <li>Level 4
                <ul>
                  <li>Level 5 - Too deep!</li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </li>
</ul>
```

✅ **Limit to 3-4 levels**
```html
<ul>
  <li>Level 1
    <ul>
      <li>Level 2
        <ul>
          <li>Level 3</li>
        </ul>
      </li>
    </ul>
  </li>
</ul>
```

## Additional Resources

- **MDN Web Docs**: [HTML Lists](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul)
- **W3Schools**: [HTML Nested Lists](https://www.w3schools.com/html/html_lists.asp)

---

**Previous Topic**: [Description Lists](./description-lists.md)
**Next Topic**: [Table Structure](./table-structure.md)
**Category**: [Lists and Tables](./README.md)
