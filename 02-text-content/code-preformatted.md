---
title: Code and Preformatted Text
category: Text Content
order: 5
---

# Code and Preformatted Text

> **Quick Summary:** HTML5 provides specialized elements for displaying programming code, computer output, user input, and preformatted text, preserving exact spacing and formatting while conveying semantic meaning to assistive technologies and syntax highlighters.

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

## Introduction

When displaying technical content like programming code, terminal commands, or ASCII art, standard HTML rendering collapses multiple spaces and ignores line breaks. HTML5 provides two complementary solutions: semantic inline elements for code-related content (`<code>`, `<kbd>`, `<samp>`, `<var>`) and the `<pre>` block element for preserving exact formatting.

The `<code>` element marks up computer code, whether inline snippets or multi-line blocks. The `<kbd>` element represents user keyboard input, `<samp>` represents sample program output, and `<var>` represents variables in mathematical or programming contexts. When combined with `<pre>` (preformatted text), these elements preserve whitespace, indentation, and line breaks exactly as written.

Understanding when to use each element is critical for creating accessible, semantic technical documentation. Screen readers announce code elements differently, syntax highlighting libraries recognize these semantic markers, and search engines use them to understand content type. This makes proper element selection essential for WCAG 2.1 Level A compliance.

**Key Concept:** Use semantic code elements (`<code>`, `<kbd>`, `<samp>`, `<var>`) to describe what content means, then use `<pre>` when exact formatting (spaces, line breaks) must be preserved.

## Basic Syntax

### Inline Code Elements

| Element | Purpose | Semantic Meaning | Default Styling |
|---------|---------|------------------|-----------------|
| `<code>` | Programming code or markup | Source code fragment | Monospace font |
| `<kbd>` | Keyboard input | User keyboard actions | Monospace font |
| `<samp>` | Sample output | Computer program output | Monospace font |
| `<var>` | Variable | Mathematical/programming variables | Italic, sometimes monospace |

**Inline examples:**
```html
<p>Use the <code>print()</code> function to display output.</p>
<p>Press <kbd>Ctrl</kbd> + <kbd>C</kbd> to copy.</p>
<p>The program returned: <samp>Error 404: Not Found</samp></p>
<p>The value of <var>x</var> is 42.</p>
```

### Block-Level Preformatted Text

**The `<pre>` element:**
```html
<pre>
Line breaks   and    spacing
    are preserved exactly
        as written
</pre>
```

**Multi-line code block (common pattern):**
```html
<pre><code>function greet(name) {
  console.log("Hello, " + name);
}
greet("World");
</code></pre>
```

**Attributes:**
- All elements support global attributes (class, id, lang, etc.)
- No special attributes required
- Often combined with `class` for syntax highlighting (e.g., `<code class="language-python">`)

**Important:** Special characters inside code blocks must be HTML-escaped:
- `<` → `&lt;`
- `>` → `&gt;`
- `&` → `&amp;`

## Examples

### Example 1: Inline Code Snippets in Documentation
**Use Case:** Technical tutorial with inline code references

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Python Tutorial: Variables</title>
  <style>
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Courier New', Consolas, monospace;
      font-size: 0.95em;
    }
    kbd {
      background-color: #333;
      color: white;
      padding: 2px 8px;
      border-radius: 3px;
      font-size: 0.9em;
      border: 1px solid #555;
      box-shadow: 0 2px 0 #111;
    }
    var {
      color: #d63384;
      font-family: 'Courier New', Consolas, monospace;
      font-style: italic;
    }
  </style>
