---
title: Abbreviations
category: Text Content
order: 6
---

# Abbreviations

> **Quick Summary:** The abbr element marks up abbreviations and acronyms with optional expansions via the title attribute, improving accessibility for screen reader users and providing context for unfamiliar terms.

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

Abbreviations and acronyms are ubiquitous in technical writing, legal documents, and professional communication. The `<abbr>` element provides a semantic way to mark up shortened forms of words or phrases, with the `title` attribute supplying the full expansion. This dual approach serves both human readers (who can hover to see the expansion) and assistive technologies (which can announce the full form to screen reader users).

The HTML5 specification consolidated the older `<abbr>` and `<acronym>` elements into a single `<abbr>` element that handles both abbreviations (shortened forms like "Dr." for "Doctor") and acronyms (initialisms like "NASA" for "National Aeronautics and Space Administration"). This simplification improves consistency and reduces confusion about which element to use.

While the `title` attribute provides machine-readable expansion, it's often best practice to also spell out abbreviations on first use within body text, especially for critical terminology. This ensures accessibility for users who may not interact with hover tooltips (mobile users, keyboard-only users) and improves comprehension for all readers.

**Key Concept:** Use `<abbr>` to mark abbreviated forms and provide full expansions via the `title` attribute. Spell out important abbreviations on first use for maximum accessibility.

## Basic Syntax

**Basic abbreviation with expansion:**
```html
<abbr title="HyperText Markup Language">HTML</abbr>
```

**Abbreviation without title attribute:**
```html
<abbr>HTML</abbr>  <!-- Valid but not recommended -->
```

**Abbreviation with first-use pattern:**
```html
<p>
  The <abbr title="World Health Organization">WHO</abbr> is a specialized
  agency of the United Nations. The WHO coordinates global health initiatives.
</p>
```

**Attributes:**

| Attribute | Purpose | Value | Required |
|-----------|---------|-------|----------|
| `title` | Full expansion of abbreviation | Plain text | Recommended (not required) |
| Global attributes | id, class, lang, dir, etc. | Varies | Optional |

**Note:** The `<abbr>` element is an inline element and can be used anywhere inline text is allowed.

## Examples

### Example 1: Technical Documentation with Abbreviations
**Use Case:** Software documentation with technical acronyms

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>API Documentation</title>
  <style>
    abbr {
      text-decoration: underline dotted;
      cursor: help;
    }
    abbr[title]:hover {
      text-decoration: underline solid;
    }
  </style>
</head>
<body>
  <article>
    <h1>REST API Integration Guide</h1>

    <section>
      <h2>Introduction</h2>
      <p>
        This guide covers how to integrate with our
        <abbr title="Representational State Transfer">REST</abbr>
        <abbr title="Application Programming Interface">API</abbr>.
        You'll need to understand <abbr title="HyperText Transfer Protocol">HTTP</abbr>
        methods and <abbr title="JavaScript Object Notation">JSON</abbr>
        data formatting.
      </p>

      <p>
        All API requests require an <abbr title="Application Programming Interface">API</abbr>
        key sent via the <code>Authorization</code> header. You can obtain
        your API key from the dashboard.
      </p>
    </section>

    <section>
      <h2>Authentication</h2>
      <p>
        We support two authentication methods:
        <abbr title="JSON Web Token">JWT</abbr> and
        <abbr title="OAuth 2.0">OAuth</abbr>.
        JWT is recommended for server-to-server communication, while
        OAuth is better suited for user-facing applications.
      </p>

      <p>
        <strong>Note:</strong> All requests must use
        <abbr title="HyperText Transfer Protocol Secure">HTTPS</abbr>
        to protect sensitive data in transit.
      </p>
    </section>

    <section>
      <h2>Response Formats</h2>
      <p>
        API responses are returned in JSON format with appropriate
        <abbr title="HyperText Transfer Protocol">HTTP</abbr> status codes:
      </p>

      <ul>
        <li>200 OK - Request succeeded</li>
        <li>201 Created - Resource created successfully</li>
        <li>400 Bad Request - Invalid request parameters</li>
        <li>401 Unauthorized - Missing or invalid API key</li>
        <li>404 Not Found - Resource doesn't exist</li>
        <li>500 Internal Server Error - Server encountered an error</li>
      </ul>
    </section>
  </article>
