---
title: Drag and Drop API
category: HTML5 APIs
order: 31
---

# Drag and Drop API

> **Quick Summary:** The HTML5 Drag and Drop API enables intuitive drag-and-drop interactions for files, text, and elements. Essential for file uploaders, kanban boards, sortable lists, and interactive UIs. Works with native browser events—no libraries needed.

## Table of Contents
- [Introduction](#introduction)
- [Making Elements Draggable](#making-elements-draggable)
- [Drag Events](#drag-events)
- [DataTransfer Object](#datatransfer-object)
- [Drop Zones](#drop-zones)
- [File Drag and Drop](#file-drag-and-drop)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The Drag and Drop API provides events and methods for dragging elements and dropping them onto target areas.

**Key concepts:**
- **Draggable elements** - Set `draggable="true"`
- **Drag events** - `dragstart`, `drag`, `dragend`, `dragenter`, `dragover`, `dragleave`, `drop`
- **DataTransfer** - Carries data during drag operation
- **Drop zones** - Elements that accept drops

**Key Concept:** Drag and drop is like picking up a physical object and placing it somewhere else. The browser tracks what you're dragging (`dataTransfer`), where you're hovering (`dragover`), and where you drop it (`drop`).

---

## Making Elements Draggable

### Basic Draggable Element

```html
<div draggable="true">Drag me!</div>
```

### Draggable Values

| Value | Description |
|-------|-------------|
| `true` | Element is draggable |
| `false` | Element is not draggable |
| `auto` | Default browser behavior (text, images, links) |

### Example

```html
<style>
  .draggable {
    padding: 20px;
    margin: 10px;
    background: #007bff;
    color: white;
    cursor: move;
  }
</style>

<div class="draggable" draggable="true">
  Drag me around!
</div>
```

---

## Drag Events

### Event Flow

1. **dragstart** - User starts dragging
2. **drag** - Element is being dragged (fires continuously)
3. **dragenter** - Dragged element enters drop zone
4. **dragover** - Dragged element is over drop zone (fires continuously)
5. **dragleave** - Dragged element leaves drop zone
6. **drop** - Element is dropped
7. **dragend** - Drag operation ends (success or cancel)

### Basic Event Handlers

```javascript
const draggable = document.querySelector('.draggable');

draggable.addEventListener('dragstart', function(e) {
  console.log('Started dragging');
  e.dataTransfer.setData('text/plain', 'Hello');
});

draggable.addEventListener('dragend', function(e) {
  console.log('Finished dragging');
});
```

---

## DataTransfer Object

The `dataTransfer` object carries data during drag operations.

### Methods

```javascript
// Set data
e.dataTransfer.setData(format, data);

// Get data
const data = e.dataTransfer.getData(format);

// Clear data
e.dataTransfer.clearData();

// Set drag image
e.dataTransfer.setDragImage(img, xOffset, yOffset);
```

### Data Formats

```javascript
// Text
e.dataTransfer.setData('text/plain', 'Hello World');

// HTML
e.dataTransfer.setData('text/html', '<strong>Bold</strong>');

// URL
e.dataTransfer.setData('text/uri-list', 'https://example.com');

// Custom
e.dataTransfer.setData('application/my-app', JSON.stringify(data));
```

### Example

```html
<style>
  .item {
    padding: 15px;
    margin: 10px;
    background: #007bff;
    color: white;
    cursor: move;
  }

  .dropzone {
    min-height: 200px;
    padding: 20px;
    border: 2px dashed #ddd;
    margin: 20px 0;
  }

  .dropzone.over {
    border-color: #007bff;
    background: #f0f8ff;
  }
</style>

<div class="item" draggable="true" id="item1">Item 1</div>
<div class="item" draggable="true" id="item2">Item 2</div>

<div class="dropzone" id="dropzone">
  Drop items here
</div>

<script>
  const items = document.querySelectorAll('.item');
  const dropzone = document.getElementById('dropzone');

  items.forEach(item => {
    item.addEventListener('dragstart', function(e) {
      e.dataTransfer.setData('text/plain', this.id);
      e.dataTransfer.effectAllowed = 'move';
    });
  });

  dropzone.addEventListener('dragover', function(e) {
    e.preventDefault();
    this.classList.add('over');
    e.dataTransfer.dropEffect = 'move';
  });

  dropzone.addEventListener('dragleave', function(e) {
    this.classList.remove('over');
  });

  dropzone.addEventListener('drop', function(e) {
    e.preventDefault();
    this.classList.remove('over');

    const id = e.dataTransfer.getData('text/plain');
    const draggable = document.getElementById(id);
    this.appendChild(draggable);
  });
</script>
```

---

## Drop Zones

### Creating a Drop Zone

```javascript
const dropzone = document.querySelector('.dropzone');

// Required: prevent default to allow drop
dropzone.addEventListener('dragover', function(e) {
  e.preventDefault();
  e.dataTransfer.dropEffect = 'move';
});

// Handle drop
dropzone.addEventListener('drop', function(e) {
  e.preventDefault();
  const data = e.dataTransfer.getData('text/plain');
  // Process data
});
```

### Drop Effects

```javascript
e.dataTransfer.dropEffect = 'copy';  // Copy operation
e.dataTransfer.dropEffect = 'move';  // Move operation
e.dataTransfer.dropEffect = 'link';  // Link operation
e.dataTransfer.dropEffect = 'none';  // No drop allowed
```

---

## File Drag and Drop

### Handling File Drops

```html
<style>
  .file-dropzone {
    width: 100%;
    height: 300px;
    border: 3px dashed #ddd;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 20px;
    color: #999;
  }

  .file-dropzone.dragover {
    border-color: #007bff;
    background: #f0f8ff;
  }
</style>

<div class="file-dropzone" id="file-drop">
  Drag files here to upload
</div>

<div id="file-list"></div>

<script>
  const dropZone = document.getElementById('file-drop');
  const fileList = document.getElementById('file-list');

  dropZone.addEventListener('dragover', function(e) {
    e.preventDefault();
    this.classList.add('dragover');
  });

  dropZone.addEventListener('dragleave', function(e) {
    this.classList.remove('dragover');
  });

  dropZone.addEventListener('drop', function(e) {
    e.preventDefault();
    this.classList.remove('dragover');

    const files = e.dataTransfer.files;

    fileList.innerHTML = '<h3>Files:</h3>';
    for (let file of files) {
      fileList.innerHTML += `
        <p>
          <strong>${file.name}</strong>
          (${(file.size / 1024).toFixed(2)} KB)
          - ${file.type || 'unknown type'}
        </p>
      `;
    }
  });
</script>
```

---

## Examples

### Example 1: Sortable List

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Sortable List</title>
  <style>
    .sortable-list {
      list-style: none;
      padding: 0;
      max-width: 400px;
      margin: 20px auto;
    }

    .sortable-item {
      padding: 15px;
      margin: 5px 0;
      background: #007bff;
      color: white;
      cursor: move;
      border-radius: 5px;
    }

    .sortable-item.dragging {
      opacity: 0.5;
    }

    .sortable-item.over {
      border-top: 3px solid #ffc107;
    }
  </style>
</head>
<body>
  <h1>Drag to Reorder</h1>

  <ul class="sortable-list" id="list">
    <li class="sortable-item" draggable="true">Item 1</li>
    <li class="sortable-item" draggable="true">Item 2</li>
    <li class="sortable-item" draggable="true">Item 3</li>
    <li class="sortable-item" draggable="true">Item 4</li>
    <li class="sortable-item" draggable="true">Item 5</li>
  </ul>

  <script>
    const items = document.querySelectorAll('.sortable-item');
    let draggedItem = null;

    items.forEach(item => {
      item.addEventListener('dragstart', function() {
        draggedItem = this;
        this.classList.add('dragging');
      });

      item.addEventListener('dragend', function() {
        this.classList.remove('dragging');
        draggedItem = null;
      });

      item.addEventListener('dragover', function(e) {
        e.preventDefault();
        if (this !== draggedItem) {
          this.classList.add('over');
        }
      });

      item.addEventListener('dragleave', function() {
        this.classList.remove('over');
      });

      item.addEventListener('drop', function(e) {
        e.preventDefault();
        this.classList.remove('over');

        if (draggedItem && this !== draggedItem) {
          const list = this.parentNode;
          const allItems = [...list.children];
          const draggedIndex = allItems.indexOf(draggedItem);
          const targetIndex = allItems.indexOf(this);

          if (draggedIndex < targetIndex) {
            this.parentNode.insertBefore(draggedItem, this.nextSibling);
          } else {
            this.parentNode.insertBefore(draggedItem, this);
          }
        }
      });
    });
  </script>
</body>
</html>
```

### Example 2: Kanban Board

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
      padding: 20px;
    }

    .column {
      flex: 1;
      background: #f8f9fa;
      padding: 15px;
      border-radius: 8px;
      min-height: 400px;
    }

    .column h2 {
      margin-top: 0;
    }

    .card {
      background: white;
      padding: 15px;
      margin: 10px 0;
      border-radius: 5px;
      cursor: move;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    }

    .card.dragging {
      opacity: 0.5;
    }

    .column.over {
      background: #e9ecef;
    }
  </style>
</head>
<body>
  <h1>Task Board</h1>

  <div class="board">
    <div class="column" data-status="todo">
      <h2>To Do</h2>
      <div class="card" draggable="true">Design homepage</div>
      <div class="card" draggable="true">Write documentation</div>
    </div>

    <div class="column" data-status="in-progress">
      <h2>In Progress</h2>
      <div class="card" draggable="true">Build API</div>
    </div>

    <div class="column" data-status="done">
      <h2>Done</h2>
      <div class="card" draggable="true">Setup repository</div>
    </div>
  </div>

  <script>
    let draggedCard = null;

    document.querySelectorAll('.card').forEach(card => {
      card.addEventListener('dragstart', function() {
        draggedCard = this;
        this.classList.add('dragging');
      });

      card.addEventListener('dragend', function() {
        this.classList.remove('dragging');
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

## Best Practices

### Do This

1. **Provide visual feedback**
   ```javascript
   dragstart: element.classList.add('dragging');
   dragend: element.classList.remove('dragging');
   dragover: dropzone.classList.add('over');
   ```

2. **Always preventDefault() in dragover**
   ```javascript
   dropzone.addEventListener('dragover', function(e) {
     e.preventDefault(); // Required for drop to work!
   });
   ```

3. **Set appropriate drop effect**
   ```javascript
   e.dataTransfer.dropEffect = 'move'; // or 'copy', 'link'
   ```

### Avoid This

1. **Don't forget preventDefault() in drop event**
   ```javascript
   // WRONG: Browser may navigate away
   dropzone.addEventListener('drop', function(e) {
     // Missing e.preventDefault()
   });

   // CORRECT
   dropzone.addEventListener('drop', function(e) {
     e.preventDefault();
   });
   ```

2. **Don't use drag events for everything**
   ```javascript
   // WRONG: Too many events firing
   element.addEventListener('drag', updatePosition); // Fires continuously!

   // CORRECT: Use dragend
   element.addEventListener('dragend', updatePosition);
   ```

---

## Quick Reference

### Events

```javascript
dragstart   // Drag begins
drag        // During drag (continuous)
dragend     // Drag ends
dragenter   // Enter drop zone
dragover    // Over drop zone (continuous)
dragleave   // Leave drop zone
drop        // Dropped
```

### DataTransfer Methods

```javascript
setData(format, data)
getData(format)
clearData()
setDragImage(img, x, y)
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE |
|---------|--------|---------|--------|------|-----|
| Drag and Drop API | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |
| File drag/drop | ✅ All | ✅ 3.6+ | ✅ 6+ | ✅ All | ✅ 10+ |
| `dataTransfer` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ |

---

## Related Topics
- [Geolocation](geolocation.md)
- [Web Storage](web-storage.md)
- [File API](../04-media-elements/lazy-loading.md)

---

**Last Updated:** November 17, 2025
**Category:** HTML5 APIs
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
