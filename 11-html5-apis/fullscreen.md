---
title: Fullscreen API
category: HTML5 APIs
order: 7
---

# Fullscreen API

> **Quick Summary:** The Fullscreen API allows web applications to display elements (videos, images, games) in fullscreen mode, providing immersive experiences similar to native apps.

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

The Fullscreen API enables any element on a web page to be displayed in fullscreen mode, taking over the entire screen. This is essential for video players, image galleries, games, and interactive presentations.

**The Problem:** Before this API, only native browser controls (like right-clicking a video) could trigger fullscreen. Developers couldn't create custom fullscreen experiences or make arbitrary elements fullscreen.

**The Solution:** The Fullscreen API provides `requestFullscreen()` to enter fullscreen and `exitFullscreen()` to leave, plus events to detect changes. Works with any HTML element.

**Key Concept:** Fullscreen requests must be triggered by user interaction (click, keypress) for security—you can't force users into fullscreen without their action.

---

## Basic Syntax

### Entering Fullscreen

```javascript
// Make any element fullscreen
const element = document.getElementById('myVideo');

element.requestFullscreen()
  .then(() => console.log('Entered fullscreen'))
  .catch(err => console.error('Fullscreen error:', err));

// Vendor prefixes for older browsers
element.requestFullscreen = element.requestFullscreen ||
                            element.webkitRequestFullscreen ||
                            element.mozRequestFullScreen ||
                            element.msRequestFullscreen;
```

### Exiting Fullscreen

```javascript
// Exit fullscreen (called on document, not element)
document.exitFullscreen()
  .then(() => console.log('Exited fullscreen'))
  .catch(err => console.error('Exit error:', err));
```

### Checking Fullscreen State

```javascript
// Check if currently in fullscreen
if (document.fullscreenElement) {
  console.log('Fullscreen element:', document.fullscreenElement);
} else {
  console.log('Not in fullscreen');
}

// Check if fullscreen is available
if (document.fullscreenEnabled) {
  console.log('Fullscreen is supported');
}
```

### Listening for Fullscreen Changes

```javascript
document.addEventListener('fullscreenchange', function() {
  if (document.fullscreenElement) {
    console.log('Entered fullscreen:', document.fullscreenElement);
  } else {
    console.log('Exited fullscreen');
  }
});

document.addEventListener('fullscreenerror', function(event) {
  console.error('Fullscreen error occurred');
});
```

### Key Properties and Methods

| Property/Method | Description |
|----------------|-------------|
| `element.requestFullscreen()` | Request fullscreen for the element (returns Promise) |
| `document.exitFullscreen()` | Exit fullscreen mode (returns Promise) |
| `document.fullscreenElement` | Currently fullscreen element (or `null`) |
| `document.fullscreenEnabled` | Boolean - is fullscreen available |
| `fullscreenchange` event | Fired when entering/exiting fullscreen |
| `fullscreenerror` event | Fired if fullscreen request fails |

---

## Examples

### Example 1: Fullscreen Video Player

**Scenario:** Create a custom video player with a fullscreen button

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fullscreen Video</title>
  <style>
    .video-container {
      max-width: 800px;
      margin: 20px auto;
      position: relative;
      background: #000;
    }
    video {
      width: 100%;
      display: block;
    }
    .controls {
      position: absolute;
      bottom: 10px;
      right: 10px;
      display: flex;
      gap: 10px;
    }
    button {
      padding: 10px 15px;
      background: rgba(255, 255, 255, 0.9);
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background: white;
    }
    /* Fullscreen-specific styles */
    .video-container:fullscreen {
      background: #000;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .video-container:fullscreen video {
      max-height: 100vh;
      max-width: 100vw;
    }
  </style>
