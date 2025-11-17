---
title: Link States and Styling
category: Links and Navigation
order: 2
---

# Link States and Styling

> **Quick Summary:** CSS pseudo-classes enable styling links based on user interaction states (hover, active, focus, visited), improving usability, accessibility, and visual feedback for navigation elements across all devices.

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

Links are interactive elements that change appearance based on user actions—hovering with a mouse, clicking, navigating via keyboard, or having been previously visited. CSS pseudo-classes target these different link states, allowing designers to provide visual feedback that enhances usability and guides users through navigation flows.

The five primary link pseudo-classes are `:link` (unvisited), `:visited` (previously visited), `:hover` (mouse over), `:active` (being clicked), and `:focus` (keyboard selected). Understanding the cascade order of these states is critical: applying them in the wrong sequence can cause some states to never display due to CSS specificity rules. The mnemonic **LoVe/HAte** helps remember the correct order: **L**ink, **V**isited, **H**over, **A**ctive (with **F**ocus typically alongside :hover).

Proper link styling serves both aesthetic and functional purposes. Visual feedback confirms interactivity, distinguishes clickable elements from static text, and provides accessibility for users who navigate via keyboard or assistive technologies. WCAG 2.1 guidelines require visible focus indicators and sufficient color contrast, making thoughtful link state styling essential for compliance.

**Key Concept:** Link pseudo-classes must be ordered correctly (LoVe/HAte: :link, :visited, :hover/:focus, :active) to ensure all states display properly. Always include visible focus styles for keyboard accessibility.

## Basic Syntax

**CSS Pseudo-Classes for Links:**

| Pseudo-Class | Targets | User Action | Specificity |
|--------------|---------|-------------|-------------|
| `:link` | Unvisited links | Default state | (0,1,0) |
| `:visited` | Visited links | After navigation | (0,1,0) |
| `:hover` | Mouse hovering over link | Mouse interaction | (0,1,0) |
| `:active` | Link being clicked | During click | (0,1,0) |
| `:focus` | Keyboard-selected link | Keyboard navigation | (0,1,0) |
| `:focus-visible` | Keyboard focus (not mouse) | Keyboard-only indication | (0,1,0) |

**Correct Cascade Order (LoVe/HAte):**

```css
/* 1. Unvisited links */
a:link {
  color: #0066cc;
}

/* 2. Visited links */
a:visited {
  color: #551A8B;
}

/* 3. Hover AND Focus (together for parity) */
a:hover,
a:focus {
  color: #004499;
  text-decoration: underline;
}

/* 4. Active (being clicked) */
a:active {
  color: #FF6B6B;
}
```

**Why Order Matters:**

```css
/* WRONG ORDER - :hover will never display! */
a:hover { color: red; }
a:link { color: blue; }  /* This overrides :hover due to cascade */

/* CORRECT ORDER - All states display properly */
a:link { color: blue; }
a:hover { color: red; }  /* Now works correctly */
```

**Modern Shorthand (No :link/:visited separation):**

```css
/* Default state (combines :link and :visited) */
a {
  color: #0066cc;
  text-decoration: underline;
}

/* Visited (override default) */
a:visited {
  color: #551A8B;
}

/* Hover and Focus */
a:hover,
a:focus {
  color: #004499;
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}

/* Active */
a:active {
  color: #FF6B6B;
}
```

## Examples

### Example 1: Classic Link Styling with All States
**Use Case:** Traditional website with distinct visual feedback for each link state

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Classic Link Styles</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 40px 20px;
      line-height: 1.8;
      background-color: #f9f9f9;
    }
    h1 {
      color: #2c3e50;
    }

    /* Link States (LoVe/HAte Order) */
    a:link {
      color: #0066cc;
      text-decoration: underline;
    }
    a:visited {
      color: #551A8B;
    }
    a:hover,
    a:focus {
      color: #003d7a;
      text-decoration-thickness: 2px;
      background-color: #fff3cd;
      padding: 2px 4px;
      border-radius: 3px;
    }
    a:focus {
      outline: 2px solid #FF6B6B;
      outline-offset: 2px;
    }
    a:active {
      color: #FF6B6B;
      background-color: #ffe6e6;
    }

    /* Remove focus outline for mouse users (modern approach) */
    a:focus:not(:focus-visible) {
      outline: none;
    }
    a:focus-visible {
      outline: 2px solid #FF6B6B;
      outline-offset: 2px;
    }
  </style>
