---
title: Video Formats and Codecs
category: Multimedia Embedding
order: 1
---

# Video Formats and Codecs

> **Quick Summary:** Understanding video formats (MP4, WebM, OGG) and codecs (H.264, VP9, AV1) is essential for delivering cross-browser compatible video content with optimal quality and file size.

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

Video formats and codecs determine how video data is compressed, stored, and played back. Different browsers support different formats, so providing multiple sources ensures compatibility.

**The Problem:** No single video format works across all browsers. MP4 works everywhere but has patent issues. WebM is royalty-free but older browsers don't support it.

**The Solution:** Use the `<video>` element with multiple `<source>` elements. Browsers automatically pick the first format they support.

**Key Concept:** A **container format** (MP4, WebM, OGG) holds video/audio streams. A **codec** (H.264, VP9, AV1) is the compression algorithm. Container ≠ Codec!

---

## Basic Syntax

### Video Element with Multiple Formats

```html
<video controls width="640" height="360">
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
  <source src="video.ogv" type="video/ogg">
  Your browser doesn't support HTML5 video.
</video>
```

### Specifying Codecs

```html
<video controls>
  <!-- MP4 with H.264 video + AAC audio -->
  <source src="video.mp4" type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'>

  <!-- WebM with VP9 video + Opus audio -->
  <source src="video.webm" type='video/webm; codecs="vp9, opus"'>

  Fallback text for unsupported browsers
</video>
```

### Common Video Formats

| Format | Container | Video Codec | Audio Codec | Browser Support |
|--------|-----------|-------------|-------------|-----------------|
| **MP4** | MPEG-4 | H.264 (AVC) | AAC | All modern browsers |
| **WebM** | WebM | VP8/VP9/AV1 | Vorbis/Opus | Chrome, Firefox, Edge (not Safari) |
| **OGG** | Ogg | Theora | Vorbis | Firefox, Chrome (not Safari/IE) |

---

## Examples

### Example 1: Cross-Browser Video Player

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Video Format Example</title>
  <style>
    video {
      width: 100%;
      max-width: 800px;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
    }
  </style>
</head>
<body>
  <h1>Multi-Format Video Player</h1>

  <video controls preload="metadata" poster="thumbnail.jpg">
    <!-- Modern format with best compression -->
    <source src="sample.webm" type="video/webm; codecs=vp9,opus">

    <!-- Universal fallback -->
    <source src="sample.mp4" type="video/mp4; codecs=avc1.42E01E,mp4a.40.2">

    <!-- Older fallback -->
    <source src="sample.ogv" type="video/ogg">

    <p>Your browser doesn't support HTML5 video. <a href="sample.mp4">Download the video</a> instead.</p>
  </video>

  <script>
    const video = document.querySelector('video');

    video.addEventListener('loadedmetadata', function() {
      console.log('Duration:', video.duration);
      console.log('Dimensions:', video.videoWidth, 'x', video.videoHeight);
    });

    video.addEventListener('error', function(e) {
      console.error('Video error:', e);
    });
  </script>
</body>
</html>
```

**Result:** Browser picks the best supported format automatically.

---

### Example 2: Responsive Video with Different Qualities

**HTML:**
```html
<video controls width="640">
  <!-- High quality for desktop -->
  <source src="video-1080p.mp4" type="video/mp4" media="(min-width: 1024px)">

  <!-- Medium quality for tablets -->
  <source src="video-720p.mp4" type="video/mp4" media="(min-width: 768px)">

  <!-- Low quality for mobile -->
  <source src="video-480p.mp4" type="video/mp4">

  Your browser doesn't support video.
