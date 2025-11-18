---
title: Audio Accessibility
category: Multimedia Embedding
order: 2
---

# Audio Accessibility

> **Quick Summary:** Audio accessibility ensures that audio content (podcasts, music, sound effects) is accessible to users who are deaf, hard of hearing, or in sound-restricted environments through captions, transcripts, and audio descriptions.

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

Audio accessibility is a legal requirement under WCAG 2.1 and ADA. It ensures all users can access audio content regardless of hearing ability or environment.

**The Problem:** Audio-only content excludes deaf/hard-of-hearing users. Videos without captions are inaccessible. Background noise or quiet environments make audio difficult.

**The Solution:** Provide captions, transcripts, and audio descriptions. Use WebVTT format for timed text tracks.

**Key Concept:** **Captions** ≠ **Subtitles**. Captions include sound effects and speaker identification. Subtitles only translate dialogue.

---

## Basic Syntax

### Audio with Transcript

```html
<audio controls>
  <source src="podcast.mp3" type="audio/mpeg">
  <source src="podcast.ogg" type="audio/ogg">
  Your browser doesn't support audio.
</audio>

<details>
  <summary>Transcript</summary>
  <p><strong>Host:</strong> Welcome to our podcast...</p>
  <p><strong>Guest:</strong> Thanks for having me...</p>
</details>
```

### Video with Captions

```html
<video controls>
  <source src="video.mp4" type="video/mp4">

  <!-- Captions (includes sound effects) -->
  <track kind="captions" src="captions-en.vtt" srclang="en" label="English" default>

  <!-- Subtitles (translation only) -->
  <track kind="subtitles" src="subtitles-es.vtt" srclang="es" label="Spanish">

  <!-- Descriptions (for blind users) -->
  <track kind="descriptions" src="descriptions.vtt" srclang="en">
</video>
```

### WebVTT Caption File (captions-en.vtt)

```
WEBVTT

00:00:00.000 --> 00:00:03.000
[upbeat music playing]

00:00:03.000 --> 00:00:07.000
<v Host>Welcome to our show!</v>

00:00:07.500 --> 00:00:12.000
<v Guest>Thanks for having me.</v>

00:00:12.000 --> 00:00:15.000
[applause]
```

---

## Examples