</head>
<body>
  <article>
    <h1>Understanding Link States</h1>

    <p>
      Hyperlinks change appearance based on user interaction. Try interacting
      with these links to see different states:
    </p>

    <ul>
      <li>
        <a href="https://developer.mozilla.org/">MDN Web Docs</a>
        (unvisited link - blue)
      </li>
      <li>
        <a href="https://www.google.com/">Google</a>
        (likely visited - purple if you've been there)
      </li>
      <li>
        <a href="/example-page.html">Example Page</a>
        (hover to see background highlight)
      </li>
      <li>
        Tab through links to see <strong>:focus</strong> state
        (red outline for keyboard users)
      </li>
      <li>
        Click and hold to see <strong>:active</strong> state
        (pink background while clicking)
      </li>
    </ul>

    <p>
      These visual cues help users understand:
    </p>
    <ul>
      <li><strong>Blue:</strong> Link you haven't visited yet</li>
      <li><strong>Purple:</strong> Link you've already visited</li>
      <li><strong>Yellow background:</strong> Link you're hovering over</li>
      <li><strong>Red outline:</strong> Link selected via keyboard</li>
      <li><strong>Pink background:</strong> Link being actively clicked</li>
    </ul>
  </article>
</body>
</html>
```

### Example 2: Modern Button-Style Links
**Use Case:** Call-to-action buttons with smooth transitions

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Modern Button Links</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 40px 20px;
      background-color: #ecf0f1;
    }
    h1 {
      color: #2c3e50;
      text-align: center;
    }
    .button-container {
      display: flex;
      gap: 1.5em;
      justify-content: center;
      margin: 3em 0;
      flex-wrap: wrap;
    }

    /* Primary Button Link */
    .btn-primary {
      display: inline-block;
      padding: 0.75em 2em;
      background-color: #3498db;
      color: white;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      transition: all 0.3s ease;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .btn-primary:visited {
      color: white;  /* Override browser default */
    }
    .btn-primary:hover,
    .btn-primary:focus {
      background-color: #2980b9;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      transform: translateY(-2px);
    }
    .btn-primary:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }
    .btn-primary:active {
      background-color: #21618c;
      transform: translateY(0);
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    }

    /* Secondary Button Link */
    .btn-secondary {
      display: inline-block;
      padding: 0.75em 2em;
      background-color: white;
      color: #3498db;
      text-decoration: none;
      border: 2px solid #3498db;
      border-radius: 6px;
      font-weight: bold;
      transition: all 0.3s ease;
    }
    .btn-secondary:visited {
      color: #3498db;
    }
    .btn-secondary:hover,
    .btn-secondary:focus {
      background-color: #3498db;
      color: white;
    }
    .btn-secondary:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }
    .btn-secondary:active {
      background-color: #2980b9;
      border-color: #2980b9;
    }

    /* Danger Button Link */
    .btn-danger {
      display: inline-block;
      padding: 0.75em 2em;
      background-color: #e74c3c;
      color: white;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      transition: all 0.3s ease;
    }
    .btn-danger:visited {
      color: white;
    }
    .btn-danger:hover,
    .btn-danger:focus {
      background-color: #c0392b;
    }
    .btn-danger:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }
    .btn-danger:active {
      background-color: #a93226;
    }
  </style>
</head>
<body>
  <article>
    <h1>Modern Button-Style Links</h1>

    <p style="text-align: center;">
      Buttons styled as links provide clear calls-to-action with
      smooth hover and focus transitions.
    </p>

    <div class="button-container">
      <a href="/signup.html" class="btn-primary">Sign Up Free</a>
      <a href="/learn-more.html" class="btn-secondary">Learn More</a>
      <a href="/delete-account.html" class="btn-danger">Delete Account</a>
    </div>

    <p style="text-align: center;">
      <strong>Try it:</strong> Hover, tab through with keyboard, and click
      to see different states with smooth animations.
    </p>
  </article>
</body>
</html>
```

### Example 3: Navigation Menu with Active State
**Use Case:** Website navigation highlighting current page

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Navigation with Active States</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
    }

    /* Navigation Bar */
    nav {
      background-color: #2c3e50;
      padding: 0;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    nav ul {
      list-style: none;
      display: flex;
      justify-content: center;
    }
    nav li {
      position: relative;
    }

    /* Navigation Links (Default State) */
    nav a {
      display: block;
      padding: 1.25em 2em;
      color: #ecf0f1;
      text-decoration: none;
      font-weight: 500;
      transition: all 0.3s ease;
      position: relative;
    }

    /* Visited (keep same color) */
    nav a:visited {
      color: #ecf0f1;
    }

    /* Hover and Focus */
    nav a:hover,
    nav a:focus {
      background-color: #34495e;
      color: white;
    }

    /* Underline animation on hover/focus */
    nav a::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 50%;
      width: 0;
      height: 3px;
      background-color: #3498db;
      transition: all 0.3s ease;
      transform: translateX(-50%);
    }
    nav a:hover::after,
    nav a:focus::after {
      width: 80%;
    }

    /* Focus visible (keyboard navigation) */
    nav a:focus {
      outline: 3px solid #FFD700;
      outline-offset: -3px;
    }

    /* Active (being clicked) */
    nav a:active {
      background-color: #1abc9c;
    }

    /* Current Page Indicator */
    nav a[aria-current="page"] {
      background-color: #3498db;
      color: white;
    }
    nav a[aria-current="page"]::after {
      width: 80%;
    }

    /* Main Content */
    main {
      max-width: 900px;
      margin: 3em auto;
      padding: 0 20px;
    }
    h1 {
      color: #2c3e50;
      margin-bottom: 1em;
    }
  </style>