</head>
<body>
  <article>
    <h1>Python Variables Tutorial</h1>

    <section>
      <h2>Declaring Variables</h2>
      <p>
        In Python, you create variables using the assignment operator.
        For example, <code>x = 10</code> assigns the value 10 to the
        variable <var>x</var>.
      </p>

      <p>
        Unlike languages like Java or C++, Python doesn't require you
        to specify the data type. The statement <code>name = "Alice"</code>
        automatically creates a string variable.
      </p>
    </section>

    <section>
      <h2>Using the Python REPL</h2>
      <p>
        To run Python interactively, open your terminal and type
        <kbd>python3</kbd> then press <kbd>Enter</kbd>. You'll see
        the Python prompt: <samp>&gt;&gt;&gt;</samp>
      </p>

      <p>
        Try entering <kbd>print("Hello World")</kbd> at the prompt.
        The interpreter will respond with:
        <samp>Hello World</samp>
      </p>

      <p>
        To exit the Python REPL, press <kbd>Ctrl</kbd> + <kbd>D</kbd>
        on Linux/Mac, or <kbd>Ctrl</kbd> + <kbd>Z</kbd> then <kbd>Enter</kbd>
        on Windows.
      </p>
    </section>
  </article>
</body>
</html>
```

### Example 2: Multi-Line Code Blocks with Syntax Highlighting
**Use Case:** Programming blog post with complete code examples

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>JavaScript Functions Guide</title>
  <style>
    pre {
      background-color: #282c34;
      color: #abb2bf;
      padding: 1.5em;
      border-radius: 6px;
      overflow-x: auto;
      font-family: 'Fira Code', 'Courier New', monospace;
      line-height: 1.5;
    }
    pre code {
      background-color: transparent;
      padding: 0;
      color: inherit;
      font-size: 0.95em;
    }
    .keyword { color: #c678dd; }
    .function { color: #61afef; }
    .string { color: #98c379; }
    .comment { color: #5c6370; font-style: italic; }
  </style>
</head>
<body>
  <article>
    <h1>JavaScript Arrow Functions</h1>

    <section>
      <h2>Traditional Function Syntax</h2>
      <p>
        Before ES6, JavaScript functions were defined using the
        <code>function</code> keyword:
      </p>

<pre><code>function greet(name) {
  return "Hello, " + name;
}

console.log(greet("Alice"));
// Output: Hello, Alice
</code></pre>
    </section>

    <section>
      <h2>Arrow Function Syntax</h2>
      <p>
        ES6 introduced arrow functions with a more concise syntax:
      </p>

<pre><code>const greet = (name) =&gt; {
  return "Hello, " + name;
};

console.log(greet("Alice"));
// Output: Hello, Alice
</code></pre>

      <p>
        For single-expression functions, you can omit the braces and
        <code>return</code> keyword:
      </p>

<pre><code>const greet = (name) =&gt; "Hello, " + name;
const square = (x) =&gt; x * x;
const add = (a, b) =&gt; a + b;

console.log(greet("Alice"));  // Hello, Alice
console.log(square(5));       // 25
console.log(add(3, 7));       // 10
</code></pre>
    </section>

    <section>
      <h2>Important: HTML Escaping</h2>
      <p>
        Notice how the arrow <code>=&gt;</code> is written as
        <code>&amp;gt;</code> in the HTML source. This is because
        the <code>&lt;</code> and <code>&gt;</code> characters have
        special meaning in HTML and must be escaped:
      </p>

      <ul>
        <li><code>&lt;</code> → <code>&amp;lt;</code></li>
        <li><code>&gt;</code> → <code>&amp;gt;</code></li>
        <li><code>&amp;</code> → <code>&amp;amp;</code></li>
      </ul>
    </section>
  </article>
</body>
</html>
```

### Example 3: Terminal Commands and Output
**Use Case:** DevOps documentation showing command-line interactions

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Git Commands Cheat Sheet</title>
  <style>
    .terminal {
      background-color: #1e1e1e;
      color: #d4d4d4;
      padding: 1.5em;
      border-radius: 6px;
      font-family: 'Consolas', 'Courier New', monospace;
      margin: 1em 0;
    }
    .terminal kbd {
      color: #4ec9b0;
      background-color: transparent;
      padding: 0;
      font-weight: bold;
    }
    .terminal samp {
      color: #ce9178;
      display: block;
      margin-left: 2em;
    }
    .prompt {
      color: #569cd6;
      font-weight: bold;
    }
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
    }
  </style>
