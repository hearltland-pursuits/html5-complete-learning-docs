---
title: Email and Telephone Links
category: Links and Navigation
order: 3
---

# Email and Telephone Links

> **Quick Summary:** Special URL schemes (mailto: and tel:) enable anchor elements to trigger email composition and phone dialing directly from web pages, improving user convenience on devices with email clients and telephony capabilities.

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

Beyond standard HTTP/HTTPS URLs, HTML anchor elements support special URI schemes that trigger specific actions on user devices. The `mailto:` protocol launches the user's default email client with a pre-populated composition window, while the `tel:` protocol initiates phone calls on devices with telephony capabilities (smartphones, VoIP software).

These protocols provide seamless integration between web content and device functionality, eliminating the need for users to manually copy contact information. Email links can pre-fill not only the recipient address but also subject lines, body text, CC/BCC recipients, and even multiple recipients. Telephone links can include international dialing codes, extensions, and pause characters for automated phone systems.

Understanding when and how to use these special links is essential for creating user-friendly contact pages, especially for mobile-responsive websites where one-tap dialing and emailing significantly improve user experience. However, these links require careful accessibility consideration—screen reader users need context about what action the link will trigger, and desktop users without configured email clients may experience broken functionality.

**Key Concept:** `mailto:` and `tel:` are URI schemes that delegate actions to external applications (email clients, phone dialers). Always provide clear link text indicating the action, and consider fallback options for users without configured applications.

## Basic Syntax

### Email Links (mailto:)

**Basic email link:**
```html
<a href="mailto:contact@example.com">Email Us</a>
```

**Multiple recipients (comma-separated):**
```html
<a href="mailto:sales@example.com,support@example.com">Email Sales & Support</a>
```

**Pre-filled subject line:**
```html
<a href="mailto:support@example.com?subject=Technical Support Request">
  Contact Support
</a>
```

**Pre-filled subject + body:**
```html
<a href="mailto:contact@example.com?subject=Feedback&body=Hello, I wanted to share...">
  Send Feedback
</a>
```

**CC and BCC recipients:**
```html
<a href="mailto:primary@example.com?cc=manager@example.com&bcc=archive@example.com&subject=Project Update">
  Email Team
</a>
```

**mailto: Parameters:**

| Parameter | Purpose | Example | Notes |
|-----------|---------|---------|-------|
| `subject` | Pre-fill subject line | `?subject=Hello` | URL-encode spaces (%20) |
| `body` | Pre-fill message body | `?body=Message text` | URL-encode special chars |
| `cc` | Carbon copy recipients | `?cc=user@example.com` | Comma-separate multiple |
| `bcc` | Blind carbon copy | `?bcc=secret@example.com` | Hidden recipients |

**Multiple parameters (use & separator):**
```html
<a href="mailto:support@example.com?subject=Bug%20Report&body=Describe%20the%20issue:&cc=dev@example.com">
  Report Bug
</a>
```

### Telephone Links (tel:)

**Basic phone link:**
```html
<a href="tel:+15551234567">Call Us: (555) 123-4567</a>
```

**International format (E.164 recommended):**
```html
<a href="tel:+14155552671">+1 (415) 555-2671</a>
```

**With extension (pause characters):**
```html
<!-- Comma = 2-second pause -->
<a href="tel:+15551234567,,,123">Call Main Office (ext. 123)</a>

<!-- Semicolon = wait for user -->
<a href="tel:+15551234567;123">Call with Extension</a>
```

**Formatting guidelines:**
- Use E.164 format: `+[country code][area code][number]`
- Include `+` prefix for international dialing
- Remove spaces, hyphens, parentheses from href (visual formatting OK in link text)
- Use commas (`,`) for automatic pauses, semicolons (`;`) for user-initiated prompts

## Examples

