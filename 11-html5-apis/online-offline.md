---
title: Online/Offline Detection
category: HTML5 APIs
order: 9
---

# Online/Offline Detection

> **Quick Summary:** The Online/Offline Detection API allows web applications to detect network connectivity changes, enabling better offline experiences and graceful handling of network failures.

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

The Online/Offline Detection API provides a simple way to detect whether the browser has network connectivity. This enables applications to adapt their behavior based on connection status.

**The Problem:** Users expect apps to work offline or handle network failures gracefully. Without connectivity detection, apps can't warn users, queue actions, or switch to offline mode.

**The Solution:** The `navigator.onLine` property and `online`/`offline` events tell you when the browser loses or regains connectivity.

**Key Concept:** `navigator.onLine` only tells you if the browser thinks it has connectivity—it doesn't guarantee internet access. A browser connected to a router without internet will still report `onLine: true`.

---

## Basic Syntax

### Checking Current Status

```javascript
// Check if browser is online
if (navigator.onLine) {
  console.log('Online - has network connection');
} else {
  console.log('Offline - no network connection');
}
```

### Listening for Connectivity Changes

```javascript
// Detect when browser goes online
window.addEventListener('online', function() {
  console.log('Connection restored!');
  syncPendingData();
});

// Detect when browser goes offline
window.addEventListener('offline', function() {
  console.log('Connection lost!');
  enableOfflineMode();
});
```

### Key Properties and Events

| Property/Event | Description |
|---------------|-------------|
| `navigator.onLine` | Boolean - `true` if browser thinks it's online |
| `online` event | Fired when browser gains connectivity |
| `offline` event | Fired when browser loses connectivity |

---

## Examples

### Example 1: Connection Status Indicator

**Scenario:** Display a visual indicator showing current connection status

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Connection Monitor</title>
  <style>
    .status-bar {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      padding: 10px;
      text-align: center;
      font-weight: bold;
      z-index: 1000;
      transition: all 0.3s;
    }
    .status-bar.online {
      background: #4CAF50;
      color: white;
    }
    .status-bar.offline {
      background: #f44336;
      color: white;
    }
    .content {
      margin-top: 60px;
      padding: 20px;
    }
  </style>
</head>
<body>
  <div class="status-bar" id="statusBar">
    <span id="statusText"></span>
  </div>

  <div class="content">
    <h1>Network Status Monitor</h1>
    <p>Try disconnecting your internet to see the status change.</p>
    <p>You can also use browser DevTools (F12) → Network tab → Toggle "Offline" mode.</p>
  </div>

  <script>
    const statusBar = document.getElementById('statusBar');
    const statusText = document.getElementById('statusText');

    function updateStatus() {
      if (navigator.onLine) {
        statusBar.className = 'status-bar online';
        statusText.textContent = '✓ Online - Connected to network';
      } else {
        statusBar.className = 'status-bar offline';
        statusText.textContent = '✗ Offline - No network connection';
      }
    }

    // Update on page load
    updateStatus();

    // Listen for connectivity changes
    window.addEventListener('online', updateStatus);
    window.addEventListener('offline', updateStatus);
  </script>
