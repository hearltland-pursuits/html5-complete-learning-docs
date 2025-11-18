---
title: Page Visibility API
category: HTML5 APIs
order: 8
---

# Page Visibility API

> **Quick Summary:** The Page Visibility API detects when users switch tabs or minimize the browser, allowing you to pause animations, stop videos, or reduce resource usage when your page isn't visible.

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

The Page Visibility API provides information about whether a web page is currently visible to the user. This is crucial for optimizing performance and user experience by pausing unnecessary work when users aren't looking.

**The Problem:** Before this API, web pages couldn't tell if they were visible. Videos kept playing, animations consumed CPU, and timers ran even when users switched tabs—wasting battery and bandwidth.

**The Solution:** The Page Visibility API exposes `document.hidden` (boolean) and `document.visibilityState` (string), plus a `visibilitychange` event that fires when the page's visibility changes.

**Key Concept:** "Hidden" means the page is in a background tab, minimized, or the OS screen is locked. It doesn't mean scrolled out of view.

---

## Basic Syntax

### Checking Visibility State

```javascript
// Check if page is currently hidden
if (document.hidden) {
  console.log('Page is hidden');
} else {
  console.log('Page is visible');
}

// Get detailed visibility state
console.log(document.visibilityState);
// Possible values: 'visible', 'hidden', 'prerender'
```

### Listening for Visibility Changes

```javascript
document.addEventListener('visibilitychange', function() {
  if (document.hidden) {
    console.log('User switched away from this tab');
    pauseAnimation();
  } else {
    console.log('User came back to this tab');
    resumeAnimation();
  }
});
```

### Key Properties and Events

| Property/Event | Description |
|---------------|-------------|
| `document.hidden` | Boolean - `true` if page is hidden |
| `document.visibilityState` | String - 'visible', 'hidden', or 'prerender' |
| `visibilitychange` event | Fired when visibility changes |

---

## Examples

### Example 1: Pause Video When Tab is Hidden

**Scenario:** Automatically pause video playback when users switch tabs

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Auto-Pause Video</title>
</head>
<body>
  <h1>Video Auto-Pause Demo</h1>
  <p>Switch tabs to see the video pause automatically</p>

  <video id="video" controls width="640">
    <source src="sample.mp4" type="video/mp4">
  </video>

  <div id="status"></div>

  <script>
    const video = document.getElementById('video');
    const status = document.getElementById('status');

    document.addEventListener('visibilitychange', function() {
      if (document.hidden) {
        if (!video.paused) {
          video.pause();
          status.textContent = '⏸️ Video paused (tab hidden)';
        }
      } else {
        status.textContent = '✅ Tab visible - you can play the video';
      }
    });
  </script>
</body>
</html>
```

**Result:** Video automatically pauses when you switch tabs, saving bandwidth and battery.

---

### Example 2: Pause Animations and Timers

**Scenario:** Stop resource-intensive animations when page isn't visible

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Animation Optimization</title>
  <style>
    .ball {
      width: 50px;
      height: 50px;
      background: #2196F3;
      border-radius: 50%;
      position: absolute;
      transition: transform 0.3s;
    }
    .container {
      position: relative;
      width: 600px;
      height: 400px;
      border: 2px solid #ddd;
      margin: 20px auto;
      overflow: hidden;
    }
  </style>
</head>
<body>
  <h1>Bouncing Ball Animation</h1>
  <p>Animation pauses when you switch tabs</p>

  <div class="container">
    <div class="ball" id="ball"></div>
  </div>

  <div id="status">Status: <span id="state">Active</span></div>
  <div>Frame count: <span id="frameCount">0</span></div>

  <script>
    const ball = document.getElementById('ball');
    const stateSpan = document.getElementById('state');
    const frameCountSpan = document.getElementById('frameCount');

    let x = 0, y = 0;
    let dx = 2, dy = 3;
    let animationId;
    let frameCount = 0;

    function animate() {
      frameCount++;
      frameCountSpan.textContent = frameCount;

      // Update ball position
      x += dx;
      y += dy;

      // Bounce off walls
      if (x >= 550 || x <= 0) dx = -dx;
      if (y >= 350 || y <= 0) dy = -dy;

      ball.style.transform = `translate(${x}px, ${y}px)`;

      animationId = requestAnimationFrame(animate);
    }

    function startAnimation() {
      if (!animationId) {
        animationId = requestAnimationFrame(animate);
        stateSpan.textContent = 'Active ✅';
        stateSpan.style.color = 'green';
      }
    }

    function stopAnimation() {
      if (animationId) {
        cancelAnimationFrame(animationId);
        animationId = null;
        stateSpan.textContent = 'Paused ⏸️';
        stateSpan.style.color = 'orange';
      }
    }

    // Handle visibility changes
    document.addEventListener('visibilitychange', function() {
      if (document.hidden) {
        stopAnimation();
      } else {
        startAnimation();
      }
    });

    // Start animation initially
    startAnimation();
  </script>
</body>
</html>
```

**Result:** The ball animation stops when you switch tabs, conserving CPU resources.

---

### Example 3: Notifications for Background Updates