### Example 1: Contact Page with Email and Phone Links
**Use Case:** Business contact page with multiple communication methods

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Us</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 40px 20px;
      line-height: 1.7;
    }
    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #3498db;
      padding-bottom: 0.5em;
    }
    .contact-section {
      background-color: #ecf0f1;
      padding: 2em;
      border-radius: 8px;
      margin: 2em 0;
    }
    .contact-method {
      margin: 1.5em 0;
    }
    .contact-method strong {
      display: block;
      color: #34495e;
      margin-bottom: 0.5em;
      font-size: 1.1em;
    }
    a[href^="mailto:"],
    a[href^="tel:"] {
      color: #0066cc;
      text-decoration: none;
      padding: 0.5em 1em;
      background-color: white;
      border-radius: 6px;
      display: inline-block;
      transition: all 0.3s ease;
      border: 2px solid #3498db;
    }
    a[href^="mailto:"]:hover,
    a[href^="mailto:"]:focus,
    a[href^="tel:"]:hover,
    a[href^="tel:"]:focus {
      background-color: #3498db;
      color: white;
      transform: translateY(-2px);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }
    a[href^="mailto:"]:focus,
    a[href^="tel:"]:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }
    /* Icon indicators */
    a[href^="mailto:"]::before {
      content: "✉ ";
      margin-right: 0.5em;
    }
    a[href^="tel:"]::before {
      content: "📞 ";
      margin-right: 0.5em;
    }
  </style>
</head>
<body>
  <article>
    <h1>Contact Us</h1>

    <section class="contact-section">
      <h2>Get in Touch</h2>

      <div class="contact-method">
        <strong>General Inquiries:</strong>
        <a href="mailto:info@example.com">info@example.com</a>
      </div>

      <div class="contact-method">
        <strong>Sales Department:</strong>
        <a href="mailto:sales@example.com?subject=Sales Inquiry">
          sales@example.com
        </a>
      </div>

      <div class="contact-method">
        <strong>Technical Support:</strong>
        <a href="mailto:support@example.com?subject=Support Request&body=Please describe your issue:">
          support@example.com
        </a>
      </div>

      <div class="contact-method">
        <strong>Main Office:</strong>
        <a href="tel:+15551234567">+1 (555) 123-4567</a>
      </div>

      <div class="contact-method">
        <strong>Customer Service:</strong>
        <a href="tel:+15559876543">+1 (555) 987-6543</a>
      </div>

      <div class="contact-method">
        <strong>International:</strong>
        <a href="tel:+442012345678">+44 20 1234 5678</a>
        (UK Office)
      </div>
    </section>

    <section>
      <h2>Office Hours</h2>
      <p>
        <strong>Monday - Friday:</strong> 9:00 AM - 6:00 PM (EST)<br>
        <strong>Saturday:</strong> 10:00 AM - 4:00 PM (EST)<br>
        <strong>Sunday:</strong> Closed
      </p>
      <p>
        Prefer email? Send us a message at
        <a href="mailto:contact@example.com?subject=Website Inquiry">
          contact@example.com
        </a>
        and we'll respond within 24 hours.
      </p>
    </section>
  </article>