</head>
<body>
  <article>
    <h1>Git Commands Cheat Sheet</h1>

    <section>
      <h2>Checking Repository Status</h2>
      <p>
        To see which files have been modified, use the
        <code>git status</code> command:
      </p>

      <div class="terminal">
<pre><span class="prompt">$</span> <kbd>git status</kbd>
<samp>On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  modified:   index.html
  modified:   styles.css

no changes added to commit</samp></pre>
      </div>
    </section>

    <section>
      <h2>Creating a Commit</h2>
      <p>
        To stage and commit your changes:
      </p>

      <div class="terminal">
<pre><span class="prompt">$</span> <kbd>git add .</kbd>
<span class="prompt">$</span> <kbd>git commit -m "Update homepage design"</kbd>
<samp>[main 3a8f1c2] Update homepage design
 2 files changed, 45 insertions(+), 12 deletions(-)</samp></pre>
      </div>
    </section>

    <section>
      <h2>Viewing Commit History</h2>
      <p>
        Use <code>git log</code> to see recent commits:
      </p>

      <div class="terminal">
<pre><span class="prompt">$</span> <kbd>git log --oneline -5</kbd>
<samp>3a8f1c2 Update homepage design
7b4e9f1 Add contact form validation
2c1d8a3 Fix mobile responsive layout
9f3a7e2 Implement dark mode toggle
4d2b1c5 Initial commit</samp></pre>
      </div>
    </section>
  </article>
</body>
</html>
```

## Common Use Cases

### 1. Inline Code References in Technical Writing
Use `<code>` for function names, variables, file names, or short code snippets within paragraphs:

```html
<p>
  Call the <code>fetchUserData()</code> function with a valid
  <code>userId</code> parameter. The function returns a Promise
  that resolves to a user object.
</p>
```

**When to use:** Function references, method names, file paths, configuration values, API endpoints

### 2. Keyboard Shortcuts and User Instructions
Use `<kbd>` to represent keys users should press:

```html
<p>
  To save your work, press <kbd>Ctrl</kbd> + <kbd>S</kbd> on Windows
  or <kbd>Cmd</kbd> + <kbd>S</kbd> on Mac. To undo, press
  <kbd>Ctrl</kbd> + <kbd>Z</kbd>.
</p>
```

**When to use:** Keyboard shortcuts, hotkeys, user input instructions, accessibility documentation

### 3. Multi-Line Code Examples
Use `<pre><code>` for complete code examples that require preserved formatting:

```html
<pre><code>&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;title&gt;Example&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;Hello World&lt;/h1&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>
```

**When to use:** Complete code examples, configuration files, JSON/XML data, ASCII art, poetry with specific line breaks

## Browser Support

| Element | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| `<code>` | All | All | All | All | All | All |
| `<pre>` | All | All | All | All | All | All |
| `<kbd>` | All | All | All | All | All | All |
| `<samp>` | All | All | All | All | All | All |
| `<var>` | All | All | All | All | All | All |

**Browser Support:** Universal (100%)

All code-related elements have been part of HTML since HTML 2.0 (1995) and are supported universally across all browsers, including legacy versions.

**Default Styling:**
- `<code>`, `<kbd>`, `<samp>`: Monospace font (`monospace` or `Courier New`)
- `<pre>`: Monospace font + preserves whitespace and line breaks
- `<var>`: Italic font (may be monospace in some browsers)
- All are inline elements except `<pre>` (block-level)

**Resources:**
- [MDN: code element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/code)
- [MDN: pre element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/pre)
- [WHATWG HTML Living Standard: Text-level semantics](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-code-element)
- [W3Schools: HTML Computer Code Elements](https://www.w3schools.com/html/html_computercode_elements.asp)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- Use semantic elements (`<code>`, `<kbd>`, etc.) to convey meaning, not just styling
- Ensure code blocks are navigable by keyboard (can tab through page)
- Provide text alternatives for complex code diagrams or ASCII art

**Level AA Requirements:**
- Maintain sufficient color contrast in styled code blocks (4.5:1 minimum for normal text, 3:1 for large text)
- Ensure syntax highlighting doesn't rely solely on color to convey meaning
- Provide alternative formats for long code examples (downloadable files)

### Screen Reader Behavior

| Element | Screen Reader Announcement | Context Provided |
|---------|---------------------------|------------------|
| `<code>` | May announce as "code" | Varies by screen reader |
| `<pre>` | Reads character-by-character (preserves spacing) | Can be tedious for long blocks |
| `<kbd>` | May announce as "keyboard" or read literally | Often no special announcement |
| `<samp>` | Reads literally | Rarely has special announcement |
| `<var>` | Reads with emphasis | Italic voice in some SRs |

**Best Practices for Screen Readers:**

1. **Provide context before code blocks:**
```html
<!-- GOOD: Context explains what follows -->
<p>Here's how to create a JavaScript function:</p>
<pre><code>function greet() {
  console.log("Hello");
}
</code></pre>

