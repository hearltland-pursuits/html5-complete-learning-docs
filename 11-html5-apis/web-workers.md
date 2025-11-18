---
title: Web Workers API
category: HTML5 APIs
order: 4
---

# Web Workers API

> **Quick Summary:** Web Workers allow JavaScript to run in background threads, preventing heavy computations from freezing the user interface and enabling true multithreading in web applications.

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

Web Workers are a powerful HTML5 API that enables JavaScript to execute code in background threads, separate from the main browser thread. This is crucial for maintaining responsive user interfaces when performing computationally intensive tasks.

**The Problem:** JavaScript is single-threaded by default. Heavy operations (large data processing, complex calculations, image manipulation) block the main thread, causing the UI to freeze and creating a poor user experience.

**The Solution:** Web Workers run scripts in separate threads. They can't access the DOM directly, but they can perform calculations, process data, and communicate with the main thread via message passing.

**Key Concept:** Workers operate in complete isolation from the main thread. All communication happens through `postMessage()` and `onmessage` event handlers, using structured cloning to pass data.

---

## Basic Syntax

### Creating a Worker

**Main Script (main.js):**
```javascript
// Create a new worker from an external JavaScript file
const worker = new Worker('worker.js');

// Send data to the worker
worker.postMessage({ command: 'start', data: [1, 2, 3, 4, 5] });

// Receive messages from the worker
worker.onmessage = function(event) {
  console.log('Result from worker:', event.data);
};

// Handle errors
worker.onerror = function(error) {
  console.error('Worker error:', error.message);
};

// Terminate the worker when done
worker.terminate();
```

**Worker Script (worker.js):**
```javascript
// Listen for messages from the main thread
self.onmessage = function(event) {
  const { command, data } = event.data;

  if (command === 'start') {
    // Perform heavy computation
    const result = data.reduce((sum, num) => sum + num, 0);

    // Send result back to main thread
    self.postMessage(result);
  }
};
```

### Key Methods and Events

| Method/Event | Target | Description |
|--------------|--------|-------------|
| `new Worker(url)` | Main thread | Creates a new worker from a JavaScript file |
| `postMessage(data)` | Both | Sends a message to the other context |
| `onmessage` | Both | Event handler for receiving messages |
| `onerror` | Main thread | Handles errors from the worker |
| `terminate()` | Main thread | Immediately stops the worker |
| `close()` | Worker | Worker terminates itself |

### Communication Flow

```
Main Thread                    Worker Thread
     |                              |
     |--- postMessage(data) ------->|
     |                              |
     |                       [Processing]
     |                              |
     |<---- postMessage(result) ----|
     |                              |
```

---

## Examples

### Example 1: Simple Calculation Worker

**Scenario:** Calculate the sum of first N numbers without blocking the UI

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Web Worker Example</title>
</head>
<body>
  <div class="calculator">
    <input type="number" id="numberInput" value="1000000" placeholder="Enter a number">
    <button id="calculateBtn">Calculate Sum</button>
    <div id="result"></div>
    <div id="status">UI is responsive - try clicking this!</div>
  </div>

  <script src="main.js"></script>
</body>
</html>
```

**Main Script (main.js):**
```javascript
const calculateBtn = document.getElementById('calculateBtn');
const numberInput = document.getElementById('numberInput');
const resultDiv = document.getElementById('result');

