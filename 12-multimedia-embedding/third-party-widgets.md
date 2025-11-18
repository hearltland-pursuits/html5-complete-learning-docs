---
title: Third-Party Widgets
category: Multimedia Embedding
order: 6
---

# Third-Party Widgets

> **Quick Summary:** Integrate third-party services like Google Maps, Calendly schedulers, CodePen demos, Disqus comments, and analytics dashboards into your website using embed codes and APIs.

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

Third-party widgets add functionality to websites without building features from scratch—maps, payment processors, chat widgets, calendars, and more.

**The Problem:** Building maps, payment systems, or chat from scratch takes months. Maintaining them requires ongoing updates and security patches.

**The Solution:** Use trusted third-party widgets via embed codes or APIs. They handle complexity, updates, and compliance.

**Key Concept:** Widgets load external JavaScript which can affect performance and privacy. Use lazy loading and understand data collection implications.

---

## Basic Syntax

### Google Maps Embed

```html
<iframe
  src="https://www.google.com/maps/embed?pb=!1m18!1m12!..."
  width="600"
  height="450"
  style="border:0;"
  allowfullscreen=""
  loading="lazy"
  referrerpolicy="no-referrer-when-downgrade">
</iframe>
```

### Calendly Scheduling Widget

```html
<!-- Calendly inline widget -->
<div class="calendly-inline-widget" data-url="https://calendly.com/your-link" style="min-width:320px;height:630px;"></div>
<script type="text/javascript" src="https://assets.calendly.com/assets/external/widget.js" async></script>
```

### CodePen Embed

```html
<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="EXAMPLE" data-user="username">
  <span>See the Pen</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>
```

### Stripe Payment Button

```html
<script async src="https://js.stripe.com/v3/buy-button.js"></script>
<stripe-buy-button
  buy-button-id="buy_btn_XXXXX"
  publishable-key="pk_live_XXXXX">
</stripe-buy-button>
```

### Disqus Comments

```html
<div id="disqus_thread"></div>
<script>
var disqus_config = function () {
  this.page.url = 'https://yoursite.com/page';
  this.page.identifier = 'page-id';
};
(function() {
  var d = document, s = d.createElement('script');
  s.src = 'https://YOUR-SITE.disqus.com/embed.js';
  s.setAttribute('data-timestamp', +new Date());
  (d.head || d.body).appendChild(s);
})();
</script>
```

---

## Examples