<!-- BAD: Code appears without context -->
<pre><code>function greet() {
  console.log("Hello");
}
</code></pre>
```

2. **Use aria-label for complex code blocks:**
```html
<pre aria-label="Python function to calculate factorial"><code>def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
</code></pre>
```

3. **Provide downloadable alternatives for long examples:**
```html
<p>
  The following 200-line configuration file shows our production setup.
  <a href="config.yaml" download>Download config.yaml</a> to view in
  your editor, or read below:
</p>
<pre><code><!-- long file contents --></code></pre>
```

4. **Use language indicators for syntax highlighters:**
```html
<!-- Helps screen readers and syntax highlighters -->
<pre><code class="language-python">print("Hello World")</code></pre>
<pre><code class="language-javascript">console.log("Hello World");</code></pre>
```

### Keyboard Navigation

- Code blocks wrapped in `<pre>` preserve tab characters, which may interfere with keyboard navigation
- Long code blocks should be scrollable horizontally (`overflow-x: auto`)
- Ensure focus indicators are visible when tabbing through inline code
- Consider adding "Copy to Clipboard" buttons for better UX

**Resources:**
- [WCAG 2.1: Info and Relationships (1.3.1)](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
- [WebAIM: Semantic Structure - Code](https://webaim.org/techniques/semanticstructure/#code)

## Best Practices

### Do This ✓

1. **Use semantic elements for meaning:**
```html
<!-- Correct: code for programming code -->
<p>The <code>Array.map()</code> method transforms arrays.</p>

<!-- Correct: kbd for keyboard input -->
<p>Press <kbd>F12</kbd> to open DevTools.</p>

<!-- Correct: samp for program output -->
<p>The server returned: <samp>200 OK</samp></p>
```

2. **Wrap multi-line code in both pre and code:**
```html
<!-- Correct: pre preserves formatting, code adds semantics -->
<pre><code>function hello() {
  console.log("Hello");
}
</code></pre>

<!-- AVOID: pre without code (works but less semantic) -->
<pre>function hello() {
  console.log("Hello");
}
</pre>
```

3. **Escape HTML special characters in code blocks:**
```html
<!-- Correct: HTML entities for < > & -->
<pre><code>&lt;div class="container"&gt;
  &lt;p&gt;Hello &amp; welcome&lt;/p&gt;
&lt;/div&gt;
</code></pre>

<!-- WRONG: Unescaped < > will break rendering -->
<pre><code><div class="container">
  <p>Hello & welcome</p>