calculateBtn.addEventListener('click', () => {
  const n = parseInt(numberInput.value);

  // Create worker
  const worker = new Worker('sum-worker.js');

  // Send data to worker
  worker.postMessage(n);

  // Receive result
  worker.onmessage = function(event) {
    resultDiv.textContent = `Sum of 1 to ${n} = ${event.data}`;
    worker.terminate(); // Clean up
  };

  worker.onerror = function(error) {
    resultDiv.textContent = `Error: ${error.message}`;
  };
});
```

**Worker Script (sum-worker.js):**
```javascript
self.onmessage = function(event) {
  const n = event.data;
  let sum = 0;

  // Heavy computation
  for (let i = 1; i <= n; i++) {
    sum += i;
  }

  // Send result back
  self.postMessage(sum);
};
```

**Result:** The calculation happens in the background, and the UI remains fully responsive. Users can interact with other page elements while the worker processes data.

---

### Example 2: Progress Updates with Shared Worker Communication

**Scenario:** Process a large dataset and provide real-time progress updates

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Worker with Progress</title>
  <style>
    .progress-bar {
      width: 100%;
      height: 30px;
      background: #eee;
      border-radius: 5px;
      overflow: hidden;
    }
    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #4CAF50, #45a049);
      width: 0%;
      transition: width 0.3s;
    }
  </style>
</head>
<body>
  <button id="startBtn">Process Data</button>
  <div class="progress-bar">
    <div class="progress-fill" id="progressBar"></div>
  </div>
  <div id="status"></div>

  <script>
    const startBtn = document.getElementById('startBtn');
    const progressBar = document.getElementById('progressBar');
    const status = document.getElementById('status');

    startBtn.addEventListener('click', () => {
      const worker = new Worker('progress-worker.js');

      worker.postMessage({ items: 1000 });

      worker.onmessage = function(event) {
        if (event.data.type === 'progress') {
          progressBar.style.width = event.data.percent + '%';
          status.textContent = `Processing: ${event.data.percent}%`;
        } else if (event.data.type === 'complete') {
          status.textContent = 'Processing complete!';
          worker.terminate();
        }
      };
    });
  </script>
</body>
</html>
```

**Worker Script (progress-worker.js):**
```javascript
self.onmessage = function(event) {
  const totalItems = event.data.items;

  for (let i = 0; i < totalItems; i++) {
    // Simulate processing
    const result = Math.sqrt(i) * Math.random();

    // Send progress every 10 items
    if (i % 10 === 0) {
      const percent = Math.round((i / totalItems) * 100);
      self.postMessage({ type: 'progress', percent });
    }
  }

  // Send completion message
  self.postMessage({ type: 'complete' });
};
```

**Result:** A smooth progress bar updates in real-time while the worker processes data, demonstrating non-blocking UI updates.

---

### Example 3: Image Processing Worker

**Scenario:** Apply filters to images without freezing the browser

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Image Processing Worker</title>
</head>
<body>
  <input type="file" id="imageInput" accept="image/*">
  <canvas id="canvas"></canvas>
  <button id="grayscaleBtn">Apply Grayscale</button>
  <button id="invertBtn">Invert Colors</button>

  <script>
    const imageInput = document.getElementById('imageInput');
    const canvas = document.getElementById('canvas');
    const ctx = canvas.getContext('2d');
    const worker = new Worker('image-worker.js');

    let imageData;

    imageInput.addEventListener('change', (e) => {
      const file = e.target.files[0];
      const img = new Image();

      img.onload = function() {
        canvas.width = img.width;
        canvas.height = img.height;
        ctx.drawImage(img, 0, 0);
        imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
      };

      img.src = URL.createObjectURL(file);
    });

    document.getElementById('grayscaleBtn').addEventListener('click', () => {
      worker.postMessage({ filter: 'grayscale', imageData });
    });

    document.getElementById('invertBtn').addEventListener('click', () => {
      worker.postMessage({ filter: 'invert', imageData });
    });

    worker.onmessage = function(event) {
      ctx.putImageData(event.data, 0, 0);
    };
  </script>
</body>
</html>
```

**Worker Script (image-worker.js):**
```javascript
self.onmessage = function(event) {
  const { filter, imageData } = event.data;
  const data = imageData.data;

  if (filter === 'grayscale') {
    for (let i = 0; i < data.length; i += 4) {
      const avg = (data[i] + data[i + 1] + data[i + 2]) / 3;
      data[i] = data[i + 1] = data[i + 2] = avg;
    }
  } else if (filter === 'invert') {
    for (let i = 0; i < data.length; i += 4) {
      data[i] = 255 - data[i];       // Red
      data[i + 1] = 255 - data[i + 1]; // Green
      data[i + 2] = 255 - data[i + 2]; // Blue
    }
  }

  self.postMessage(imageData);
};
```

**Result:** Image filters are applied without blocking the UI, even for large images.

**Notes:**
- ImageData is transferred using structured cloning (copies the data)
- For better performance, use Transferable Objects (covered in Best Practices)
- Workers can't access the DOM, so all Canvas manipulation happens in the main thread

---

## Common Use Cases

### Use Case 1: Large Data Processing
**When:** Processing JSON, CSV, or other large datasets that would block the UI
**How:**
```javascript
// Main thread
const worker = new Worker('data-processor.js');
worker.postMessage(largeDataArray);
worker.onmessage = (e) => displayResults(e.data);

