---
title: Accessibility Overview
category: Accessibility
order: 1
---

# Accessibility Overview

> **Quick Summary:** Web accessibility ensures websites are usable by everyone, including people with disabilities. Following WCAG 2.1 guidelines is both a legal requirement and ethical responsibility.

## Table of Contents
- [Introduction](#introduction)
- [WCAG 2.1 Principles](#wcag-21-principles)
- [Why Accessibility Matters](#why-accessibility-matters)
- [Common Disabilities](#common-disabilities)
- [Accessibility Standards](#accessibility-standards)
- [Testing Tools](#testing-tools)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

Web accessibility means designing websites that can be perceived, understood, navigated, and interacted with by all people, regardless of disability. This includes visual, auditory, motor, cognitive, and neurological disabilities.

**The Problem:** 15% of the world's population (1+ billion people) live with some form of disability. Inaccessible websites exclude these users and violate laws like ADA (USA), EAA (EU), and AODA (Canada).

**The Solution:** Follow WCAG 2.1 (Web Content Accessibility Guidelines) standards, use semantic HTML, provide alternatives for non-text content, and ensure keyboard navigation.

**Key Concept:** Accessibility benefits everyone - not just people with disabilities. Captions help in noisy environments, keyboard navigation speeds up power users, and clear structure improves SEO.

---

## WCAG 2.1 Principles

WCAG is organized around **four principles (POUR)**:

### 1. Perceivable
Information must be presentable to users in ways they can perceive.

**Requirements:**
- Text alternatives for non-text content (alt text for images)
- Captions and transcripts for audio/video
- Content adaptable to different presentations (screen readers, zoom)
- Sufficient color contrast (4.5:1 for normal text, 3:1 for large text)

**Example:**
```html
<!-- ✅ GOOD - Image with descriptive alt text -->
<img src="chart.png" alt="Sales increased 35% from Q1 to Q2 2024">

<!-- ❌ BAD - Missing alt text -->
<img src="chart.png">
```

### 2. Operable
User interface components must be operable.

**Requirements:**
- All functionality available via keyboard
- Users have enough time to read and use content
- No content causes seizures (avoid flashing more than 3 times/second)
- Easy navigation and orientation (skip links, headings, breadcrumbs)

**Example:**
```html
<!-- ✅ GOOD - Keyboard accessible custom button -->
<div role="button" tabindex="0"
     onkeydown="if(event.key==='Enter'||event.key===' ')handleClick()"
     onclick="handleClick()">
  Submit
</div>

<!-- ❌ BAD - Not keyboard accessible -->
<div onclick="handleClick()">Submit</div>
```

### 3. Understandable
Information and operation of the user interface must be understandable.

**Requirements:**
- Text is readable and understandable
- Pages appear and operate in predictable ways
- Users are helped to avoid and correct mistakes

**Example:**
```html
<!-- ✅ GOOD - Clear error messages -->
<label for="email">Email:</label>
<input type="email" id="email" required aria-describedby="email-error">
<span id="email-error" role="alert">Please enter a valid email address</span>

<!-- ❌ BAD - Vague error -->
<input type="email">
<span>Invalid</span>
```

### 4. Robust
Content must be robust enough to be interpreted by a wide variety of user agents, including assistive technologies.

**Requirements:**
- Valid HTML (passes W3C validation)
- Compatible with current and future assistive technologies
- Proper use of ARIA attributes

---

## Why Accessibility Matters

### Legal Requirements

| Region | Law | Requirements |
|--------|-----|--------------|
| USA | ADA (Americans with Disabilities Act) | Public websites must be accessible |
| EU | European Accessibility Act (EAA) | All public sector websites WCAG 2.1 AA compliant |
| Canada | AODA (Accessibility for Ontarians with Disabilities Act) | WCAG 2.0 AA minimum |
| UK | Equality Act 2010 | Reasonable accessibility accommodations |

**Penalties:** Lawsuits, fines up to $75,000 (first offense), loss of government contracts.

### Business Benefits

1. **Larger Audience:** 15% more potential users
2. **Better SEO:** Semantic HTML and alt text improve search rankings
3. **Improved UX:** Clear structure benefits all users
4. **Brand Reputation:** Shows social responsibility
5. **Legal Protection:** Avoid costly lawsuits

### Ethical Responsibility

>"The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect." - Tim Berners-Lee, W3C Director

---

## Common Disabilities

### Visual Disabilities
- **Blindness:** Use screen readers (JAWS, NVDA, VoiceOver)
- **Low vision:** Use screen magnifiers, high contrast
- **Color blindness:** Affects 8% of men, 0.5% of women

**Solutions:**
- Alt text for images
- Sufficient color contrast
- Don't rely on color alone
- Text resizable to 200% without loss of functionality

### Auditory Disabilities
- **Deafness:** Cannot hear audio content
- **Hard of hearing:** May miss some audio

**Solutions:**
- Captions for videos (synchronized text)
- Transcripts for podcasts
- Visual alerts instead of audio-only

### Motor Disabilities
- **Limited hand use:** Difficulty using mouse
- **Tremors:** Hard to click small targets
- **Paralysis:** Keyboard or voice control only

**Solutions:**
- Keyboard navigation (Tab, Enter, Space, Arrow keys)
- Large click targets (min 44x44 pixels)
- No time-based actions (or provide extensions)

### Cognitive Disabilities
- **Dyslexia:** Difficulty reading
- **ADHD:** Easily distracted
- **Autism:** Sensory sensitivities

**Solutions:**
- Simple, clear language
- Consistent layouts
- Avoid auto-playing videos/animations
- Provide options to pause/stop motion

---

## Accessibility Standards

### WCAG 2.1 Conformance Levels

| Level | Description | Required For |
|-------|-------------|--------------|
| **A** | Basic accessibility | Minimum legal requirement |
| **AA** | Addresses major barriers | Most legal standards (ADA, EAA) |
| **AAA** | Highest accessibility | Specialized sites (government, healthcare) |

**Target:** Aim for **WCAG 2.1 Level AA** as industry standard.

### Key Success Criteria (AA)

- **1.4.3:** Contrast ratio 4.5:1 (text), 3:1 (large text)
- **2.4.6:** Descriptive headings and labels
- **3.2.3:** Consistent navigation
- **3.3.3:** Error suggestions provided
- **4.1.2:** Name, role, value available to assistive tech

---

## Testing Tools

### Automated Testing

| Tool | Purpose | Cost |
|------|---------|------|
| **axe DevTools** | Browser extension, detects 57% of issues | Free |
| **WAVE** | Visual feedback on accessibility | Free |
| **Lighthouse** | Chrome built-in auditing tool | Free |
| **Pa11y** | Command-line testing | Free |

**Note:** Automated tools catch only ~30-50% of issues. Manual testing required.

### Manual Testing

1. **Keyboard Navigation**
   - Tab through page
   - Ensure all interactive elements reachable
   - Visible focus indicators

2. **Screen Reader Testing**
   - **Windows:** NVDA (free), JAWS (commercial)
   - **Mac:** VoiceOver (built-in)
   - **Mobile:** TalkBack (Android), VoiceOver (iOS)

3. **Color Contrast**
   - Use contrast checker tools
   - Test with color blindness simulators

4. **Browser Zoom**
   - Zoom to 200%
   - Ensure no content loss or horizontal scrolling

---

## Best Practices

### 1. Use Semantic HTML

```html
<!-- ✅ GOOD - Semantic -->
<nav>
  <ul>
    <li><a href="/">Home</a></li>
  </ul>
</nav>

<main>
  <article>
    <h1>Article Title</h1>
    <p>Content...</p>
  </article>
</main>

<!-- ❌ BAD - Divs only -->
<div class="nav">
  <div class="link">Home</div>
</div>
```

### 2. Provide Text Alternatives

```html
<img src="logo.png" alt="Company Name">
<video controls>
  <source src="video.mp4">
  <track kind="captions" src="captions.vtt">
</video>
```

### 3. Ensure Keyboard Accessibility

```html
<button onclick="submit()">Submit</button> <!-- ✅ Natively keyboard accessible -->
<div onclick="submit()">Submit</div> <!-- ❌ Not keyboard accessible -->
```

### 4. Use ARIA When Needed

```html
<div role="button" tabindex="0" aria-label="Close dialog">×</div>
<div aria-live="polite" aria-atomic="true">Loading...</div>
```

### 5. Test with Real Users

- Hire accessibility testers with disabilities
- Conduct usability testing
- Gather feedback continuously

---

## Related Topics

- [ARIA Roles](aria-roles.md)
- [ARIA States and Properties](aria-states.md)
- [Keyboard Navigation](keyboard-navigation.md)
- [Screen Readers](screen-readers.md)
- [Alt Text Best Practices](alt-text.md)

**External Resources:**
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [WebAIM](https://webaim.org/)
- [A11y Project](https://www.a11yproject.com/)

---

## Navigation

**Previous:** [Third-Party Widgets](../12-multimedia-embedding/third-party-widgets.md)
**Next:** [ARIA Roles](aria-roles.md)
**Up:** [Back to Accessibility](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
