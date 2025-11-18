---
title: Server-Sent Events (SSE)
category: HTML5 APIs
order: 5
---

# Server-Sent Events (SSE)

> **Quick Summary:** Server-Sent Events enable servers to push real-time updates to web clients over a single HTTP connection, perfect for live notifications, stock tickers, news feeds, and real-time dashboards.

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

Server-Sent Events (SSE) is an HTML5 API that allows servers to push data to web pages over HTTP. Unlike traditional polling (where the client repeatedly asks "any updates?"), SSE establishes a persistent connection where the server sends updates whenever they're available.

**The Problem:** Real-time applications need constant updates (stock prices, notifications, live scores). Traditional polling wastes bandwidth and causes delays. WebSockets are overkill for one-way communication.

**The Solution:** SSE provides automatic reconnection, event IDs, and a simple text-based protocol. It works over standard HTTP/HTTPS, passes through most firewalls, and is much simpler than WebSockets for server-to-client updates.

**Key Concept:** SSE is **unidirectional** (server → client only). For two-way communication, use WebSockets. For simple real-time updates, SSE is perfect.

---

## Basic Syntax

### Client-Side (JavaScript)

```javascript
// Create EventSource connection
const eventSource = new EventSource('/api/events');

// Listen for messages
eventSource.onmessage = function(event) {
  console.log('New message:', event.data);
};

// Listen for specific event types
eventSource.addEventListener('userConnected', function(event) {
  const data = JSON.parse(event.data);
  console.log('User connected:', data.username);
});

// Handle connection open
eventSource.onopen = function() {
  console.log('Connection established');
};

// Handle errors
eventSource.onerror = function(error) {
  console.error('EventSource error:', error);
  // Browser automatically reconnects
};

// Close connection when done
eventSource.close();
```

### Server-Side Response Format

```
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive

data: This is a simple message

data: {"user": "John", "message": "Hello"}

event: userConnected
data: {"username": "Jane", "id": 123}

id: 42
event: stockUpdate
data: {"symbol": "AAPL", "price": 150.25}
retry: 10000

: This is a comment (ignored by clients)
```

### Key Properties and Methods

| Property/Method | Description |
|----------------|-------------|
| `new EventSource(url)` | Creates connection to SSE endpoint |
| `onmessage` | Handler for messages without explicit event type |
| `addEventListener(type, handler)` | Listen for specific event types |
| `onopen` | Called when connection opens |
| `onerror` | Called on errors (auto-reconnects) |
| `close()` | Closes the connection permanently |
| `readyState` | 0 (CONNECTING), 1 (OPEN), 2 (CLOSED) |
| `url` | The connected URL |
| `withCredentials` | Boolean for CORS with credentials |

---

## Examples

### Example 1: Real-Time Notifications