</body>
</html>
```

**Result:** A status bar at the top of the page shows green when online, red when offline, with automatic updates.

---

### Example 2: Form Data Queue System

**Scenario:** Queue form submissions when offline and sync when back online

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Offline Form Queue</title>
  <style>
    .form-container {
      max-width: 500px;
      margin: 20px auto;
      padding: 20px;
      border: 1px solid #ddd;
      border-radius: 8px;
    }
    .notification {
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      display: none;
    }
    .notification.show { display: block; }
    .notification.success { background: #d4edda; color: #155724; }
    .notification.warning { background: #fff3cd; color: #856404; }
    input, textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ddd;
      border-radius: 4px;
    }
    button {
      width: 100%;
      padding: 12px;
      background: #2196F3;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover { background: #1976D2; }
  </style>
</head>
<body>
  <div class="form-container">
    <h2>Contact Form (Offline-Ready)</h2>

    <div class="notification" id="notification"></div>

    <form id="contactForm">
      <input type="text" name="name" placeholder="Your Name" required>
      <input type="email" name="email" placeholder="Your Email" required>
      <textarea name="message" rows="5" placeholder="Your Message" required></textarea>
      <button type="submit">Send Message</button>
    </form>

    <div id="queueStatus"></div>
  </div>

  <script>
    const form = document.getElementById('contactForm');
    const notification = document.getElementById('notification');
    const queueStatus = document.getElementById('queueStatus');

    // Get queued items from localStorage
    function getQueue() {
      const queue = localStorage.getItem('formQueue');
      return queue ? JSON.parse(queue) : [];
    }

    // Save queue to localStorage
    function saveQueue(queue) {
      localStorage.setItem('formQueue', JSON.stringify(queue));
      updateQueueDisplay();
    }

    // Add form data to queue
    function queueFormData(formData) {
      const queue = getQueue();
      queue.push({
        data: formData,
        timestamp: new Date().toISOString()
      });
      saveQueue(queue);
    }

    // Send queued data to server
    async function processQueue() {
      const queue = getQueue();
      if (queue.length === 0) return;

      showNotification(`Syncing ${queue.length} queued submission(s)...`, 'warning');

      for (let i = 0; i < queue.length; i++) {
        try {
          await submitToServer(queue[i].data);
        } catch (error) {
          console.error('Failed to sync:', error);
          return; // Stop if any submission fails
        }
      }

      // Clear queue after successful sync
      localStorage.removeItem('formQueue');
      updateQueueDisplay();
      showNotification('All queued submissions synced!', 'success');
    }

    // Simulate server submission
    async function submitToServer(formData) {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          console.log('Submitted:', formData);
          resolve();
        }, 1000);
      });
    }

    // Handle form submission
    form.addEventListener('submit', async function(e) {
      e.preventDefault();

      const formData = {
        name: form.name.value,
        email: form.email.value,
        message: form.message.value
      };

      if (navigator.onLine) {
        try {
          await submitToServer(formData);
          showNotification('Message sent successfully!', 'success');
          form.reset();
        } catch (error) {
          showNotification('Failed to send. Queued for later.', 'warning');
          queueFormData(formData);
        }
      } else {
        queueFormData(formData);
        showNotification('Offline. Message queued for sending when online.', 'warning');
        form.reset();
      }
    });

    // Show notification
    function showNotification(message, type) {
      notification.textContent = message;
      notification.className = `notification show ${type}`;
      setTimeout(() => {
        notification.classList.remove('show');
      }, 5000);
    }

    // Update queue display
    function updateQueueDisplay() {
      const queue = getQueue();
      if (queue.length > 0) {
        queueStatus.innerHTML = `
          <p style="background: #fff3cd; padding: 10px; border-radius: 5px; margin-top: 15px;">
            📋 <strong>${queue.length}</strong> message(s) queued for sending
          </p>
        `;
      } else {
        queueStatus.innerHTML = '';
      }
    }

    // Handle online event
    window.addEventListener('online', function() {
      showNotification('Connection restored! Syncing queued data...', 'success');
      processQueue();
    });

    // Handle offline event
    window.addEventListener('offline', function() {
      showNotification('Connection lost. Form submissions will be queued.', 'warning');
    });

    // Initialize queue display
    updateQueueDisplay();
  </script>
</body>
</html>
```

**Result:** Form submissions are queued when offline and automatically synced when connection is restored.

---

### Example 3: Adaptive Content Loading

**Scenario:** Load different content based on connection status

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Adaptive Loading</title>
</head>
<body>
  <h1>Article Viewer</h1>
  <div id="content"></div>

  <script>
    const contentDiv = document.getElementById('content');

    async function loadContent() {
      if (navigator.onLine) {
        try {
          // Load high-quality content when online
          contentDiv.innerHTML = '<p>Loading latest articles...</p>';
          const response = await fetch('/api/articles');
          const articles = await response.json();
          displayArticles(articles);
        } catch (error) {
          loadCachedContent();
        }
      } else {
        loadCachedContent();
      }
    }

    function loadCachedContent() {
      contentDiv.innerHTML = `
        <div style="background: #fff3cd; padding: 15px; border-radius: 5px;">
          ⚠️ <strong>Offline Mode</strong><br>
          Showing cached content. Connect to internet for latest updates.
        </div>
        <p>Cached article content would appear here...</p>
      `;
    }

    function displayArticles(articles) {
      contentDiv.innerHTML = articles.map(article => `
        <div style="margin: 20px 0; padding: 15px; border: 1px solid #ddd; border-radius: 5px;">
          <h3>${article.title}</h3>
          <p>${article.content}</p>
        </div>
      `).join('');
    }

    // Load content on page load
    loadContent();

    // Reload when connection status changes
    window.addEventListener('online', loadContent);
    window.addEventListener('offline', loadContent);
  </script>