// Worker (data-processor.js)
self.onmessage = (e) => {
  const processed = e.data.map(item => complexTransformation(item));
  self.postMessage(processed);
};
```
**Why:** Keeps the UI responsive while processing thousands or millions of records.

---

### Use Case 2: Real-Time Calculations
**When:** Financial calculations, physics simulations, game logic
**How:**
```javascript
// Main thread - game loop
const physicsWorker = new Worker('physics.js');
setInterval(() => {
  physicsWorker.postMessage(gameState);
}, 16); // 60 FPS

physicsWorker.onmessage = (e) => {
  updateGameObjects(e.data);
};

// Worker - physics calculations
self.onmessage = (e) => {
  const updatedState = calculatePhysics(e.data);
  self.postMessage(updatedState);
};
```
**Why:** Offloads heavy physics calculations, maintaining smooth 60 FPS rendering.

---

### Use Case 3: Background API Polling
**When:** Checking for updates, notifications, or status changes without user interaction
**How:**
```javascript
// Main thread
const pollingWorker = new Worker('poll-api.js');
pollingWorker.onmessage = (e) => {
  if (e.data.newMessages) {
    showNotification(e.data.newMessages);
  }
};

// Worker - polls every 30 seconds
setInterval(() => {
  fetch('https://api.example.com/messages')
    .then(res => res.json())
    .then(data => self.postMessage(data));
}, 30000);
```
**Why:** Background polling doesn't interfere with user interactions or animations.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 4+      | Full Support  | Excellent support since 2010 |
| Firefox | 3.5+    | Full Support  | Early adopter |
| Safari  | 4+      | Full Support  | iOS Safari 5+ |
| Edge    | All     | Full Support  | Including legacy Edge |
| IE      | 10+     | Full Support  | IE 10-11 only |

**Fallback Strategy:**
```javascript
if (typeof Worker !== 'undefined') {
  // Use Web Worker
  const worker = new Worker('worker.js');
} else {
  // Fallback to main thread
  console.warn('Web Workers not supported. Running on main thread.');
  performTaskOnMainThread();
}
```

**Can I Use Link:** [https://caniuse.com/webworkers](https://caniuse.com/webworkers)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Workers must not prevent keyboard navigation or screen reader functionality
- Progress updates from workers should be communicated to assistive technologies

**Level AA Requirements:**
- Provide alternative feedback mechanisms if worker operations are long-running
- Ensure timeout periods accommodate users who need more time

### Screen Reader Support

```html
<!-- Use ARIA live regions for worker status updates -->
<div id="workerStatus" aria-live="polite" aria-atomic="true">
  Processing...
</div>

<script>
  worker.onmessage = function(event) {
    const statusDiv = document.getElementById('workerStatus');
    statusDiv.textContent = event.data.message;
  };