**Scenario:** Display live notifications to users (new messages, alerts, updates)

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Live Notifications</title>
  <style>
    .notification {
      padding: 15px;
      margin: 10px 0;
      border-radius: 5px;
      background: #e3f2fd;
      border-left: 4px solid #2196F3;
      animation: slideIn 0.3s ease;
    }
    @keyframes slideIn {
      from { transform: translateX(-100%); opacity: 0; }
      to { transform: translateX(0); opacity: 1; }
    }
    .status {
      padding: 10px;
      background: #f5f5f5;
      border-radius: 5px;
      margin-bottom: 10px;
    }
    .status.connected { background: #c8e6c9; }
    .status.disconnected { background: #ffcdd2; }
  </style>
</head>
<body>
  <h1>Live Notification Dashboard</h1>

  <div class="status" id="status">Connecting...</div>
  <div id="notifications"></div>

  <script>
    const statusDiv = document.getElementById('status');
    const notificationsDiv = document.getElementById('notifications');

    // Connect to SSE endpoint
    const eventSource = new EventSource('/api/notifications');

    eventSource.onopen = function() {
      statusDiv.textContent = 'Connected - Listening for notifications';
      statusDiv.className = 'status connected';
    };

    eventSource.onmessage = function(event) {
      const data = JSON.parse(event.data);
      addNotification(data.message, data.type);
    };

    eventSource.onerror = function() {
      statusDiv.textContent = 'Disconnected - Reconnecting...';
      statusDiv.className = 'status disconnected';
    };

    function addNotification(message, type = 'info') {
      const notification = document.createElement('div');
      notification.className = 'notification';
      notification.textContent = `[${new Date().toLocaleTimeString()}] ${message}`;
      notificationsDiv.prepend(notification);

      // Remove after 10 seconds
      setTimeout(() => notification.remove(), 10000);
    }

    // Clean up on page unload
    window.addEventListener('beforeunload', () => {
      eventSource.close();
    });
  </script>
</body>
</html>
```

**Server-Side (Node.js/Express Example):**
```javascript
app.get('/api/notifications', (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  res.setHeader('Cache-Control', 'no-cache');
  res.setHeader('Connection', 'keep-alive');

  // Send initial connection message
  res.write('data: {"message": "Connected to notification service", "type": "info"}\n\n');

  // Simulate notifications every 5 seconds
  const intervalId = setInterval(() => {
    const notifications = [
      'New message from John',
      'Your report is ready',
      'Server backup completed',
      'System update available'
    ];

    const message = notifications[Math.floor(Math.random() * notifications.length)];
    res.write(`data: ${JSON.stringify({ message, type: 'info' })}\n\n`);
  }, 5000);

  // Clean up when client disconnects
  req.on('close', () => {
    clearInterval(intervalId);
    res.end();
  });
});
```

**Result:** Notifications appear automatically as the server sends them, with smooth animations and automatic reconnection if the connection drops.

---

### Example 2: Live Stock Ticker

**Scenario:** Display real-time stock prices that update automatically

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Stock Ticker</title>
  <style>
    .stock-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      padding: 20px;
    }
    .stock-card {
      padding: 20px;
      border-radius: 8px;
      background: white;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
    .symbol { font-size: 1.5em; font-weight: bold; }
    .price { font-size: 2em; margin: 10px 0; }
    .change { font-weight: bold; }
    .change.up { color: #4CAF50; }
    .change.down { color: #f44336; }
  </style>
</head>
<body>
  <h1>Live Stock Market</h1>
  <div class="stock-grid" id="stockGrid"></div>

  <script>
    const stockGrid = document.getElementById('stockGrid');
    const stocks = new Map();

    const eventSource = new EventSource('/api/stocks');

    eventSource.addEventListener('stockUpdate', function(event) {
      const data = JSON.parse(event.data);
      updateStock(data);
    });

    function updateStock({ symbol, price, change, changePercent }) {
      let stockCard = stocks.get(symbol);

      if (!stockCard) {
        stockCard = createStockCard(symbol);
        stocks.set(symbol, stockCard);
        stockGrid.appendChild(stockCard);
      }

      const priceEl = stockCard.querySelector('.price');
      const changeEl = stockCard.querySelector('.change');

      priceEl.textContent = `$${price.toFixed(2)}`;
      changeEl.textContent = `${change >= 0 ? '+' : ''}${change.toFixed(2)} (${changePercent.toFixed(2)}%)`;
      changeEl.className = `change ${change >= 0 ? 'up' : 'down'}`;

      // Highlight animation
      stockCard.style.background = change >= 0 ? '#e8f5e9' : '#ffebee';
      setTimeout(() => { stockCard.style.background = 'white'; }, 500);
    }

    function createStockCard(symbol) {
      const card = document.createElement('div');
      card.className = 'stock-card';
      card.innerHTML = `
        <div class="symbol">${symbol}</div>
        <div class="price">--</div>
        <div class="change">--</div>
      `;
      return card;
    }
  </script>
</body>
</html>
```

**Result:** Stock prices update in real-time with visual feedback (green for gains, red for losses), and cards animate when prices change.

---

### Example 3: Server Progress Monitoring

**Scenario:** Monitor a long-running server task (file upload, data processing, build process)

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Server Task Monitor</title>
  <style>
    .progress-container {
      max-width: 600px;
      margin: 20px auto;
      padding: 20px;
      background: white;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    .progress-bar {
      width: 100%;
      height: 30px;
      background: #e0e0e0;
      border-radius: 15px;
      overflow: hidden;
      margin: 15px 0;
    }
    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #2196F3, #21CBF3);
      width: 0%;
      transition: width 0.5s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
    }
    .log {
      background: #f5f5f5;
      padding: 10px;
      border-radius: 5px;
      max-height: 200px;
      overflow-y: auto;
      font-family: monospace;
      font-size: 0.9em;
    }
    .log-entry {
      padding: 3px 0;
      border-bottom: 1px solid #ddd;
    }
  </style>
</head>
<body>
  <div class="progress-container">
    <h2>Data Processing Task</h2>
    <div id="status">Waiting to start...</div>

    <div class="progress-bar">
      <div class="progress-fill" id="progressBar">0%</div>
    </div>

    <button id="startBtn">Start Processing</button>

    <h3>Activity Log:</h3>
    <div class="log" id="log"></div>
  </div>

  <script>
    const progressBar = document.getElementById('progressBar');
    const status = document.getElementById('status');
    const log = document.getElementById('log');
    const startBtn = document.getElementById('startBtn');

    startBtn.addEventListener('click', () => {
      startBtn.disabled = true;
      const eventSource = new EventSource('/api/process-data');

      eventSource.addEventListener('progress', function(event) {
        const data = JSON.parse(event.data);
        progressBar.style.width = data.percent + '%';
        progressBar.textContent = data.percent + '%';
        status.textContent = data.message;
        addLogEntry(data.message);
      });

      eventSource.addEventListener('complete', function(event) {
        const data = JSON.parse(event.data);
        status.textContent = 'Processing complete!';
        addLogEntry('✓ Task completed successfully');
        eventSource.close();
        startBtn.disabled = false;
      });

      eventSource.addEventListener('error', function(event) {
        const data = JSON.parse(event.data);
        status.textContent = 'Error: ' + data.message;
        addLogEntry('✗ Error: ' + data.message);
        eventSource.close();
        startBtn.disabled = false;
      });
    });

    function addLogEntry(message) {
      const entry = document.createElement('div');
      entry.className = 'log-entry';
      entry.textContent = `[${new Date().toLocaleTimeString()}] ${message}`;
      log.prepend(entry);
    }
  </script>
</body>
</html>
```

**Result:** Real-time progress bar and activity log showing server task progress without polling.

**Notes:**
- The server sends custom event types (`progress`, `complete`, `error`)
- Automatic reconnection isn't desired here, so we manually `close()` when done
- Perfect for file uploads, batch processing, or CI/CD build monitoring

---

## Common Use Cases

### Use Case 1: Live News/Social Media Feeds
**When:** Displaying real-time updates from social platforms, news sites, or activity streams
**How:**
```javascript
const eventSource = new EventSource('/api/feed');
eventSource.onmessage = (e) => {
  const post = JSON.parse(e.data);
  prependPost(post);
};
```
**Why:** Users see new content immediately without refreshing, improving engagement.

---

### Use Case 2: IoT Sensor Data
**When:** Displaying live data from sensors (temperature, humidity, traffic, etc.)
**How:**
```javascript
const eventSource = new EventSource('/api/sensors');
eventSource.addEventListener('sensorUpdate', (e) => {
  const { sensorId, value, timestamp } = JSON.parse(e.data);
  updateSensorDisplay(sensorId, value);
});
```
**Why:** Continuous monitoring without polling reduces server load and provides real-time insights.

---

### Use Case 3: Admin Dashboards
**When:** Monitoring server health, user activity, system metrics
**How:**
```javascript
const eventSource = new EventSource('/api/metrics');
eventSource.addEventListener('cpuUsage', (e) => updateCPUChart(e.data));
eventSource.addEventListener('memoryUsage', (e) => updateMemoryChart(e.data));
eventSource.addEventListener('activeUsers', (e) => updateUserCount(e.data));
```
**Why:** Real-time dashboards help admins respond quickly to issues without constant page refreshing.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 6+      | Full Support  | Excellent support since 2010 |
| Firefox | 6+      | Full Support  | Full support |
| Safari  | 5+      | Full Support  | iOS Safari 4+ |
| Edge    | All     | Full Support  | Including legacy Edge 79+ |
| IE      | -       | No Support    | Use polyfill or fallback to polling |

**Fallback Strategy:**
```javascript
if (typeof EventSource !== 'undefined') {
  const eventSource = new EventSource('/api/events');
} else {
  // Fallback to polling for IE
  setInterval(() => {
    fetch('/api/latest-events')
      .then(res => res.json())
      .then(data => processEvents(data));
  }, 5000);
}
```

**Can I Use Link:** [https://caniuse.com/eventsource](https://caniuse.com/eventsource)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Ensure live updates don't disrupt screen reader navigation
- Provide controls to pause/stop live updates

**Level AA Requirements:**
- Use ARIA live regions for announcing updates
- Allow users to control update frequency or disable them entirely

### Screen Reader Support

```html
<!-- Use ARIA live regions for SSE updates -->
<div aria-live="polite" aria-atomic="true" id="liveRegion">
  <span class="sr-only">Live updates:</span>
  <div id="latestUpdate"></div>
</div>

<script>
  const eventSource = new EventSource('/api/events');
  eventSource.onmessage = function(event) {
    const liveRegion = document.getElementById('latestUpdate');
    liveRegion.textContent = event.data;
  };
</script>
```

**Key Points:**
- Use `aria-live="polite"` to avoid interrupting screen readers
- Use `aria-live="assertive"` only for critical alerts
- Provide a "Pause updates" button for users who need time to process content
- Visually indicate when live updates are active

### Keyboard Navigation

- **Escape:** Should pause live updates
- **Space/Enter:** Resume updates if paused
- **Tab:** Must navigate normally even during rapid updates

```javascript
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    eventSource.close();
    showPausedIndicator();
  }
});
```

---

## Best Practices

### Do This

1. **Always Set Proper Headers**
   ```javascript
   // Server-side (Node.js/Express)
   res.setHeader('Content-Type', 'text/event-stream');
   res.setHeader('Cache-Control', 'no-cache');
   res.setHeader('Connection', 'keep-alive');
   res.setHeader('X-Accel-Buffering', 'no'); // Disable nginx buffering
   ```
   **Why:** Without these headers, proxies and browsers may buffer the response, breaking real-time updates.

2. **Use Event IDs for Resumption**
   ```javascript
   // Server sends
   id: 1234
   data: {"message": "Update"}

   // Client automatically sends Last-Event-ID header on reconnect
   app.get('/api/events', (req, res) => {
     const lastEventId = req.headers['last-event-id'];
     // Send only events after lastEventId
   });
   ```
   **Why:** Prevents missing updates if the connection briefly drops.

3. **Handle Reconnection Logic**
   ```javascript
   const eventSource = new EventSource('/api/events');

   eventSource.onerror = function() {
     if (eventSource.readyState === EventSource.CLOSED) {
       console.log('Connection lost, attempting to reconnect...');
       // Browser automatically reconnects after 3 seconds
     }
   };
   ```
   **Why:** Browsers auto-reconnect, but you should provide user feedback during outages.

4. **Close Connections Properly**
   ```javascript
   window.addEventListener('beforeunload', () => {
     eventSource.close();
   });

   // Or after specific events
   eventSource.addEventListener('sessionEnd', () => {
     eventSource.close();
   });
   ```
   **Why:** Prevents orphaned connections that waste server resources.

---

### Avoid This

1. **Don't Forget CORS Headers**
   ```javascript
   // ❌ WRONG - Cross-origin SSE will fail
   res.setHeader('Content-Type', 'text/event-stream');

   // ✅ CORRECT
   res.setHeader('Access-Control-Allow-Origin', 'https://example.com');
   res.setHeader('Access-Control-Allow-Credentials', 'true');
   ```
   **Why Not:** SSE respects CORS. Cross-origin requests fail without proper headers.
   **Instead:** Set CORS headers on the server.

2. **Don't Send Huge Messages**
   ```javascript
   // ❌ WRONG - Sending 10MB JSON
   res.write(`data: ${JSON.stringify(hugeObject)}\n\n`);

   // ✅ CORRECT - Send paginated or summarized data
   res.write(`data: ${JSON.stringify(summary)}\n\n`);
   ```
   **Why Not:** SSE is for frequent small updates, not large payloads.
   **Instead:** Use chunked file downloads or fetch API for large data.

3. **Don't Use SSE for Two-Way Communication**
   ```javascript
   // ❌ WRONG - Trying to send data to server via EventSource
   eventSource.send('message'); // This doesn't exist!

   // ✅ CORRECT - Use WebSockets for bidirectional
   const socket = new WebSocket('ws://example.com');
   socket.send('message');
   ```
   **Why Not:** SSE is server → client only.
   **Instead:** Use WebSockets or combine SSE with fetch/AJAX for client → server.

---

## Related Topics

**Prerequisites (Learn These First):**
- [JavaScript Fetch API](../01-fundamentals/javascript-basics.md) - Understanding async JS
- [JSON](../05-semantic-html5/metadata-tags.md) - Data format used with SSE

**Related Concepts:**
- [Web Workers](web-workers.md) - Can use SSE inside workers for background updates
- [Web Storage](web-storage.md) - Store received events locally
- [Online/Offline Detection](online-offline.md) - Detect when SSE might fail

**Next Steps (Learn These Next):**
- [WebSockets](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket) - Two-way real-time communication
- [Push API](https://developer.mozilla.org/en-US/docs/Web/API/Push_API) - Server push notifications

**External Resources:**
- [MDN Web Docs - Server-Sent Events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)
- [HTML Living Standard - SSE](https://html.spec.whatwg.org/multipage/server-sent-events.html)
- [EventSource API Specification](https://www.w3.org/TR/eventsource/)

---

## Practice Exercise

### Challenge: Build a Live Chat System

**Objective:** Create a simple live chat application where messages from the server appear in real-time using SSE.

**Requirements:**
- [ ] Display incoming messages in a chat window
- [ ] Show connection status (connected/disconnected)
- [ ] Auto-scroll to newest messages
- [ ] Display timestamps for each message
- [ ] Bonus: Add message categorization (system messages vs. user messages)

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Live Chat</title>
  <style>
    .chat-container {
      max-width: 600px;
      margin: 20px auto;
      border: 1px solid #ddd;
      border-radius: 8px;
      overflow: hidden;
    }
    .chat-header {
      padding: 15px;
      background: #2196F3;
      color: white;
    }
    .chat-messages {
      height: 400px;
      overflow-y: auto;
      padding: 15px;
      background: #f9f9f9;
    }
    .message {
      margin: 10px 0;
      padding: 10px;
      border-radius: 5px;
      background: white;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="chat-header">
      <h2>Live Chat</h2>
      <div id="status">Connecting...</div>
    </div>
    <div class="chat-messages" id="messages"></div>
  </div>

  <!-- Add your JavaScript here -->
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**Client-Side (HTML + JavaScript):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Live Chat</title>
  <style>
    .chat-container {
      max-width: 600px;
      margin: 20px auto;
      border: 1px solid #ddd;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    .chat-header {
      padding: 15px;
      background: #2196F3;
      color: white;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .status { font-size: 0.9em; }
    .status.connected::before { content: '● '; color: #4CAF50; }
    .status.disconnected::before { content: '● '; color: #f44336; }
    .chat-messages {
      height: 400px;
      overflow-y: auto;
      padding: 15px;
      background: #f9f9f9;
    }
    .message {
      margin: 10px 0;
      padding: 10px;
      border-radius: 5px;
      background: white;
      box-shadow: 0 1px 3px rgba(0,0,0,0.1);
    }
    .message.system {
      background: #fff3cd;
      border-left: 3px solid #ffc107;
    }
    .message-time {
      font-size: 0.8em;
      color: #666;
    }
    .message-user {
      font-weight: bold;
      color: #2196F3;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <div class="chat-header">
      <h2>Live Chat</h2>
      <div class="status disconnected" id="status">Connecting...</div>
    </div>
    <div class="chat-messages" id="messages"></div>
  </div>

  <script>
    const messagesDiv = document.getElementById('messages');
    const statusDiv = document.getElementById('status');

    const eventSource = new EventSource('/api/chat');

    eventSource.onopen = function() {
      statusDiv.textContent = 'Connected';
      statusDiv.className = 'status connected';
    };

    eventSource.addEventListener('message', function(event) {
      const data = JSON.parse(event.data);
      addMessage(data.user, data.text, 'user');
    });

    eventSource.addEventListener('system', function(event) {
      const data = JSON.parse(event.data);
      addMessage('System', data.text, 'system');
    });

    eventSource.onerror = function() {
      statusDiv.textContent = 'Disconnected';
      statusDiv.className = 'status disconnected';
    };

    function addMessage(user, text, type = 'user') {
      const message = document.createElement('div');
      message.className = `message ${type}`;

      const time = new Date().toLocaleTimeString();
      message.innerHTML = `
        <div class="message-user">${user}</div>
        <div>${text}</div>
        <div class="message-time">${time}</div>
      `;

      messagesDiv.appendChild(message);
      messagesDiv.scrollTop = messagesDiv.scrollHeight; // Auto-scroll
    }
  </script>
</body>
</html>
```

