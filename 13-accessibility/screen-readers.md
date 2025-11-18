---
title: Screen Reader Compatibility
category: Accessibility
order: 6
---

# Screen Reader Compatibility

> **Quick Summary:** Screen readers convert web content to speech or braille. Proper HTML structure, alt text, ARIA labels, and semantic markup ensure screen reader users can navigate effectively.

## Popular Screen Readers

| Screen Reader | Platform | Cost | Market Share |
|---------------|----------|------|--------------|
| **JAWS** | Windows | $90-1,200/year | ~40% |
| **NVDA** | Windows | Free | ~30% |
| **VoiceOver** | macOS/iOS | Built-in | ~10-15% |
| **TalkBack** | Android | Built-in | ~5-10% |
| **Narrator** | Windows | Built-in | ~3% |

---

## How Screen Readers Work

1. **Parse HTML** - Read DOM structure
2. **Build Accessibility Tree** - Map elements to roles
3. **Announce Content** - Convert to speech/braille
4. **Navigate** - Headings, landmarks, links, forms

**Example Announcement:**
```html
<button aria-label="Close dialog">×</button>
```
**Screen reader says:** "Close dialog, button"

---

## Screen Reader Navigation

### By Headings
```html
<h1>Main Title</h1>
<h2>Section 1</h2>
<h3>Subsection 1.1</h3>
```
**User presses:** `H` key → Jumps between headings

### By Landmarks
```html
<nav aria-label="Main">...</nav>
<main>...</main>
<footer>...</footer>
```
**User presses:** `D` key (NVDA/JAWS) → Jumps between landmarks

### By Links
```html
<a href="/about">About Us</a>
```
**User presses:** `K` key → Jumps between links

---

## Visually Hidden Text

For screen readers only (not visible on screen):

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}
```

```html
<button>
  <span aria-hidden="true">×</span>
  <span class="sr-only">Close</span>
</button>
```

---

## Testing with Screen Readers

### Windows (NVDA - Free)

1. Download from [nvaccess.org](https://www.nvaccess.org/)
2. **Start:** `Ctrl + Alt + N`
3. **Navigate:** Arrow keys, `H` (headings), `K` (links)
4. **Stop reading:** `Ctrl`

### macOS (VoiceOver - Built-in)

1. **Enable:** System Preferences → Accessibility → VoiceOver
2. **Start:** `Cmd + F5`
3. **Navigate:** `Ctrl + Option + Arrow keys`
4. **Web Rotor:** `Ctrl + Option + U` (browse headings/links)

---

## Best Practices

### 1. Meaningful Alt Text

```html
<!-- ✅ GOOD -->
<img src="chart.png" alt="Revenue increased 40% from Q1 to Q2">

<!-- ❌ BAD -->
<img src="chart.png" alt="chart">
```

### 2. Descriptive Links

```html
<!-- ✅ GOOD -->
<a href="report.pdf">Download 2024 Annual Report (PDF, 2.1MB)</a>

<!-- ❌ BAD -->
<a href="report.pdf">Click here</a>
```

### 3. Form Labels

```html
<!-- ✅ GOOD -->
<label for="email">Email Address:</label>
<input type="email" id="email">

<!-- ❌ BAD - No label -->
<input type="email" placeholder="Email">
```

### 4. Live Regions for Dynamic Content

```html
<div aria-live="polite" role="status">
  5 items in cart
</div>
```

---

## Common Announcements

| HTML | Screen Reader Says |
|------|-------------------|
| `<button>Submit</button>` | "Submit, button" |
| `<a href="/">Home</a>` | "Home, link" |
| `<h1>Title</h1>` | "Heading level 1, Title" |
| `<img alt="Logo">` | "Logo, image" |
| `<nav aria-label="Main">` | "Main, navigation landmark" |

---

## Related Topics

- [Alt Text](alt-text.md)
- [ARIA Labels](aria-states.md)
- [Keyboard Navigation](keyboard-navigation.md)

---

**Last Updated:** November 18, 2025
**Category:** Accessibility
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