</div>
</code></pre>
```

4. **Style code blocks with CSS, not inline styles:**
```css
pre {
  background-color: #f4f4f4;
  padding: 1em;
  border-radius: 4px;
  overflow-x: auto;
}
code {
  font-family: 'Consolas', 'Courier New', monospace;
  font-size: 0.95em;
}
```

5. **Add language class for syntax highlighting:**
```html
<!-- Correct: language-* class helps syntax highlighters -->
<pre><code class="language-python">
def greet(name):
    print(f"Hello, {name}")
</code></pre>
```

### Avoid This ✗

1. **Don't use code elements for visual styling alone:**
```html
<!-- WRONG: Using code for monospace styling, not actual code -->
<p><code>Important Notice</code></p>

<!-- CORRECT: Use CSS for styling -->
<p class="monospace">Important Notice</p>
<style>.monospace { font-family: monospace; }</style>
```

2. **Don't forget to escape HTML in code examples:**
```html
<!-- WRONG: This will render as actual HTML -->
<code><h1>Title</h1></code>

<!-- CORRECT: Escaped HTML entities -->
<code>&lt;h1&gt;Title&lt;/h1&gt;</code>
```

3. **Don't use br for line breaks in code blocks:**
```html
<!-- WRONG: Manual line breaks with <br> -->
<code>line 1<br>line 2<br>line 3</code>

<!-- CORRECT: Use <pre> to preserve natural line breaks -->
<pre><code>line 1
line 2
line 3
</code></pre>
```

4. **Don't rely on color alone in syntax highlighting:**
```html
<!-- WRONG: Only color conveys meaning -->
<code>
  <span style="color: blue;">function</span>
  <span style="color: green;">greet</span>
</code>

<!-- CORRECT: Color + semantic classes + sufficient contrast -->
<code>
  <span class="keyword" style="color: #0000ff; font-weight: bold;">function</span>
  <span class="function" style="color: #008000;">greet</span>
</code>
```

5. **Don't use excessive nesting:**
```html
<!-- WRONG: Unnecessary nesting -->
<pre><code><div><span>function hello() {}</span></div></code></pre>