**Server-Side (Node.js/Express):**
```javascript
app.get('/api/chat', (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  res.setHeader('Cache-Control', 'no-cache');
  res.setHeader('Connection', 'keep-alive');

  // Welcome message
  res.write('event: system\n');
  res.write(`data: ${JSON.stringify({ text: 'Welcome to the chat!' })}\n\n`);

  // Simulate chat messages
  const messages = [
    { user: 'Alice', text: 'Hey everyone!' },
    { user: 'Bob', text: 'Hi Alice, how are you?' },
    { user: 'Charlie', text: 'Anyone up for lunch?' },
  ];

  let index = 0;
  const intervalId = setInterval(() => {
    if (index < messages.length) {
      res.write(`data: ${JSON.stringify(messages[index])}\n\n`);
      index++;
    }
  }, 3000);

  req.on('close', () => {
    clearInterval(intervalId);
    res.end();
  });
});
```

**Explanation:**
This chat system uses SSE to push messages from the server to all connected clients. The server sends two event types: `message` (regular chat) and `system` (announcements). The client automatically reconnects if the connection drops, and messages auto-scroll as they arrive.

</details>

---

### Expected Result

**Visual Outcome:**
- Messages appear automatically as the server sends them
- Connection status shows "Connected" (green) or "Disconnected" (red)
- Chat window auto-scrolls to show latest messages
- System messages are visually distinct from user messages

**Key Learnings:**
- How to establish and maintain SSE connections
- Using custom event types for different message categories
- Proper error handling and connection status feedback
- Real-world application: Live chat, notifications, dashboards

---

## Navigation

**Previous:** [Web Workers](web-workers.md)
**Next:** [History API](history-api.md)
**Up:** [Back to HTML5 APIs](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** HTML5 APIs
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