</head>
<body>
  <header>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="/" aria-current="page">Home</a></li>
        <li><a href="/about.html">About</a></li>
        <li><a href="/services.html">Services</a></li>
        <li><a href="/portfolio.html">Portfolio</a></li>
        <li><a href="/blog/">Blog</a></li>
        <li><a href="/contact.html">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <h1>Navigation with Link States</h1>

    <p>
      This navigation demonstrates advanced link states:
    </p>

    <ul>
      <li><strong>Default:</strong> Light gray text on dark background</li>
      <li><strong>Hover:</strong> Darker background + animated underline</li>
      <li><strong>Focus:</strong> Gold outline for keyboard users</li>
      <li><strong>Active:</strong> Teal background while clicking</li>
      <li><strong>Current Page:</strong> Blue background (Home is current)</li>
    </ul>

    <p>
      The <code>aria-current="page"</code> attribute marks the current page,
      which receives special styling (blue background). This helps users
      orient themselves within the site.
    </p>
  </main>
</body>
</html>
```

## Common Use Cases

### 1. Standard Text Links in Content
Basic in-content links with underline and color changes:

```css
a {
  color: #0066cc;
  text-decoration: underline;
}
a:visited {
  color: #551A8B;
}
a:hover,
a:focus {
  color: #004499;
  text-decoration-thickness: 2px;
}
a:focus {
  outline: 2px solid #FF6B6B;
  outline-offset: 2px;
}
```

**When to use:** Blog posts, articles, documentation, informational pages

### 2. Navigation Menus
Remove underlines, add backgrounds, highlight current page:

```css
nav a {
  text-decoration: none;
  color: white;
  padding: 0.75em 1.5em;
  display: block;
}
nav a:hover,
nav a:focus {
  background-color: rgba(255, 255, 255, 0.1);
}
nav a[aria-current="page"] {
  background-color: rgba(255, 255, 255, 0.2);
  font-weight: bold;
}
```

**When to use:** Site headers, sidebars, footer navigation

### 3. Call-to-Action Buttons
High contrast, clear hover states, prominent focus indicators:

```css
.cta-button {
  background-color: #e74c3c;
  color: white;
  padding: 1em 2.5em;
  text-decoration: none;
  border-radius: 6px;
  font-weight: bold;
  transition: all 0.3s;
}
.cta-button:hover,
.cta-button:focus {
  background-color: #c0392b;
  transform: scale(1.05);
}
.cta-button:focus {
  outline: 3px solid #FFD700;
  outline-offset: 3px;
}
```

**When to use:** Landing pages, pricing pages, forms, CTAs

## Browser Support

| Pseudo-Class | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|--------------|--------|---------|--------|------|---------------|---------------|
| `:link` | All | All | All | All | All | All |
| `:visited` | All | All | All | All | All | All |
| `:hover` | All | All | All | All | All | All |
| `:active` | All | All | All | All | All | All |
| `:focus` | All | All | All | All | All | All |
| `:focus-visible` | 86+ | 85+ | 15.4+ | 86+ | 15.4+ | 86+ |

**Browser Support:** Universal for core pseudo-classes

The `:link`, `:visited`, `:hover`, `:active`, and `:focus` pseudo-classes have been part of CSS since CSS1 (1996) and CSS2 (1998), with universal browser support.

The `:focus-visible` pseudo-class is newer (CSS Selectors Level 4) and has excellent modern browser support (95%+ as of 2025).

**Mobile Considerations:**
- `:hover` doesn't work on touchscreens (tapping triggers `:active` instead)
- `:focus` may behave differently on mobile browsers
- Always style `:active` for mobile touch feedback

**Resources:**
- [MDN: CSS Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
- [MDN: :focus-visible](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible)
- [Can I Use: :focus-visible](https://caniuse.com/css-focus-visible)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- **Focus Visible (2.4.7 - Level AA):** Links must have visible focus indicator for keyboard users
- **Keyboard Operable (2.1.1):** All links must be operable via keyboard (default browser behavior)

**Level AA Requirements:**
- **Contrast (1.4.3):** Link text must have 4.5:1 contrast ratio against background
- **Focus Visible (2.4.7):** Focus indicator must be clearly visible (2px minimum, preferably 3px)

**Level AAA Recommendations:**
- **Enhanced Contrast (1.4.6):** 7:1 contrast ratio for link text
- **Link Purpose (2.4.9):** Link purpose determinable from link text alone

### Focus Indicators

**Required for WCAG 2.4.7:**

```css
/* MINIMUM: Visible focus indicator */
a:focus {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}