### Example 1: Google Maps with Lazy Loading

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact Us</title>
  <style>
    .map-container {
      position: relative;
      width: 100%;
      max-width: 800px;
      height: 450px;
      margin: 20px auto;
      background: #f0f0f0;
    }
    .map-container iframe {
      width: 100%;
      height: 100%;
      border: 0;
    }
    .map-placeholder {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;
      background: url('map-screenshot.jpg') center/cover;
      cursor: pointer;
    }
    .map-placeholder button {
      padding: 15px 30px;
      font-size: 16px;
      background: #2196F3;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Visit Our Office</h1>

  <div class="map-container">
    <div class="map-placeholder" id="mapPlaceholder">
      <button onclick="loadMap()">📍 Load Interactive Map</button>
    </div>
  </div>

  <script>
    function loadMap() {
      const placeholder = document.getElementById('mapPlaceholder');
      placeholder.innerHTML = `
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3153.1234567890!2d-122.4194!3d37.7749!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMzfCsDQ2JzI5LjYiTiAxMjLCsDI1JzA5LjgiVw!5e0!3m2!1sen!2sus!4v1234567890"
          allowfullscreen=""
          loading="lazy">
        </iframe>
      `;
    }
  </script>
</body>
</html>
```

**Result:** Map loads only when user clicks button, saving bandwidth.

---

### Example 2: Multi-Widget Dashboard

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Service Dashboard</title>
  <style>
    .widget-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 20px;
      padding: 20px;
    }
    .widget {
      background: white;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    .widget h2 {
      margin-top: 0;
      color: #333;
    }
  </style>
</head>
<body>
  <h1>Customer Portal</h1>

  <div class="widget-grid">
    <!-- Calendly Widget -->
    <div class="widget">
      <h2>Schedule a Meeting</h2>
      <div class="calendly-inline-widget"
           data-url="https://calendly.com/your-link"
           style="min-width:280px;height:400px;">
      </div>
      <script type="text/javascript" src="https://assets.calendly.com/assets/external/widget.js" async></script>
    </div>

    <!-- Location Widget -->
    <div class="widget">
      <h2>Our Location</h2>
      <iframe
        src="https://www.google.com/maps/embed?pb=..."
        width="100%"
        height="400"
        style="border:0;"
        loading="lazy">
      </iframe>
    </div>

    <!-- Contact Form Widget (Typeform) -->
    <div class="widget">
      <h2>Quick Contact</h2>
      <div data-tf-widget="YOUR_FORM_ID" data-tf-iframe-props="title=Contact Form" style="width:100%;height:400px;"></div>
      <script src="//embed.typeform.com/next/embed.js"></script>
    </div>
  </div>
</body>
</html>
```

---

### Example 3: Code Embedding (CodePen, JSFiddle, GitHub Gist)

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Code Examples</title>
</head>
<body>
  <h1>Interactive Code Examples</h1>

  <!-- CodePen Embed -->
  <h2>CSS Grid Example</h2>
  <p class="codepen" data-height="400" data-default-tab="css,result" data-slug-hash="EXAMPLE" data-user="username">
    <span>See the Pen <a href="https://codepen.io/username/pen/EXAMPLE">CSS Grid</a></span>
  </p>
  <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

  <!-- GitHub Gist -->
  <h2>Code Snippet</h2>
  <script src="https://gist.github.com/username/GIST_ID.js"></script>

  <!-- JSFiddle Embed -->
  <h2>JavaScript Demo</h2>
  <iframe width="100%" height="300" src="//jsfiddle.net/username/EXAMPLE/embedded/js,html,result/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>
</body>
</html>
```

---

## Common Use Cases

### Use Case 1: Business Websites
**Widgets:** Google Maps, Calendly, Live chat (Intercom, Drift)
**Why:** Essential for customer engagement

### Use Case 2: E-commerce
**Widgets:** Stripe payments, reviews (Trustpilot), shipping calculators
**Why:** Conversion optimization

### Use Case 3: Developer Blogs
**Widgets:** CodePen, GitHub Gists, Disqus comments
**Why:** Interactive code examples and community engagement

---

## Browser Support

All modern browsers support iframe-based widgets. JavaScript widgets require JS enabled.

---

## Accessibility Considerations

### WCAG Requirements

1. **Provide Alternatives**
   ```html
   <iframe src="https://calendly.com/...">
     <p>Unable to load scheduling widget.
       <a href="https://calendly.com/your-link">Schedule via Calendly</a>
       or email us at contact@example.com.</p>
   </iframe>
   ```

2. **Descriptive Titles**
   ```html
   <iframe src="map-widget" title="Interactive map showing office location"></iframe>
   ```

3. **Keyboard Accessibility**
   - Ensure widgets are keyboard navigable
   - Test with Tab key
   - Provide skip links for complex widgets

---

## Best Practices

### Do This

1. **Lazy Load Widgets**
   ```html
   <iframe src="widget-url" loading="lazy"></iframe>
   ```
   **Why:** Improves initial page load performance.

2. **Use Privacy-Friendly Options**
   ```html
   <!-- Google Maps with privacy mode -->
   <iframe src="...&privacy=1"></iframe>
   ```

3. **Set Dimensions**
   ```html
   <iframe src="..." width="600" height="400"></iframe>
   ```
   **Why:** Prevents layout shifts (CLS).

4. **Monitor Third-Party Performance**
   ```javascript
   // Use Performance API to track widget load times
   window.addEventListener('load', () => {
     const entries = performance.getEntriesByType('resource');
     entries.forEach(entry => {
       if (entry.name.includes('third-party-domain.com')) {
         console.log(`Widget loaded in ${entry.duration}ms`);
       }
     });
   });
   ```

---

### Avoid This

1. **Don't Load Too Many Widgets**
   ```html
   <!-- ❌ WRONG - 10 different widgets -->
   ```
   **Instead:** Limit to 2-3 essential widgets per page.

2. **Don't Trust All Widgets**
   ```html
   <!-- ❌ WRONG - Unknown/sketchy widget -->
   <script src="https://suspicious-site.com/widget.js"></script>
   ```
   **Instead:** Only use trusted, reputable services.

3. **Don't Block Page Render**
   ```html
   <!-- ❌ WRONG - Synchronous script in <head> -->
   <script src="widget.js"></script>

   <!-- ✅ CORRECT - Async loading -->
   <script async src="widget.js"></script>
   ```

---

## Related Topics

- [YouTube Embedding](youtube-embedding.md)
- [Social Media Embeds](social-media-embeds.md)
- [IFrame Element](../05-semantic-html5/iframe.md)

**External Resources:**
- [Google Maps Embed API](https://developers.google.com/maps/documentation/embed)
- [Calendly Embed Options](https://help.calendly.com/hc/en-us/articles/223147027-Embed-options-overview)
- [Stripe Elements](https://stripe.com/docs/payments/elements)

---

## Practice Exercise

### Challenge: Build a Service Landing Page

**Requirements:**
- [ ] Embed Google Maps showing business location
- [ ] Add Calendly booking widget
- [ ] Include contact form (Typeform or Google Forms)
- [ ] Lazy load all widgets

---

## Navigation

**Previous:** [PDF Embedding](pdf-embedding.md)
**Next:** [Accessibility Overview](../13-accessibility/accessibility-overview.md)
**Up:** [Back to Multimedia Embedding](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** Multimedia Embedding
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
