# Video in HTML5

## Overview
The `<video>` element embeds video content into HTML documents, providing native browser support for video playback without plugins. It supports multiple formats, subtitles, and can be controlled via JavaScript.

## Basic Syntax

```html
<video controls width="640" height="360">
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
  Your browser doesn't support the video element.
</video>
```

**Key Points:**
- Multiple `<source>` elements provide format fallbacks
- Browser uses first supported format
- `width` and `height` prevent layout shift
- Text displays if video not supported

## Essential Attributes

### controls
Displays browser's default video controls (play, pause, volume, fullscreen, timeline).

```html
<!-- With controls -->
<video controls src="demo.mp4" width="640" height="360"></video>

<!-- Without controls (custom player required) -->
<video src="video.mp4" width="640" height="360"></video>
```

### width and height
Specifies video dimensions in pixels.

```html
<video controls width="1920" height="1080" src="video.mp4"></video>

<!-- Responsive with CSS -->
<video controls style="width: 100%; height: auto;" src="video.mp4"></video>
```

### poster
Image displayed before video plays.

```html
<video controls
       width="640"
       height="360"
       poster="thumbnail.jpg"
       src="video.mp4">
</video>
```

### autoplay
Automatically starts playing (usually requires `muted`).

```html
<!-- Muted autoplay (allowed by browsers) -->
<video autoplay muted loop width="640" height="360" src="bg-video.mp4"></video>

<!-- Autoplay with sound (blocked by most browsers) -->
<video autoplay controls src="video.mp4"></video>
```

**⚠️ Autoplay Policy**: Browsers block autoplay with sound. Must be muted OR user must interact with page first.

### loop
Repeats video indefinitely.

```html
<video controls loop src="animation.mp4" width="400" height="400"></video>
```

### muted
Starts with audio muted.

```html
<video controls muted src="video.mp4" width="640" height="360"></video>
```

### preload
Hints how browser should load video.

```html
<!-- Preload entire video -->
<video controls preload="auto" src="video.mp4"></video>

<!-- Preload only metadata (recommended for large files) -->
<video controls preload="metadata" src="long-video.mp4"></video>

<!-- Don't preload (save bandwidth) -->
<video controls preload="none" src="video.mp4"></video>
```

**When to use:**
- `preload="auto"`: Short videos, main content
- `preload="metadata"`: Large videos, multiple videos on page
- `preload="none"`: User might not watch, background videos

### playsinline
Plays video inline on mobile (iOS) instead of fullscreen.

```html
<video controls playsinline src="video.mp4" width="640" height="360"></video>
```

## Video Formats

### Format Support by Browser

| Format | Chrome | Firefox | Safari | Edge | Container | Codec |
|--------|--------|---------|--------|------|-----------|-------|
| **MP4** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | MPEG-4 | H.264 |
| **WebM** | ✅ Yes | ✅ Yes | ✅ Yes (14.1+) | ✅ Yes | WebM | VP8/VP9 |
| **OGG** | ✅ Yes | ✅ Yes | ❌ No | ❌ No | Ogg | Theora |

### Best Practice: Multiple Formats

```html
<video controls width="640" height="360" poster="poster.jpg">
  <!-- WebM: Open format, excellent compression -->
  <source src="video.webm" type="video/webm">

  <!-- MP4: Universal support -->
  <source src="video.mp4" type="video/mp4">

  <!-- Fallback message -->
  Your browser doesn't support HTML5 video.
  <a href="video.mp4">Download the video</a>.
</video>
```

### Format Selection Guide

**MP4 (H.264)** - Recommended primary format
- ✅ Universal browser support
- ✅ Excellent compression
- ✅ Hardware acceleration
- 💰 Patent-encumbered (licensing may apply for encoding)

**WebM (VP8/VP9)** - Open source alternative
- ✅ Open format (no licensing)
- ✅ Better quality than MP4 at same bitrate
- ✅ Smaller file sizes (VP9)
- ❌ Limited Safari support until 2021

**Recommended setup**: MP4 as primary, WebM as optional enhancement.

## Subtitles and Captions

### Using Track Element

```html
<video controls width="640" height="360">
  <source src="video.mp4" type="video/mp4">

  <!-- English subtitles -->
  <track kind="subtitles"
         src="subtitles-en.vtt"
         srclang="en"
         label="English"
         default>

  <!-- Spanish subtitles -->
  <track kind="subtitles"
         src="subtitles-es.vtt"
         srclang="es"
         label="Español">

  <!-- French subtitles -->
  <track kind="subtitles"
         src="subtitles-fr.vtt"
         srclang="fr"
         label="Français">
</video>
```

