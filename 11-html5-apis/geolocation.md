---
title: Geolocation API
category: HTML5 APIs
order: 30
---

# Geolocation API

> **Quick Summary:** The Geolocation API allows web applications to access the user's geographic location (latitude/longitude). Requires user permission for privacy. Perfect for location-based services, maps, store locators, and weather apps. Works on desktop and mobile browsers.

## Table of Contents
- [Introduction](#introduction)
- [Basic Usage](#basic-usage)
- [Getting Current Position](#getting-current-position)
- [Watching Position](#watching-position)
- [Position Options](#position-options)
- [Error Handling](#error-handling)
- [Privacy and Permissions](#privacy-and-permissions)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The Geolocation API provides JavaScript access to the user's geographic location through the `navigator.geolocation` object. Location data comes from GPS (mobile), Wi-Fi networks, IP address, or cell towers.

**Key characteristics:**
- **User permission required** - Browser prompts before sharing location
- **Cross-platform** - Works on desktop and mobile
- **Accuracy varies** - GPS (5-10m) vs IP (city-level)
- **Privacy-focused** - User controls access
- **HTTPS required** - Security requirement for modern browsers

**Key Concept:** Geolocation is like asking someone "Where are you?" - they can choose to tell you precisely (GPS), approximately (Wi-Fi), or refuse to answer. The browser acts as the middleman, always requiring the user's consent before sharing their location.

---

## Basic Usage

### Check for Support

```javascript
if ('geolocation' in navigator) {
  console.log('Geolocation is available');
} else {
  console.log('Geolocation not supported');
}
```

### Geolocation Object

```javascript
navigator.geolocation.getCurrentPosition(success, error, options);
navigator.geolocation.watchPosition(success, error, options);
navigator.geolocation.clearWatch(watchId);
```

---

## Getting Current Position

### Basic Example

```javascript
navigator.geolocation.getCurrentPosition(
  // Success callback
  function(position) {
    const lat = position.coords.latitude;
    const lon = position.coords.longitude;
    console.log(`Latitude: ${lat}, Longitude: ${lon}`);
  },

  // Error callback
  function(error) {
    console.error(`Error: ${error.message}`);
  }
);
```

### Position Object

The `position` object contains:

```javascript
{
  coords: {
    latitude: 37.7749,          // Decimal degrees
    longitude: -122.4194,       // Decimal degrees
    altitude: 10,               // Meters (or null)
    accuracy: 20,               // Meters
    altitudeAccuracy: 10,       // Meters (or null)
    heading: 90,                // Degrees (0-360, or null)
    speed: 5.5                  // Meters/second (or null)
  },
  timestamp: 1638360000000      // Milliseconds since epoch
}
```

### Full Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Geolocation Demo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
    }

    button {
      padding: 15px 30px;
      font-size: 16px;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background: #0056b3;
    }

    #result {
      margin-top: 20px;
      padding: 20px;
      background: #f8f9fa;
      border-radius: 5px;
    }

    .error {
      background: #f8d7da;
      color: #721c24;
    }
  </style>
</head>
<body>
  <h1>Get My Location</h1>
  <button id="get-location">Get Current Position</button>
  <div id="result"></div>

  <script>
    const button = document.getElementById('get-location');
    const resultDiv = document.getElementById('result');

    button.addEventListener('click', function() {
      if (!('geolocation' in navigator)) {
        resultDiv.innerHTML = '<p class="error">Geolocation not supported</p>';
        return;
      }

      resultDiv.innerHTML = '<p>Getting location...</p>';

      navigator.geolocation.getCurrentPosition(
        // Success
        function(position) {
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;
          const accuracy = position.coords.accuracy;

          resultDiv.innerHTML = `
            <h3>Location Found!</h3>
            <p><strong>Latitude:</strong> ${lat.toFixed(6)}</p>
            <p><strong>Longitude:</strong> ${lon.toFixed(6)}</p>
            <p><strong>Accuracy:</strong> ±${accuracy.toFixed(0)} meters</p>
            <p><a href="https://www.google.com/maps?q=${lat},${lon}" target="_blank">
              View on Google Maps
            </a></p>
          `;
        },

        // Error
        function(error) {
          let message = '';
          switch(error.code) {
            case error.PERMISSION_DENIED:
              message = 'User denied location access';
              break;
            case error.POSITION_UNAVAILABLE:
              message = 'Location information unavailable';
              break;
            case error.TIMEOUT:
              message = 'Location request timed out';
              break;
            default:
              message = 'Unknown error occurred';
          }

          resultDiv.innerHTML = `<p class="error">${message}</p>`;
        }
      );
    });
  </script>
</body>
</html>
```

---

## Watching Position

Use `watchPosition()` to continuously track location changes (e.g., navigation apps).

### Basic Watch

```javascript
const watchId = navigator.geolocation.watchPosition(
  function(position) {
    const lat = position.coords.latitude;
    const lon = position.coords.longitude;
    console.log(`New position: ${lat}, ${lon}`);
    updateMap(lat, lon);
  },

  function(error) {
    console.error(`Error: ${error.message}`);
  }
);

// Stop watching
navigator.geolocation.clearWatch(watchId);
```

### Example: Real-Time Tracking

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Real-Time Location Tracking</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
    }

    button {
      padding: 15px 30px;
      margin: 5px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .start {
      background: #28a745;
      color: white;
    }

    .stop {
      background: #dc3545;
      color: white;
    }

    #tracking-info {
      margin-top: 20px;
      padding: 20px;
      background: #f8f9fa;
      border-radius: 5px;
    }

    .position-log {
      max-height: 300px;
      overflow-y: auto;
      border: 1px solid #ddd;
      padding: 10px;
      margin-top: 10px;
      font-family: monospace;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <h1>Real-Time Location Tracking</h1>

  <button id="start-btn" class="start">Start Tracking</button>
  <button id="stop-btn" class="stop" disabled>Stop Tracking</button>

  <div id="tracking-info"></div>
  <div id="log" class="position-log"></div>

  <script>
    const startBtn = document.getElementById('start-btn');
    const stopBtn = document.getElementById('stop-btn');
    const infoDiv = document.getElementById('tracking-info');
    const logDiv = document.getElementById('log');

    let watchId = null;
    let positionCount = 0;

    startBtn.addEventListener('click', function() {
      if (!('geolocation' in navigator)) {
        alert('Geolocation not supported');
        return;
      }

      positionCount = 0;
      logDiv.innerHTML = '';

      watchId = navigator.geolocation.watchPosition(
        // Success
        function(position) {
          positionCount++;
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;
          const accuracy = position.coords.accuracy;
          const speed = position.coords.speed;
          const time = new Date(position.timestamp).toLocaleTimeString();

          infoDiv.innerHTML = `
            <h3>Tracking Active (Update #${positionCount})</h3>
            <p><strong>Latitude:</strong> ${lat.toFixed(6)}</p>
            <p><strong>Longitude:</strong> ${lon.toFixed(6)}</p>
            <p><strong>Accuracy:</strong> ±${accuracy.toFixed(0)}m</p>
            <p><strong>Speed:</strong> ${speed ? (speed * 3.6).toFixed(1) + ' km/h' : 'N/A'}</p>
            <p><strong>Last Update:</strong> ${time}</p>
          `;

          // Log entry
          const logEntry = `[${time}] Lat: ${lat.toFixed(6)}, Lon: ${lon.toFixed(6)}, Acc: ±${accuracy.toFixed(0)}m\n`;
          logDiv.innerHTML += logEntry;
          logDiv.scrollTop = logDiv.scrollHeight;
        },

        // Error
        function(error) {
          infoDiv.innerHTML = `<p class="error">Error: ${error.message}</p>`;
        },

        // Options
        {
          enableHighAccuracy: true,
          maximumAge: 0,
          timeout: 10000
        }
      );

      startBtn.disabled = true;
      stopBtn.disabled = false;
    });

    stopBtn.addEventListener('click', function() {
      if (watchId !== null) {
        navigator.geolocation.clearWatch(watchId);
        watchId = null;
        infoDiv.innerHTML = '<p>Tracking stopped</p>';
        startBtn.disabled = false;
        stopBtn.disabled = true;
      }
    });
  </script>
</body>
</html>
```

---

## Position Options

Configure geolocation behavior with options object:

```javascript
const options = {
  enableHighAccuracy: true,    // Use GPS (more battery)
  timeout: 10000,              // Max wait time (ms)
  maximumAge: 0                // Max cached position age (ms)
};

navigator.geolocation.getCurrentPosition(success, error, options);
```

### Options Explained

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `enableHighAccuracy` | boolean | `false` | Use GPS for better accuracy (uses more battery) |
| `timeout` | number | `Infinity` | Max time to wait for position (milliseconds) |
| `maximumAge` | number | `0` | Accept cached position if newer than this (milliseconds) |

**Example:**

```javascript
// High accuracy, 5-second timeout, no cache
const options = {
  enableHighAccuracy: true,
  timeout: 5000,
  maximumAge: 0
};

// Low accuracy, 10-second timeout, accept 1-minute-old cache
const options = {
  enableHighAccuracy: false,
  timeout: 10000,
  maximumAge: 60000
};
```

---

## Error Handling

### Error Codes

```javascript
navigator.geolocation.getCurrentPosition(
  success,
  function(error) {
    switch(error.code) {
      case error.PERMISSION_DENIED:
        console.error('User denied permission');
        break;

      case error.POSITION_UNAVAILABLE:
        console.error('Location unavailable');
        break;

      case error.TIMEOUT:
        console.error('Request timed out');
        break;

      default:
        console.error('Unknown error');
    }
  }
);
```

### Error Object

```javascript
{
  code: 1,                    // Error code (1, 2, or 3)
  message: "User denied..."   // Human-readable message
}
```

**Error codes:**
- **1** (`PERMISSION_DENIED`) - User denied location access
- **2** (`POSITION_UNAVAILABLE`) - Cannot determine location
- **3** (`TIMEOUT`) - Request took too long

---

## Privacy and Permissions

### HTTPS Requirement

Modern browsers require HTTPS for geolocation (except localhost).

```
✅ https://example.com - Works
✅ http://localhost - Works (development)
❌ http://example.com - Blocked
```

### Permission Prompt

Browser shows permission prompt on first request:

```
[example.com] wants to know your location
[Block] [Allow]
```

### Best Practices

1. **Explain before requesting:**
   ```html
   <p>We need your location to show nearby stores.</p>
   <button onclick="requestLocation()">Find Stores Near Me</button>
   ```

2. **Handle permission denial gracefully:**
   ```javascript
   if (error.code === error.PERMISSION_DENIED) {
     showManualLocationInput();
   }
   ```

3. **Use appropriate accuracy:**
   ```javascript
   // City-level search (save battery)
   { enableHighAccuracy: false }

   // Turn-by-turn navigation (high accuracy)
   { enableHighAccuracy: true }
   ```

---

## Examples

### Example 1: Store Locator

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Store Locator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 50px auto;
      padding: 20px;
    }

    .store {
      padding: 15px;
      margin: 10px 0;
      border: 1px solid #ddd;
      border-radius: 5px;
      background: #f8f9fa;
    }

    .distance {
      color: #007bff;
      font-weight: bold;
    }

    button {
      padding: 15px 30px;
      background: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <h1>Find Nearest Stores</h1>
  <button id="find-stores">Find Stores Near Me</button>
  <div id="results"></div>

  <script>
    // Sample store locations
    const stores = [
      { name: 'Store A', lat: 37.7749, lon: -122.4194 },
      { name: 'Store B', lat: 37.7849, lon: -122.4094 },
      { name: 'Store C', lat: 37.7649, lon: -122.4294 },
      { name: 'Store D', lat: 37.7949, lon: -122.3994 }
    ];

    // Calculate distance between two points (Haversine formula)
    function calculateDistance(lat1, lon1, lat2, lon2) {
      const R = 6371; // Earth radius in km
      const dLat = (lat2 - lat1) * Math.PI / 180;
      const dLon = (lon2 - lon1) * Math.PI / 180;
      const a =
        Math.sin(dLat/2) * Math.sin(dLat/2) +
        Math.cos(lat1 * Math.PI / 180) * Math.cos(lat2 * Math.PI / 180) *
        Math.sin(dLon/2) * Math.sin(dLon/2);
      const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
      return R * c;
    }

    document.getElementById('find-stores').addEventListener('click', function() {
      const resultsDiv = document.getElementById('results');
      resultsDiv.innerHTML = '<p>Getting your location...</p>';

      navigator.geolocation.getCurrentPosition(
        function(position) {
          const userLat = position.coords.latitude;
          const userLon = position.coords.longitude;

          // Calculate distances
          const storesWithDistance = stores.map(store => {
            const distance = calculateDistance(userLat, userLon, store.lat, store.lon);
            return { ...store, distance };
          });

          // Sort by distance
          storesWithDistance.sort((a, b) => a.distance - b.distance);

          // Display results
          resultsDiv.innerHTML = '<h2>Nearest Stores:</h2>';
          storesWithDistance.forEach((store, index) => {
            resultsDiv.innerHTML += `
              <div class="store">
                <h3>${index + 1}. ${store.name}</h3>
                <p class="distance">${store.distance.toFixed(2)} km away</p>
                <a href="https://www.google.com/maps/dir/?api=1&origin=${userLat},${userLon}&destination=${store.lat},${store.lon}" target="_blank">
                  Get Directions
                </a>
              </div>
            `;
          });
        },

        function(error) {
          resultsDiv.innerHTML = `<p class="error">Error: ${error.message}</p>`;
        }
      );
    });
  </script>
</body>
</html>
```

### Example 2: Weather App

```javascript
function getWeatherForCurrentLocation() {
  navigator.geolocation.getCurrentPosition(
    function(position) {
      const lat = position.coords.latitude;
      const lon = position.coords.longitude;

      // Call weather API
      fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&appid=YOUR_API_KEY`)
        .then(response => response.json())
        .then(data => {
          displayWeather(data);
        })
        .catch(error => {
          console.error('Weather API error:', error);
        });
    },

    function(error) {
      console.error('Geolocation error:', error.message);
      // Fallback: Ask user for city name
      showCityInput();
    }
  );
}
```

---

## Best Practices

### Do This

1. **Request permission with context**
   ```html
   <p>We'll use your location to show nearby restaurants.</p>
   <button onclick="findRestaurants()">Find Restaurants</button>
   ```

2. **Provide fallback for denied permission**
   ```javascript
   if (error.code === error.PERMISSION_DENIED) {
     showManualLocationInput();
   }
   ```

3. **Use appropriate accuracy settings**
   ```javascript
   // Store locator (low accuracy OK)
   { enableHighAccuracy: false, maximumAge: 300000 }

   // Navigation app (high accuracy required)
   { enableHighAccuracy: true, maximumAge: 0 }
   ```

4. **Cache positions when appropriate**
   ```javascript
   // Accept position up to 5 minutes old
   { maximumAge: 300000 }
   ```

### Avoid This

1. **Don't request location immediately on page load**
   ```javascript
   // WRONG: Confusing to user
   window.onload = function() {
     navigator.geolocation.getCurrentPosition(...);
   };

   // CORRECT: User-initiated
   button.onclick = function() {
     navigator.geolocation.getCurrentPosition(...);
   };
   ```

2. **Don't use geolocation without HTTPS**
   ```
   ❌ http://example.com - Won't work
   ✅ https://example.com - Works
   ```

3. **Don't ignore errors**
   ```javascript
   // WRONG: No error handling
   navigator.geolocation.getCurrentPosition(success);

   // CORRECT: Handle errors
   navigator.geolocation.getCurrentPosition(success, error);
   ```

---

## Quick Reference

### Methods

```javascript
// Get current position (one-time)
navigator.geolocation.getCurrentPosition(success, error, options);

// Watch position (continuous)
const watchId = navigator.geolocation.watchPosition(success, error, options);

// Stop watching
navigator.geolocation.clearWatch(watchId);
```

### Position Object

```javascript
position.coords.latitude      // Decimal degrees
position.coords.longitude     // Decimal degrees
position.coords.accuracy      // Meters
position.coords.altitude      // Meters (or null)
position.coords.heading       // Degrees 0-360 (or null)
position.coords.speed         // Meters/second (or null)
position.timestamp            // Milliseconds since epoch
```

### Error Codes

```javascript
error.PERMISSION_DENIED      // 1
error.POSITION_UNAVAILABLE   // 2
error.TIMEOUT                // 3
```

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | IE | Mobile |
|---------|--------|---------|--------|------|-----|--------|
| Geolocation API | ✅ 5+ | ✅ 3.5+ | ✅ 5+ | ✅ All | ✅ 9+ | ✅ All |
| `getCurrentPosition` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ | ✅ All |
| `watchPosition` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 9+ | ✅ All |
| HTTPS requirement | ✅ 50+ | ✅ 55+ | ✅ 10+ | ✅ All | ❌ No | ⚠️ Varies |

---

## Related Topics
- [Drag and Drop](drag-drop.md)
- [Web Storage](web-storage.md)
- [Page Visibility](page-visibility.md)

---

**Last Updated:** November 17, 2025
**Category:** HTML5 APIs
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