</body>
</html>
```

### Example 2: Medical/Scientific Document
**Use Case:** Health article with medical abbreviations and first-use pattern

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Understanding Blood Pressure</title>
  <style>
    abbr {
      text-decoration: underline dotted #0066cc;
      cursor: help;
      color: #0066cc;
    }
    .first-use {
      font-weight: bold;
    }
  </style>
</head>
<body>
  <article>
    <h1>Understanding Blood Pressure</h1>

    <section>
      <h2>What is Blood Pressure?</h2>
      <p>
        Blood pressure (<abbr title="Blood Pressure" class="first-use">BP</abbr>)
        is the force of blood pushing against artery walls. It's measured in
        millimeters of mercury (<abbr title="millimeters of mercury">mmHg</abbr>).
      </p>

      <p>
        A normal BP reading is typically around 120/80 mmHg. The first number
        (systolic) measures pressure when your heart beats. The second number
        (diastolic) measures pressure when your heart rests between beats.
      </p>
    </section>

    <section>
      <h2>High Blood Pressure</h2>
      <p>
        High blood pressure, or hypertension (<abbr title="High Blood Pressure">HBP</abbr>),
        affects millions worldwide. The
        <abbr title="American Heart Association">AHA</abbr> defines
        hypertension as BP consistently at or above 130/80 mmHg.
      </p>

      <p>
        Left untreated, HBP can increase your risk of
        <abbr title="Cardiovascular Disease">CVD</abbr>, stroke, and
        kidney disease. Regular monitoring by your
        <abbr title="Medical Doctor">MD</abbr> or
        <abbr title="Registered Nurse">RN</abbr> is essential.
      </p>
    </section>

    <section>
      <h2>Treatment Options</h2>
      <p>
        Treatment may include lifestyle changes and medication. Your doctor
        might prescribe <abbr title="Angiotensin-Converting Enzyme">ACE</abbr>
        inhibitors or <abbr title="Angiotensin Receptor Blockers">ARBs</abbr>
        to help lower blood pressure.
      </p>

      <p>
        The <abbr title="Food and Drug Administration">FDA</abbr> has
        approved multiple medications for HBP. Work with your healthcare
        provider to find the right treatment plan.
      </p>
    </section>
  </article>
</body>
</html>
```

### Example 3: Business Document with Mixed Abbreviations
**Use Case:** Corporate memo with business and technical abbreviations

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Q4 2025 Strategic Plan</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    abbr {
      text-decoration: underline dotted;
      cursor: help;
    }
    .memo-header {
      border-bottom: 2px solid #333;
      padding-bottom: 1em;
      margin-bottom: 1.5em;
    }
    .memo-header p {
      margin: 0.25em 0;
    }
  </style>
</head>
<body>
  <article>
    <div class="memo-header">
      <p><strong>TO:</strong> Executive Team</p>
      <p><strong>FROM:</strong> <abbr title="Chief Executive Officer">CEO</abbr></p>
      <p><strong>DATE:</strong> November 17, 2025</p>
      <p><strong>RE:</strong> Q4 2025 Strategic Initiatives</p>
    </div>

    <section>
      <h2>Financial Goals</h2>
      <p>
        Our <abbr title="Fourth Quarter">Q4</abbr> revenue target is
        $15M, representing a 25%
        <abbr title="Year Over Year">YoY</abbr> increase. The
        <abbr title="Chief Financial Officer">CFO</abbr> projects we'll
        exceed this target based on current
        <abbr title="Annual Recurring Revenue">ARR</abbr> growth.
      </p>

      <p>
        Key performance indicators (<abbr title="Key Performance Indicators">KPIs</abbr>)
        to monitor include:
      </p>

      <ul>
        <li><abbr title="Customer Acquisition Cost">CAC</abbr></li>
        <li><abbr title="Lifetime Value">LTV</abbr></li>
        <li><abbr title="Monthly Recurring Revenue">MRR</abbr></li>
        <li><abbr title="Net Promoter Score">NPS</abbr></li>
      </ul>
    </section>

    <section>
      <h2>Product Development</h2>
      <p>
        The <abbr title="Chief Technology Officer">CTO</abbr> has
        prioritized three initiatives for Q4:
      </p>

      <ol>
        <li>
          Complete the <abbr title="Single Sign-On">SSO</abbr>
          integration with major identity providers
        </li>
        <li>
          Achieve <abbr title="Service Organization Control 2">SOC 2</abbr>
          Type II certification
        </li>
        <li>
          Launch our <abbr title="Application Programming Interface">API</abbr>
          v2 with improved <abbr title="Software Development Kit">SDK</abbr>
          support
        </li>
      </ol>

      <p>
        All projects must comply with
        <abbr title="General Data Protection Regulation">GDPR</abbr>,
        <abbr title="California Consumer Privacy Act">CCPA</abbr>, and
        <abbr title="Health Insurance Portability and Accountability Act">HIPAA</abbr>
        requirements where applicable.
      </p>
    </section>

    <section>
      <h2>Marketing Initiatives</h2>
      <p>
        The <abbr title="Chief Marketing Officer">CMO</abbr> will focus on
        improving our <abbr title="Search Engine Optimization">SEO</abbr>
        rankings and expanding our
        <abbr title="Pay-Per-Click">PPC</abbr> campaigns. We'll also
        invest in <abbr title="Content Management System">CMS</abbr>
        improvements to support our content marketing strategy.
      </p>

      <p>
        Our target <abbr title="Return on Investment">ROI</abbr> for
        marketing spend is 3:1. The team will report metrics via our
        <abbr title="Customer Relationship Management">CRM</abbr>
        dashboard weekly.
      </p>
    </section>
  </article>