</body>
</html>
```

### Example 2: Email Link with Pre-filled Form Data
**Use Case:** Bug report submission with template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Report a Bug</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 700px;
      margin: 0 auto;
      padding: 40px 20px;
      line-height: 1.6;
    }
    .report-button {
      display: inline-block;
      padding: 1em 2em;
      background-color: #e74c3c;
      color: white;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      font-size: 1.1em;
      margin: 2em 0;
      transition: all 0.3s ease;
    }
    .report-button:hover,
    .report-button:focus {
      background-color: #c0392b;
      transform: scale(1.05);
    }
    .report-button:focus {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    code {
      background-color: #f4f4f4;
      padding: 2px 6px;
      border-radius: 3px;
      font-family: 'Courier New', monospace;
    }
  </style>
</head>
<body>
  <article>
    <h1>Report a Bug</h1>

    <p>
      Found a bug in our application? Click the button below to send us
      a detailed report. Your email client will open with a pre-filled
      template—just fill in the details and send!
    </p>

    <a href="mailto:bugs@example.com?subject=Bug%20Report%3A%20%5BApp%20Name%5D&body=**Bug%20Report**%0A%0A**Description%3A**%0APlease%20describe%20the%20bug%20in%20detail.%0A%0A**Steps%20to%20Reproduce%3A**%0A1.%20%0A2.%20%0A3.%20%0A%0A**Expected%20Behavior%3A**%0AWhat%20should%20happen%3F%0A%0A**Actual%20Behavior%3A**%0AWhat%20actually%20happened%3F%0A%0A**Browser%2FOS%3A**%0A(e.g.%2C%20Chrome%20120%20on%20Windows%2011)%0A%0A**Screenshots%3A**%0AAttach%20screenshots%20if%20applicable.%0A%0AThank%20you%20for%20helping%20us%20improve!"
       class="report-button">
      📧 Report Bug via Email
    </a>

    <section>
      <h2>What Information to Include</h2>
      <ul>
        <li><strong>Description:</strong> What is the bug?</li>
        <li><strong>Steps to Reproduce:</strong> How can we recreate it?</li>
        <li><strong>Expected Behavior:</strong> What should happen?</li>
        <li><strong>Actual Behavior:</strong> What actually happened?</li>
        <li><strong>Browser/OS:</strong> Your system information</li>
        <li><strong>Screenshots:</strong> Visual evidence (if applicable)</li>
      </ul>
    </section>

    <section>
      <h2>Prefer a Web Form?</h2>
      <p>
        If your email client doesn't open automatically, you can also submit
        bugs through our <a href="/bug-report-form.html">online form</a>.
      </p>
    </section>
  </article>
</body>
</html>
```

### Example 3: Mobile-Optimized Contact Card
**Use Case:** Business card-style contact information for mobile devices

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact - Sarah Johnson</title>
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      margin: 0;
      padding: 20px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .contact-card {
      background-color: white;
      border-radius: 16px;
      padding: 2.5em;
      max-width: 400px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    }
    .profile-image {
      width: 120px;
      height: 120px;
      border-radius: 50%;
      margin: 0 auto 1.5em;
      background-color: #3498db;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 3em;
      color: white;
    }
    h1 {
      text-align: center;
      color: #2c3e50;
      margin-bottom: 0.25em;
      font-size: 1.75em;
    }
    .title {
      text-align: center;
      color: #7f8c8d;
      margin-bottom: 2em;
      font-size: 1.1em;
    }
    .contact-links {
      display: flex;
      flex-direction: column;
      gap: 1em;
    }
    .contact-links a {
      display: flex;
      align-items: center;
      padding: 1em 1.5em;
      background-color: #ecf0f1;
      color: #2c3e50;
      text-decoration: none;
      border-radius: 8px;
      font-weight: 500;
      transition: all 0.3s ease;
      border-left: 4px solid transparent;
    }
    .contact-links a:hover,
    .contact-links a:focus {
      background-color: #3498db;
      color: white;
      border-left-color: #2980b9;
      transform: translateX(4px);
    }
    .contact-links a:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }
    .contact-links a::before {
      font-size: 1.5em;
      margin-right: 0.75em;
    }
    a[href^="tel:"]::before {
      content: "📞";
    }
    a[href^="mailto:"]::before {
      content: "✉";
    }
    a[href^="sms:"]::before {
      content: "💬";
    }
    @media (max-width: 480px) {
      .contact-card {
        padding: 2em 1.5em;
      }
    }
  </style>
</head>
<body>
  <div class="contact-card">
    <div class="profile-image" aria-hidden="true">SJ</div>
    <h1>Sarah Johnson</h1>
    <p class="title">Senior Web Developer</p>

    <div class="contact-links">
      <a href="tel:+15551234567">
        Call Mobile: (555) 123-4567
      </a>
      <a href="tel:+15559876543,,,205">
        Call Office: (555) 987-6543 ext. 205
      </a>
      <a href="mailto:sarah.johnson@example.com?subject=Hello from the web">
        Email: sarah.johnson@example.com
      </a>
      <a href="sms:+15551234567&body=Hi Sarah, ">
        Send Text Message
      </a>
    </div>

    <p style="text-align: center; margin-top: 2em; color: #95a5a6; font-size: 0.9em;">
      <small>Tap to call, email, or text instantly</small>
    </p>
  </div>
