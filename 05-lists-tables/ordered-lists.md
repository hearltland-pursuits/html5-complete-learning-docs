# Ordered Lists

## Overview
The `<ol>` (ordered list) element represents a list of items where the order matters. Items are typically displayed with numbers, letters, or Roman numerals. Ordered lists are used for sequential steps, rankings, instructions, and any content where order is significant.

## Basic Syntax

```html
<ol>
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ol>
```

**Output:**
1. First item
2. Second item
3. Third item

## List Item Element

### The `<li>` Element

Each list item is wrapped in an `<li>` (list item) element.

```html
<ol>
  <li>Mix dry ingredients</li>
  <li>Add wet ingredients</li>
  <li>Stir until combined</li>
  <li>Bake at 350°F for 30 minutes</li>
</ol>
```

### Value Attribute

Set a specific starting number for an item (affects subsequent items).

```html
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
  <li value="10">Item 10</li>  <!-- Jumps to 10 -->
  <li>Item 11</li>              <!-- Continues from 10 -->
  <li>Item 12</li>
</ol>
```

**Output:**
1. Item 1
2. Item 2
10. Item 10
11. Item 11
12. Item 12

## Ordered List Attributes

### start

Specify the starting number for the list.

```html
<ol start="5">
  <li>Fifth item</li>
  <li>Sixth item</li>
  <li>Seventh item</li>
</ol>
```

**Output:**
5. Fifth item
6. Sixth item
7. Seventh item

### type

Change the numbering style.

```html
<!-- Decimal numbers (default) -->
<ol type="1">
  <li>One</li>
  <li>Two</li>
  <li>Three</li>
</ol>

<!-- Lowercase letters -->
<ol type="a">
  <li>Alpha</li>
  <li>Bravo</li>
  <li>Charlie</li>
</ol>

<!-- Uppercase letters -->
<ol type="A">
  <li>Alpha</li>
  <li>Bravo</li>
  <li>Charlie</li>
</ol>

<!-- Lowercase Roman numerals -->
<ol type="i">
  <li>Unus</li>
  <li>Duo</li>
  <li>Tres</li>
</ol>

<!-- Uppercase Roman numerals -->
<ol type="I">
  <li>Unus</li>
  <li>Duo</li>
  <li>Tres</li>
</ol>
```

**Output:**

**type="1"** (default):
1. One
2. Two
3. Three

**type="a"**:
a. Alpha
b. Bravo
c. Charlie

**type="A"**:
A. Alpha
B. Bravo
C. Charlie

**type="i"**:
i. Unus
ii. Duo
iii. Tres

**type="I"**:
I. Unus
II. Duo
III. Tres

### reversed

Display list in reverse order (countdown).

```html
<ol reversed>
  <li>Third place</li>
  <li>Second place</li>
  <li>First place - Winner!</li>
</ol>
```

**Output:**
3. Third place
2. Second place
1. First place - Winner!

**Countdown example:**
```html
<h2>Top 5 Movies of 2024</h2>
<ol start="5" reversed>
  <li>Movie Title #5</li>
  <li>Movie Title #4</li>
  <li>Movie Title #3</li>
  <li>Movie Title #2</li>
  <li>Movie Title #1 (Best!)</li>
</ol>
```

**Output:**
5. Movie Title #5
4. Movie Title #4
3. Movie Title #3
2. Movie Title #2
1. Movie Title #1 (Best!)

## Common Use Cases

### Step-by-Step Instructions

```html
<h2>How to Make Coffee</h2>
<ol>
  <li>Boil water</li>
  <li>Grind coffee beans (medium-coarse)</li>
  <li>Add 2 tablespoons of coffee to French press</li>
  <li>Pour hot water over grounds</li>
  <li>Wait 4 minutes</li>
  <li>Press plunger down slowly</li>
  <li>Pour and enjoy!</li>
</ol>
```

### Ranking or Top Lists

```html
<h2>Top 3 Programming Languages 2024</h2>
<ol>
  <li>Python</li>
  <li>JavaScript</li>
  <li>Java</li>
</ol>
```

### Table of Contents

```html
<h1>User Manual</h1>
<ol>
  <li><a href="#introduction">Introduction</a></li>
  <li><a href="#installation">Installation</a></li>
  <li><a href="#configuration">Configuration</a></li>
  <li><a href="#usage">Usage</a></li>
  <li><a href="#troubleshooting">Troubleshooting</a></li>
</ol>
```

### Multi-level Numbered Sections