### Track Kinds

```html
<!-- Subtitles (translation for foreign language) -->
<track kind="subtitles" src="subs-en.vtt" srclang="en" label="English">

<!-- Captions (for deaf/hard of hearing, includes sound effects) -->
<track kind="captions" src="captions-en.vtt" srclang="en" label="English CC">

<!-- Descriptions (for blind/visually impaired) -->
<track kind="descriptions" src="audio-desc.vtt" srclang="en" label="Audio Description">

<!-- Chapters (navigation) -->
<track kind="chapters" src="chapters.vtt" srclang="en" label="Chapters">

<!-- Metadata (not visible to user) -->
<track kind="metadata" src="metadata.vtt" srclang="en">
```

### WebVTT Format Example

**subtitles-en.vtt:**
```
WEBVTT

1
00:00:00.000 --> 00:00:03.000
Welcome to our tutorial video.

2
00:00:03.500 --> 00:00:07.000
Today we'll learn about HTML5 video.

3
00:00:07.500 --> 00:00:11.000
Let's start with the basics.
```

## Common Use Cases

### Video Tutorial

```html
<article>
  <h2>HTML5 Video Tutorial</h2>
  <p>Learn how to embed videos in your web pages</p>

  <video controls
         width="800"
         height="450"
         poster="tutorial-thumbnail.jpg"
         preload="metadata">
    <source src="tutorial.mp4" type="video/mp4">
    <source src="tutorial.webm" type="video/webm">
    <track kind="subtitles" src="subs-en.vtt" srclang="en" label="English" default>
    <track kind="subtitles" src="subs-es.vtt" srclang="es" label="Español">
    Your browser doesn't support video. <a href="tutorial.mp4">Download instead</a>.
  </video>
</article>
```

### Background Video (Hero Section)

```html
<section class="hero">
  <video autoplay muted loop playsinline class="hero-video">
    <source src="background.mp4" type="video/mp4">
    <source src="background.webm" type="video/webm">
  </video>

  <div class="hero-content">
    <h1>Welcome to Our Platform</h1>
    <p>Innovation in every pixel</p>
    <button>Get Started</button>
  </div>
</section>

<style>
  .hero {
    position: relative;
    height: 100vh;
    overflow: hidden;
  }

  .hero-video {
    position: absolute;
    top: 50%;
    left: 50%;
    min-width: 100%;
    min-height: 100%;
    width: auto;
    height: auto;
    transform: translate(-50%, -50%);
    z-index: 1;
  }

  .hero-content {
    position: relative;
    z-index: 2;
    text-align: center;
    color: white;
    padding-top: 30vh;
  }
</style>
```

### Product Demo

```html
<figure>
  <video controls width="1280" height="720" poster="product-demo-poster.jpg">
    <source src="product-demo.mp4" type="video/mp4">
    <track kind="captions" src="captions.vtt" srclang="en" label="English" default>
  </video>
  <figcaption>
    Product Demo: Dashboard Features Overview (3:45)
  </figcaption>
</figure>
```

### Responsive Video Grid

```html
<div class="video-grid">
  <div class="video-item">
    <video controls preload="metadata" poster="thumb1.jpg">
      <source src="video1.mp4" type="video/mp4">
    </video>
    <h3>Tutorial 1: Getting Started</h3>
  </div>

  <div class="video-item">
    <video controls preload="metadata" poster="thumb2.jpg">
      <source src="video2.mp4" type="video/mp4">
    </video>
    <h3>Tutorial 2: Advanced Features</h3>
  </div>

  <div class="video-item">
    <video controls preload="metadata" poster="thumb3.jpg">
      <source src="video3.mp4" type="video/mp4">
    </video>
    <h3>Tutorial 3: Best Practices</h3>
  </div>
</div>

<style>
  .video-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
    padding: 20px;
  }

  .video-item video {
    width: 100%;
    height: auto;
    border-radius: 8px;
  }

  .video-item h3 {
    margin-top: 10px;
    font-size: 1rem;
  }
</style>
```

## JavaScript Video Control

### Basic Controls

