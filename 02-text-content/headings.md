---
title: HTML Headings (h1-h6)
category: Text Content Elements
order: 1
---

# HTML Headings (h1-h6)

> **Quick Summary:** Headings structure content hierarchically from h1 (most important) to h6 (least important), creating a document outline that improves accessibility, SEO, and readability.

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

HTML headings are the skeleton of your content. Just as a book has chapter titles, section headings, and subsections, web pages use h1 through h6 elements to create hierarchical structure. This hierarchy isn't just visual—it communicates importance to search engines, screen readers, and users scanning your page.

The heading hierarchy is strict: h1 is the top level (typically the page title), h2 elements are major sections, h3 elements are subsections of h2, and so on. Skipping levels (h1 → h3) confuses assistive technologies and hurts SEO. Think of headings as a table of contents: each level must logically nest within its parent.

Headings serve three critical purposes: they create visual hierarchy for sighted users, provide navigation landmarks for screen reader users, and signal content structure to search engines. A well-structured heading hierarchy can improve your search rankings and make your content accessible to millions of users with disabilities.

**Key Concept:** Use only one h1 per page (the main topic), and maintain logical heading hierarchy. Never choose headings based on visual size—use CSS for styling, headings for structure.

---

## Basic Syntax

```html
<h1>Main Page Title</h1>
<h2>Major Section</h2>
<h3>Subsection of h2</h3>
<h4>Subsection of h3</h4>
<h5>Subsection of h4</h5>
<h6>Subsection of h5</h6>
```

### Heading Levels

| Element | Level | Use Case | Visual Default |
|---------|-------|----------|----------------|
| `<h1>` | 1 | Page title, main topic | Largest (2em) |
| `<h2>` | 2 | Major sections | Large (1.5em) |
| `<h3>` | 3 | Subsections | Medium-large (1.17em) |
| `<h4>` | 4 | Sub-subsections | Medium (1em) |
| `<h5>` | 5 | Minor headings | Small (0.83em) |
| `<h6>` | 6 | Smallest headings | Smallest (0.67em) |

### Heading Hierarchy Rules

```html
<!-- CORRECT: Logical hierarchy -->
<h1>Article Title</h1>
  <h2>Section 1</h2>
    <h3>Subsection 1.1</h3>
    <h3>Subsection 1.2</h3>
  <h2>Section 2</h2>
    <h3>Subsection 2.1</h3>

<!-- WRONG: Skipping levels -->
<h1>Article Title</h1>
  <h3>Section (skipped h2!)</h3>  ❌

<!-- WRONG: Multiple h1 elements -->
<h1>First Title</h1>
<h1>Second Title</h1>  ❌
```

---

## Examples

### Example 1: Blog Post Structure

**Scenario:** Creating a well-structured blog post with proper heading hierarchy

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Getting Started with HTML5</title>
</head>
<body>
  <article>
    <!-- h1: Main page title (only one per page) -->
    <h1>Getting Started with HTML5</h1>

    <!-- h2: Major sections -->
    <h2>What is HTML5?</h2>
    <p>HTML5 is the latest evolution of HTML...</p>

    <h2>Key Features of HTML5</h2>
    <p>HTML5 introduced many improvements...</p>

    <!-- h3: Subsections of "Key Features" -->
    <h3>Semantic Elements</h3>
    <p>Elements like header, nav, article...</p>

    <h3>Multimedia Support</h3>
    <p>Native video and audio elements...</p>

    <h3>Graphics and Canvas</h3>
    <p>Canvas and SVG for drawing...</p>

    <h2>Getting Started</h2>
    <p>To begin using HTML5...</p>

    <!-- h3: Subsections of "Getting Started" -->
    <h3>Setting Up Your Environment</h3>
    <p>You'll need a text editor...</p>

    <h3>Your First HTML5 Page</h3>
    <p>Create a new file...</p>
  </article>