```html
<h2>Document Outline</h2>
<ol>
  <li>Introduction
    <ol>
      <li>Background</li>
      <li>Objectives</li>
    </ol>
  </li>
  <li>Methodology
    <ol>
      <li>Data Collection</li>
      <li>Analysis</li>
    </ol>
  </li>
  <li>Results</li>
  <li>Conclusion</li>
</ol>
```

### Legal or Technical Documents

```html
<h2>Terms and Conditions</h2>
<ol>
  <li>Acceptance of Terms</li>
  <li>User Obligations</li>
  <li>Privacy Policy</li>
  <li>Limitation of Liability</li>
  <li>Termination</li>
</ol>
```

### Recipe Instructions

```html
<article>
  <h2>Chocolate Chip Cookies</h2>

  <h3>Ingredients:</h3>
  <ul>
    <li>2 cups flour</li>
    <li>1 cup butter</li>
    <li>1 cup sugar</li>
    <li>2 eggs</li>
    <li>2 cups chocolate chips</li>
  </ul>

  <h3>Instructions:</h3>
  <ol>
    <li>Preheat oven to 375°F (190°C)</li>
    <li>Mix butter and sugar until creamy</li>
    <li>Beat in eggs one at a time</li>
    <li>Gradually blend in flour</li>
    <li>Stir in chocolate chips</li>
    <li>Drop spoonfuls onto baking sheet</li>
    <li>Bake for 10-12 minutes</li>
    <li>Cool on wire rack</li>
  </ol>
</article>
```

## Styling Ordered Lists

### Basic CSS Styling

```html
<style>
  .custom-list {
    list-style-type: upper-roman;
    padding-left: 40px;
    color: #333;
  }

  .custom-list li {
    margin: 10px 0;
    padding: 5px;
  }

  .custom-list li:hover {
    background: #f0f0f0;
  }
</style>

<ol class="custom-list">
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
</ol>
```

### Custom Markers with list-style-type

```css
/* CSS list-style-type values */
ol { list-style-type: decimal; }        /* 1, 2, 3 (default) */
ol { list-style-type: decimal-leading-zero; } /* 01, 02, 03 */
ol { list-style-type: lower-alpha; }    /* a, b, c */
ol { list-style-type: upper-alpha; }    /* A, B, C */
ol { list-style-type: lower-roman; }    /* i, ii, iii */
ol { list-style-type: upper-roman; }    /* I, II, III */
ol { list-style-type: lower-greek; }    /* α, β, γ */
ol { list-style-type: none; }           /* No markers */
```

### Custom Counter Styling

```html
<style>
  .custom-counter {
    list-style: none;
    counter-reset: item;
    padding-left: 0;
  }

  .custom-counter li {
    counter-increment: item;
    margin: 15px 0;
    padding-left: 40px;
    position: relative;
  }

  .custom-counter li::before {
    content: counter(item);
    position: absolute;
    left: 0;
    top: 0;
    background: #3498db;
    color: white;
    width: 28px;
    height: 28px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
  }
</style>

<ol class="custom-counter">
  <li>First step with custom circular marker</li>
  <li>Second step</li>
  <li>Third step</li>
</ol>
```

### Styled Steps List

```html
<style>
  .steps {
    list-style: none;
    padding: 0;
    counter-reset: step;
  }

  .steps li {
    counter-increment: step;
    margin: 20px 0;
    padding: 20px 20px 20px 70px;
    background: #f8f9fa;
    border-left: 4px solid #3498db;
    position: relative;
    border-radius: 4px;
  }

  .steps li::before {
    content: "Step " counter(step);
    position: absolute;
    left: 15px;
    top: 20px;
    font-weight: bold;
    color: #3498db;
    font-size: 0.85rem;
    text-transform: uppercase;
  }
</style>

<ol class="steps">
  <li>Create a new HTML file and open it in your editor</li>
  <li>Add the basic HTML5 document structure</li>
  <li>Insert your content within the body tags</li>
  <li>Save and preview in a browser</li>
</ol>
```

## Accessibility Considerations

### Proper Semantic Use

```html
<!-- ✅ Good: Sequential content -->
<h2>Assembly Instructions</h2>
<ol>
  <li>Unpack all components</li>
  <li>Identify parts A, B, and C</li>
  <li>Connect part A to part B</li>
  <li>Secure with screws</li>
</ol>

<!-- ❌ Bad: Non-sequential content -->
<h2>Product Features</h2>
<ol> <!-- Should be <ul> instead -->
  <li>Wireless connectivity</li>
  <li>Long battery life</li>
  <li>Compact design</li>
</ol>
```

### Screen Reader Friendly