**Scenario:** Notify users of new messages when they're on another tab

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Background Notifications</title>
</head>
<body>
  <h1>Message Dashboard</h1>
  <p>Switch tabs to see title notifications for new messages</p>

  <div id="messages"></div>

  <script>
    const messagesDiv = document.getElementById('messages');
    let originalTitle = document.title;
    let newMessageCount = 0;
    let titleInterval;

    // Simulate receiving new messages
    setInterval(() => {
      const message = `Message ${Date.now().toString().slice(-4)}`;
      addMessage(message);

      // If page is hidden, notify via title
      if (document.hidden) {
        newMessageCount++;
        notifyInTitle();
      }
    }, 5000);

    function addMessage(text) {
      const msg = document.createElement('div');
      msg.style.padding = '10px';
      msg.style.margin = '5px 0';
      msg.style.background = '#e3f2fd';
      msg.style.borderRadius = '5px';
      msg.textContent = `[${new Date().toLocaleTimeString()}] ${text}`;
      messagesDiv.prepend(msg);
    }

    function notifyInTitle() {
      // Flash title with message count
      if (!titleInterval) {
        titleInterval = setInterval(() => {
          document.title = document.title === originalTitle
            ? `(${newMessageCount}) New messages!`
            : originalTitle;
        }, 1000);
      }
    }

    function resetTitleNotification() {
      clearInterval(titleInterval);
      titleInterval = null;
      document.title = originalTitle;
      newMessageCount = 0;
    }

    // Handle visibility changes
    document.addEventListener('visibilitychange', function() {
      if (!document.hidden) {
        // User came back to tab - reset notifications
        resetTitleNotification();
      }
    });
  </script>
</body>
</html>
```

**Result:** When on another tab, the page title flashes to notify you of new messages.

---

## Common Use Cases

### Use Case 1: Video/Audio Players
**When:** Pause media when users switch tabs
**How:**
```javascript
document.addEventListener('visibilitychange', () => {
  if (document.hidden) {
    videoElement.pause();
  }
});
```
**Why:** Saves bandwidth, improves battery life, prevents audio from multiple tabs.

---

### Use Case 2: Games
**When:** Pause game loops when tab is hidden
**How:**
```javascript
document.addEventListener('visibilitychange', () => {
  if (document.hidden) {
    game.pause();
  } else {
    game.resume();
  }
});
```
**Why:** Prevents unfair gameplay and conserves resources.

---

### Use Case 3: Analytics
**When:** Track time users actually spend viewing your page
**How:**
```javascript
let visibleTime = 0;
let startTime = Date.now();

document.addEventListener('visibilitychange', () => {
  if (document.hidden) {
    visibleTime += Date.now() - startTime;
  } else {
    startTime = Date.now();
  }
});
```
**Why:** Provides accurate engagement metrics (not just tab-open time).

---

## Browser Support

| Browser | Version | Support Level |
|---------|---------|---------------|
| Chrome  | 33+     | Full Support  |
| Firefox | 18+     | Full Support  |
| Safari  | 7+      | Full Support  |
| Edge    | All     | Full Support  |
| IE      | 10+     | Full Support  |

**Fallback Strategy:**
```javascript
if (typeof document.hidden !== 'undefined') {
  // Use Page Visibility API
  document.addEventListener('visibilitychange', handleVisibilityChange);
} else {
  // Fallback: use blur/focus events
  window.addEventListener('blur', handlePageHidden);
  window.addEventListener('focus', handlePageVisible);
}
```

**Can I Use Link:** [https://caniuse.com/pagevisibility](https://caniuse.com/pagevisibility)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Don't rely solely on visibility changes for critical functionality
- Ensure paused content can be manually resumed

**Level AA Requirements:**
- Provide visible indicators when content is auto-paused
- Allow users to disable auto-pause behavior

### Screen Reader Support

**Key Points:**
- Visibility changes don't affect screen readers directly
- Ensure status changes (paused/playing) are announced
- Use ARIA live regions for important state changes

---

## Best Practices

### Do This

1. **Pause Expensive Operations**
   ```javascript
   document.addEventListener('visibilitychange', () => {
     if (document.hidden) {
       stopPollingAPI();
       pauseAnimations();
     } else {
       resumePollingAPI();
       resumeAnimations();
     }
   });
   ```
   **Why:** Conserves battery, reduces server load, improves performance.

2. **Track Actual Viewing Time**
   ```javascript
   let activeTime = 0;
   let sessionStart = Date.now();

   document.addEventListener('visibilitychange', () => {
     if (document.hidden) {
       activeTime += Date.now() - sessionStart;
     } else {
       sessionStart = Date.now();
     }
   });
   ```
   **Why:** Provides accurate analytics about user engagement.

---

### Avoid This

1. **Don't Assume Hidden = User Left**
   ```javascript
   // ❌ WRONG - User might come back
   document.addEventListener('visibilitychange', () => {
     if (document.hidden) {
       logout(); // Too aggressive!
     }
   });
   ```
   **Why Not:** Hidden just means background tab—user might return immediately.
   **Instead:** Use a timeout or save state for later.

---

## Related Topics

**Prerequisites (Learn These First):**
- [JavaScript Events](../01-fundamentals/javascript-basics.md)

**Related Concepts:**
- [Web Workers](web-workers.md) - Continue background tasks
- [Online/Offline Detection](online-offline.md) - Network status

**External Resources:**
- [MDN Web Docs - Page Visibility API](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API)

---

## Practice Exercise

### Challenge: Build an Auto-Pausing Slideshow

**Objective:** Create a slideshow that automatically pauses when the tab is hidden.

**Requirements:**
- [ ] Display images that change every 3 seconds
- [ ] Pause slideshow when tab is hidden
- [ ] Resume when tab becomes visible
- [ ] Show current state (playing/paused)

---

### Expected Result

**Key Learnings:**
- How to detect page visibility changes
- Optimizing performance by pausing background tasks
- Improving battery life and user experience

---

## Navigation

**Previous:** [Fullscreen API](fullscreen.md)
**Next:** [Online/Offline Detection](online-offline.md)
**Up:** [Back to HTML5 APIs](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** HTML5 APIs
**Difficulty:** Beginner
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