</script>
```

**Key Points:**
- Workers themselves don't affect accessibility directly (they can't access DOM)
- How you display worker results matters: use semantic HTML and ARIA
- Provide visible feedback for all worker operations
- Never rely solely on visual indicators (e.g., spinners) without text alternatives

### Keyboard Navigation

- **Tab:** Must still work normally while worker is running
- **Escape:** Consider allowing users to cancel long-running worker operations
- **Enter/Space:** Interactive elements should remain functional during worker execution

---

## Best Practices

### Do This

1. **Use Transferable Objects for Large Data**
   ```javascript
   // Instead of copying, transfer ownership (much faster)
   const buffer = new ArrayBuffer(1024 * 1024); // 1MB
   worker.postMessage({ buffer }, [buffer]);
   // Note: buffer is now unusable in main thread
   ```
   **Why:** Transferring is nearly instantaneous, while cloning large data can take seconds.

2. **Terminate Workers When Finished**
   ```javascript
   worker.onmessage = function(event) {
     displayResults(event.data);
     worker.terminate(); // Free up memory
   };
   ```
   **Why:** Workers consume memory and CPU. Terminating them releases resources.

3. **Handle Errors Gracefully**
   ```javascript
   worker.onerror = function(error) {
     console.error('Worker error:', error);
     fallbackToMainThread();
   };

   // In worker
   try {
     riskyOperation();
   } catch (error) {
     self.postMessage({ error: error.message });
   }
   ```
   **Why:** Workers fail silently if you don't handle errors, making debugging difficult.

4. **Use Worker Pools for Repeated Tasks**
   ```javascript
   class WorkerPool {
     constructor(workerUrl, poolSize = 4) {
       this.workers = [];
       for (let i = 0; i < poolSize; i++) {
         this.workers.push(new Worker(workerUrl));
       }
       this.currentWorker = 0;
     }

     execute(data) {
       const worker = this.workers[this.currentWorker];
       this.currentWorker = (this.currentWorker + 1) % this.workers.length;
       worker.postMessage(data);
       return worker;
     }
   }
   ```
   **Why:** Reusing workers is more efficient than creating new ones repeatedly.

---

### Avoid This

1. **Don't Try to Access the DOM**
   ```javascript
   // ❌ WRONG - This will fail in worker
   self.onmessage = function() {
     document.getElementById('result').textContent = 'Done';
   };
   ```
   **Why Not:** Workers have no access to `window`, `document`, or `DOM` APIs.
   **Instead:** Send data back to main thread and update DOM there.

2. **Don't Send Functions to Workers**
   ```javascript
   // ❌ WRONG - Functions can't be cloned
   const worker = new Worker('worker.js');
   worker.postMessage({
     callback: () => console.log('done')
   });
   ```
   **Why Not:** Functions aren't serializable via structured cloning.
   **Instead:** Use string identifiers and define logic in the worker.

3. **Don't Create Workers in Loops Without Limits**
   ```javascript
   // ❌ WRONG - Creates hundreds of workers
   for (let i = 0; i < 1000; i++) {
     const worker = new Worker('worker.js');
     worker.postMessage(data[i]);
   }
   ```
   **Why Not:** Too many workers cause performance degradation and memory issues.
   **Instead:** Use a worker pool (typically 4-8 workers max).

---

## Related Topics

**Prerequisites (Learn These First):**
- [JavaScript Basics](../01-fundamentals/javascript-basics.md) - Understanding JS is essential
- [DOM Manipulation](../03-links-navigation/anchor-links.md) - To understand why workers can't access DOM

**Related Concepts:**
- [Web Storage](web-storage.md) - Workers can access localStorage via importScripts
- [Drag and Drop](drag-drop.md) - Workers can process dropped files
- [Canvas](../10-graphics-canvas/canvas-drawing.md) - Common use case for workers

**Next Steps (Learn These Next):**
- [Server-Sent Events](server-sent-events.md) - Another async API pattern
- [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) - Advanced workers for offline functionality

**External Resources:**
- [MDN Web Docs - Web Workers API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)
- [HTML Living Standard - Workers](https://html.spec.whatwg.org/multipage/workers.html)
- [Using Web Workers (Google)](https://web.dev/workers-overview/)

---

## Practice Exercise

### Challenge: Build a Prime Number Calculator

**Objective:** Create a prime number finder that uses a Web Worker to find all primes up to a given number without blocking the UI.

**Requirements:**
- [ ] Accept a number input from the user (e.g., 100,000)
- [ ] Use a Web Worker to calculate prime numbers
- [ ] Display a progress bar showing completion percentage
- [ ] Show the count and list of primes when complete
- [ ] Bonus: Allow users to cancel the operation mid-calculation

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Prime Finder</title>
  <style>
    .progress {
      width: 100%;
      height: 25px;
      background: #e0e0e0;
      border-radius: 5px;
      margin: 10px 0;
    }
    .progress-bar {
      height: 100%;
      background: #4CAF50;
      width: 0%;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <h1>Prime Number Finder</h1>
  <input type="number" id="maxNumber" value="10000" placeholder="Find primes up to...">
  <button id="startBtn">Find Primes</button>
  <button id="cancelBtn" disabled>Cancel</button>

  <div class="progress">
    <div class="progress-bar" id="progress"></div>
  </div>

  <div id="status"></div>
  <div id="results"></div>

  <!-- Add your JavaScript here -->
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**Main Script (main.js):**
```javascript
const maxNumberInput = document.getElementById('maxNumber');
const startBtn = document.getElementById('startBtn');
const cancelBtn = document.getElementById('cancelBtn');
const progress = document.getElementById('progress');
const status = document.getElementById('status');
const results = document.getElementById('results');