</body>
</html>
```

## Common Use Cases

### 1. Contact Pages
Provide easy one-click email and phone contact:

```html
<section>
  <h2>Contact Us</h2>
  <p>
    <strong>Email:</strong>
    <a href="mailto:contact@example.com">contact@example.com</a>
  </p>
  <p>
    <strong>Phone:</strong>
    <a href="tel:+15551234567">+1 (555) 123-4567</a>
  </p>
</section>
```

**When to use:** Business websites, portfolios, landing pages, support pages

### 2. Click-to-Call Buttons (Mobile)
Enable one-tap dialing on smartphones:

```html
<a href="tel:+15551234567" class="cta-button">
  📞 Call Now for Free Consultation
</a>
```

**When to use:** Service businesses, emergency services, sales-focused landing pages

### 3. Pre-filled Support Requests
Guide users to submit structured support emails:

```html
<a href="mailto:support@example.com?subject=Support Request&body=Account ID:%0ADescription:%0A">
  Contact Support
</a>
```

**When to use:** SaaS platforms, technical support pages, bug reporting

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| `mailto:` links | All | All | All | All | All | All |
| `mailto:` parameters (subject, body, cc) | All | All | All | All | All | All |
| `tel:` links | All | 4+ | All | All | All | All |
| `tel:` click-to-call | Desktop: Opens Skype/etc | Desktop: Prompt | Desktop: FaceTime | Desktop: App | Mobile: Native dialer | Mobile: Native dialer |
| `sms:` links | Android only | No | iOS only | No | iOS: iMessage | Android: Messages |

**Browser Support:** Universal for desktop and mobile

`mailto:` has been supported since the earliest browsers (1990s). `tel:` support is universal on mobile (iOS, Android) and works on desktop if telephony software is installed (Skype, FaceTime, etc.).

**Platform Behavior:**
- **iOS:** `tel:` opens native Phone app, `mailto:` opens Mail app
- **Android:** `tel:` opens Phone app, `mailto:` opens Gmail/default email client
- **Desktop:** `mailto:` opens configured email client (Outlook, Thunderbird, webmail), `tel:` opens Skype/FaceTime if installed
- **No configured app:** Link may do nothing or show error dialog

**Resources:**
- [MDN: mailto: links](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#e-mail_links)
- [MDN: tel: links](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#linking_to_telephone_numbers)
- [RFC 6068: mailto URI scheme](https://datatracker.ietf.org/doc/html/rfc6068)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- **Link Purpose (2.4.4):** Link text must describe what happens when activated
- **Keyboard:** All links must be keyboard-accessible (default behavior)

**Level AA Requirements:**
- **Link Purpose in Context (2.4.4):** Avoid generic "Email" or "Call" text—be specific
- **Consistent Identification (3.2.4):** Email and phone links styled consistently across site

### Best Practices for Accessibility

1. **Provide descriptive link text:**

```html
<!-- BAD: Generic, unclear -->
<a href="mailto:info@example.com">Click here</a>
<a href="tel:+15551234567">Call</a>

<!-- GOOD: Descriptive, clear action -->
<a href="mailto:info@example.com">Email us at info@example.com</a>
<a href="tel:+15551234567">Call our office at (555) 123-4567</a>
```

2. **Indicate action with icons or text:**

```html
<!-- Visual icon + descriptive text -->
<a href="mailto:support@example.com">
  <span aria-hidden="true">📧</span>
  Email support@example.com
</a>

<a href="tel:+15551234567">
  <span aria-hidden="true">📞</span>
  Call (555) 123-4567
</a>
```

3. **Provide context for screen readers:**

```html
<!-- Screen reader announces: "Email Sales Department at sales@example.com" -->
<a href="mailto:sales@example.com">
  Email Sales Department: sales@example.com