</body>
</html>
```

## Common Use Cases

### 1. Technical Documentation
Mark up technical acronyms and initialisms in developer documentation, API guides, or system specifications:

```html
<p>
  Configure your <abbr title="Domain Name System">DNS</abbr> settings
  to point to our <abbr title="Content Delivery Network">CDN</abbr>.
  Use <abbr title="Secure Sockets Layer">SSL</abbr> certificates for
  all production domains.
</p>
```

**When to use:** API documentation, technical manuals, configuration guides, system requirements

### 2. Medical and Scientific Writing
Provide expansions for medical abbreviations, scientific notation, and clinical terminology:

```html
<p>
  The patient's <abbr title="Blood Pressure">BP</abbr> was 140/90
  <abbr title="millimeters of mercury">mmHg</abbr>. Lab results showed
  elevated <abbr title="Low-Density Lipoprotein">LDL</abbr> cholesterol.
</p>
```

**When to use:** Medical articles, research papers, health information, scientific reports

### 3. Business and Legal Documents
Clarify business acronyms, legal terms, and organizational abbreviations:

```html
<p>
  The <abbr title="Chief Executive Officer">CEO</abbr> announced that
  <abbr title="Return on Investment">ROI</abbr> increased 35% this quarter.
  Our <abbr title="Intellectual Property">IP</abbr> portfolio now includes
  12 patents.
</p>
```

**When to use:** Corporate communications, financial reports, legal contracts, policy documents

## Browser Support

| Element | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| `<abbr>` | All | All | All | All | All | All |
| `title` attribute | All | All | All | All | All | All |

**Browser Support:** Universal (100%)

The `<abbr>` element has been part of HTML since HTML 4.01 and is supported by all browsers. The deprecated `<acronym>` element (HTML 4.01 only) has been replaced by `<abbr>` in HTML5.

**Default Styling:**
- Most browsers apply dotted underline to `<abbr>` elements (Firefox, Chrome, Edge)
- Safari may not apply any default styling
- `title` attribute shows as tooltip on hover (desktop browsers)
- Mobile browsers typically don't display tooltips reliably

**Resources:**
- [MDN: abbr element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/abbr)
- [WHATWG HTML Living Standard: abbr](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-abbr-element)
- [W3Schools: HTML abbr Tag](https://www.w3schools.com/tags/tag_abbr.asp)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- Provide text expansions for abbreviations that may be unfamiliar to users (3.1.4 Abbreviations - Level AAA guideline, but good practice)
- Ensure `<abbr>` elements don't rely solely on visual styling (dotted underline) to convey meaning

**Level AA Requirements:**
- Maintain sufficient color contrast if styling abbreviations with color
- Ensure abbreviations are understandable without requiring hover interactions (critical for mobile)

**Level AAA Recommendations:**
- Provide expansions for all abbreviations except those that have become more common than the expanded form (e.g., "radar", "laser")
- Spell out abbreviations on first use in body text, then use `<abbr>` for subsequent occurrences

### Screen Reader Behavior

| Screen Reader | Behavior | Announcement |
|---------------|----------|--------------|
| NVDA | Announces title attribute | Reads abbreviation, then "abbreviation: [expansion]" |
| JAWS | Announces title attribute (configurable) | May read expansion automatically or on request |
| VoiceOver | May announce title (iOS/macOS differences) | Inconsistent - may not announce title |
| TalkBack | Limited support | Often doesn't announce title attribute |

**Best Practices for Screen Readers:**

1. **Spell out abbreviations on first use:**
```html
<!-- GOOD: First use provides context -->
<p>
  The World Wide Web Consortium (<abbr title="World Wide Web Consortium">W3C</abbr>)
  develops web standards. The W3C was founded in 1994.