let worker;

startBtn.addEventListener('click', () => {
  const maxNumber = parseInt(maxNumberInput.value);

  // Create worker
  worker = new Worker('prime-worker.js');

  // Send start command
  worker.postMessage({ command: 'start', maxNumber });

  // UI updates
  startBtn.disabled = true;
  cancelBtn.disabled = false;
  results.textContent = '';

  // Handle progress updates
  worker.onmessage = function(event) {
    const { type, percent, primes, count } = event.data;

    if (type === 'progress') {
      progress.style.width = percent + '%';
      status.textContent = `Finding primes: ${percent}%`;
    } else if (type === 'complete') {
      progress.style.width = '100%';
      status.textContent = `Complete! Found ${count} primes.`;
      results.textContent = `First 100 primes: ${primes.slice(0, 100).join(', ')}...`;

      startBtn.disabled = false;
      cancelBtn.disabled = true;
      worker.terminate();
    }
  };

  worker.onerror = function(error) {
    status.textContent = `Error: ${error.message}`;
    startBtn.disabled = false;
    cancelBtn.disabled = true;
  };
});

cancelBtn.addEventListener('click', () => {
  if (worker) {
    worker.terminate();
    status.textContent = 'Cancelled by user';
    startBtn.disabled = false;
    cancelBtn.disabled = true;
  }
});
```

**Worker Script (prime-worker.js):**
```javascript
function isPrime(num) {
  if (num < 2) return false;
  if (num === 2) return true;
  if (num % 2 === 0) return false;

  const sqrt = Math.sqrt(num);
  for (let i = 3; i <= sqrt; i += 2) {
    if (num % i === 0) return false;
  }
  return true;
}

self.onmessage = function(event) {
  const { command, maxNumber } = event.data;

  if (command === 'start') {
    const primes = [];
    const updateInterval = Math.floor(maxNumber / 100); // Update every 1%

    for (let i = 2; i <= maxNumber; i++) {
      if (isPrime(i)) {
        primes.push(i);
      }

      // Send progress update
      if (i % updateInterval === 0) {
        const percent = Math.round((i / maxNumber) * 100);
        self.postMessage({ type: 'progress', percent });
      }
    }

    // Send final results
    self.postMessage({
      type: 'complete',
      primes: primes,
      count: primes.length
    });
  }
};
```

**Explanation:**
This solution demonstrates core Web Worker concepts: creating a worker, bidirectional communication via `postMessage()`, progress updates, and proper cleanup with `terminate()`. The prime calculation happens entirely in the background, keeping the UI responsive even when processing large numbers.

</details>

---

### Expected Result

**Visual Outcome:**
- A smooth progress bar that updates in real-time
- The UI remains clickable and responsive throughout the calculation
- Results display immediately upon completion
- Cancel button allows users to stop the operation anytime

**Key Learnings:**
- How to create and communicate with Web Workers
- The importance of offloading heavy computations to prevent UI blocking
- Proper cleanup and error handling in worker contexts
- Real-world application: Any CPU-intensive task benefits from this pattern

---

## Navigation

**Previous:** [Web Storage](web-storage.md)
**Next:** [Server-Sent Events](server-sent-events.md)
**Up:** [Back to HTML5 APIs](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** HTML5 APIs
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
