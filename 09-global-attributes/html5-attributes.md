---
title: HTML5 Global Attributes
category: Global Attributes
order: 21
---

# HTML5 Global Attributes

> **Quick Summary:** HTML5 introduced new global attributes like `contenteditable`, `draggable`, `hidden`, `spellcheck`, and `translate`. These enhance interactivity, accessibility, and user experience without requiring JavaScript for basic functionality.

## Table of Contents
- [Introduction](#introduction)
- [Contenteditable](#contenteditable)
- [Draggable](#draggable)
- [Hidden](#hidden)
- [Spellcheck](#spellcheck)
- [Translate](#translate)
- [Tabindex](#tabindex)
- [Accesskey](#accesskey)
- [Examples](#examples)
- [Quick Reference](#quick-reference)
- [Related Topics](#related-topics)

---

## Introduction

HTML5 added several global attributes that work on all HTML elements. These attributes provide enhanced functionality for user interaction, accessibility, and content management.

**HTML5 Global Attributes:**
- `contenteditable` - Make elements editable
- `draggable` - Enable drag-and-drop
- `hidden` - Hide elements
- `spellcheck` - Enable/disable spell-checking
- `translate` - Control translation behavior
- `tabindex` - Control tab order
- `accesskey` - Keyboard shortcuts

**Key Concept:** HTML5 global attributes add interactive capabilities directly in HTML, reducing the need for complex JavaScript for common tasks like making text editable or hiding elements.

---

## Contenteditable

### Syntax

```html
<element contenteditable="true|false">Content</element>
```

### Description

Makes element content editable by users. Creates inline editing experience without `<textarea>` or `<input>`.

### Values

| Value | Description |
|-------|-------------|
| `true` | Element is editable |
| `false` | Element is not editable |
| (empty) | Inherits from parent |

### Examples

**Basic editable text:**
```html
<div contenteditable="true">
  Click to edit this text!
</div>
```

**Editable heading:**
```html
<h1 contenteditable="true">Edit this heading</h1>
```

**Rich text editor:**
```html
<div contenteditable="true"
     style="border: 1px solid #ddd; padding: 20px; min-height: 200px;">
  <h2>Rich Text Editor</h2>
  <p>You can edit this content with <strong>bold</strong>, <em>italic</em>, and more!</p>
</div>
```

**Editable list:**
```html
<ul contenteditable="true">
  <li>Edit me</li>
  <li>Add items</li>
  <li>Remove items</li>
</ul>
```

### JavaScript Integration

```html
<div id="editor" contenteditable="true">
  Edit me
</div>

<button id="save-btn">Save</button>

<script>
const editor = document.getElementById('editor');
const saveBtn = document.getElementById('save-btn');

saveBtn.addEventListener('click', function() {
  const content = editor.innerHTML;
  console.log('Saved content:', content);
  // Send to server, localStorage, etc.
});

// Track changes
editor.addEventListener('input', function() {
  console.log('Content changed:', this.innerHTML);
});
</script>
```

---

## Draggable

### Syntax

```html
<element draggable="true|false">Content</element>
```

### Description

Makes elements draggable using HTML5 Drag and Drop API.

### Values

| Value | Description |
|-------|-------------|
| `true` | Element is draggable |
| `false` | Element is not draggable |
| `auto` | Default browser behavior |

### Examples

**Simple draggable element:**
```html
<div draggable="true" style="width: 100px; height: 100px; background: blue; color: white; padding: 20px;">
  Drag me
</div>
```

**Drag and drop example:**
```html
<style>
  .drag-item {
    width: 100px;
    height: 100px;
    background: #007bff;
    color: white;
    text-align: center;
    line-height: 100px;
    margin: 10px;
    cursor: move;
  }

  .drop-zone {
    width: 300px;
    height: 300px;
    border: 2px dashed #ddd;
    padding: 20px;
    margin: 20px 0;
  }

  .drop-zone.over {
    background: #f0f0f0;
    border-color: #007bff;
  }
</style>

<div draggable="true" class="drag-item" id="item1">
  Drag me
</div>

<div class="drop-zone" id="drop-zone">
  Drop here
</div>

<script>
const item = document.getElementById('item1');
const zone = document.getElementById('drop-zone');

item.addEventListener('dragstart', function(e) {
  e.dataTransfer.effectAllowed = 'move';
  e.dataTransfer.setData('text/html', this.innerHTML);
});

zone.addEventListener('dragover', function(e) {
  e.preventDefault();
  this.classList.add('over');
  e.dataTransfer.dropEffect = 'move';
  return false;
});

zone.addEventListener('dragleave', function() {
  this.classList.remove('over');
});

zone.addEventListener('drop', function(e) {
  e.preventDefault();
  this.classList.remove('over');
  const data = e.dataTransfer.getData('text/html');
  this.innerHTML += '<div class="drag-item">' + data + '</div>';
  return false;
});
</script>
```

---

## Hidden

### Syntax

```html
<element hidden>Content</element>
```

### Description

Hides element from display (similar to `display: none` in CSS). Element is not rendered and not accessible.

### Examples

**Hide element:**
```html
<p>This is visible.</p>
<p hidden>This is hidden.</p>
<p>This is also visible.</p>
```

**Toggle visibility with JavaScript:**
```html
<button id="toggle-btn">Toggle Content</button>

<div id="content">
  <p>This content can be toggled.</p>
</div>

<script>
const btn = document.getElementById('toggle-btn');
const content = document.getElementById('content');

btn.addEventListener('click', function() {
  content.hidden = !content.hidden;
});
</script>
```

**Hidden until loaded:**
```html
<div id="data-container" hidden>
  Loading...
</div>

<script>
// Show when data is loaded
fetch('/api/data')
  .then(response => response.json())
  .then(data => {
    const container = document.getElementById('data-container');
    container.textContent = data.message;
    container.hidden = false;
  });
</script>
```

**vs. CSS display:none:**
```html
<!-- HTML hidden attribute -->
<p hidden>Hidden with attribute</p>

<!-- CSS display:none -->
<p style="display: none;">Hidden with CSS</p>

<!-- Both have same effect, but hidden is semantic -->
```

---

## Spellcheck

### Syntax

```html
<element spellcheck="true|false">Content</element>
```

### Description

Controls whether browser should check spelling/grammar. Useful for disabling spell-check on code, usernames, or technical content.

### Values

| Value | Description |
|-------|-------------|
| `true` | Enable spell-check |
| `false` | Disable spell-check |

### Examples

**Enable spell-check (default for text inputs):**
```html
<textarea spellcheck="true">
  This textt will be spellchecked.
</textarea>
```

**Disable spell-check for code:**
```html
<textarea spellcheck="false" placeholder="Enter code here">
function helloWorld() {
  console.log('Hello');
}
</textarea>
```

**Disable for username:**
```html
<label for="username">Username:</label>
<input type="text" id="username" spellcheck="false">
```

**Contenteditable with spellcheck:**
```html
<div contenteditable="true" spellcheck="true">
  Edit this text with spellcheck enabled.
</div>
```

---

## Translate

### Syntax

```html
<element translate="yes|no">Content</element>
```

### Description

Tells translation tools (Google Translate, browser translation) whether to translate element content.

### Values

| Value | Description |
|-------|-------------|
| `yes` | Translate this content (default) |
| `no` | Don't translate this content |

### Examples

**Prevent translation of brand name:**
```html
<p>
  Welcome to <span translate="no">TechCorp</span>!
  We're glad you're here.
</p>
```

**Prevent translation of code:**
```html
<p>Use the command <code translate="no">npm install</code> to install packages.</p>
```

**Prevent translation of proper nouns:**
```html
<article>
  <h1 translate="no">Joshua P. Hickman</h1>
  <p>
    <span translate="no">Joshua</span> is a web developer based in
    <span translate="no">New York</span>.
  </p>
</article>
```

---

## Tabindex

### Syntax

```html
<element tabindex="number">Content</element>
```

### Description

Controls keyboard navigation order and focus. Allows non-interactive elements to receive focus.

### Values

| Value | Description |
|-------|-------------|
| Negative (e.g., `-1`) | Focusable via JavaScript, not via Tab key |
| `0` | Natural tab order (focusable via Tab) |
| Positive (e.g., `1`, `2`) | Custom tab order (not recommended) |

### Examples

**Make div focusable:**
```html
<div tabindex="0" style="padding: 20px; border: 1px solid #ddd;">
  This div can receive focus with Tab key
</div>
```

**Programmatic focus (not tab-accessible):**
```html
<div id="modal" tabindex="-1" style="display:none;">
  Modal content
</div>

<button id="open-modal-btn">Open Modal</button>

<script>
document.getElementById('open-modal-btn').addEventListener('click', function() {
  const modal = document.getElementById('modal');
  modal.style.display = 'block';
  modal.focus(); // Focus modal (tabindex="-1" allows this)
});
</script>
```

**Skip navigation link:**
```html
<a href="#main-content" tabindex="1">Skip to main content</a>

<!-- Header and nav here -->

<main id="main-content" tabindex="-1">
  Main content
</main>
```

---

## Accesskey

### Syntax

```html
<element accesskey="key">Content</element>
```

### Description

Defines keyboard shortcut to activate/focus element. Activation varies by browser:
- Windows: `Alt` + key
- Mac: `Control` + `Option` + key
- Linux: `Alt` + key

### Examples

**Button with accesskey:**
```html
<button accesskey="s">Save (Alt+S)</button>
<button accesskey="c">Cancel (Alt+C)</button>
```

**Form fields:**
```html
<label for="name">Name (Alt+N):</label>
<input type="text" id="name" accesskey="n">

<label for="email">Email (Alt+E):</label>
<input type="email" id="email" accesskey="e">
```

**⚠️ Warning:** Accesskeys can conflict with browser/OS shortcuts. Use sparingly.

---

## Examples

### Example 1: Note-Taking App with Contenteditable

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Simple Notes</title>
  <style>
    .note-editor {
      border: 1px solid #ddd;
      padding: 20px;
      min-height: 300px;
      margin: 20px 0;
      background: #fffbe6;
      font-family: 'Courier New', monospace;
    }

    .toolbar {
      margin-bottom: 10px;
    }

    button {
      padding: 8px 16px;
      margin-right: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Simple Note-Taking App</h1>

  <div class="toolbar">
    <button id="bold-btn" accesskey="b">Bold (Alt+B)</button>
    <button id="italic-btn" accesskey="i">Italic (Alt+I)</button>
    <button id="clear-btn" accesskey="c">Clear (Alt+C)</button>
    <button id="save-btn" accesskey="s">Save (Alt+S)</button>
  </div>

  <div class="note-editor"
       contenteditable="true"
       spellcheck="true"
       id="editor">
    Start typing your notes here...
  </div>

  <script>
    const editor = document.getElementById('editor');

    document.getElementById('bold-btn').addEventListener('click', () => {
      document.execCommand('bold');
    });

    document.getElementById('italic-btn').addEventListener('click', () => {
      document.execCommand('italic');
    });

    document.getElementById('clear-btn').addEventListener('click', () => {
      editor.innerHTML = '';
    });

    document.getElementById('save-btn').addEventListener('click', () => {
      localStorage.setItem('notes', editor.innerHTML);
      alert('Notes saved!');
    });

    // Load saved notes
    window.addEventListener('load', () => {
      const saved = localStorage.getItem('notes');
      if (saved) {
        editor.innerHTML = saved;
      }
    });
  </script>
</body>
</html>
```

### Example 2: Kanban Board with Drag and Drop

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Kanban Board</title>
  <style>
    .board {
      display: flex;
      gap: 20px;
    }

    .column {
      flex: 1;
      background: #f8f9fa;
      padding: 20px;
      border-radius: 8px;
      min-height: 400px;
    }

    .card {
      background: white;
      padding: 15px;
      margin: 10px 0;
      border-radius: 4px;
      cursor: move;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .column.over {
      background: #e9ecef;
    }
  </style>
</head>
<body>
  <h1>Kanban Board</h1>

  <div class="board">
    <div class="column" id="todo" data-status="todo">
      <h2>To Do</h2>
      <div class="card" draggable="true">Task 1: Design homepage</div>
      <div class="card" draggable="true">Task 2: Write documentation</div>
    </div>

    <div class="column" id="in-progress" data-status="in-progress">
      <h2>In Progress</h2>
      <div class="card" draggable="true">Task 3: Build API</div>
    </div>

    <div class="column" id="done" data-status="done">
      <h2>Done</h2>
      <div class="card" draggable="true">Task 4: Setup repository</div>
    </div>
  </div>

  <script>
    let draggedCard = null;

    document.querySelectorAll('.card').forEach(card => {
      card.addEventListener('dragstart', function() {
        draggedCard = this;
        setTimeout(() => this.classList.add('dragging'), 0);
      });

      card.addEventListener('dragend', function() {
        this.classList.remove('dragging');
        draggedCard = null;
      });
    });

    document.querySelectorAll('.column').forEach(column => {
      column.addEventListener('dragover', function(e) {
        e.preventDefault();
        this.classList.add('over');
      });

      column.addEventListener('dragleave', function() {
        this.classList.remove('over');
      });

      column.addEventListener('drop', function(e) {
        e.preventDefault();
        this.classList.remove('over');
        if (draggedCard) {
          this.appendChild(draggedCard);
        }
      });
    });
  </script>
</body>
</html>
```

---

## Quick Reference

### HTML5 Global Attributes

| Attribute | Values | Purpose |
|-----------|--------|---------|
| `contenteditable` | `true`, `false` | Make content editable |
| `draggable` | `true`, `false`, `auto` | Enable drag-and-drop |
| `hidden` | (boolean) | Hide element |
| `spellcheck` | `true`, `false` | Control spell-checking |
| `translate` | `yes`, `no` | Control translation |
| `tabindex` | number | Control focus order |
| `accesskey` | letter | Keyboard shortcut |

---

## Browser Support

| Attribute | Chrome | Firefox | Safari | Edge | IE |
|-----------|--------|---------|--------|------|----|
| `contenteditable` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `draggable` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 11+ |
| `hidden` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 11+ |
| `spellcheck` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 10+ |
| `translate` | ✅ 19+ | ✅ No | ✅ 6+ | ✅ All | ✅ 11+ |
| `tabindex` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `accesskey` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |

---

## Related Topics
- [ID and Class](id-class.md)
- [Data Attributes](data-attributes.md)
- [ARIA Attributes](aria-attributes.md)

---

**Last Updated:** November 17, 2025
**Category:** Global Attributes
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