</p>

<!-- BAD: Relies on title attribute alone -->
<p>
  The <abbr title="World Wide Web Consortium">W3C</abbr> develops web standards.
</p>
```

2. **Don't rely on title attribute for critical information:**
```html
<!-- GOOD: Expansion in visible text -->
<p>
  Submit your request via the <abbr title="Hypertext Transfer Protocol">HTTP</abbr>
  POST method. HTTP is the foundation of data communication on the web.
</p>

<!-- BAD: Critical info only in title -->
<p>
  Use <abbr title="Hypertext Transfer Protocol - the foundation of web communication">HTTP</abbr>
  for all requests.
</p>
```

3. **Consider providing a glossary for heavily abbreviated content:**
```html
<article>
  <!-- Main content with abbreviations -->
  <p>Configure your DNS, CDN, and SSL settings...</p>

  <!-- Glossary section -->
  <section id="glossary">
    <h2>Glossary</h2>
    <dl>
      <dt><abbr title="Domain Name System">DNS</abbr></dt>
      <dd>Domain Name System - translates domain names to IP addresses</dd>

      <dt><abbr title="Content Delivery Network">CDN</abbr></dt>
      <dd>Content Delivery Network - distributed servers for fast content delivery</dd>
    </dl>
  </section>
</article>
```

### Mobile Considerations

- Mobile browsers typically **don't show tooltips** on tap/touch
- Consider spelling out abbreviations inline on mobile-focused content
- Use CSS to add visual indicators (dotted underline, color) that work without hover

**Resources:**
- [WCAG 2.1: Abbreviations (3.1.4)](https://www.w3.org/WAI/WCAG21/Understanding/abbreviations.html)
- [WebAIM: Semantic Structure - Abbreviations](https://webaim.org/techniques/semanticstructure/)

## Best Practices

### Do This ✓

1. **Spell out abbreviations on first use:**
```html
<!-- Correct: First-use pattern -->
<p>
  The Federal Bureau of Investigation
  (<abbr title="Federal Bureau of Investigation">FBI</abbr>)
  announced new cyber security guidelines. The FBI will publish
  updates quarterly.
</p>
```

2. **Use title attribute for machine-readable expansion:**
```html
<!-- Correct: title provides full expansion -->
<abbr title="HyperText Markup Language">HTML</abbr>
<abbr title="Cascading Style Sheets">CSS</abbr>
<abbr title="JavaScript">JS</abbr>
```

3. **Style abbreviations for visual clarity:**
```css
abbr {
  text-decoration: underline dotted;
  cursor: help;
}
abbr[title]:hover {
  text-decoration: underline solid;
}
```

4. **Use abbr for both abbreviations and acronyms:**
```html
<!-- Correct: Use <abbr> for both types -->
<abbr title="Doctor">Dr.</abbr> Smith  <!-- abbreviation -->
<abbr title="National Aeronautics and Space Administration">NASA</abbr>  <!-- acronym -->
<abbr title="Incorporated">Inc.</abbr>  <!-- abbreviation -->
```

5. **Provide glossaries for technical documents:**
```html
<article>
  <p>Content with many abbreviations...</p>

  <aside>
    <h3>Abbreviations Used in This Document</h3>
    <dl>
      <dt>API</dt>
      <dd>Application Programming Interface</dd>
      <dt>REST</dt>
      <dd>Representational State Transfer</dd>
    </dl>
  </aside>
</article>
```

### Avoid This ✗

1. **Don't use abbr without title attribute for unfamiliar terms:**
```html
<!-- WRONG: No expansion provided -->
<p>Configure the <abbr>CDN</abbr> settings.</p>