</video>
```

---

### Example 3: Video with Format Detection

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Format Detection</title>
</head>
<body>
  <h1>Supported Video Formats</h1>
  <div id="formatSupport"></div>

  <video id="video" controls>
    <source src="video.webm" type="video/webm">
    <source src="video.mp4" type="video/mp4">
  </video>

  <script>
    const video = document.getElementById('video');
    const formatSupport = document.getElementById('formatSupport');

    // Check format support
    const formats = {
      'MP4 (H.264)': 'video/mp4; codecs="avc1.42E01E"',
      'WebM (VP8)': 'video/webm; codecs="vp8"',
      'WebM (VP9)': 'video/webm; codecs="vp9"',
      'OGG (Theora)': 'video/ogg; codecs="theora"'
    };

    let html = '<h3>This browser supports:</h3><ul>';
    for (const [name, type] of Object.entries(formats)) {
      const support = video.canPlayType(type);
      const status = support === 'probably' ? '✅ Full support' :
                     support === 'maybe' ? '⚠️ Might work' :
                     '❌ Not supported';
      html += `<li><strong>${name}:</strong> ${status}</li>`;
    }
    html += '</ul>';
    formatSupport.innerHTML = html;
  </script>
</body>
</html>
```

---

## Common Use Cases

### Use Case 1: Tutorial/Educational Videos
**Format:** MP4 (H.264) for universal compatibility
**Why:** Needs to work on all devices, including older browsers

### Use Case 2: Streaming Video
**Format:** HLS (.m3u8) or DASH for adaptive bitrate
**Why:** Adjusts quality based on connection speed

### Use Case 3: Background Videos
**Format:** WebM (VP9) with low bitrate
**Why:** Smaller file size for decorative content

---

## Browser Support

| Format | Chrome | Firefox | Safari | Edge | IE |
|--------|--------|---------|--------|------|----|
| MP4 (H.264) | ✅ | ✅ | ✅ | ✅ | ✅ 9+ |
| WebM (VP8) | ✅ | ✅ | ❌ | ✅ | ❌ |
| WebM (VP9) | ✅ | ✅ | ❌ | ✅ | ❌ |
| OGG (Theora) | ✅ | ✅ | ❌ | ❌ | ❌ |

**Recommended Strategy:**
```html
<video controls>
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
</video>
```
Order: WebM first (better compression), MP4 fallback (universal support)

---

## Accessibility Considerations

```html
<video controls>
  <source src="video.mp4" type="video/mp4">
  <track kind="captions" src="captions-en.vtt" srclang="en" label="English" default>
  <track kind="captions" src="captions-es.vtt" srclang="es" label="Spanish">
  <track kind="descriptions" src="descriptions.vtt" srclang="en" label="English Descriptions">
</video>
```

---

## Best Practices

### Do This

1. **Provide Multiple Formats**
   ```html
   <video controls>
     <source src="video.webm" type="video/webm">
     <source src="video.mp4" type="video/mp4">
   </video>
   ```
   **Why:** Ensures compatibility across all browsers.

2. **Specify Codecs**
   ```html
   <source src="video.mp4" type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'>
   ```
   **Why:** Helps browser determine compatibility faster.

3. **Use Poster Images**
   ```html
   <video controls poster="thumbnail.jpg">
   ```
   **Why:** Shows preview before video loads.

---

### Avoid This

1. **Don't Use Only WebM**
   ```html
   <!-- ❌ WRONG - Safari doesn't support WebM -->
   <video src="video.webm" controls></video>
   ```
   **Instead:** Always include MP4 fallback.

2. **Don't Autoplay Without Mute**
   ```html
   <!-- ❌ WRONG - Browsers block this -->
   <video autoplay controls></video>

   <!-- ✅ CORRECT -->
   <video autoplay muted controls></video>
   ```

---

## Related Topics

- [Video/Audio Elements](../08-media-elements/video-audio.md)
- [YouTube Embedding](youtube-embedding.md)
- [Audio Accessibility](audio-accessibility.md)

**External Resources:**
- [MDN - Video Formats](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Video_codecs)
- [Can I Use - Video Formats](https://caniuse.com/?search=video)

---

## Practice Exercise

### Challenge: Create a Responsive Video Player

**Requirements:**
- [ ] Multiple video sources (WebM + MP4)
- [ ] Poster image
- [ ] Check format support with JavaScript
- [ ] Display which format is playing

---

## Navigation

**Previous:** [Online/Offline Detection](../11-html5-apis/online-offline.md)
**Next:** [Audio Accessibility](audio-accessibility.md)
**Up:** [Back to Multimedia Embedding](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** Multimedia Embedding
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