</body>
</html>
```

**Result:** Clear document outline with one h1 (page title) and logical h2/h3 hierarchy. Screen readers can navigate by headings, and search engines understand content structure.

---

### Example 2: Documentation Page with Deep Hierarchy

**Scenario:** Technical documentation with multiple nesting levels

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>API Documentation</title>
</head>
<body>
  <main>
    <h1>API Documentation</h1>

    <h2>Authentication</h2>
    <p>All API requests require authentication...</p>

    <h3>API Keys</h3>
    <p>Generate an API key in your dashboard...</p>

    <h4>Creating an API Key</h4>
    <p>Step 1: Navigate to Settings...</p>

    <h4>Rotating API Keys</h4>
    <p>For security, rotate keys every 90 days...</p>

    <h3>OAuth 2.0</h3>
    <p>For user-specific access...</p>

    <h4>Authorization Code Flow</h4>
    <p>The most secure OAuth flow...</p>

    <h5>Step 1: Authorization Request</h5>
    <p>Redirect users to the authorization endpoint...</p>

    <h5>Step 2: Handle Callback</h5>
    <p>After user approval, handle the callback...</p>

    <h2>Making Requests</h2>
    <p>Use HTTPS for all API requests...</p>

    <h3>GET Requests</h3>
    <p>Retrieve data from the API...</p>

    <h3>POST Requests</h3>
    <p>Create new resources...</p>
  </main>
</body>
</html>
```

**Result:** Deep hierarchy (h1 → h2 → h3 → h4 → h5) maintains logical structure. Each level nests properly within its parent, creating a clear outline for complex documentation.

---

### Example 3: Landing Page with Semantic Sections