```html
<nav aria-label="Tutorial navigation">
  <h2>Course Modules</h2>
  <ol>
    <li><a href="#module1">Introduction to HTML</a></li>
    <li><a href="#module2">CSS Basics</a></li>
    <li><a href="#module3">JavaScript Fundamentals</a></li>
  </ol>
</nav>
```

### Complex Lists with Context

```html
<article>
  <h2>Project Timeline</h2>
  <p>Complete the following phases in order:</p>
  <ol>
    <li>
      <strong>Planning Phase</strong> (Week 1-2)
      <p>Define project scope and requirements</p>
    </li>
    <li>
      <strong>Development Phase</strong> (Week 3-8)
      <p>Build and test core features</p>
    </li>
    <li>
      <strong>Deployment Phase</strong> (Week 9-10)
      <p>Launch to production and monitor</p>
    </li>
  </ol>
</article>
```

## Complete Examples

### Tutorial Steps

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Git Tutorial</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 50px auto;
      padding: 20px;
      line-height: 1.6;
    }

    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #3498db;
      padding-bottom: 10px;
    }

    .tutorial-steps {
      list-style: none;
      counter-reset: step;
      padding: 0;
    }

    .tutorial-steps li {
      counter-increment: step;
      margin: 30px 0;
      padding: 25px;
      background: #f8f9fa;
      border-radius: 8px;
      position: relative;
      padding-left: 80px;
    }

    .tutorial-steps li::before {
      content: counter(step);
      position: absolute;
      left: 20px;
      top: 50%;
      transform: translateY(-50%);
      background: #3498db;
      color: white;
      width: 45px;
      height: 45px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.5rem;
      font-weight: bold;
    }

    .tutorial-steps h3 {
      margin-top: 0;
      color: #2c3e50;
    }

    code {
      background: #2c3e50;
      color: #ecf0f1;
      padding: 2px 8px;
      border-radius: 3px;
      font-family: 'Courier New', monospace;
    }

    pre {
      background: #2c3e50;
      color: #ecf0f1;
      padding: 15px;
      border-radius: 5px;
      overflow-x: auto;
    }
  </style>
</head>
<body>
  <h1>Git Basics Tutorial</h1>
  <p>Follow these steps to get started with Git version control</p>

  <ol class="tutorial-steps">
    <li>
      <h3>Install Git</h3>
      <p>Download and install Git from the official website:</p>
      <pre>https://git-scm.com/downloads</pre>
      <p>Verify installation by running:</p>
      <pre>git --version</pre>
    </li>

    <li>
      <h3>Configure Git</h3>
      <p>Set your username and email:</p>
      <pre>git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"</pre>
    </li>

    <li>
      <h3>Initialize Repository</h3>
      <p>Create a new Git repository in your project folder:</p>
      <pre>cd your-project
git init</pre>
    </li>

    <li>
      <h3>Add Files</h3>
      <p>Stage files for commit:</p>
      <pre>git add .
# or add specific files
git add file1.html file2.css</pre>
    </li>

    <li>
      <h3>Commit Changes</h3>
      <p>Create your first commit:</p>
      <pre>git commit -m "Initial commit"</pre>
    </li>

    <li>
      <h3>Connect to Remote</h3>
      <p>Link your local repository to GitHub:</p>
      <pre>git remote add origin https://github.com/username/repo.git
git push -u origin main</pre>
    </li>
  </ol>
</body>
</html>
```

### Top 10 Ranking

```html
<article style="max-width: 600px; margin: 0 auto; padding: 20px;">
  <h1>Top 10 Web Development Tools 2024</h1>

  <ol start="10" reversed style="font-size: 1.1rem; line-height: 2;">
    <li><strong>WebStorm</strong> - Powerful JavaScript IDE</li>
    <li><strong>Postman</strong> - API testing platform</li>
    <li><strong>Figma</strong> - Collaborative design tool</li>
    <li><strong>Docker</strong> - Containerization platform</li>
    <li><strong>GitHub</strong> - Version control and collaboration</li>
    <li><strong>npm</strong> - Package manager for JavaScript</li>
    <li><strong>Chrome DevTools</strong> - Browser debugging tools</li>
    <li><strong>VS Code</strong> - Popular code editor</li>
    <li><strong>Git</strong> - Distributed version control system</li>
    <li><strong>Stack Overflow</strong> - Developer Q&A community 🏆</li>
  </ol>