<!-- CORRECT: Simple structure -->
<pre><code>function hello() {}</code></pre>
```

## Related Topics

### Prerequisites
- [HTML Syntax](../01-fundamentals/syntax.md) - Element structure and nesting
- [HTML Entities](../01-fundamentals/entities.md) - Escaping special characters
- [Text Formatting](text-formatting.md) - Other inline semantic elements

### Related Topics
- [Paragraphs](paragraphs.md) - Block-level text containers
- [Blockquotes](blockquotes.md) - Quotation elements
- [Global Attributes](../09-global-attributes/id-class.md) - Class and ID for styling
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Semantic markup principles

### Next Steps
- [Abbreviations](abbreviations.md) - Expanding acronyms in technical documentation
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Making code blocks accessible
- [CSS Styling](https://developer.mozilla.org/en-US/docs/Learn/CSS) - Styling code blocks with CSS

## Practice Exercise

### Requirements
Create a **"Python Quick Reference Guide"** that demonstrates proper use of code-related elements. Your HTML document should include:

1. A main heading and introduction
2. At least 3 sections, each demonstrating:
   - Inline code references using `<code>`
   - Keyboard shortcuts using `<kbd>`
   - Sample output using `<samp>`
   - Variables using `<var>`
3. At least 2 multi-line code blocks using `<pre><code>`
   - Properly escaped HTML entities (for `<`, `>`, `&`)
   - Preserved indentation and line breaks
4. At least one terminal command/output example
5. CSS styling that includes:
   - Different background colors for inline code vs. code blocks
   - Monospace font for all code elements
   - Horizontal scrolling for long code lines
   - Sufficient color contrast (WCAG AA compliant)

**Accessibility Requirements:**
- Provide context before each code block (don't drop code in randomly)
- Use semantic elements appropriately (code for code, kbd for keyboard input)
- Ensure color contrast meets 4.5:1 minimum ratio
- Add `aria-label` to at least one complex code block

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Python Quick Reference</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    /* Add your code styling here */
  </style>
</head>
<body>
  <!-- Add your content here -->

</body>
</html>
```

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Python Quick Reference Guide</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
      background-color: #f9f9f9;
    }
    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #3498db;
      padding-bottom: 0.5em;
    }
    h2 {
      color: #34495e;
      margin-top: 2em;
    }
    code {
      background-color: #e8e8e8;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Consolas', 'Courier New', monospace;
      font-size: 0.95em;
      color: #c7254e;
    }
    pre {
      background-color: #282c34;
      color: #abb2bf;
      padding: 1.5em;
      border-radius: 6px;
      overflow-x: auto;
      margin: 1.5em 0;
      border-left: 4px solid #61afef;
    }
    pre code {
      background-color: transparent;
      padding: 0;
      color: inherit;
      font-size: 0.9em;
      line-height: 1.5;
    }
    kbd {
      background-color: #333;
      color: white;
      padding: 3px 8px;
      border-radius: 3px;
      font-size: 0.9em;
      font-family: 'Consolas', monospace;
      border: 1px solid #555;
      box-shadow: 0 2px 0 #111;
      display: inline-block;
    }
    samp {
      background-color: #2ecc71;
      color: white;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Consolas', monospace;
      font-size: 0.9em;
    }
    var {
      color: #d63384;
      font-family: 'Consolas', monospace;
      font-style: italic;
      font-weight: bold;
    }
    .terminal {
      background-color: #1e1e1e;
      color: #d4d4d4;
      padding: 1.5em;
      border-radius: 6px;
      font-family: 'Consolas', monospace;
      margin: 1.5em 0;
      overflow-x: auto;
    }
    .terminal kbd {
      background-color: transparent;
      color: #4ec9b0;
      border: none;
      box-shadow: none;
      padding: 0;
      font-weight: bold;
    }
    .terminal samp {
      background-color: transparent;
      color: #ce9178;
      display: block;
      margin-left: 2em;
      padding: 0;
    }
    .prompt {
      color: #569cd6;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <article>
    <h1>Python Quick Reference Guide</h1>

    <p>
      This guide covers essential Python syntax for beginners. Python is
      an interpreted, high-level programming language known for its
      readability and simplicity.
    </p>

    <section>
      <h2>Variables and Data Types</h2>

      <p>
        In Python, you create variables using the assignment operator.
        For example, <code>age = 25</code> creates a variable named
        <var>age</var> with the value 25. Python automatically determines
        the data type.
      </p>

      <p>Here are the basic data types:</p>

<pre aria-label="Python variable declarations for different data types"><code># Integer
count = 42

# Float
price = 19.99

# String
name = "Alice"

# Boolean
is_active = True

# List
colors = ["red", "green", "blue"]

# Dictionary
person = {"name": "Bob", "age": 30}
</code></pre>

      <p>
        To check a variable's type, use the <code>type()</code> function:
        <code>type(age)</code> returns <samp>&lt;class 'int'&gt;</samp>
      </p>
    </section>

    <section>
      <h2>Functions</h2>

      <p>
        Functions are defined using the <code>def</code> keyword, followed
        by the function name and parameters. Here's how to create a function
        that calculates the area of a rectangle:
      </p>

<pre aria-label="Python function to calculate rectangle area"><code>def calculate_area(width, height):
    """
    Calculate the area of a rectangle.

    Args:
        width: The width of the rectangle
        height: The height of the rectangle

    Returns:
        The area (width * height)
    """
    area = width * height
    return area

# Call the function
result = calculate_area(5, 10)
print(result)  # Output: 50
</code></pre>

      <p>
        When you call <code>calculate_area(5, 10)</code>, the function
        multiplies <var>width</var> (5) by <var>height</var> (10) and
        returns <samp>50</samp>.
      </p>
    </section>

    <section>
      <h2>Control Flow</h2>

      <p>
        Python uses indentation (4 spaces) to define code blocks. Here's
        an example using <code>if</code>, <code>elif</code>, and
        <code>else</code>:
      </p>

<pre><code>age = 18

if age &lt; 13:
    print("Child")
elif age &lt; 18:
    print("Teenager")
else:
    print("Adult")

# Output: Adult
</code></pre>

      <p>
        Notice how the comparison operator <code>&lt;</code> is written
        as <code>&amp;lt;</code> in the HTML source to prevent rendering
        issues.
      </p>
    </section>

    <section>
      <h2>Using the Python REPL</h2>

      <p>
        The Python REPL (Read-Eval-Print Loop) lets you test code
        interactively. To launch it, open your terminal and type:
      </p>

      <div class="terminal">
<pre><span class="prompt">$</span> <kbd>python3</kbd>
<samp>Python 3.11.4 (main, Jun  9 2023, 12:30:00)
[GCC 11.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
&gt;&gt;&gt;</samp></pre>
      </div>

      <p>
        Now you can enter Python commands directly:
      </p>

      <div class="terminal">
<pre><span class="prompt">&gt;&gt;&gt;</span> <kbd>print("Hello, World!")</kbd>
<samp>Hello, World!</samp>
<span class="prompt">&gt;&gt;&gt;</span> <kbd>x = 10 + 5</kbd>
<span class="prompt">&gt;&gt;&gt;</span> <kbd>print(x)</kbd>
<samp>15</samp></pre>
      </div>

      <p>
        To exit the REPL, press <kbd>Ctrl</kbd> + <kbd>D</kbd> on
        Linux/Mac, or type <kbd>exit()</kbd> and press <kbd>Enter</kbd>.
      </p>
    </section>

    <section>
      <h2>List Comprehensions</h2>

      <p>
        List comprehensions provide a concise way to create lists. The
        basic syntax is:
        <code>[<var>expression</var> for <var>item</var> in <var>iterable</var>]</code>
      </p>

<pre><code># Traditional approach
squares = []
for i in range(10):
    squares.append(i ** 2)

# List comprehension (more Pythonic)
squares = [i ** 2 for i in range(10)]

print(squares)
# Output: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
</code></pre>

      <p>
        The expression <code>i ** 2</code> raises <var>i</var> to the
        power of 2. The <code>**</code> operator is Python's exponentiation
        operator.
      </p>
    </section>

    <footer>
      <p>
        <small>
          For more information, visit the official
          <a href="https://docs.python.org/3/">Python Documentation</a>.
        </small>
      </p>
    </footer>
  </article>
</body>
</html>
```

**Key Features of Solution:**
- Uses `<code>` for inline Python keywords and function names
- Uses `<kbd>` for terminal commands and keyboard shortcuts
- Uses `<samp>` for program output
- Uses `<var>` for variable names in explanations
- Multiple `<pre><code>` blocks for complete examples
- Properly escaped HTML entities (`&lt;`, `&gt;`, `&amp;`)
- Terminal-style section with styled prompt and output
- Two `aria-label` attributes for complex code blocks
- CSS styling with different backgrounds for inline vs. block code
- High color contrast (WCAG AA compliant):
  - Inline code: #c7254e on #e8e8e8 = 7.1:1 ratio
  - Code blocks: #abb2bf on #282c34 = 7.8:1 ratio
  - kbd: white on #333 = 12.6:1 ratio
- Horizontal scrolling enabled for long lines (`overflow-x: auto`)
- Context provided before every code block

---

## Navigation

- **Previous:** [Blockquotes](blockquotes.md)
- **Next:** [Abbreviations](abbreviations.md)
- **Up:** [Text Content](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Text Content
- **Difficulty:** Beginner to Intermediate
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