</head>
<body>
  <h1>Fullscreen Video Player</h1>

  <div class="video-container" id="videoContainer">
    <video id="video" controls>
      <source src="sample-video.mp4" type="video/mp4">
      Your browser doesn't support video.
    </video>

    <div class="controls">
      <button id="playBtn">▶️ Play</button>
      <button id="fullscreenBtn">⛶ Fullscreen</button>
    </div>
  </div>

  <script>
    const video = document.getElementById('video');
    const videoContainer = document.getElementById('videoContainer');
    const playBtn = document.getElementById('playBtn');
    const fullscreenBtn = document.getElementById('fullscreenBtn');

    // Play/Pause toggle
    playBtn.addEventListener('click', () => {
      if (video.paused) {
        video.play();
        playBtn.textContent = '⏸️ Pause';
      } else {
        video.pause();
        playBtn.textContent = '▶️ Play';
      }
    });

    // Fullscreen toggle
    fullscreenBtn.addEventListener('click', async () => {
      try {
        if (!document.fullscreenElement) {
          await videoContainer.requestFullscreen();
        } else {
          await document.exitFullscreen();
        }
      } catch (err) {
        console.error('Fullscreen error:', err);
      }
    });

    // Update button text based on fullscreen state
    document.addEventListener('fullscreenchange', () => {
      if (document.fullscreenElement) {
        fullscreenBtn.textContent = '⛶ Exit Fullscreen';
      } else {
        fullscreenBtn.textContent = '⛶ Fullscreen';
      }
    });

    // ESC key reminder
    document.addEventListener('fullscreenerror', () => {
      alert('Could not enter fullscreen mode. Please try again.');
    });
  </script>
</body>
</html>
```

**Result:** Clicking the fullscreen button makes the entire video container fullscreen. ESC key exits fullscreen. Button text updates automatically.

---

### Example 2: Fullscreen Image Gallery

**Scenario:** View images in fullscreen with navigation controls

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Fullscreen Gallery</title>
  <style>
    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      padding: 20px;
    }
    .gallery img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      cursor: pointer;
      border-radius: 8px;
      transition: transform 0.2s;
    }
    .gallery img:hover {
      transform: scale(1.05);
    }
    .lightbox {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.95);
      z-index: 1000;
    }
    .lightbox.active {
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .lightbox img {
      max-width: 90%;
      max-height: 90%;
      object-fit: contain;
    }
    .lightbox-controls {
      position: absolute;
      bottom: 20px;
      display: flex;
      gap: 15px;
    }
    .lightbox-controls button {
      padding: 12px 20px;
      background: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <h1>Click any image to view fullscreen</h1>

  <div class="gallery">
    <img src="https://picsum.photos/400/300?random=1" alt="Image 1">
    <img src="https://picsum.photos/400/300?random=2" alt="Image 2">
    <img src="https://picsum.photos/400/300?random=3" alt="Image 3">
    <img src="https://picsum.photos/400/300?random=4" alt="Image 4">
    <img src="https://picsum.photos/400/300?random=5" alt="Image 5">
    <img src="https://picsum.photos/400/300?random=6" alt="Image 6">
  </div>

  <div class="lightbox" id="lightbox">
    <img id="lightboxImg" src="" alt="">
    <div class="lightbox-controls">
      <button id="fullscreenBtn">⛶ Fullscreen</button>
      <button id="closeBtn">✕ Close</button>
    </div>
  </div>

  <script>
    const lightbox = document.getElementById('lightbox');
    const lightboxImg = document.getElementById('lightboxImg');
    const fullscreenBtn = document.getElementById('fullscreenBtn');
    const closeBtn = document.getElementById('closeBtn');
    const galleryImages = document.querySelectorAll('.gallery img');

    // Open lightbox on image click
    galleryImages.forEach(img => {
      img.addEventListener('click', () => {
        lightboxImg.src = img.src;
        lightboxImg.alt = img.alt;
        lightbox.classList.add('active');
      });
    });

    // Close lightbox
    closeBtn.addEventListener('click', () => {
      lightbox.classList.remove('active');
      if (document.fullscreenElement) {
        document.exitFullscreen();
      }
    });

    // Fullscreen toggle
    fullscreenBtn.addEventListener('click', async () => {
      if (!document.fullscreenElement) {
        await lightbox.requestFullscreen();
      } else {
        await document.exitFullscreen();
      }
    });

    // Update button on fullscreen change
    document.addEventListener('fullscreenchange', () => {
      fullscreenBtn.textContent = document.fullscreenElement
        ? '⛶ Exit Fullscreen'
        : '⛶ Fullscreen';
    });

    // ESC key closes lightbox
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' && !document.fullscreenElement) {
        lightbox.classList.remove('active');
      }
    });
  </script>
</body>
</html>
```