</article>
```

## Browser Support

- **`<ol>` and `<li>`**: Universal support (all browsers, all versions)
- **`start` attribute**: Universal support
- **`type` attribute**: Universal support
- **`reversed` attribute**: Modern browsers (Chrome 18+, Firefox 18+, Safari 6+, Edge 79+)
- **`value` attribute on `<li>`**: Universal support

## Common Mistakes

❌ **Skipping closing tags**
```html
<ol>
  <li>Item 1
  <li>Item 2
  <li>Item 3
</ol>
```

✅ **Always close li tags**
```html
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ol>
```

---

❌ **Direct text in ol (no li)**
```html
<ol>
  First item
  Second item
</ol>
```

✅ **Wrap items in li elements**
```html
<ol>
  <li>First item</li>
  <li>Second item</li>
</ol>
```

---

❌ **Using ol for non-sequential content**
```html
<ol>
  <li>Red color</li>
  <li>Blue color</li>
  <li>Green color</li>
</ol>
```

✅ **Use ul for non-sequential items**
```html
<ul>
  <li>Red color</li>
  <li>Blue color</li>
  <li>Green color</li>
</ul>
```

## Practice Exercise

Create a recipe page with:
1. Recipe title
2. Ingredients list (unordered)
3. Instructions (ordered)
4. Custom styling
5. Prep time and cook time info

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Classic Pancakes Recipe</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 700px;
      margin: 50px auto;
      padding: 20px;
      background: #f9f9f9;
    }

    .recipe {
      background: white;
      padding: 40px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    h1 {
      color: #2c3e50;
      font-size: 2.5rem;
      margin-bottom: 10px;
    }

    .meta {
      display: flex;
      gap: 30px;
      margin: 20px 0;
      padding: 15px;
      background: #fff3cd;
      border-radius: 5px;
    }

    .meta-item {
      display: flex;
      flex-direction: column;
    }

    .meta-item strong {
      color: #856404;
      font-size: 0.85rem;
      text-transform: uppercase;
    }

    .meta-item span {
      font-size: 1.2rem;
      color: #2c3e50;
    }

    h2 {
      color: #3498db;
      margin-top: 30px;
      border-bottom: 2px solid #3498db;
      padding-bottom: 5px;
    }

    ul {
      line-height: 2;
    }

    ol {
      line-height: 2;
      padding-left: 25px;
    }

    ol li {
      margin: 15px 0;
    }
  </style>
</head>
<body>
  <article class="recipe">
    <h1>Classic Pancakes</h1>
    <p>Fluffy, golden pancakes perfect for breakfast or brunch</p>

    <div class="meta">
      <div class="meta-item">
        <strong>Prep Time</strong>
        <span>10 min</span>
      </div>
      <div class="meta-item">
        <strong>Cook Time</strong>
        <span>15 min</span>
      </div>
      <div class="meta-item">
        <strong>Servings</strong>
        <span>4 people</span>
      </div>
    </div>

    <h2>Ingredients</h2>
    <ul>
      <li>1½ cups all-purpose flour</li>
      <li>3½ teaspoons baking powder</li>
      <li>1 tablespoon white sugar</li>
      <li>¼ teaspoon salt</li>
      <li>1¼ cups milk</li>
      <li>3 tablespoons melted butter</li>
      <li>1 egg</li>
    </ul>

    <h2>Instructions</h2>
    <ol>
      <li>In a large bowl, sift together flour, baking powder, sugar, and salt</li>
      <li>Make a well in the center and add milk, melted butter, and egg</li>
      <li>Mix until smooth (don't overmix - small lumps are okay)</li>
      <li>Heat a lightly oiled griddle or frying pan over medium-high heat</li>
      <li>Pour ¼ cup batter onto the griddle for each pancake</li>
      <li>Cook until bubbles form on surface (about 2-3 minutes)</li>
      <li>Flip and cook until golden brown on other side (about 2 minutes)</li>
      <li>Serve hot with butter, maple syrup, and fresh berries</li>
    </ol>

    <p style="margin-top: 30px; padding: 15px; background: #e8f4f8; border-left: 4px solid #3498db; border-radius: 4px;">
      <strong>💡 Tip:</strong> For extra fluffy pancakes, let the batter rest for 5 minutes before cooking.
    </p>
  </article>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [The Ordered List element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ol)
- **W3Schools**: [HTML Ordered Lists](https://www.w3schools.com/html/html_lists_ordered.asp)
- **CSS-Tricks**: [Styling Lists](https://css-tricks.com/almanac/properties/l/list-style/)

---

**Previous Topic**: [Lazy Loading](../04-media-elements/lazy-loading.md)
**Next Topic**: [Unordered Lists](./unordered-lists.md)
**Category**: [Lists and Tables](./README.md)