```html
<video id="myVideo" width="640" height="360">
  <source src="video.mp4" type="video/mp4">
</video>

<button onclick="playVideo()">Play</button>
<button onclick="pauseVideo()">Pause</button>
<button onclick="stopVideo()">Stop</button>
<button onclick="fullscreen()">Fullscreen</button>
<button onclick="speedUp()">1.5x Speed</button>
<button onclick="normalSpeed()">1x Speed</button>

<script>
const video = document.getElementById('myVideo');

function playVideo() {
  video.play();
}

function pauseVideo() {
  video.pause();
}

function stopVideo() {
  video.pause();
  video.currentTime = 0;
}

function fullscreen() {
  if (video.requestFullscreen) {
    video.requestFullscreen();
  } else if (video.webkitRequestFullscreen) {
    video.webkitRequestFullscreen();
  }
}

function speedUp() {
  video.playbackRate = 1.5;
}

function normalSpeed() {
  video.playbackRate = 1.0;
}
</script>
```

### Video Properties

```javascript
const video = document.getElementById('myVideo');

// Playback control
video.play();                    // Start playback
video.pause();                   // Pause playback
video.currentTime = 30;          // Jump to 30 seconds
video.playbackRate = 1.5;        // Play at 1.5x speed
video.volume = 0.5;              // Set volume to 50%
video.muted = true;              // Mute video

// Read-only properties
video.duration;                  // Total length in seconds
video.paused;                    // true if paused
video.ended;                     // true if finished
video.videoWidth;                // Intrinsic width
video.videoHeight;               // Intrinsic height
video.buffered;                  // TimeRanges object
```

### Video Events

```javascript
const video = document.getElementById('myVideo');

// Playback events
video.addEventListener('play', () => {
  console.log('Video started playing');
});

video.addEventListener('pause', () => {
  console.log('Video paused');
});

video.addEventListener('ended', () => {
  console.log('Video finished');
});

// Loading events
video.addEventListener('loadedmetadata', () => {
  console.log(`Duration: ${video.duration}s`);
  console.log(`Dimensions: ${video.videoWidth}x${video.videoHeight}`);
});

video.addEventListener('timeupdate', () => {
  const percent = (video.currentTime / video.duration) * 100;
  console.log(`Progress: ${percent}%`);
});

video.addEventListener('volumechange', () => {
  console.log(`Volume: ${video.volume * 100}%`);
});
```

## Accessibility Considerations

### Always Include Captions

```html
<video controls width="640" height="360">
  <source src="video.mp4" type="video/mp4">
  <track kind="captions"
         src="captions-en.vtt"
         srclang="en"
         label="English"
         default>
  <track kind="descriptions"
         src="audio-desc-en.vtt"
         srclang="en"
         label="Audio Description">
</video>
```

### Descriptive Poster Images

```html
<video controls
       width="640"
       height="360"
       poster="coding-tutorial-thumbnail.jpg"
       aria-label="JavaScript coding tutorial video">
  <source src="tutorial.mp4" type="video/mp4">
  <track kind="captions" src="captions.vtt" srclang="en" label="English" default>
</video>
```

### Keyboard Accessibility

Native `<video controls>` are keyboard accessible:
- **Space/Enter**: Play/pause
- **Arrow left/right**: Seek backward/forward
- **Arrow up/down**: Volume up/down
- **F**: Toggle fullscreen
- **M**: Mute/unmute

### Transcript Provision

```html
<article>
  <video controls width="800" height="450">
    <source src="lecture.mp4" type="video/mp4">
    <track kind="captions" src="captions.vtt" srclang="en" label="English" default>
  </video>

  <details>
    <summary>Video Transcript</summary>
    <div class="transcript">
      <p><strong>[00:00]</strong> Welcome to today's lecture on HTML5 video...</p>
      <p><strong>[00:45]</strong> Let's start by discussing the video element...</p>
      <p><strong>[02:30]</strong> As you can see in this example...</p>
    </div>
  </details>
</article>
```

## Performance Best Practices