</body>
</html>
```

**Result:** Shows live content when online, cached content when offline.

---

## Common Use Cases

### Use Case 1: PWA Offline Support
**When:** Building Progressive Web Apps that work offline
**How:**
```javascript
window.addEventListener('offline', () => {
  showOfflineBanner();
  switchToServiceWorkerCache();
});
```
**Why:** Users expect modern web apps to work offline like native apps.

---

### Use Case 2: Real-Time Applications
**When:** Chat apps, collaborative editing, live dashboards
**How:**
```javascript
window.addEventListener('offline', () => {
  pauseRealTimeSync();
  queueLocalChanges();
});

window.addEventListener('online', () => {
  resumeRealTimeSync();
  syncQueuedChanges();
});
```
**Why:** Prevents errors and data loss during network interruptions.

---

### Use Case 3: E-commerce Checkout
**When:** Handling payment forms and order submissions
**How:**
```javascript
if (!navigator.onLine) {
  disableCheckoutButton();
  showOfflineWarning('Payment requires internet connection');
}
```
**Why:** Prevents failed transactions and improves user experience.

---

## Browser Support

| Browser | Version | Support Level |
|---------|---------|---------------|
| Chrome  | All     | Full Support  |
| Firefox | All     | Full Support  |
| Safari  | All     | Full Support  |
| Edge    | All     | Full Support  |
| IE      | 9+      | Full Support  |

**Can I Use Link:** [https://caniuse.com/online-status](https://caniuse.com/online-status)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Announce connection status changes to screen readers
- Provide text alternatives to visual indicators

### Screen Reader Support

```html
<div role="status" aria-live="polite" aria-atomic="true" id="connectionStatus">
  Connected to network
</div>

<script>
  window.addEventListener('offline', () => {
    document.getElementById('connectionStatus').textContent =
      'Connection lost. Working in offline mode.';
  });

  window.addEventListener('online', () => {
    document.getElementById('connectionStatus').textContent =
      'Connection restored.';
  });
</script>
```

---

## Best Practices

### Do This

1. **Verify with Actual Network Request**
   ```javascript
   async function checkRealConnectivity() {
     if (!navigator.onLine) return false;

     try {
       const response = await fetch('/ping', { method: 'HEAD' });
       return response.ok;
     } catch {
       return false;
     }
   }
   ```
   **Why:** `navigator.onLine` can report false positives.

2. **Provide Clear User Feedback**
   ```javascript
   window.addEventListener('offline', () => {
     showNotification('You are offline. Changes will be saved locally.');
   });
   ```
   **Why:** Users need to know how the app will behave offline.

3. **Implement Retry Logic**
   ```javascript
   async function submitWithRetry(data, maxRetries = 3) {
     for (let i = 0; i < maxRetries; i++) {
       if (navigator.onLine) {
         try {
           return await fetch('/api', { method: 'POST', body: data });
         } catch (error) {
           if (i === maxRetries - 1) throw error;
           await delay(1000 * Math.pow(2, i)); // Exponential backoff
         }
       }
     }
   }
   ```
   **Why:** Network issues are often temporary—retrying improves success rate.

---

### Avoid This

1. **Don't Trust `navigator.onLine` Completely**
   ```javascript
   // ❌ WRONG - Assumes onLine means internet access
   if (navigator.onLine) {
     submitPayment(); // Might fail if connected to router without internet
   }

   // ✅ CORRECT - Verify with actual request
   async function submitPayment() {
     try {
       const response = await fetch('/api/payment', { method: 'POST' });
       return response;
     } catch (error) {
       showError('Unable to process payment. Please check your connection.');
     }
   }
   ```
   **Why Not:** `navigator.onLine` only checks browser's connection to a network.
   **Instead:** Always handle fetch errors and verify connectivity.

---

## Related Topics

**Prerequisites (Learn These First):**
- [JavaScript Fetch API](../01-fundamentals/javascript-basics.md)
- [Local Storage](web-storage.md)

**Related Concepts:**
- [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) - Advanced offline caching
- [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) - Offline data storage

**External Resources:**
- [MDN Web Docs - Online/Offline Events](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/onLine)

---

## Practice Exercise

### Challenge: Build an Offline-Ready Note-Taking App

**Objective:** Create a note app that works offline and syncs when online.

**Requirements:**
- [ ] Save notes to localStorage
- [ ] Show connection status indicator
- [ ] Queue "sync to server" when offline
- [ ] Auto-sync when connection restored

---

### Expected Result

**Key Learnings:**
- How to detect online/offline status
- Building resilient applications that handle network failures
- Implementing data synchronization patterns

---

## Navigation

**Previous:** [Page Visibility API](page-visibility.md)
**Next:** [Video Formats](../12-multimedia-embedding/video-formats.md)
**Up:** [Back to HTML5 APIs](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** HTML5 APIs
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