**Result:** Click any thumbnail to open a lightbox. Click "Fullscreen" to view the image in fullscreen mode. ESC exits fullscreen and closes the lightbox.

---

### Example 3: Fullscreen Presentation Mode

**Scenario:** Create a slide deck that can be presented in fullscreen

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Fullscreen Presentation</title>
  <style>
    .presentation {
      max-width: 900px;
      margin: 20px auto;
      padding: 20px;
      background: #f5f5f5;
      border-radius: 10px;
    }
    .slide {
      display: none;
      padding: 60px;
      background: white;
      border-radius: 8px;
      min-height: 400px;
    }
    .slide.active {
      display: block;
    }
    .slide h2 {
      color: #2196F3;
      margin-bottom: 20px;
    }
    .controls {
      margin-top: 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    button {
      padding: 12px 20px;
      background: #2196F3;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background: #1976D2;
    }
    button:disabled {
      background: #ccc;
      cursor: not-allowed;
    }
    /* Fullscreen styles */
    .presentation:fullscreen {
      background: #000;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
    .presentation:fullscreen .slide {
      font-size: 1.5em;
      padding: 100px;
    }
  </style>
</head>
<body>
  <div class="presentation" id="presentation">
    <div class="slide active" data-slide="1">
      <h2>Slide 1: Introduction</h2>
      <p>Welcome to this presentation about the Fullscreen API!</p>
      <ul>
        <li>Press F to toggle fullscreen</li>
        <li>Use arrow keys to navigate</li>
        <li>Press ESC to exit fullscreen</li>
      </ul>
    </div>

    <div class="slide" data-slide="2">
      <h2>Slide 2: Key Benefits</h2>
      <ul>
        <li>Immersive viewing experience</li>
        <li>No distractions from browser UI</li>
        <li>Perfect for presentations and media</li>
      </ul>
    </div>

    <div class="slide" data-slide="3">
      <h2>Slide 3: Conclusion</h2>
      <p>The Fullscreen API enables powerful user experiences.</p>
      <p><strong>Thank you for watching!</strong></p>
    </div>

    <div class="controls">
      <button id="prevBtn">← Previous</button>
      <span id="slideCounter">Slide 1 of 3</span>
      <button id="nextBtn">Next →</button>
      <button id="fullscreenBtn">⛶ Present Fullscreen</button>
    </div>
  </div>

  <script>
    const presentation = document.getElementById('presentation');
    const slides = document.querySelectorAll('.slide');
    const prevBtn = document.getElementById('prevBtn');
    const nextBtn = document.getElementById('nextBtn');
    const fullscreenBtn = document.getElementById('fullscreenBtn');
    const slideCounter = document.getElementById('slideCounter');

    let currentSlide = 0;
    const totalSlides = slides.length;

    function showSlide(n) {
      slides.forEach(slide => slide.classList.remove('active'));
      currentSlide = Math.max(0, Math.min(n, totalSlides - 1));
      slides[currentSlide].classList.add('active');

      slideCounter.textContent = `Slide ${currentSlide + 1} of ${totalSlides}`;
      prevBtn.disabled = currentSlide === 0;
      nextBtn.disabled = currentSlide === totalSlides - 1;
    }

    prevBtn.addEventListener('click', () => showSlide(currentSlide - 1));
    nextBtn.addEventListener('click', () => showSlide(currentSlide + 1));

    // Keyboard navigation
    document.addEventListener('keydown', async (e) => {
      if (e.key === 'ArrowLeft') showSlide(currentSlide - 1);
      if (e.key === 'ArrowRight') showSlide(currentSlide + 1);

      if (e.key === 'f' || e.key === 'F') {
        if (!document.fullscreenElement) {
          await presentation.requestFullscreen();
        } else {
          await document.exitFullscreen();
        }
      }
    });

    // Fullscreen toggle
    fullscreenBtn.addEventListener('click', async () => {
      if (!document.fullscreenElement) {
        await presentation.requestFullscreen();
      } else {
        await document.exitFullscreen();
      }
    });

    // Update button text
    document.addEventListener('fullscreenchange', () => {
      fullscreenBtn.textContent = document.fullscreenElement
        ? '⛶ Exit Fullscreen'
        : '⛶ Present Fullscreen';
    });
  </script>
</body>
</html>
```

**Result:** A presentation that can be viewed fullscreen with keyboard navigation. Arrow keys change slides, F toggles fullscreen, ESC exits.

**Notes:**
- Fullscreen mode enlarges text and centers content
- Keyboard shortcuts work both in and out of fullscreen
- Useful for conferences, teaching, or product demos

---

## Common Use Cases

### Use Case 1: Video Players
**When:** Any video player implementation (YouTube-style, Netflix-style)
**How:**
```javascript
videoElement.addEventListener('dblclick', () => {
  videoElement.requestFullscreen();
});
```
**Why:** Users expect double-click to enter fullscreen for videos.

---

### Use Case 2: Web Games
**When:** HTML5 canvas games, WebGL games
**How:**
```javascript
startGameBtn.addEventListener('click', async () => {
  await gameCanvas.requestFullscreen();
  startGame();
});
```
**Why:** Fullscreen provides immersive gaming experience without browser UI distractions.

---

### Use Case 3: Data Visualizations
**When:** Charts, dashboards, data presentations
**How:**
```javascript
expandBtn.addEventListener('click', () => {
  dashboardContainer.requestFullscreen();
});
```
**Why:** Fullscreen allows users to focus on complex data without distractions.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 71+     | Full Support (unprefixed)  | 15+ with prefix |
| Firefox | 64+     | Full Support (unprefixed)  | 9+ with prefix |
| Safari  | 16.4+   | Full Support (unprefixed)  | 5.1+ with prefix |
| Edge    | 79+     | Full Support  | Legacy Edge 12+ |
| IE      | 11      | Partial (prefixed) | ms prefix required |

**Fallback Strategy:**
```javascript
function requestFullscreen(element) {
  if (element.requestFullscreen) {
    return element.requestFullscreen();
  } else if (element.webkitRequestFullscreen) {
    return element.webkitRequestFullscreen();
  } else if (element.mozRequestFullScreen) {
    return element.mozRequestFullScreen();
  } else if (element.msRequestFullscreen) {
    return element.msRequestFullscreen();
  } else {
    console.warn('Fullscreen API not supported');
    return Promise.reject();
  }
}
```

**Can I Use Link:** [https://caniuse.com/fullscreen](https://caniuse.com/fullscreen)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Provide clear instructions on how to exit fullscreen
- Ensure keyboard navigation works in fullscreen mode

**Level AA Requirements:**
- Don't trap users in fullscreen (always allow ESC to exit)
- Provide visible controls for users with motor impairments

### Screen Reader Support

```html
<!-- Announce fullscreen state changes -->
<div aria-live="polite" aria-atomic="true" id="fullscreenStatus" class="sr-only"></div>

<script>
  document.addEventListener('fullscreenchange', () => {
    const status = document.getElementById('fullscreenStatus');
    if (document.fullscreenElement) {
      status.textContent = 'Entered fullscreen mode. Press Escape to exit.';
    } else {
      status.textContent = 'Exited fullscreen mode.';
    }
  });
</script>
```

**Key Points:**
- Always inform users how to exit fullscreen (ESC key)
- Use ARIA live regions to announce fullscreen changes
- Provide visible buttons, not just keyboard shortcuts
- Ensure focus remains on interactive elements in fullscreen

### Keyboard Navigation

- **F11:** Native browser fullscreen (different from Fullscreen API)
- **ESC:** Always exits fullscreen (cannot be overridden)
- **Tab:** Must work to navigate controls in fullscreen
- **Custom shortcuts:** Document them clearly (e.g., "Press F to toggle fullscreen")

---

## Best Practices

### Do This

1. **Always Request Fullscreen from User Interaction**
   ```javascript
   // ✅ CORRECT - Triggered by user click
   button.addEventListener('click', () => {
     element.requestFullscreen();
   });
   ```
   **Why:** Browsers block automatic fullscreen requests for security.

2. **Provide Clear Exit Instructions**
   ```html
   <div class="fullscreen-hint">
     Press ESC to exit fullscreen
   </div>
   ```
   **Why:** Users unfamiliar with fullscreen may feel trapped.

3. **Handle Fullscreen Changes**
   ```javascript
   document.addEventListener('fullscreenchange', () => {
     if (document.fullscreenElement) {
       pauseBackgroundTasks();
     } else {
       resumeBackgroundTasks();
     }
   });
   ```
   **Why:** Allows you to optimize performance or update UI based on state.

4. **Use CSS to Optimize Fullscreen Layout**
   ```css
   .video-container:fullscreen {
     background: #000;
     display: flex;
     align-items: center;
     justify-content: center;
   }
   ```
   **Why:** Fullscreen elements should look polished, not just enlarged.

---

### Avoid This

1. **Don't Request Fullscreen Without User Action**
   ```javascript
   // ❌ WRONG - Automatic fullscreen on page load
   window.addEventListener('load', () => {
     document.body.requestFullscreen(); // Will fail!
   });
   ```
   **Why Not:** Browsers reject this for security (prevents malicious sites from tricking users).
   **Instead:** Require a button click or keypress.

2. **Don't Assume Fullscreen Will Succeed**
   ```javascript
   // ❌ WRONG - No error handling
   element.requestFullscreen();

   // ✅ CORRECT
   element.requestFullscreen().catch(err => {
     console.error('Fullscreen failed:', err);
     showFallbackUI();
   });
   ```
   **Why Not:** Fullscreen can fail (user denies permission, browser restrictions).
   **Instead:** Always handle the returned Promise.

3. **Don't Forget Vendor Prefixes**
   ```javascript
   // ❌ WRONG - Only works in modern browsers
   element.requestFullscreen();

   // ✅ CORRECT - Cross-browser support
   const requestFS = element.requestFullscreen ||
                     element.webkitRequestFullscreen ||
                     element.mozRequestFullScreen;
   requestFS.call(element);
   ```
   **Why Not:** Older browsers need prefixed methods.
   **Instead:** Use a polyfill or check for vendor prefixes.

---

## Related Topics

**Prerequisites (Learn These First):**
- [Video Elements](../08-media-elements/video-audio.md) - Common fullscreen use case
- [Canvas](../10-graphics-canvas/canvas-introduction.md) - For games

**Related Concepts:**
- [Page Visibility API](page-visibility.md) - Detect when user switches tabs
- [Screen Orientation API](https://developer.mozilla.org/en-US/docs/Web/API/Screen_Orientation_API) - Lock orientation in fullscreen

**Next Steps (Learn These Next):**
- [Pointer Lock API](https://developer.mozilla.org/en-US/docs/Web/API/Pointer_Lock_API) - For games (hides cursor)
- [Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API) - Animate fullscreen transitions

**External Resources:**
- [MDN Web Docs - Fullscreen API](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API)
- [HTML Living Standard - Fullscreen](https://fullscreen.spec.whatwg.org/)
- [Using Fullscreen Mode (MDN Guide)](https://developer.mozilla.org/en-US/docs/Web/API/Fullscreen_API/Guide)

---

## Practice Exercise

### Challenge: Build a Fullscreen Photo Viewer

**Objective:** Create an image viewer that supports fullscreen mode with zoom and pan controls.

**Requirements:**
- [ ] Display a sample image with a "View Fullscreen" button
- [ ] Clicking the button enters fullscreen
- [ ] Add zoom in/out buttons that work in fullscreen
- [ ] Allow panning (dragging) the zoomed image
- [ ] Display current zoom level
- [ ] Bonus: Add keyboard shortcuts (+ to zoom in, - to zoom out, ESC to exit)

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fullscreen Photo Viewer</title>
  <style>
    .viewer {
      max-width: 800px;
      margin: 20px auto;
      border: 2px solid #ddd;
      border-radius: 8px;
      overflow: hidden;
    }
    .image-container {
      width: 100%;
      height: 500px;
      background: #000;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      position: relative;
    }
    img {
      max-width: 100%;
      max-height: 100%;
      transition: transform 0.3s;
    }
    .controls {
      padding: 15px;
      background: #f5f5f5;
      display: flex;
      gap: 10px;
      justify-content: center;
    }
    button {
      padding: 10px 15px;
      border: none;
      background: #2196F3;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="viewer" id="viewer">
    <div class="image-container" id="imageContainer">
      <img src="https://picsum.photos/1200/800" alt="Sample Photo" id="photo">
    </div>
    <div class="controls">
      <button id="zoomInBtn">🔍+ Zoom In</button>
      <button id="zoomOutBtn">🔍- Zoom Out</button>
      <span id="zoomLevel">100%</span>
      <button id="fullscreenBtn">⛶ Fullscreen</button>
    </div>
  </div>

  <!-- Add your JavaScript here -->
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**Complete Solution:**
```html
<script>
  const viewer = document.getElementById('viewer');
  const photo = document.getElementById('photo');
  const imageContainer = document.getElementById('imageContainer');
  const zoomInBtn = document.getElementById('zoomInBtn');
  const zoomOutBtn = document.getElementById('zoomOutBtn');
  const fullscreenBtn = document.getElementById('fullscreenBtn');
  const zoomLevel = document.getElementById('zoomLevel');

  let scale = 1;
  let isDragging = false;
  let startX, startY, translateX = 0, translateY = 0;

  function updateTransform() {
    photo.style.transform = `translate(${translateX}px, ${translateY}px) scale(${scale})`;
    zoomLevel.textContent = `${Math.round(scale * 100)}%`;
  }

  zoomInBtn.addEventListener('click', () => {
    scale = Math.min(scale + 0.25, 3);
    updateTransform();
  });

  zoomOutBtn.addEventListener('click', () => {
    scale = Math.max(scale - 0.25, 0.5);
    if (scale === 1) {
      translateX = translateY = 0;
    }
    updateTransform();
  });

  // Drag to pan
  photo.addEventListener('mousedown', (e) => {
    if (scale > 1) {
      isDragging = true;
      startX = e.clientX - translateX;
      startY = e.clientY - translateY;
      photo.style.cursor = 'grabbing';
    }
  });

  document.addEventListener('mousemove', (e) => {
    if (isDragging) {
      translateX = e.clientX - startX;
      translateY = e.clientY - startY;
      updateTransform();
    }
  });

  document.addEventListener('mouseup', () => {
    isDragging = false;
    photo.style.cursor = scale > 1 ? 'grab' : 'default';
  });

  // Fullscreen
  fullscreenBtn.addEventListener('click', async () => {
    if (!document.fullscreenElement) {
      await viewer.requestFullscreen();
    } else {
      await document.exitFullscreen();
    }
  });

  document.addEventListener('fullscreenchange', () => {
    fullscreenBtn.textContent = document.fullscreenElement
      ? '⛶ Exit Fullscreen'
      : '⛶ Fullscreen';
  });

  // Keyboard shortcuts
  document.addEventListener('keydown', (e) => {
    if (e.key === '+' || e.key === '=') {
      zoomInBtn.click();
    } else if (e.key === '-' || e.key === '_') {
      zoomOutBtn.click();
    }
  });
</script>
```

**Explanation:**
This photo viewer allows users to zoom in/out and pan the image. Fullscreen mode provides an immersive viewing experience. The solution uses CSS transforms for smooth zooming and dragging logic for panning. Keyboard shortcuts (+/-) provide quick access to zoom controls.

</details>

---

### Expected Result

**Visual Outcome:**
- Image viewer with zoom and fullscreen controls
- Smooth zoom transitions
- Draggable panning when zoomed in
- Fullscreen button toggles state
- Keyboard shortcuts work as expected

**Key Learnings:**
- How to implement fullscreen functionality
- Combining Fullscreen API with other interactions (zoom, pan)
- Handling user input in fullscreen mode
- Real-world application: Photo galleries, maps, design tools

---

## Navigation

**Previous:** [History API](history-api.md)
**Next:** [Page Visibility API](page-visibility.md)
**Up:** [Back to HTML5 APIs](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** HTML5 APIs
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