1. **Use preload="metadata"** for large files
2. **Include poster images** to improve perceived load time
3. **Compress videos** with appropriate codecs (H.264, VP9)
4. **Use appropriate resolution** (don't serve 4K when 1080p suffices)
5. **Lazy load below-the-fold videos**
6. **Use CDN** for video hosting
7. **Consider adaptive streaming** (HLS, DASH) for long-form content

```html
<!-- Optimized video setup -->
<video controls
       width="1920"
       height="1080"
       poster="poster-optimized.jpg"
       preload="metadata"
       loading="lazy">
  <source src="video-1080p.mp4" type="video/mp4">
  <track kind="subtitles" src="subs.vtt" srclang="en" label="English" default>
</video>
```

## Browser Support

- **`<video>` element**: All modern browsers (IE 9+, Chrome 4+, Firefox 3.5+, Safari 3.1+)
- **MP4 (H.264)**: Universal support
- **WebM (VP8/VP9)**: Chrome, Firefox, Edge, Safari 14.1+
- **`<track>` element**: All modern browsers (IE 10+)

## Common Mistakes

❌ **Autoplay with sound (blocked)**
```html
<video autoplay controls src="video.mp4"></video>
```

✅ **Muted autoplay**
```html
<video autoplay muted loop controls src="video.mp4"></video>
```

---

❌ **No dimensions specified**
```html
<video controls src="video.mp4"></video>
```

✅ **Include width and height**
```html
<video controls width="1920" height="1080" src="video.mp4"></video>
```

---

❌ **No poster image**
```html
<video controls src="video.mp4"></video>
```

✅ **Include poster**
```html
<video controls poster="thumbnail.jpg" src="video.mp4"></video>
```

---

❌ **No captions/subtitles**
```html
<video controls src="video.mp4"></video>
```

✅ **Include accessibility tracks**
```html
<video controls src="video.mp4">
  <track kind="captions" src="captions.vtt" srclang="en" label="English" default>
</video>
```

---

❌ **Single format only**
```html
<video controls src="video.mp4"></video>
```

✅ **Multiple formats**
```html
<video controls>
  <source src="video.webm" type="video/webm">
  <source src="video.mp4" type="video/mp4">
</video>
```

## Practice Exercise

Create a video landing page with:
1. Hero video background (autoplay, loop, muted)
2. Featured video with controls, poster, and subtitles
3. Video grid with 3 tutorial videos
4. Responsive design
5. Proper accessibility features

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Video Learning Platform</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
    }

    /* Hero Section with Background Video */
    .hero {
      position: relative;
      height: 100vh;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .hero-video {
      position: absolute;
      top: 50%;
      left: 50%;
      min-width: 100%;
      min-height: 100%;
      width: auto;
      height: auto;
      transform: translate(-50%, -50%);
      z-index: 1;
      object-fit: cover;
    }

    .hero::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.5);
      z-index: 2;
    }

    .hero-content {
      position: relative;
      z-index: 3;
      text-align: center;
      color: white;
      padding: 20px;
    }

    .hero h1 {
      font-size: clamp(2rem, 5vw, 4rem);
      margin-bottom: 20px;
    }

    .hero p {
      font-size: clamp(1rem, 2vw, 1.5rem);
      margin-bottom: 30px;
    }

    .cta-button {
      display: inline-block;
      padding: 15px 40px;
      background: #e74c3c;
      color: white;
      text-decoration: none;
      border-radius: 50px;
      font-size: 1.1rem;
      font-weight: bold;
      transition: background 0.3s;
    }

    .cta-button:hover {
      background: #c0392b;
    }

    /* Featured Video Section */
    .featured {
      max-width: 1200px;
      margin: 80px auto;
      padding: 0 20px;
    }

    .featured h2 {
      font-size: 2rem;
      margin-bottom: 20px;
      color: #2c3e50;
    }

    .featured video {
      width: 100%;
      max-width: 100%;
      height: auto;
      border-radius: 10px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.2);
    }

    .featured-description {
      margin-top: 20px;
      line-height: 1.6;
      color: #555;
    }

    /* Video Grid */
    .video-grid-section {
      background: #f5f5f5;
      padding: 80px 20px;
    }

    .video-grid-section h2 {
      text-align: center;
      font-size: 2rem;
      margin-bottom: 50px;
      color: #2c3e50;
    }

    .video-grid {
      max-width: 1200px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 30px;
    }

    .video-card {
      background: white;
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }

    .video-card:hover {
      transform: translateY(-5px);
    }

    .video-card video {
      width: 100%;
      display: block;
    }

    .video-card-content {
      padding: 20px;
    }

    .video-card h3 {
      color: #2c3e50;
      margin-bottom: 10px;
    }

    .video-card p {
      color: #7f8c8d;
      font-size: 0.9rem;
      line-height: 1.5;
    }

    .video-meta {
      margin-top: 15px;
      font-size: 0.85rem;
      color: #95a5a6;
    }
  </style>