**Scenario:** Marketing landing page with semantic HTML5 structure

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CloudTech - Cloud Infrastructure Solutions</title>
  <style>
    /* Styling headings with CSS (not inline attributes) */
    h1 { font-size: 3em; color: #2c3e50; }
    h2 { font-size: 2em; color: #34495e; margin-top: 40px; }
    h3 { font-size: 1.5em; color: #7f8c8d; }
  </style>
</head>
<body>
  <header>
    <h1>CloudTech</h1>
    <p>Enterprise Cloud Infrastructure Solutions</p>
  </header>

  <main>
    <section>
      <h2>Why Choose CloudTech?</h2>
      <p>We provide scalable, secure cloud solutions...</p>

      <h3>99.99% Uptime Guarantee</h3>
      <p>Our infrastructure is built for reliability...</p>

      <h3>Enterprise-Grade Security</h3>
      <p>SOC 2 Type II certified...</p>

      <h3>24/7 Support</h3>
      <p>Our expert team is always available...</p>
    </section>

    <section>
      <h2>Pricing Plans</h2>
      <p>Choose the plan that fits your needs...</p>

      <h3>Startup Plan</h3>
      <p>Perfect for small teams...</p>

      <h3>Business Plan</h3>
      <p>For growing companies...</p>

      <h3>Enterprise Plan</h3>
      <p>Custom solutions for large organizations...</p>
    </section>

    <section>
      <h2>Get Started Today</h2>
      <p>Sign up now for a free trial...</p>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 CloudTech. All rights reserved.</p>
  </footer>
</body>
</html>
```

**Result:** Semantic sections with consistent h2/h3 hierarchy. CSS handles visual styling, while HTML headings provide structural meaning for accessibility and SEO.

**Notes:**
- One h1 (CloudTech brand/page title)
- Multiple h2 elements for major sections
- h3 elements for subsections within each h2
- CSS controls visual appearance, not heading level choice

---

## Common Use Cases

### Use Case 1: Article/Blog Post Structure
**When:** Writing content-heavy pages (articles, blog posts, news)
**How:**
```html
<article>
  <h1>Article Title</h1>
  <p class="byline">By Joshua Hickman | November 17, 2025</p>

  <h2>Introduction</h2>
  <p>Opening paragraph...</p>

  <h2>Main Points</h2>
  <h3>Point 1</h3>
  <p>Details...</p>

  <h3>Point 2</h3>
  <p>Details...</p>

  <h2>Conclusion</h2>
  <p>Summary...</p>
</article>
```
**Why:** Clear hierarchy helps readers scan content and screen readers navigate sections efficiently.

---

### Use Case 2: E-Commerce Product Categories
**When:** Organizing product listings hierarchically
**How:**
```html
<main>
  <h1>Electronics</h1>

  <h2>Computers</h2>
  <h3>Laptops</h3>
  <h3>Desktops</h3>
  <h3>Tablets</h3>

  <h2>Audio</h2>
  <h3>Headphones</h3>
  <h3>Speakers</h3>

  <h2>Gaming</h2>
  <h3>Consoles</h3>
  <h3>Accessories</h3>
</main>
```
**Why:** Hierarchical headings create natural navigation for both users and search engines, improving product discoverability.

---

### Use Case 3: FAQ Page Structure
**When:** Creating frequently asked questions pages
**How:**
```html
<main>
  <h1>Frequently Asked Questions</h1>

  <h2>Account & Billing</h2>

  <h3>How do I create an account?</h3>
  <p>To create an account, click Sign Up...</p>

  <h3>How do I update billing information?</h3>
  <p>Navigate to Account Settings...</p>

  <h2>Technical Support</h2>

  <h3>How do I reset my password?</h3>
  <p>Click "Forgot Password" on the login page...</p>

  <h3>What browsers are supported?</h3>
  <p>We support Chrome, Firefox, Safari, and Edge...</p>
</main>
```
**Why:** h2 elements group related questions, h3 elements present individual questions. Screen reader users can jump between question categories or individual questions.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | Perfect heading support since inception |
| Firefox | All     | Full Support  | Excellent accessibility support |
| Safari  | All     | Full Support  | Full support on desktop and iOS |
| Edge    | All     | Full Support  | Chromium-based, perfect compatibility |
| IE 11   | All     | Full Support  | Headings supported since HTML 2.0 |

**Fallback Strategy:**
Headings have been supported since HTML 2.0 (1995). No fallback needed—universal support across all browsers.

**Can I Use Link:** N/A (core HTML since 1995)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Information and relationships must be programmatically determined (headings create this structure)
- Headings must be used to organize content
- Heading hierarchy must be logical (no skipping levels)

**Level AA Requirements:**
- Page titles (h1) must describe topic or purpose
- Headings must accurately describe sections
- Multiple ways to navigate must exist (headings are one way)

### Screen Reader Support

```html
<!-- Screen reader navigation -->
<h1>Main Topic</h1>  <!-- Screen reader: "Heading level 1, Main Topic" -->
<h2>Section A</h2>   <!-- Screen reader: "Heading level 2, Section A" -->
<h3>Detail 1</h3>    <!-- Screen reader: "Heading level 3, Detail 1" -->

<!-- Screen readers can:
  - List all headings
  - Jump between heading levels
  - Skip to next/previous heading
  - Navigate by heading level (e.g., "next h2")
-->
```

**Key Points:**
- Screen readers announce heading level and text
- Users can navigate by headings (most common navigation method)
- Proper hierarchy creates logical navigation structure
- Skipping levels confuses navigation ("why jump from h2 to h4?")

### Keyboard Navigation

Most screen readers use keyboard shortcuts for heading navigation:
- **H:** Next heading
- **Shift + H:** Previous heading
- **1-6:** Jump to specific heading level (e.g., "2" = next h2)

---

## Best Practices

### Do This

1. **Use One h1 Per Page**
   ```html
   <!-- GOOD: One h1 (page topic) -->
   <h1>Cloud Infrastructure Best Practices</h1>
   <h2>Security</h2>
   <h2>Performance</h2>
   ```
   **Why:** Multiple h1 elements confuse search engines and screen readers about page topic. One h1 clearly identifies the main subject.

2. **Maintain Logical Hierarchy**
   ```html
   <!-- GOOD: Logical nesting -->
   <h1>Guide Title</h1>
     <h2>Chapter 1</h2>
       <h3>Section 1.1</h3>
       <h3>Section 1.2</h3>
     <h2>Chapter 2</h2>
       <h3>Section 2.1</h3>
   ```
   **Why:** Logical hierarchy creates a document outline that makes sense to both humans and assistive technologies.

3. **Use CSS for Visual Styling**
   ```html
   <!-- GOOD: Headings for structure, CSS for appearance -->
   <h2 class="large-blue-heading">Important Section</h2>

   <style>
     .large-blue-heading {
       font-size: 2.5em;
       color: #0066cc;
     }
   </style>
   ```
   **Why:** Don't choose h3 over h2 because you want smaller text. Use the semantically correct level and style it with CSS.

---

### Avoid This

1. **Don't Skip Heading Levels**
   ```html
   <!-- BAD: Skips h2, goes straight to h3 -->
   <h1>Page Title</h1>
   <h3>Subsection</h3>  ❌

   <!-- GOOD: Logical progression -->
   <h1>Page Title</h1>
   <h2>Section</h2>
   <h3>Subsection</h3>
   ```
   **Why Not:** Skipping levels breaks the document outline and confuses screen reader navigation.
   **Instead:** Always use the next logical level.

2. **Don't Use Multiple h1 Elements**
   ```html
   <!-- BAD: Multiple h1 elements -->
   <h1>Company Name</h1>
   <h1>Product Name</h1>
   <h1>Feature List</h1>  ❌
   ```
   **Why Not:** Search engines and screen readers expect one main topic per page. Multiple h1 elements dilute SEO and confuse accessibility.
   **Instead:** Use one h1 for page title, h2 for major sections.

3. **Don't Use Headings for Styling Only**
   ```html
   <!-- BAD: h3 chosen for visual size, not semantic meaning -->
   <h3>This text looks nice at h3 size</h3>
   <p>This is actually the main content...</p>  ❌

   <!-- GOOD: Semantic heading, styled with CSS if needed -->
   <p class="intro-text">This text looks nice</p>
   <style>
     .intro-text { font-size: 1.2em; font-weight: bold; }
   </style>
   ```
   **Why Not:** Headings communicate structure, not just visual appearance. Using them for styling breaks accessibility.
   **Instead:** Use CSS to style any element to look like a heading if needed.

---

## Related Topics

**Prerequisites (Learn These First):**
- [HTML5 Introduction](../01-fundamentals/introduction.md) - Semantic HTML basics
- [Document Structure](../01-fundamentals/document-structure.md) - Page organization

**Related Concepts:**
- [Paragraphs](paragraphs.md) - Body text following headings
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Meaningful markup
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - WCAG compliance

**Next Steps (Learn These Next):**
- [Paragraphs](paragraphs.md) - Text content under headings
- [Text Formatting](text-formatting.md) - Emphasizing text
- [Semantic HTML5 Sections](../07-semantic-html5/section.md) - Grouping content

**External Resources:**
- [MDN - Heading Elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements)
- [W3C - Headings and Labels](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels)
- [WebAIM - Semantic Structure](https://webaim.org/techniques/semanticstructure/)

---

## Practice Exercise

### Challenge: Create a Well-Structured Documentation Page

**Objective:** Build a technical documentation page with proper heading hierarchy covering an API reference.

**Requirements:**
- [ ] Use one h1 for page title
- [ ] Create at least 3 h2 sections
- [ ] Include h3 subsections under each h2
- [ ] Add one h4 level (optional h5/h6 for practice)
- [ ] Ensure no heading levels are skipped
- [ ] Validate heading outline using browser DevTools or validator
- [ ] Bonus: Test navigation with a screen reader

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>API Documentation</title>
</head>
<body>
  <!-- Create a documentation page here with proper heading hierarchy -->
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
  <title>Weather API Documentation</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #3498db;
      padding-bottom: 10px;
    }
    h2 {
      color: #34495e;
      margin-top: 30px;
      border-left: 4px solid #3498db;
      padding-left: 10px;
    }
    h3 {
      color: #7f8c8d;
    }
    h4 {
      color: #95a5a6;
      font-style: italic;
    }
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
    }
  </style>
</head>
<body>
  <!-- h1: Main page title (only one) -->
  <h1>Weather API Documentation</h1>
  <p>Access real-time weather data for any location worldwide.</p>

  <!-- h2: Major section - Getting Started -->
  <h2>Getting Started</h2>
  <p>Follow these steps to integrate the Weather API into your application.</p>

  <!-- h3: Subsection of Getting Started -->
  <h3>Authentication</h3>
  <p>All API requests require an API key. Include your key in the header:</p>
  <code>Authorization: Bearer YOUR_API_KEY</code>

  <h3>Base URL</h3>
  <p>All endpoints use the following base URL:</p>
  <code>https://api.weather.example.com/v1/</code>

  <h3>Rate Limits</h3>
  <p>Free tier: 1,000 requests per day. Premium tier: Unlimited requests.</p>

  <!-- h2: Major section - Endpoints -->
  <h2>Endpoints</h2>
  <p>The Weather API provides the following endpoints:</p>

  <!-- h3: Subsection of Endpoints -->
  <h3>Current Weather</h3>
  <p>Get current weather conditions for a location.</p>

  <!-- h4: Sub-subsection -->
  <h4>Request Format</h4>
  <code>GET /weather/current?location={city}</code>

  <h4>Parameters</h4>
  <ul>
    <li><code>location</code> (required): City name or coordinates</li>
    <li><code>units</code> (optional): metric or imperial (default: metric)</li>
  </ul>

  <h4>Example Response</h4>
  <pre><code>{
  "temperature": 22,
  "humidity": 65,
  "conditions": "Partly Cloudy"
}</code></pre>

  <!-- h3: Another subsection of Endpoints -->
  <h3>Weather Forecast</h3>
  <p>Get 7-day weather forecast for a location.</p>

  <h4>Request Format</h4>
  <code>GET /weather/forecast?location={city}&days=7</code>

  <h4>Parameters</h4>
  <ul>
    <li><code>location</code> (required): City name or coordinates</li>
    <li><code>days</code> (optional): Number of days (1-14, default: 7)</li>
  </ul>

  <!-- h2: Major section - Error Handling -->
  <h2>Error Handling</h2>
  <p>The API uses standard HTTP status codes to indicate success or failure.</p>

  <h3>Error Codes</h3>
  <ul>
    <li><code>400</code>: Bad Request - Invalid parameters</li>
    <li><code>401</code>: Unauthorized - Invalid API key</li>
    <li><code>404</code>: Not Found - Location not found</li>
    <li><code>429</code>: Too Many Requests - Rate limit exceeded</li>
  </ul>

  <h3>Error Response Format</h3>
  <pre><code>{
  "error": {
    "code": 404,
    "message": "Location not found"
  }
}</code></pre>

  <!-- h2: Major section - Support -->
  <h2>Support</h2>
  <p>Need help? We're here to assist you.</p>

  <h3>Documentation</h3>
  <p>Visit our comprehensive documentation portal for detailed guides.</p>

  <h3>Contact Us</h3>
  <p>Email: support@weather.example.com</p>
  <p>Phone: 1-800-WEATHER</p>

  <footer>
    <p>&copy; 2025 Weather API. All rights reserved.</p>
  </footer>
</body>
</html>
```

**Explanation:**
This documentation page demonstrates proper heading hierarchy:
- **h1** (one): "Weather API Documentation" - main page topic
- **h2** (four): Getting Started, Endpoints, Error Handling, Support - major sections
- **h3** (eight): Authentication, Base URL, Rate Limits, Current Weather, Weather Forecast, Error Codes, Error Response Format, Documentation, Contact Us - subsections
- **h4** (four): Request Format, Parameters, Example Response (under both Current Weather and Forecast) - detail level

The hierarchy never skips levels. Each h3 is a child of an h2, each h4 is a child of an h3. Screen readers can navigate this structure efficiently, jumping between sections or drilling down into details. CSS styles headings visually, but structural meaning comes from heading level choice.

</details>

---

### Expected Result

**Visual Outcome:** A professional documentation page with clear visual hierarchy. Headings are styled with CSS but maintain semantic meaning.

**Key Learnings:**
- One h1 per page establishes main topic
- Logical hierarchy (h1 → h2 → h3 → h4) creates navigable structure
- CSS controls visual appearance, not heading level selection
- Screen readers use heading structure for efficient navigation
- Proper headings improve both SEO and accessibility

---

## Navigation

**Previous:** [HTML5 Fundamentals](../01-fundamentals/deprecated-elements.md)
**Next:** [Paragraphs & Line Breaks](paragraphs.md)
**Up:** [Text Content Elements](../README.md#2-text-content-elements-7-topics)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Text Content Elements
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