</a>
```

4. **Consider fallbacks for users without email clients:**

```html
<p>
  Contact us at
  <a href="mailto:contact@example.com">contact@example.com</a>
  or use our <a href="/contact-form.html">online contact form</a>.
</p>
```

5. **Warn about pre-filled content:**

```html
<!-- Indicate that clicking will open email with pre-filled content -->
<a href="mailto:bugs@example.com?subject=Bug%20Report&body=Template...">
  Report a bug (opens email template)
</a>
```

### Screen Reader Behavior

- Screen readers announce "link" + link text
- No special announcement for `mailto:` or `tel:` (announced as regular links)
- Pre-filled subject/body NOT announced (opens silently in email client)
- Users may be confused if link opens external application unexpectedly

**Resources:**
- [WCAG 2.1: Link Purpose (2.4.4)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
- [WebAIM: Links and Hypertext](https://webaim.org/techniques/hypertext/)

## Best Practices

### Do This ✓

1. **Use descriptive link text:**
```html
<!-- Correct -->
<a href="mailto:support@example.com">Email support@example.com</a>
<a href="tel:+15551234567">Call (555) 123-4567</a>
```

2. **Use E.164 format for telephone links:**
```html
<!-- Correct: International format -->
<a href="tel:+14155551234">+1 (415) 555-1234</a>
<a href="tel:+442071234567">+44 20 7123 4567</a>
```

3. **URL-encode special characters in mailto:**
```html
<!-- Correct: Spaces encoded as %20, newlines as %0A -->
<a href="mailto:contact@example.com?subject=Hello%20World&body=Line%201%0ALine%202">
  Send Email
</a>
```

4. **Provide fallback for desktop users:**
```html
<!-- Correct: Alternative for users without phone app -->
<p>
  Call us at <a href="tel:+15551234567">(555) 123-4567</a>
  or <a href="/contact-form.html">submit a contact form</a>.
</p>
```

5. **Style mailto: and tel: links distinctively:**
```css
a[href^="mailto:"]::before {
  content: "📧 ";
}
a[href^="tel:"]::before {
  content: "📞 ";
}
```

### Avoid This ✗

1. **Don't use generic link text:**
```html
<!-- WRONG -->
<a href="mailto:info@example.com">Click here</a>
<a href="tel:+15551234567">Call us</a>

<!-- CORRECT -->
<a href="mailto:info@example.com">Email info@example.com</a>
<a href="tel:+15551234567">Call (555) 123-4567</a>
```

2. **Don't forget URL encoding:**
```html
<!-- WRONG: Unencoded spaces and newlines break link -->
<a href="mailto:contact@example.com?subject=Hello World&body=Line 1
Line 2">Email</a>

<!-- CORRECT: URL-encoded -->
<a href="mailto:contact@example.com?subject=Hello%20World&body=Line%201%0ALine%202">
  Email
</a>
```

3. **Don't use formatting in href:**
```html
<!-- WRONG: Formatting breaks tel: link -->
<a href="tel:(555) 123-4567">Call</a>

<!-- CORRECT: Remove formatting from href -->
<a href="tel:+15551234567">(555) 123-4567</a>
```

4. **Don't assume all users have email clients:**
```html
<!-- WRONG: No alternative -->
<a href="mailto:contact@example.com">Contact Us</a>

<!-- CORRECT: Provide web form alternative -->
<p>
  <a href="mailto:contact@example.com">Email contact@example.com</a> or
  use our <a href="/contact-form.html">online form</a>.
</p>
```

5. **Don't use mailto: for large pre-filled content:**
```html
<!-- WRONG: 500+ characters in body (URL length limits) -->
<a href="mailto:support@example.com?body=[massive block of text]">Email</a>