</head>
<body>
  <!-- Hero Section with Background Video -->
  <section class="hero">
    <video autoplay muted loop playsinline class="hero-video">
      <source src="hero-background.mp4" type="video/mp4">
      <source src="hero-background.webm" type="video/webm">
    </video>

    <div class="hero-content">
      <h1>Master Web Development</h1>
      <p>Learn HTML5, CSS3, and JavaScript through interactive video tutorials</p>
      <a href="#featured" class="cta-button">Start Learning</a>
    </div>
  </section>

  <!-- Featured Video -->
  <section class="featured" id="featured">
    <h2>🎥 Featured Course: HTML5 Complete Guide</h2>

    <video controls
           width="1920"
           height="1080"
           poster="featured-poster.jpg"
           preload="metadata">
      <source src="html5-complete-guide.mp4" type="video/mp4">
      <source src="html5-complete-guide.webm" type="video/webm">
      <track kind="subtitles"
             src="subtitles-en.vtt"
             srclang="en"
             label="English"
             default>
      <track kind="subtitles"
             src="subtitles-es.vtt"
             srclang="es"
             label="Español">
      Your browser doesn't support video.
      <a href="html5-complete-guide.mp4">Download the video</a>.
    </video>

    <div class="featured-description">
      <p>
        <strong>Duration:</strong> 2 hours 15 minutes |
        <strong>Level:</strong> Beginner to Intermediate |
        <strong>Updated:</strong> January 2024
      </p>
      <p>
        This comprehensive course covers everything you need to know about HTML5,
        from basic document structure to advanced features like Canvas, SVG,
        and HTML5 APIs. Perfect for beginners and developers looking to refresh
        their knowledge.
      </p>
    </div>
  </section>

  <!-- Video Grid -->
  <section class="video-grid-section">
    <h2>📚 Tutorial Library</h2>

    <div class="video-grid">
      <article class="video-card">
        <video controls preload="metadata" poster="tutorial-1-poster.jpg">
          <source src="tutorial-1.mp4" type="video/mp4">
          <track kind="subtitles" src="tut1-subs.vtt" srclang="en" label="English">
        </video>
        <div class="video-card-content">
          <h3>Getting Started with HTML5</h3>
          <p>
            Learn the fundamentals of HTML5 including semantic elements,
            document structure, and best practices.
          </p>
          <div class="video-meta">
            ⏱️ 35 minutes | 👁️ 12,453 views
          </div>
        </div>
      </article>

      <article class="video-card">
        <video controls preload="metadata" poster="tutorial-2-poster.jpg">
          <source src="tutorial-2.mp4" type="video/mp4">
          <track kind="subtitles" src="tut2-subs.vtt" srclang="en" label="English">
        </video>
        <div class="video-card-content">
          <h3>HTML5 Forms and Validation</h3>
          <p>
            Master HTML5 form elements, input types, and built-in validation
            for better user experiences.
          </p>
          <div class="video-meta">
            ⏱️ 48 minutes | 👁️ 8,921 views
          </div>
        </div>
      </article>

      <article class="video-card">
        <video controls preload="metadata" poster="tutorial-3-poster.jpg">
          <source src="tutorial-3.mp4" type="video/mp4">
          <track kind="subtitles" src="tut3-subs.vtt" srclang="en" label="English">
        </video>
        <div class="video-card-content">
          <h3>HTML5 APIs and Storage</h3>
          <p>
            Explore HTML5 APIs including Web Storage, Geolocation, Drag and Drop,
            and more advanced features.
          </p>
          <div class="video-meta">
            ⏱️ 52 minutes | 👁️ 6,742 views
          </div>
        </div>
      </article>
    </div>
  </section>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [The Video element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)
- **W3Schools**: [HTML Video](https://www.w3schools.com/html/html5_video.asp)
- **WebVTT Standard**: [Web Video Text Tracks Format](https://w3c.github.io/webvtt/)
- **Web.dev**: [Video and Source Tags](https://web.dev/media-source/)

---

**Previous Topic**: [Audio](./audio.md)
**Next Topic**: [Embed and Object](./embed-object.md)
**Category**: [Media Elements](./README.md)