<!-- CORRECT: Title provides expansion -->
<p>Configure the <abbr title="Content Delivery Network">CDN</abbr> settings.</p>
```

2. **Don't use the deprecated acronym element:**
```html
<!-- WRONG: <acronym> is obsolete (HTML4 only) -->
<acronym title="National Aeronautics and Space Administration">NASA</acronym>

<!-- CORRECT: Use <abbr> for all abbreviations -->
<abbr title="National Aeronautics and Space Administration">NASA</abbr>
```

3. **Don't put full expansions in title for well-known abbreviations:**
```html
<!-- WRONG: Redundant for universally known terms -->
<abbr title="United States of America">USA</abbr>
<abbr title="Unidentified Flying Object">UFO</abbr>

<!-- CORRECT: Skip <abbr> for universally known terms -->
<p>USA, UFO, DNA, radar, laser</p>  <!-- No <abbr> needed -->
```

4. **Don't use abbr for visual styling alone:**
```html
<!-- WRONG: Not an abbreviation, just styled text -->
<abbr>Important</abbr>

<!-- CORRECT: Use appropriate element or CSS -->
<strong>Important</strong>
```

5. **Don't assume title tooltips work on all devices:**
```html
<!-- WRONG: Relies on tooltip for critical info -->
<p>
  Contact us at <abbr title="support@example.com - available 24/7">support</abbr>.
</p>

<!-- CORRECT: Critical info visible in text -->
<p>
  Contact us at <a href="mailto:support@example.com">support@example.com</a>
  (available 24/7).