/* BETTER: High-contrast focus indicator */
a:focus {
  outline: 3px solid #FFD700;  /* Gold is visible on dark AND light backgrounds */
  outline-offset: 2px;
}

/* MODERN: Show focus only for keyboard (not mouse clicks) */
a:focus-visible {
  outline: 3px solid #FFD700;
  outline-offset: 2px;
}
a:focus:not(:focus-visible) {
  outline: none;  /* Remove focus ring for mouse users */
}
```

**DON'T remove focus outlines:**

```css
/* WRONG: Violates WCAG 2.4.7 */
a:focus {
  outline: none;  /* ❌ Keyboard users can't see focus! */
}
```

### Color Contrast

**Minimum contrast ratios (WCAG 1.4.3):**

- Normal text (< 18px or < 14px bold): 4.5:1
- Large text (≥ 18px or ≥ 14px bold): 3:1
- Enhanced (Level AAA): 7:1 / 4.5:1

**Good contrast examples:**

```css
/* GOOD: 7.7:1 ratio */
a { color: #0066cc; }  /* on white background */

/* GOOD: 8.6:1 ratio */
a:visited { color: #551A8B; }  /* on white background */

/* BAD: 2.3:1 ratio (fails WCAG) */
a { color: #cccccc; }  /* on white background */
```

**Tools to check contrast:**
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- Chrome DevTools (Inspect > Accessibility pane)
- Firefox Accessibility Inspector

### Screen Reader Announcements

- Screen readers announce link text + "link" (e.g., "Home, link")
- `:visited` state is NOT announced (privacy protection)
- `:focus` triggers screen reader cursor movement
- `aria-current="page"` announces "current page" or "current location"

**Resources:**
- [WCAG 2.1: Focus Visible (2.4.7)](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
- [WCAG 2.1: Contrast (Minimum) (1.4.3)](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
- [WebAIM: Links and Hypertext - Link Appearance](https://webaim.org/techniques/hypertext/link_text)

## Best Practices

### Do This ✓

1. **Follow LoVe/HAte order:**
```css
/* Correct order */
a:link { color: blue; }
a:visited { color: purple; }
a:hover, a:focus { color: darkblue; }
a:active { color: red; }
```

2. **Always style :focus for keyboard accessibility:**
```css
a:focus {
  outline: 3px solid #FFD700;
  outline-offset: 2px;
}
```

3. **Group :hover and :focus together:**
```css
/* Ensures keyboard and mouse users get same visual feedback */
a:hover,
a:focus {
  background-color: #ffffcc;
  color: #000;
}
```

4. **Use :focus-visible for modern browsers:**
```css
/* Remove focus for mouse, keep for keyboard */
a:focus:not(:focus-visible) {
  outline: none;
}
a:focus-visible {
  outline: 3px solid #FFD700;
  outline-offset: 2px;
}
```

5. **Add smooth transitions:**
```css
a {
  transition: all 0.3s ease;
}
```

### Avoid This ✗

1. **Don't remove :focus outlines without replacement:**
```css
/* WRONG: Violates WCAG */
a:focus {
  outline: none;
}

/* CORRECT: Replace with visible alternative */
a:focus {
  outline: none;
  box-shadow: 0 0 0 3px #FFD700;
}
```

2. **Don't use :hover alone without :focus:**
```css
/* WRONG: Excludes keyboard users */
a:hover {
  background-color: yellow;
}

/* CORRECT: Include :focus */
a:hover,
a:focus {
  background-color: yellow;
}
```

3. **Don't rely on color alone:**
```css
/* WRONG: Only color changes */
a { color: blue; }
a:hover { color: red; }

/* CORRECT: Color + underline/background */
a {
  color: blue;
  text-decoration: underline;
}
a:hover {
  color: red;
  background-color: #ffeeee;
}
```

4. **Don't forget :visited states:**
```css
/* WRONG: No :visited styling */
a { color: blue; }

/* CORRECT: Distinct :visited color */
a:link { color: blue; }
a:visited { color: purple; }
```

5. **Don't use insufficient contrast:**
```css
/* WRONG: 2.1:1 ratio (fails WCAG) */
a { color: #aaaaaa; }  /* on white background */

/* CORRECT: 7.7:1 ratio */
a { color: #0066cc; }  /* on white background */
```

## Related Topics

### Prerequisites
- [Anchor Links](anchor-links.md) - Creating hyperlinks
- [HTML Syntax](../01-fundamentals/syntax.md) - Element structure

### Related Topics
- [Email and Telephone Links](email-telephone-links.md) - Styling mailto: and tel: links
- [Navigation Element](../07-semantic-html5/nav.md) - Semantic navigation structure
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Focus management

### Next Steps
- [Email and Telephone Links](email-telephone-links.md) - Special link protocols
- [Bookmark Links](bookmark-links.md) - Fragment identifier styling
- [CSS Pseudo-Classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) - Advanced selectors

## Practice Exercise

### Requirements
Create a **"Multi-Style Link System"** that demonstrates proper link state styling. Your HTML document should include:

1. A navigation menu with:
   - Distinct hover, focus, and active states
   - Current page indicator using `aria-current="page"`
   - Visible focus outlines for keyboard navigation
2. In-content text links with:
   - Traditional blue/purple color scheme
   - Underline decoration
   - All five link states styled
3. Call-to-action button links with:
   - Button-style appearance
   - Smooth transitions between states
   - Transform effects on hover
4. CSS that includes:
   - Correct LoVe/HAte ordering
   - `:focus-visible` for modern browsers
   - Sufficient color contrast (WCAG AA)
   - Transitions for smooth state changes

**Accessibility Requirements:**
- Visible focus indicators (3px minimum, high contrast color)
- 4.5:1 minimum contrast ratio for all link text
- :hover and :focus styled identically (mouse + keyboard parity)
- `aria-current="page"` for current navigation item

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Link States Practice</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    /* Add your link styling here */
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
  <title>Link States Showcase</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      line-height: 1.7;
      background-color: #f8f9fa;
    }

    /* ========== NAVIGATION MENU ========== */
    nav {
      background-color: #2c3e50;
      padding: 0;
      margin-bottom: 3em;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    nav ul {
      list-style: none;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
    }

    /* Navigation Links (LoVe/HAte Order) */
    nav a:link,
    nav a:visited {
      display: block;
      padding: 1.25em 2em;
      color: #ecf0f1;
      text-decoration: none;
      font-weight: 500;
      transition: all 0.3s ease;
      position: relative;
    }
    nav a:hover,
    nav a:focus {
      background-color: #34495e;
      color: white;
    }
    nav a:hover::after,
    nav a:focus::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 10%;
      width: 80%;
      height: 3px;
      background-color: #3498db;
    }
    nav a:focus {
      outline: 3px solid #FFD700;
      outline-offset: -3px;
    }
    nav a:focus:not(:focus-visible) {
      outline: none;
    }
    nav a:focus-visible {
      outline: 3px solid #FFD700;
      outline-offset: -3px;
    }
    nav a:active {
      background-color: #1abc9c;
    }

    /* Current Page Indicator */
    nav a[aria-current="page"] {
      background-color: #3498db;
      color: white;
    }
    nav a[aria-current="page"]::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 10%;
      width: 80%;
      height: 3px;
      background-color: white;
    }

    /* ========== MAIN CONTENT ========== */
    main {
      max-width: 900px;
      margin: 0 auto;
      padding: 0 20px 3em;
    }
    article {
      background-color: white;
      padding: 2.5em;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    h1, h2 {
      color: #2c3e50;
      margin-bottom: 0.75em;
    }
    h1 {
      border-bottom: 3px solid #3498db;
      padding-bottom: 0.5em;
    }
    h2 {
      margin-top: 2em;
      border-bottom: 2px solid #95a5a6;
      padding-bottom: 0.3em;
    }
    p {
      margin-bottom: 1em;
    }

    /* ========== CONTENT LINKS (LoVe/HAte Order) ========== */
    article a:link {
      color: #0066cc;
      text-decoration: underline;
      transition: all 0.2s ease;
    }
    article a:visited {
      color: #551A8B;
    }
    article a:hover,
    article a:focus {
      color: #004499;
      text-decoration-thickness: 2px;
      background-color: #fff3cd;
      padding: 2px 4px;
      border-radius: 3px;
    }
    article a:focus {
      outline: 2px solid #FF6B6B;
      outline-offset: 2px;
    }
    article a:focus:not(:focus-visible) {
      outline: none;
    }
    article a:focus-visible {
      outline: 2px solid #FF6B6B;
      outline-offset: 2px;
    }
    article a:active {
      color: #FF6B6B;
      background-color: #ffe6e6;
    }

    /* ========== BUTTON LINKS ========== */
    .button-row {
      display: flex;
      gap: 1.5em;
      margin: 2em 0;
      flex-wrap: wrap;
    }

    /* Primary Button (LoVe/HAte Order) */
    .btn-primary:link,
    .btn-primary:visited {
      display: inline-block;
      padding: 0.85em 2.5em;
      background-color: #3498db;
      color: white;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      font-size: 1.05em;
      transition: all 0.3s ease;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .btn-primary:hover,
    .btn-primary:focus {
      background-color: #2980b9;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      transform: translateY(-2px);
    }
    .btn-primary:focus {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .btn-primary:focus:not(:focus-visible) {
      outline: none;
    }
    .btn-primary:focus-visible {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .btn-primary:active {
      background-color: #21618c;
      transform: translateY(0);
      box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2);
    }

    /* Secondary Button (LoVe/HAte Order) */
    .btn-secondary:link,
    .btn-secondary:visited {
      display: inline-block;
      padding: 0.85em 2.5em;
      background-color: white;
      color: #3498db;
      text-decoration: none;
      border: 2px solid #3498db;
      border-radius: 6px;
      font-weight: bold;
      font-size: 1.05em;
      transition: all 0.3s ease;
    }
    .btn-secondary:hover,
    .btn-secondary:focus {
      background-color: #3498db;
      color: white;
      transform: scale(1.05);
    }
    .btn-secondary:focus {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .btn-secondary:focus:not(:focus-visible) {
      outline: none;
    }
    .btn-secondary:focus-visible {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .btn-secondary:active {
      background-color: #2980b9;
      border-color: #2980b9;
      transform: scale(1);
    }

    /* Success Button (LoVe/HAte Order) */
    .btn-success:link,
    .btn-success:visited {
      display: inline-block;
      padding: 0.85em 2.5em;
      background-color: #27ae60;
      color: white;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      font-size: 1.05em;
      transition: all 0.3s ease;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .btn-success:hover,
    .btn-success:focus {
      background-color: #229954;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    .btn-success:focus {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .btn-success:focus:not(:focus-visible) {
      outline: none;
    }
    .btn-success:focus-visible {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .btn-success:active {
      background-color: #1e8449;
    }

    /* ========== STATE EXPLANATION BOX ========== */
    .state-demo {
      background-color: #e8f4f8;
      border-left: 4px solid #3498db;
      padding: 1.5em;
      margin: 2em 0;
    }
    .state-demo ul {
      margin-left: 2em;
    }
    .state-demo li {
      margin: 0.5em 0;
    }

    /* ========== CODE EXAMPLES ========== */
    code {
      background-color: #2d2d2d;
      color: #f8f8f2;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Consolas', 'Courier New', monospace;
      font-size: 0.9em;
    }
  </style>
</head>
<body>
  <header>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="/" aria-current="page">Home</a></li>
        <li><a href="/about.html">About</a></li>
        <li><a href="/services.html">Services</a></li>
        <li><a href="/portfolio.html">Portfolio</a></li>
        <li><a href="/blog/">Blog</a></li>
        <li><a href="/contact.html">Contact</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <h1>Link States Comprehensive Guide</h1>

      <p>
        This page demonstrates proper styling for all link states, following
        WCAG 2.1 Level AA accessibility guidelines and the LoVe/HAte cascade order.
      </p>

      <section>
        <h2>Navigation Menu States</h2>
        <p>
          The navigation menu above showcases advanced link states:
        </p>
        <div class="state-demo">
          <ul>
            <li><strong>Default:</strong> Light gray text on dark blue background</li>
            <li><strong>Hover:</strong> Darker background + blue animated underline</li>
            <li><strong>Focus:</strong> Gold outline (keyboard users)</li>
            <li><strong>Active:</strong> Teal background while clicking</li>
            <li><strong>Current Page:</strong> Blue background with white underline</li>
          </ul>
        </div>
        <p>
          Try tabbing through the navigation with your keyboard to see the
          <code>:focus</code> state. The gold outline ensures keyboard users
          can track their position.
        </p>
      </section>

      <section>
        <h2>Content Link States</h2>
        <p>
          Traditional in-content links use the classic blue and purple color
          scheme. Try these links:
        </p>
        <ul>
          <li>
            <a href="https://developer.mozilla.org/">MDN Web Docs</a>
            (unvisited - blue)
          </li>
          <li>
            <a href="https://www.google.com/">Google</a>
            (likely visited - purple)
          </li>
          <li>
            <a href="/example.html">Example Page</a>
            (hover for yellow highlight)
          </li>
        </ul>
        <p>
          These links demonstrate the LoVe/HAte cascade order:
        </p>
        <div class="state-demo">
          <ol>
            <li><strong>:link</strong> - Unvisited links are blue (#0066cc)</li>
            <li><strong>:visited</strong> - Visited links are purple (#551A8B)</li>
            <li><strong>:hover/:focus</strong> - Darker blue + yellow background</li>
            <li><strong>:active</strong> - Red while clicking</li>
          </ol>
        </div>
        <p>
          Color contrast ratios meet WCAG AA standards:
          <code>:link</code> = 7.7:1, <code>:visited</code> = 8.6:1
        </p>
      </section>

      <section>
        <h2>Button Link States</h2>
        <p>
          Call-to-action links styled as buttons with smooth transitions:
        </p>
        <div class="button-row">
          <a href="/signup.html" class="btn-primary">Sign Up Free</a>
          <a href="/learn-more.html" class="btn-secondary">Learn More</a>
          <a href="/download.html" class="btn-success">Download Now</a>
        </div>
        <div class="state-demo">
          <ul>
            <li><strong>Hover:</strong> Darker shade + shadow + lift effect</li>
            <li><strong>Focus:</strong> Gold outline 3px thick (keyboard)</li>
            <li><strong>Active:</strong> Pressed down effect (translateY: 0)</li>
            <li><strong>Transitions:</strong> Smooth 0.3s ease on all properties</li>
          </ul>
        </div>
        <p>
          These buttons use <code>:focus-visible</code> to show outlines
          only for keyboard navigation, not mouse clicks.
        </p>
      </section>

      <section>
        <h2>Accessibility Features</h2>
        <p>
          This page implements several WCAG 2.1 Level AA requirements:
        </p>
        <ul>
          <li>
            <strong>Focus Visible (2.4.7):</strong> All links have 2-3px
            high-contrast focus indicators
          </li>
          <li>
            <strong>Contrast Minimum (1.4.3):</strong> All link text meets
            4.5:1 minimum contrast ratio
          </li>
          <li>
            <strong>Keyboard (2.1.1):</strong> All links operable via keyboard
            (try tabbing!)
          </li>
          <li>
            <strong>Consistent Identification (3.2.4):</strong> Similar links
            styled consistently
          </li>
          <li>
            <strong>Non-text Contrast (1.4.11):</strong> Focus indicators meet
            3:1 contrast
          </li>
        </ul>
        <p>
          The <code>:focus-visible</code> pseudo-class ensures focus outlines
          appear for keyboard users but not for mouse clicks, providing the
          best experience for both interaction methods.
        </p>
      </section>

      <section>
        <h2>Learn More</h2>
        <p>
          For additional resources, visit:
        </p>
        <ul>
          <li>
            <a href="https://www.w3.org/WAI/WCAG21/quickref/">
              WCAG 2.1 Quick Reference
            </a>
          </li>
          <li>
            <a href="https://webaim.org/articles/contrast/">
              WebAIM Contrast Checker
            </a>
          </li>
          <li>
            <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes">
              MDN: CSS Pseudo-classes
            </a>
          </li>
        </ul>
      </section>
    </article>
  </main>
</body>
</html>
```

**Key Features of Solution:**
- Correct LoVe/HAte cascade order for all link types
- Navigation with `aria-current="page"` for current link
- Content links with traditional blue/purple scheme
- Three button styles (primary, secondary, success)
- `:focus-visible` for modern browsers (outlines only for keyboard)
- Visible 3px focus indicators in high-contrast gold (#FFD700)
- Smooth transitions (0.3s ease) between states
- Transform effects on hover (translateY, scale)
- WCAG AA compliant contrast:
  - Link blue: #0066cc = 7.7:1 ratio
  - Visited purple: #551A8B = 8.6:1 ratio
  - Focus gold: #FFD700 = visible on all backgrounds
- `:hover` and `:focus` styled identically (mouse + keyboard parity)
- Active states for touch feedback on mobile
- Animated underline effects on navigation hover
- Box shadows for depth on button links

---

## Navigation

- **Previous:** [Anchor Links](anchor-links.md)
- **Next:** [Email and Telephone Links](email-telephone-links.md)
- **Up:** [Links and Navigation](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Links and Navigation
- **Difficulty:** Intermediate
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
