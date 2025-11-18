---
title: Writing Effective Alt Text
category: Accessibility
order: 7
---

# Writing Effective Alt Text

> **Quick Summary:** Alt text describes images for screen reader users and displays when images fail to load. Effective alt text is concise, descriptive, and contextual.

## Why Alt Text Matters

- **Accessibility:** Blind users rely on alt text to understand images
- **SEO:** Search engines index alt text
- **Fallback:** Shows when images fail to load
- **Legal:** WCAG 2.1 Level A requirement

---

## Alt Text Formula

```
Alt text = Purpose + Content (in context)
```

### Examples

```html
<!-- ✅ GOOD - Describes content and purpose -->
<img src="chart.png" alt="Bar chart showing 40% revenue increase Q1 to Q2 2024">

<!-- ❌ BAD - Too vague -->
<img src="chart.png" alt="chart">

<!-- ❌ BAD - Redundant -->
<img src="chart.png" alt="Image of a chart showing revenue">
```

---

## When to Use Alt Text

### Informative Images

```html
<img src="product.jpg" alt="Red leather backpack with laptop compartment">
```

### Functional Images (Links, Buttons)

```html
<!-- Image link -->
<a href="/search">
  <img src="search-icon.png" alt="Search">
</a>

<!-- Image button -->
<button>
  <img src="download.png" alt="Download report">
</button>
```

### Complex Images (Charts, Diagrams)

```html
<figure>
  <img src="org-chart.png" alt="Company organizational chart">
  <figcaption>
    CEO reports to Board. VP of Sales, VP of Engineering, and CFO report to CEO.
    Sales team (5 members) reports to VP of Sales.
  </figcaption>
</figure>
```

---

## When to Use Empty Alt

### Decorative Images

```html
<!-- Decorative icon next to text -->
<img src="star.png" alt="">
<span>Premium Member</span>

<!-- Decorative border -->
<img src="divider.png" alt="" role="presentation">
```

**Rule:** If removing the image doesn't change the meaning, use `alt=""`.

### Images Described by Nearby Text

```html
<h2>Annual Report 2024</h2>
<img src="report-cover.jpg" alt="">
<!-- Alt is empty because heading already provides context -->
```

---

## Alt Text Best Practices

### 1. Be Concise (< 125 characters)

```html
<!-- ✅ GOOD -->
<img alt="Golden retriever puppy playing with tennis ball in grass">

<!-- ❌ TOO LONG -->
<img alt="An adorable golden retriever puppy, approximately 8 weeks old, with fluffy golden fur, playfully chasing and biting a yellow tennis ball in a lush green grassy field on a sunny summer afternoon">
```

**Why:** Screen readers pause after ~125 characters.

### 2. Don't Say "Image of" or "Picture of"

```html
<!-- ✅ GOOD -->
<img alt="Sunset over ocean">

<!-- ❌ REDUNDANT -->
<img alt="Image of a sunset over the ocean">
```

**Why:** Screen readers already announce "image."

### 3. Include Context

```html
<!-- Context: News article about election -->
<img src="candidate.jpg" alt="Presidential candidate Jane Doe waving at campaign rally">

<!-- Context: Online store -->
<img src="candidate.jpg" alt="Jane Doe promotional poster, 24x36 inches">
```

**Same image, different alt text based on context.**

### 4. Transcribe Text in Images

```html
<!-- Logo with text -->
<img src="logo.png" alt="Acme Corp">

<!-- Infographic -->
<img src="tips.png" alt="5 Tips for Better Sleep: 1. Maintain consistent schedule 2. Avoid screens before bed 3. Keep room cool 4. Exercise regularly 5. Limit caffeine">
```

---

## Special Cases

### Logos

```html
<!-- ✅ Simple -->
<img src="logo.png" alt="Company Name">

<!-- ✅ As link -->
<a href="/">
  <img src="logo.png" alt="Company Name Home">
</a>
```

### Icons

```html
<!-- Icon with text (decorative) -->
<button>
  <img src="save.png" alt="">
  Save
</button>

<!-- Icon alone (functional) -->
<button>
  <img src="save.png" alt="Save">
</button>
```

### Photographs of Text

```html
<img src="sign.jpg" alt="Sign reading: 'Employees must wash hands before returning to work'">
```

### Math Formulas

```html
<img src="equation.png" alt="E equals m c squared">

<!-- Better: Use MathML -->
<math>
  <mi>E</mi><mo>=</mo><mi>m</mi><msup><mi>c</mi><mn>2</mn></msup>
</math>
```

---

## Testing Alt Text

### Ask Yourself:

1. **If I couldn't see the image, would alt text convey the same information?**
2. **Does it describe the purpose, not just appearance?**
3. **Is it concise?**
4. **Does it fit the context?**

### Testing Tools:

- **WAVE:** Highlights missing/empty alt text
- **axe DevTools:** Checks alt text presence
- **Screen Reader:** Actually listen to how it's announced

---

## Common Mistakes

### 1. Missing Alt Attribute

```html
<!-- ❌ WRONG - No alt -->
<img src="photo.jpg">

<!-- ✅ CORRECT - Even if empty -->
<img src="decorative.jpg" alt="">
```

### 2. Filename as Alt Text

```html
<!-- ❌ BAD -->
<img src="IMG_2847.jpg" alt="IMG_2847">

<!-- ✅ GOOD -->
<img src="IMG_2847.jpg" alt="Team celebrating product launch">
```

### 3. Same Alt for Multiple Images

```html
<!-- ❌ BAD -->
<img src="product1.jpg" alt="Product">
<img src="product2.jpg" alt="Product">

<!-- ✅ GOOD -->
<img src="product1.jpg" alt="Wireless mouse, black">
<img src="product2.jpg" alt="Wireless keyboard, silver">
```

---

## Related Topics

- [Images](../04-media-elements/images.md)
- [Screen Readers](screen-readers.md)
- [Accessibility Overview](accessibility-overview.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