</p>
```

## Related Topics

### Prerequisites
- [HTML Syntax](../01-fundamentals/syntax.md) - Element and attribute syntax
- [Text Formatting](text-formatting.md) - Other inline semantic elements
- [HTML Entities](../01-fundamentals/entities.md) - Special characters in abbreviations

### Related Topics
- [Links](../03-links-navigation/anchor-links.md) - Linking to glossary definitions
- [Global Attributes](../09-global-attributes/id-class.md) - title attribute details
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Making content accessible

### Next Steps
- [Text Direction](text-direction.md) - Language and direction attributes
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Semantic markup principles
- [ARIA Attributes](../09-global-attributes/aria-attributes.md) - Advanced accessibility

## Practice Exercise

### Requirements
Create a **"Web Development Glossary"** page that demonstrates proper use of abbreviations. Your HTML document should include:

1. A main heading and introduction paragraph
2. At least 2 sections of content containing:
   - At least 10 different abbreviations marked with `<abbr>`
   - `title` attributes for all abbreviations
   - First-use pattern for at least 3 abbreviations (spell out, then abbreviate)
3. A glossary section at the end with:
   - Definition list (`<dl>`, `<dt>`, `<dd>`)
   - Expansions for all abbreviations used
4. CSS styling that includes:
   - Visual indicator for abbreviations (dotted underline, color)
   - Hover effect showing the abbreviation is interactive
   - Cursor: help for abbreviations
   - Sufficient color contrast (WCAG AA)

**Accessibility Requirements:**
- Spell out at least 3 abbreviations on first use (don't rely on title alone)
- Provide a glossary section for all abbreviations
- Ensure visual indicators don't rely solely on color
- Use semantic HTML for glossary (definition list)

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Web Development Glossary</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    /* Add your abbr styling here */
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
  <title>Web Development Abbreviations Guide</title>
  <style>
    body {
      font-family: Georgia, serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.7;
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
    abbr {
      text-decoration: underline dotted #3498db;
      cursor: help;
      color: #2980b9;
      font-weight: 500;
    }
    abbr[title]:hover {
      text-decoration: underline solid #3498db;
      color: #1a5490;
    }
    .first-use {
      background-color: #fff3cd;
      padding: 2px 4px;
      border-radius: 3px;
    }
    #glossary {
      background-color: white;
      padding: 2em;
      border-radius: 8px;
      margin-top: 3em;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    dl {
      display: grid;
      grid-template-columns: auto 1fr;
      gap: 1em 2em;
    }
    dt {
      font-weight: bold;
      color: #2980b9;
    }
    dd {
      margin: 0;
      color: #555;
    }
  </style>
</head>
<body>
  <article>
    <h1>Essential Web Development Abbreviations</h1>

    <p>
      Modern web development involves numerous technologies, frameworks, and
      protocols. Understanding common abbreviations is essential for reading
      technical documentation and communicating with other developers.
    </p>

    <section>
      <h2>Fundamental Web Technologies</h2>

      <p>
        The foundation of web development consists of three core technologies:
        HyperText Markup Language
        (<abbr title="HyperText Markup Language" class="first-use">HTML</abbr>),
        Cascading Style Sheets
        (<abbr title="Cascading Style Sheets" class="first-use">CSS</abbr>),
        and JavaScript
        (<abbr title="JavaScript" class="first-use">JS</abbr>).
      </p>

      <p>
        HTML provides the structure, CSS controls the presentation, and
        JS adds interactivity. Together, these technologies enable developers
        to build dynamic, responsive web applications.
      </p>

      <p>
        Modern HTML is defined by the <abbr title="Web Hypertext Application Technology Working Group">WHATWG</abbr>
        Living Standard, which continuously evolves to meet web development needs.
        The <abbr title="World Wide Web Consortium">W3C</abbr> also publishes
        web standards and accessibility guidelines.
      </p>
    </section>

    <section>
      <h2>Web Development Frameworks and Tools</h2>

      <p>
        Popular JavaScript frameworks include
        <abbr title="React">React</abbr> (developed by Meta),
        <abbr title="Vue.js">Vue</abbr>, and
        <abbr title="Angular">Angular</abbr>. For backend development,
        developers often use <abbr title="Node.js">Node</abbr> with
        <abbr title="Express.js">Express</abbr> or other frameworks.
      </p>

      <p>
        Version control is managed through
        <abbr title="Git">Git</abbr>, with code hosted on platforms like
        <abbr title="GitHub">GitHub</abbr>,
        <abbr title="GitLab">GitLab</abbr>, or
        <abbr title="Bitbucket">Bitbucket</abbr>.
      </p>
    </section>

    <section>
      <h2>Web Protocols and APIs</h2>

      <p>
        Web communication relies on
        <abbr title="HyperText Transfer Protocol">HTTP</abbr> and its
        secure variant, <abbr title="HyperText Transfer Protocol Secure">HTTPS</abbr>.
        Modern web applications fetch data using
        <abbr title="Asynchronous JavaScript and XML">AJAX</abbr> or the
        Fetch <abbr title="Application Programming Interface">API</abbr>.
      </p>

      <p>
        <abbr title="Representational State Transfer">REST</abbr> and
        <abbr title="GraphQL">GraphQL</abbr> are popular API architectural
        styles. REST APIs use standard HTTP methods (GET, POST, PUT, DELETE),
        while GraphQL allows clients to request exactly the data they need.
      </p>

      <p>
        Data is typically exchanged in
        <abbr title="JavaScript Object Notation">JSON</abbr> or
        <abbr title="eXtensible Markup Language">XML</abbr> format.
        JSON has become the de facto standard for web APIs due to its
        simplicity and JavaScript compatibility.
      </p>
    </section>

    <section>
      <h2>Performance and Optimization</h2>

      <p>
        Developers optimize websites by using
        <abbr title="Content Delivery Network">CDN</abbr>s to distribute
        static assets globally. Proper <abbr title="Domain Name System">DNS</abbr>
        configuration ensures fast domain resolution.
      </p>

      <p>
        Security best practices include implementing
        <abbr title="Secure Sockets Layer">SSL</abbr>/
        <abbr title="Transport Layer Security">TLS</abbr> certificates,
        protecting against <abbr title="Cross-Site Scripting">XSS</abbr> and
        <abbr title="Cross-Site Request Forgery">CSRF</abbr> attacks, and
        following <abbr title="Open Web Application Security Project">OWASP</abbr>
        guidelines.
      </p>
    </section>

    <section id="glossary">
      <h2>Glossary of Abbreviations</h2>

      <dl>
        <dt><abbr title="Asynchronous JavaScript and XML">AJAX</abbr></dt>
        <dd>Asynchronous JavaScript and XML - technique for updating page content without full page reload</dd>

        <dt><abbr title="Application Programming Interface">API</abbr></dt>
        <dd>Application Programming Interface - set of rules for software communication</dd>

        <dt><abbr title="Cascading Style Sheets">CSS</abbr></dt>
        <dd>Cascading Style Sheets - stylesheet language for HTML presentation</dd>

        <dt><abbr title="Content Delivery Network">CDN</abbr></dt>
        <dd>Content Delivery Network - distributed servers for fast content delivery</dd>

        <dt><abbr title="Cross-Site Request Forgery">CSRF</abbr></dt>
        <dd>Cross-Site Request Forgery - attack forcing users to execute unwanted actions</dd>

        <dt><abbr title="Cross-Site Scripting">XSS</abbr></dt>
        <dd>Cross-Site Scripting - injection of malicious scripts into web pages</dd>

        <dt><abbr title="Domain Name System">DNS</abbr></dt>
        <dd>Domain Name System - translates domain names to IP addresses</dd>

        <dt><abbr title="Git">Git</abbr></dt>
        <dd>Distributed version control system for tracking code changes</dd>

        <dt><abbr title="GraphQL">GraphQL</abbr></dt>
        <dd>Query language for APIs developed by Facebook</dd>

        <dt><abbr title="HyperText Markup Language">HTML</abbr></dt>
        <dd>HyperText Markup Language - standard markup language for web pages</dd>

        <dt><abbr title="HyperText Transfer Protocol">HTTP</abbr></dt>
        <dd>HyperText Transfer Protocol - foundation of data communication on the web</dd>

        <dt><abbr title="HyperText Transfer Protocol Secure">HTTPS</abbr></dt>
        <dd>HyperText Transfer Protocol Secure - encrypted version of HTTP</dd>

        <dt><abbr title="JavaScript">JS</abbr></dt>
        <dd>JavaScript - programming language for web interactivity</dd>

        <dt><abbr title="JavaScript Object Notation">JSON</abbr></dt>
        <dd>JavaScript Object Notation - lightweight data interchange format</dd>

        <dt><abbr title="Open Web Application Security Project">OWASP</abbr></dt>
        <dd>Open Web Application Security Project - nonprofit focused on web security</dd>

        <dt><abbr title="Representational State Transfer">REST</abbr></dt>
        <dd>Representational State Transfer - architectural style for web services</dd>

        <dt><abbr title="Secure Sockets Layer">SSL</abbr></dt>
        <dd>Secure Sockets Layer - deprecated cryptographic protocol (replaced by TLS)</dd>

        <dt><abbr title="Transport Layer Security">TLS</abbr></dt>
        <dd>Transport Layer Security - cryptographic protocol for secure communication</dd>

        <dt><abbr title="World Wide Web Consortium">W3C</abbr></dt>
        <dd>World Wide Web Consortium - international standards organization for the web</dd>

        <dt><abbr title="Web Hypertext Application Technology Working Group">WHATWG</abbr></dt>
        <dd>Web Hypertext Application Technology Working Group - maintains HTML Living Standard</dd>

        <dt><abbr title="eXtensible Markup Language">XML</abbr></dt>
        <dd>eXtensible Markup Language - markup language for encoding documents</dd>
      </dl>
    </section>

    <footer>
      <p>
        <small>
          Last updated: November 17, 2025. For more web development resources,
          visit <abbr title="Mozilla Developer Network">MDN</abbr> Web Docs.
        </small>
      </p>
    </footer>
  </article>
</body>
</html>
```

**Key Features of Solution:**
- Uses `<abbr>` with `title` attribute for all abbreviations (20+ instances)
- Implements first-use pattern for HTML, CSS, and JS (spelled out, then abbreviated)
- Highlights first-use abbreviations with CSS class
- Comprehensive glossary using semantic definition list (`<dl>`, `<dt>`, `<dd>`)
- CSS styling with dotted underline and help cursor
- Hover effect changes underline from dotted to solid
- Color styling for abbreviations (#2980b9 on #f9f9f9 = 4.7:1 contrast ratio - WCAG AA compliant)
- Grid layout for glossary (clean two-column display)
- All abbreviations in content also appear in glossary
- Accessible without requiring tooltip interaction (first-use + glossary)
- Mobile-friendly (doesn't rely on hover for critical information)

---

## Navigation

- **Previous:** [Code and Preformatted Text](code-preformatted.md)
- **Next:** [Text Direction](text-direction.md)
- **Up:** [Text Content](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Text Content
- **Difficulty:** Beginner
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