<!-- CORRECT: Use web form instead -->
<a href="/support-form.html">Submit Support Request</a>
```

## Related Topics

### Prerequisites
- [Anchor Links](anchor-links.md) - Basic hyperlink syntax
- [Link States](link-states.md) - Styling link states

### Related Topics
- [Bookmark Links](bookmark-links.md) - Fragment identifier links
- [Download Links](download-links.md) - File download links
- [Forms](../06-forms-input/form-element.md) - Alternative to mailto: for structured data collection

### Next Steps
- [Bookmark Links](bookmark-links.md) - In-page navigation with fragments
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Accessible link design
- [Responsive Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design) - Mobile-optimized contact links

## Practice Exercise

### Requirements
Create a **"Business Contact Page"** that demonstrates proper use of email and telephone links. Your HTML document should include:

1. A contact section with:
   - At least 2 email links (one with pre-filled subject, one with subject + body)
   - At least 3 telephone links (local, toll-free, international)
   - At least one telephone link with an extension
2. A "Contact Support" section with:
   - Pre-filled bug report email template
   - URL-encoded spaces and newlines in subject/body
3. Social contact links (LinkedIn, Twitter, etc.) as regular links
4. CSS styling that:
   - Visually distinguishes email vs. phone links (icons or colors)
   - Provides hover/focus states
   - Works well on mobile devices

**Accessibility Requirements:**
- Descriptive link text (not "click here" or "email")
- Clear indication of what clicking the link does
- Provide web form alternative for users without email clients
- Use E.164 format for all telephone numbers

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Us</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
    }
    /* Add your styling here */
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
  <title>Contact - TechCorp Solutions</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      line-height: 1.7;
      background-color: #f4f4f4;
    }
    header {
      background: linear-gradient(135deg, #3498db 0%, #2c3e50 100%);
      color: white;
      padding: 3em 0;
      text-align: center;
    }
    header h1 {
      font-size: 2.5em;
      margin-bottom: 0.25em;
    }
    header p {
      font-size: 1.2em;
      opacity: 0.9;
    }
    main {
      max-width: 1000px;
      margin: -2em auto 2em;
      padding: 0 20px;
    }
    .contact-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2em;
      margin: 2em 0;
    }
    .contact-card {
      background-color: white;
      padding: 2em;
      border-radius: 12px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }
    .contact-card h2 {
      color: #2c3e50;
      margin-bottom: 1em;
      border-bottom: 2px solid #3498db;
      padding-bottom: 0.5em;
    }
    .contact-method {
      margin: 1.25em 0;
    }
    .contact-method strong {
      display: block;
      color: #34495e;
      margin-bottom: 0.5em;
    }

    /* Email Links */
    a[href^="mailto:"] {
      display: inline-flex;
      align-items: center;
      color: #0066cc;
      text-decoration: none;
      padding: 0.5em 1em;
      background-color: #e3f2fd;
      border-radius: 6px;
      transition: all 0.3s ease;
      border-left: 4px solid #2196f3;
    }
    a[href^="mailto:"]::before {
      content: "✉";
      font-size: 1.3em;
      margin-right: 0.6em;
    }
    a[href^="mailto:"]:hover,
    a[href^="mailto:"]:focus {
      background-color: #2196f3;
      color: white;
      transform: translateX(4px);
    }
    a[href^="mailto:"]:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }

    /* Telephone Links */
    a[href^="tel:"] {
      display: inline-flex;
      align-items: center;
      color: #27ae60;
      text-decoration: none;
      padding: 0.5em 1em;
      background-color: #e8f5e9;
      border-radius: 6px;
      transition: all 0.3s ease;
      border-left: 4px solid #4caf50;
    }
    a[href^="tel:"]::before {
      content: "📞";
      font-size: 1.3em;
      margin-right: 0.6em;
    }
    a[href^="tel:"]:hover,
    a[href^="tel:"]:focus {
      background-color: #4caf50;
      color: white;
      transform: translateX(4px);
    }
    a[href^="tel:"]:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }

    /* Support Section */
    .support-section {
      background-color: #fff3cd;
      border-left: 5px solid #ffc107;
      padding: 2em;
      border-radius: 8px;
      margin: 2em 0;
    }
    .support-section h2 {
      color: #856404;
      margin-bottom: 1em;
    }
    .report-button {
      display: inline-block;
      padding: 1em 2em;
      background-color: #e74c3c;
      color: white;
      text-decoration: none;
      border-radius: 8px;
      font-weight: bold;
      font-size: 1.1em;
      margin: 1em 0;
      transition: all 0.3s ease;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .report-button:hover,
    .report-button:focus {
      background-color: #c0392b;
      transform: translateY(-2px);
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }
    .report-button:focus {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }

    /* Social Links */
    .social-links {
      display: flex;
      gap: 1em;
      margin-top: 1.5em;
    }
    .social-links a {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 50px;
      height: 50px;
      background-color: #95a5a6;
      color: white;
      border-radius: 50%;
      text-decoration: none;
      font-weight: bold;
      transition: all 0.3s ease;
    }
    .social-links a:hover,
    .social-links a:focus {
      transform: scale(1.15);
    }
    .social-links a:focus {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .social-links a[href*="linkedin"] {
      background-color: #0077b5;
    }
    .social-links a[href*="twitter"] {
      background-color: #1da1f2;
    }
    .social-links a[href*="facebook"] {
      background-color: #1877f2;
    }

    @media (max-width: 768px) {
      .contact-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Contact TechCorp Solutions</h1>
    <p>We're here to help—reach out anytime!</p>
  </header>

  <main>
    <div class="contact-grid">
      <!-- General Contact -->
      <div class="contact-card">
        <h2>General Inquiries</h2>

        <div class="contact-method">
          <strong>Email:</strong>
          <a href="mailto:info@techcorp.com?subject=General Inquiry">
            info@techcorp.com
          </a>
        </div>

        <div class="contact-method">
          <strong>Main Office:</strong>
          <a href="tel:+15551234567">
            +1 (555) 123-4567
          </a>
        </div>

        <div class="contact-method">
          <strong>Toll-Free:</strong>
          <a href="tel:+18005551234">
            1-800-555-1234
          </a>
        </div>
      </div>

      <!-- Sales & Support -->
      <div class="contact-card">
        <h2>Sales & Support</h2>

        <div class="contact-method">
          <strong>Sales Team:</strong>
          <a href="mailto:sales@techcorp.com?subject=Sales%20Inquiry%3A%20Product%20Demo&body=Hello%20Sales%20Team%2C%0A%0AI%27m%20interested%20in%20learning%20more%20about%20your%20products.%0A%0ACompany%20Name%3A%0AIndustry%3A%0ANumber%20of%20Employees%3A%0A%0AThank%20you!">
            sales@techcorp.com
          </a>
        </div>

        <div class="contact-method">
          <strong>Sales Hotline:</strong>
          <a href="tel:+15559876543">
            +1 (555) 987-6543
          </a>
        </div>

        <div class="contact-method">
          <strong>Customer Support:</strong>
          <a href="mailto:support@techcorp.com?subject=Support%20Request">
            support@techcorp.com
          </a>
        </div>

        <div class="contact-method">
          <strong>Support Line:</strong>
          <a href="tel:+15554445555,,,123">
            +1 (555) 444-5555 ext. 123
          </a>
        </div>
      </div>

      <!-- International Offices -->
      <div class="contact-card">
        <h2>International Offices</h2>

        <div class="contact-method">
          <strong>UK Office:</strong>
          <a href="tel:+442071234567">
            +44 20 7123 4567
          </a>
        </div>

        <div class="contact-method">
          <strong>Australia Office:</strong>
          <a href="tel:+61298765432">
            +61 2 9876 5432
          </a>
        </div>

        <div class="contact-method">
          <strong>Singapore Office:</strong>
          <a href="tel:+6567891234">
            +65 6789 1234
          </a>
        </div>

        <div class="contact-method">
          <strong>International Email:</strong>
          <a href="mailto:global@techcorp.com">
            global@techcorp.com
          </a>
        </div>
      </div>
    </div>

    <!-- Support Section -->
    <section class="support-section">
      <h2>Need Technical Support?</h2>
      <p>
        Experiencing a bug or technical issue? Click the button below to
        send us a detailed report. Your email client will open with a
        pre-filled template—just fill in the details!
      </p>

      <a href="mailto:bugs@techcorp.com?subject=Bug%20Report%3A%20%5BApp%20Name%5D&body=%2A%2ABug%20Report%2A%2A%0A%0A%2A%2ADescription%3A%2A%2A%0APlease%20describe%20the%20bug.%0A%0A%2A%2ASteps%20to%20Reproduce%3A%2A%2A%0A1.%20Step%20one%0A2.%20Step%20two%0A3.%20Step%20three%0A%0A%2A%2AExpected%20Behavior%3A%2A%2A%0AWhat%20should%20happen%3F%0A%0A%2A%2AActual%20Behavior%3A%2A%2A%0AWhat%20actually%20happened%3F%0A%0A%2A%2ABrowser%2FOS%3A%2A%2A%0A(e.g.%2C%20Chrome%20120%20on%20Windows%2011)%0A%0A%2A%2AScreenshots%3A%2A%2A%0AAttach%20screenshots%20if%20applicable.%0A%0AThank%20you!"
         class="report-button">
        📧 Report a Bug (Email Template)
      </a>

      <p>
        <small>
          Prefer a web form?
          <a href="/bug-report-form.html">Submit via online form</a> instead.
        </small>
      </p>
    </section>

    <!-- Social Media -->
    <section class="contact-card">
      <h2>Connect on Social Media</h2>
      <p>
        Follow us for product updates, industry news, and company announcements:
      </p>

      <div class="social-links">
        <a href="https://linkedin.com/company/techcorp"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Visit our LinkedIn page (opens in new tab)">
          <span aria-hidden="true">in</span>
        </a>
        <a href="https://twitter.com/techcorp"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Follow us on Twitter (opens in new tab)">
          <span aria-hidden="true">𝕏</span>
        </a>
        <a href="https://facebook.com/techcorp"
           target="_blank"
           rel="noopener noreferrer"
           aria-label="Like us on Facebook (opens in new tab)">
          <span aria-hidden="true">f</span>
        </a>
      </div>
    </section>

    <!-- Office Hours -->
    <section class="contact-card">
      <h2>Office Hours</h2>
      <p>
        <strong>Monday - Friday:</strong> 9:00 AM - 6:00 PM (EST)<br>
        <strong>Saturday:</strong> 10:00 AM - 4:00 PM (EST)<br>
        <strong>Sunday:</strong> Closed
      </p>
      <p>
        <strong>Emergency Support:</strong> 24/7 for enterprise customers<br>
        Email <a href="mailto:emergency@techcorp.com?subject=Emergency%20Support">emergency@techcorp.com</a>
        or call <a href="tel:+18005559999">1-800-555-9999</a>
      </p>
    </section>
  </main>
</body>
</html>
```

**Key Features of Solution:**
- 10+ email links (general, sales, support, bugs, international)
- 8+ telephone links (local, toll-free, international, with extension)
- Pre-filled email templates with URL-encoded spaces (`%20`), newlines (`%0A`), special chars
- Bug report template with structured fields (description, steps, expected/actual behavior)
- E.164 international format for all phone numbers (`+[country][area][number]`)
- Extension syntax using commas for pause (`,,,123`)
- Descriptive link text (not "click here")
- Visual distinction via icons and colors (email = blue, phone = green)
- Hover and focus states with smooth transitions
- Social media links with `aria-label` for accessibility
- Web form alternative mentioned for users without email clients
- Mobile-responsive grid layout
- WCAG AA compliant focus indicators (3px gold outlines)
- Styled consistently across entire page

---

## Navigation

- **Previous:** [Link States](link-states.md)
- **Next:** [Bookmark Links](bookmark-links.md)
- **Up:** [Links and Navigation](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Links and Navigation
- **Difficulty:** Beginner to Intermediate
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