### Example 1: Podcast Player with Transcript

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Accessible Podcast</title>
  <style>
    .podcast-container {
      max-width: 800px;
      margin: 20px auto;
      padding: 20px;
      border: 1px solid #ddd;
      border-radius: 8px;
    }
    .transcript {
      margin-top: 20px;
      padding: 15px;
      background: #f9f9f9;
      border-left: 4px solid #2196F3;
      max-height: 300px;
      overflow-y: auto;
    }
    .speaker {
      font-weight: bold;
      color: #2196F3;
    }
    .timestamp {
      color: #666;
      font-size: 0.9em;
      cursor: pointer;
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <div class="podcast-container">
    <h1>Episode 42: Web Accessibility</h1>

    <audio id="podcast" controls preload="metadata">
      <source src="podcast.mp3" type="audio/mpeg">
      <source src="podcast.ogg" type="audio/ogg">
      Your browser doesn't support audio.
    </audio>

    <div class="transcript">
      <h2>Transcript</h2>

      <p data-time="0">
        <span class="timestamp">[00:00]</span>
        <span class="speaker">Host:</span>
        Welcome to episode 42! Today we're discussing web accessibility.
      </p>

      <p data-time="15">
        <span class="timestamp">[00:15]</span>
        <span class="speaker">Guest:</span>
        Thanks for having me. Accessibility is crucial for inclusive design.
      </p>

      <p data-time="30">
        <span class="timestamp">[00:30]</span>
        <span class="speaker">Host:</span>
        Let's start with audio accessibility. What should developers know?
      </p>

      <p data-time="45">
        <span class="timestamp">[00:45]</span>
        <span class="speaker">Guest:</span>
        First, always provide transcripts. They help deaf users and improve SEO.
      </p>
    </div>
  </div>

  <script>
    const podcast = document.getElementById('podcast');
    const timestamps = document.querySelectorAll('.timestamp');

    // Click timestamp to jump to that time
    timestamps.forEach(timestamp => {
      timestamp.addEventListener('click', function() {
        const paragraph = this.closest('p');
        const time = parseInt(paragraph.dataset.time);
        podcast.currentTime = time;
        podcast.play();
      });
    });

    // Highlight current transcript section
    podcast.addEventListener('timeupdate', function() {
      const currentTime = podcast.currentTime;
      const paragraphs = document.querySelectorAll('.transcript p');

      paragraphs.forEach(p => {
        const pTime = parseInt(p.dataset.time);
        const nextP = p.nextElementSibling;
        const nextTime = nextP ? parseInt(nextP.dataset.time) : Infinity;

        if (currentTime >= pTime && currentTime < nextTime) {
          p.style.background = '#e3f2fd';
        } else {
          p.style.background = 'transparent';
        }
      });
    });
  </script>
</body>
</html>
```

**Result:** Interactive transcript with clickable timestamps that jump to audio positions.

---

### Example 2: Video with Multiple Caption Tracks

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Accessible Video Player</title>
  <style>
    video::cue {
      background-color: rgba(0, 0, 0, 0.8);
      color: white;
      font-size: 1.2em;
      font-family: Arial, sans-serif;
    }
    video::cue(v[voice="Host"]) {
      color: #4CAF50;
    }
    video::cue(v[voice="Guest"]) {
      color: #2196F3;
    }
  </style>
</head>
<body>
  <h1>Interview Video (Fully Accessible)</h1>

  <video id="video" controls width="640">
    <source src="interview.mp4" type="video/mp4">

    <!-- English captions (default) -->
    <track kind="captions" src="captions-en.vtt" srclang="en" label="English Captions" default>

    <!-- Spanish subtitles -->
    <track kind="subtitles" src="subtitles-es.vtt" srclang="es" label="Español">

    <!-- Audio descriptions for blind users -->
    <track kind="descriptions" src="descriptions.vtt" srclang="en" label="Audio Descriptions">

    Your browser doesn't support video.
  </video>

  <div>
    <h2>Caption Tracks:</h2>
    <ul id="trackList"></ul>
  </div>

  <script>
    const video = document.getElementById('video');
    const trackList = document.getElementById('trackList');

    // List available tracks
    Array.from(video.textTracks).forEach((track, index) => {
      const li = document.createElement('li');
      const button = document.createElement('button');
      button.textContent = `${track.label} (${track.language})`;
      button.addEventListener('click', () => {
        // Disable all tracks
        Array.from(video.textTracks).forEach(t => t.mode = 'disabled');
        // Enable selected track
        track.mode = 'showing';
      });
      li.appendChild(button);
      trackList.appendChild(li);
    });
  </script>
</body>
</html>
```

---

## Common Use Cases

### Use Case 1: Educational Videos
**Solution:** Captions + transcript + audio descriptions
**Why:** Students may be deaf, learning English, or in quiet libraries

### Use Case 2: Podcasts
**Solution:** Full transcript with timestamps
**Why:** Searchable, SEO-friendly, accessible to deaf users

### Use Case 3: Background Music
**Solution:** Provide mute control + visual indicator
**Why:** Respects user preference and accessibility

---

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| WebVTT | ✅ | ✅ | ✅ | ✅ |
| Multiple tracks | ✅ | ✅ | ✅ | ✅ |
| CSS styling | ✅ | ✅ | ✅ | ✅ |

---

## Accessibility Considerations

### WCAG 2.1 Requirements

**Level A:**
- Captions for prerecorded audio-visual content
- Audio descriptions OR full text alternative

**Level AA:**
- Captions for live audio-visual content
- Audio descriptions for prerecorded video

**Level AAA:**
- Sign language interpretation
- Extended audio descriptions

### Best Practices

1. **Accurate Captions**
   - Include speaker names
   - Describe sound effects: [thunder rumbling], [upbeat music]
   - Indicate tone: [sarcastically], [whispers]

2. **Timing**
   - Max 2 lines per caption
   - Display for 1-7 seconds
   - Sync precisely with audio

3. **Transcripts**
   - Include all dialogue and sound effects
   - Identify speakers
   - Note important visual information

---

## Best Practices

### Do This

```html
<!-- ✅ Multiple language captions -->
<video controls>
  <source src="video.mp4" type="video/mp4">
  <track kind="captions" src="en.vtt" srclang="en" label="English" default>
  <track kind="subtitles" src="es.vtt" srclang="es" label="Español">
  <track kind="descriptions" src="desc.vtt" srclang="en" label="Descriptions">
</video>
```

**Why:** Serves multiple audiences - deaf users, non-native speakers, blind users.

---

### Avoid This

```html
<!-- ❌ WRONG - No captions at all -->
<video src="video.mp4" controls></video>

<!-- ❌ WRONG - Hardcoded captions (can't be disabled) -->
<video src="video-with-burned-captions.mp4" controls></video>
```

**Instead:** Always provide separate caption tracks that users can toggle.

---

## Related Topics

- [Video Formats](video-formats.md)
- [YouTube Embedding](youtube-embedding.md) - Auto-captions
- [ARIA Attributes](../09-global-attributes/aria-attributes.md)

**External Resources:**
- [WebVTT Specification](https://w3c.github.io/webvtt/)
- [WCAG 2.1 - Time-based Media](https://www.w3.org/WAI/WCAG21/quickref/#time-based-media)
- [Creating WebVTT Files](https://developer.mozilla.org/en-US/docs/Web/API/WebVTT_API)

---

## Practice Exercise

### Challenge: Create an Accessible Video Player

**Requirements:**
- [ ] Add English and Spanish captions
- [ ] Provide full transcript below video
- [ ] Make transcript timestamps clickable
- [ ] Style captions with CSS

---

## Navigation

**Previous:** [Video Formats](video-formats.md)
**Next:** [YouTube Embedding](youtube-embedding.md)
**Up:** [Back to Multimedia Embedding](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** Multimedia Embedding
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
