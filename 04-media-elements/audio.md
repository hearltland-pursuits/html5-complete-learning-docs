# Audio in HTML5

## Overview
The `<audio>` element embeds sound content into HTML documents. It provides native browser controls for playing, pausing, and controlling volume without requiring plugins like Flash.

## Basic Syntax

```html
<audio controls>
  <source src="audio-file.mp3" type="audio/mpeg">
  <source src="audio-file.ogg" type="audio/ogg">
  Your browser doesn't support the audio element.
</audio>
```

**Key Points:**
- Multiple `<source>` elements provide fallback formats
- Browser uses first supported format
- Text between tags displays if audio not supported
- `controls` attribute shows playback controls

## Essential Attributes

### controls
Displays browser's default audio controls (play, pause, volume, timeline).

```html
<!-- With controls -->
<audio controls src="song.mp3"></audio>

<!-- Without controls (requires JavaScript to control) -->
<audio src="background-music.mp3"></audio>
```

### src
Specifies audio file URL (use when only one format needed).

```html
<audio controls src="podcast.mp3"></audio>
```

### autoplay
Automatically starts playing when page loads.

```html
<audio controls autoplay src="intro.mp3"></audio>
```

**⚠️ Warning**: Most browsers block autoplay with sound. Users must interact with page first, or audio must be muted.

**Better approach with muted:**
```html
<audio controls autoplay muted src="background.mp3"></audio>
```

### loop
Repeats audio indefinitely when it ends.

```html
<audio controls loop src="background-music.mp3"></audio>
```

### muted
Starts with audio muted.

```html
<audio controls muted src="sound-effect.mp3"></audio>
```

### preload
Hints how browser should load audio.

```html
<!-- Load entire file (default if controls present) -->
<audio controls preload="auto" src="song.mp3"></audio>

<!-- Load only metadata (duration, dimensions) -->
<audio controls preload="metadata" src="podcast.mp3"></audio>

<!-- Don't preload anything -->
<audio controls preload="none" src="large-file.mp3"></audio>
```

**When to use:**
- `preload="auto"`: Music player, short audio clips
- `preload="metadata"`: Podcast player, large files
- `preload="none"`: User might not play audio, save bandwidth

## Audio Formats

### Format Support by Browser

| Format | Chrome | Firefox | Safari | Edge | File Extension |
|--------|--------|---------|--------|------|----------------|
| **MP3** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | .mp3 |
| **WAV** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | .wav |
| **OGG** | ✅ Yes | ✅ Yes | ❌ No | ✅ Yes | .ogg |
| **AAC** | ✅ Yes | ✅ Yes (98+) | ✅ Yes | ✅ Yes | .aac, .m4a |
| **FLAC** | ✅ Yes | ✅ Yes | ✅ Yes (11+) | ✅ Yes | .flac |

### Best Practice: Multiple Formats

```html
<audio controls>
  <!-- MP3: Universal support, good compression -->
  <source src="audio.mp3" type="audio/mpeg">

  <!-- OGG: Open format, good quality -->
  <source src="audio.ogg" type="audio/ogg">

  <!-- Fallback message -->
  Your browser doesn't support HTML5 audio.
  <a href="audio.mp3">Download the audio file</a>.
</audio>
```

### Format Selection Guide

**MP3** (Recommended for most use cases)
- ✅ Universal browser support
- ✅ Good compression (smaller file sizes)
- ✅ Acceptable quality for most content
- ❌ Lossy compression

**WAV** (High quality, large files)
- ✅ Lossless quality
- ✅ Simple format
- ❌ Very large file sizes
- 📌 Use for: Short sound effects, professional audio editing

**OGG Vorbis** (Open source alternative)
- ✅ Open format (no licensing)
- ✅ Better quality than MP3 at same bitrate
- ❌ No Safari support
- 📌 Use as: Secondary option alongside MP3

**AAC** (Apple preferred)
- ✅ Better quality than MP3
- ✅ Apple ecosystem optimized
- ✅ Good mobile support
- 📌 Use for: iOS-focused apps

## Common Use Cases

### Music Player

```html
<figure>
  <figcaption>Now Playing: "Summer Vibes"</figcaption>
  <audio controls src="summer-vibes.mp3"></audio>
</figure>
```

### Podcast Episode

```html
<article>
  <h2>Episode 42: The Future of Web Development</h2>
  <p><strong>Duration:</strong> 45 minutes | <strong>Published:</strong> Jan 15, 2024</p>

  <audio controls preload="metadata">
    <source src="podcast-ep42.mp3" type="audio/mpeg">
    <source src="podcast-ep42.ogg" type="audio/ogg">
    Your browser doesn't support audio playback.
  </audio>

  <p>In this episode, we discuss emerging trends in web development...</p>
</article>
```

### Sound Effect (Game or Interactive App)

```html
<audio id="click-sound" preload="auto">
  <source src="click.mp3" type="audio/mpeg">
  <source src="click.ogg" type="audio/ogg">
</audio>

<button onclick="document.getElementById('click-sound').play()">
  Click Me
</button>
```

### Background Music (Muted Autoplay)

```html
<audio id="bg-music" loop muted autoplay>
  <source src="background.mp3" type="audio/mpeg">
</audio>

<button onclick="toggleMusic()">Toggle Music</button>

<script>
function toggleMusic() {
  const audio = document.getElementById('bg-music');
  if (audio.muted) {
    audio.muted = false;
  } else {
    audio.muted = true;
  }
}
</script>
```

### Audio with Transcript (Accessibility)

```html
<article>
  <h2>Product Demo Recording</h2>

  <audio controls>
    <source src="demo.mp3" type="audio/mpeg">
    <track kind="captions" src="demo-captions.vtt" srclang="en" label="English">
  </audio>

  <details>
    <summary>Read Transcript</summary>
    <p>
      Welcome to our product demo. Today we'll explore the key features
      of our new dashboard interface...
    </p>
  </details>
</article>
```

## JavaScript Audio Control

### Basic Controls

```html
<audio id="myAudio" src="song.mp3"></audio>

<button onclick="playAudio()">Play</button>
<button onclick="pauseAudio()">Pause</button>
<button onclick="stopAudio()">Stop</button>
<button onclick="volumeUp()">Volume Up</button>
<button onclick="volumeDown()">Volume Down</button>

<script>
const audio = document.getElementById('myAudio');

function playAudio() {
  audio.play();
}

function pauseAudio() {
  audio.pause();
}

function stopAudio() {
  audio.pause();
  audio.currentTime = 0;
}

function volumeUp() {
  if (audio.volume < 1) {
    audio.volume += 0.1;
  }
}

function volumeDown() {
  if (audio.volume > 0) {
    audio.volume -= 0.1;
  }
}
</script>
```

### Audio Properties

```javascript
const audio = document.getElementById('myAudio');

// Playback properties
audio.play();                    // Start playback
audio.pause();                   // Pause playback
audio.currentTime = 30;          // Jump to 30 seconds
audio.playbackRate = 1.5;        // Play at 1.5x speed
audio.volume = 0.5;              // Set volume to 50%
audio.muted = true;              // Mute audio

// Read-only properties
audio.duration;                  // Total length in seconds
audio.paused;                    // true if paused
audio.ended;                     // true if playback finished
audio.buffered;                  // TimeRanges object
```

### Audio Events

```javascript
const audio = document.getElementById('myAudio');

// Playback events
audio.addEventListener('play', () => {
  console.log('Audio started playing');
});

audio.addEventListener('pause', () => {
  console.log('Audio paused');
});

audio.addEventListener('ended', () => {
  console.log('Audio finished playing');
});

// Progress events
audio.addEventListener('loadstart', () => {
  console.log('Started loading audio');
});

audio.addEventListener('loadedmetadata', () => {
  console.log('Duration:', audio.duration);
});

audio.addEventListener('timeupdate', () => {
  console.log('Current time:', audio.currentTime);
});

audio.addEventListener('volumechange', () => {
  console.log('Volume:', audio.volume);
});
```

### Custom Audio Player

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Custom Audio Player</title>
  <style>
    .audio-player {
      max-width: 500px;
      margin: 50px auto;
      padding: 20px;
      background: #2c3e50;
      border-radius: 10px;
      color: white;
    }

    .song-info {
      text-align: center;
      margin-bottom: 20px;
    }

    .song-title {
      font-size: 1.3rem;
      margin: 0;
    }

    .artist {
      color: #95a5a6;
      margin: 5px 0;
    }

    .controls {
      display: flex;
      justify-content: center;
      gap: 15px;
      margin: 20px 0;
    }

    button {
      background: #3498db;
      border: none;
      color: white;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
    }

    button:hover {
      background: #2980b9;
    }

    .progress-container {
      margin: 20px 0;
    }

    .progress-bar {
      width: 100%;
      height: 8px;
      background: #34495e;
      border-radius: 4px;
      cursor: pointer;
      position: relative;
    }

    .progress {
      height: 100%;
      background: #3498db;
      border-radius: 4px;
      width: 0%;
      transition: width 0.1s;
    }

    .time-info {
      display: flex;
      justify-content: space-between;
      font-size: 0.9rem;
      color: #95a5a6;
      margin-top: 5px;
    }

    .volume-control {
      display: flex;
      align-items: center;
      gap: 10px;
      justify-content: center;
    }

    input[type="range"] {
      width: 100px;
    }
  </style>
</head>
<body>
  <div class="audio-player">
    <div class="song-info">
      <h2 class="song-title">Summer Vibes</h2>
      <p class="artist">Artist Name</p>
    </div>

    <audio id="audio" src="song.mp3" preload="metadata"></audio>

    <div class="controls">
      <button id="playPauseBtn">▶ Play</button>
      <button id="stopBtn">■ Stop</button>
    </div>

    <div class="progress-container">
      <div class="progress-bar" id="progressBar">
        <div class="progress" id="progress"></div>
      </div>
      <div class="time-info">
        <span id="currentTime">0:00</span>
        <span id="duration">0:00</span>
      </div>
    </div>

    <div class="volume-control">
      <span>🔊</span>
      <input type="range" id="volumeSlider" min="0" max="100" value="80">
      <span id="volumeValue">80%</span>
    </div>
  </div>

  <script>
    const audio = document.getElementById('audio');
    const playPauseBtn = document.getElementById('playPauseBtn');
    const stopBtn = document.getElementById('stopBtn');
    const progressBar = document.getElementById('progressBar');
    const progress = document.getElementById('progress');
    const currentTimeEl = document.getElementById('currentTime');
    const durationEl = document.getElementById('duration');
    const volumeSlider = document.getElementById('volumeSlider');
    const volumeValue = document.getElementById('volumeValue');

    // Initialize volume
    audio.volume = 0.8;

    // Play/Pause toggle
    playPauseBtn.addEventListener('click', () => {
      if (audio.paused) {
        audio.play();
        playPauseBtn.textContent = '⏸ Pause';
      } else {
        audio.pause();
        playPauseBtn.textContent = '▶ Play';
      }
    });

    // Stop button
    stopBtn.addEventListener('click', () => {
      audio.pause();
      audio.currentTime = 0;
      playPauseBtn.textContent = '▶ Play';
    });

    // Update progress bar
    audio.addEventListener('timeupdate', () => {
      const percent = (audio.currentTime / audio.duration) * 100;
      progress.style.width = percent + '%';
      currentTimeEl.textContent = formatTime(audio.currentTime);
    });

    // Load duration
    audio.addEventListener('loadedmetadata', () => {
      durationEl.textContent = formatTime(audio.duration);
    });

    // Click on progress bar to seek
    progressBar.addEventListener('click', (e) => {
      const rect = progressBar.getBoundingClientRect();
      const percent = (e.clientX - rect.left) / rect.width;
      audio.currentTime = percent * audio.duration;
    });

    // Volume control
    volumeSlider.addEventListener('input', (e) => {
      const volume = e.target.value / 100;
      audio.volume = volume;
      volumeValue.textContent = e.target.value + '%';
    });

    // Format time helper
    function formatTime(seconds) {
      const mins = Math.floor(seconds / 60);
      const secs = Math.floor(seconds % 60);
      return `${mins}:${secs.toString().padStart(2, '0')}`;
    }

    // Reset button when audio ends
    audio.addEventListener('ended', () => {
      playPauseBtn.textContent = '▶ Play';
    });
  </script>
</body>
</html>
```

## Accessibility Considerations

### Provide Alternatives

```html
<figure>
  <figcaption>
    <strong>Podcast Episode 5:</strong> Web Accessibility Best Practices
  </figcaption>

  <audio controls>
    <source src="episode5.mp3" type="audio/mpeg">
    <source src="episode5.ogg" type="audio/ogg">
    Your browser doesn't support audio.
    <a href="episode5.mp3">Download the audio file (MP3, 25MB)</a>.
  </audio>

  <details>
    <summary>Show Transcript</summary>
    <div>
      <p><strong>[00:00]</strong> Welcome to episode 5...</p>
      <p><strong>[00:30]</strong> Today we'll discuss...</p>
    </div>
  </details>
</figure>
```

### Keyboard Accessible Controls

Native `<audio controls>` are keyboard accessible by default:
- **Space/Enter**: Play/pause
- **Arrow keys**: Seek forward/backward
- **Tab**: Navigate between controls

### ARIA Labels for Custom Players

```html
<audio id="myAudio" src="song.mp3"></audio>

<button onclick="togglePlay()" aria-label="Play or pause audio">
  <span id="playIcon">▶</span>
</button>

<div role="slider"
     aria-label="Audio progress"
     aria-valuemin="0"
     aria-valuemax="100"
     aria-valuenow="0"
     tabindex="0">
  <!-- Custom progress bar -->
</div>
```

## Browser Support

- **`<audio>` element**: All modern browsers (IE 9+, Chrome 4+, Firefox 3.5+, Safari 3.1+)
- **MP3 format**: Universal support
- **OGG format**: All except Safari/IE
- **WAV format**: Universal support
- **Controls attribute**: All browsers supporting audio

## Common Mistakes

❌ **Autoplay with sound (blocked by browsers)**
```html
<audio controls autoplay src="music.mp3"></audio>
```

✅ **Muted autoplay or user-initiated**
```html
<audio controls autoplay muted src="music.mp3"></audio>
<!-- Or require user interaction -->
```

---

❌ **Single format only**
```html
<audio controls src="audio.mp3"></audio>
```

✅ **Multiple formats for compatibility**
```html
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  <source src="audio.ogg" type="audio/ogg">
</audio>
```

---

❌ **No fallback message**
```html
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
</audio>
```

✅ **Include fallback and download link**
```html
<audio controls>
  <source src="audio.mp3" type="audio/mpeg">
  Your browser doesn't support audio.
  <a href="audio.mp3">Download audio</a>.
</audio>
```

---

❌ **Large file with preload="auto"**
```html
<audio controls preload="auto" src="podcast-100mb.mp3"></audio>
```

✅ **Use preload="metadata" for large files**
```html
<audio controls preload="metadata" src="podcast-100mb.mp3"></audio>
```

## Practice Exercise

Create a podcast player with:
1. Episode title and description
2. Audio player with multiple format support
3. Episode metadata (duration, publish date)
4. Transcript toggle
5. Custom styled player (optional)

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Podcast Player Example</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 700px;
      margin: 50px auto;
      padding: 20px;
      background: #f5f5f5;
    }

    .podcast-episode {
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    h1 {
      color: #2c3e50;
      margin-bottom: 10px;
    }

    .meta {
      color: #7f8c8d;
      font-size: 0.9rem;
      margin-bottom: 20px;
    }

    .description {
      line-height: 1.6;
      color: #555;
      margin-bottom: 25px;
    }

    audio {
      width: 100%;
      margin: 20px 0;
    }

    .transcript {
      margin-top: 30px;
      padding-top: 20px;
      border-top: 2px solid #ecf0f1;
    }

    details {
      cursor: pointer;
    }

    summary {
      font-weight: bold;
      color: #3498db;
      padding: 10px;
      background: #ecf0f1;
      border-radius: 5px;
    }

    summary:hover {
      background: #d5dbdd;
    }

    .transcript-content {
      margin-top: 15px;
      padding: 15px;
      background: #f9f9f9;
      border-left: 3px solid #3498db;
      line-height: 1.8;
    }

    .timestamp {
      color: #3498db;
      font-weight: bold;
    }

    .download-link {
      display: inline-block;
      margin-top: 15px;
      padding: 10px 20px;
      background: #3498db;
      color: white;
      text-decoration: none;
      border-radius: 5px;
    }

    .download-link:hover {
      background: #2980b9;
    }
  </style>
</head>
<body>
  <article class="podcast-episode">
    <h1>Episode 12: The Future of Web Development</h1>

    <div class="meta">
      <span>📅 Published: January 15, 2024</span> •
      <span>⏱️ Duration: 45 minutes</span> •
      <span>🎙️ Host: Sarah Chen</span>
    </div>

    <p class="description">
      In this episode, we explore emerging trends in web development for 2024
      and beyond. Topics include AI-assisted coding, WebAssembly adoption,
      edge computing, and the evolution of JavaScript frameworks. Join us as
      we interview industry experts about what's next for the web platform.
    </p>

    <figure>
      <figcaption><strong>Listen to Episode 12:</strong></figcaption>
      <audio controls preload="metadata">
        <source src="podcast-ep12.mp3" type="audio/mpeg">
        <source src="podcast-ep12.ogg" type="audio/ogg">
        Your browser doesn't support HTML5 audio.
        <a href="podcast-ep12.mp3">Download the episode (MP3, 42MB)</a>.
      </audio>
    </figure>

    <a href="podcast-ep12.mp3" class="download-link" download>
      📥 Download Episode (MP3)
    </a>

    <div class="transcript">
      <details>
        <summary>📄 Show Transcript</summary>
        <div class="transcript-content">
          <p>
            <span class="timestamp">[00:00]</span>
            Welcome to Tech Talk Podcast. I'm your host Sarah Chen, and today
            we're discussing the future of web development.
          </p>
          <p>
            <span class="timestamp">[00:35]</span>
            Let's start with AI-assisted coding. GitHub Copilot and similar
            tools are transforming how developers write code...
          </p>
          <p>
            <span class="timestamp">[05:20]</span>
            Our first guest today is Alex Martinez, a senior engineer at
            WebTech Corp...
          </p>
          <p>
            <span class="timestamp">[15:45]</span>
            Now let's talk about WebAssembly. Many developers are curious
            about when and why to use WASM instead of JavaScript...
          </p>
          <p>
            <span class="timestamp">[42:30]</span>
            Thank you for listening to this episode. Don't forget to subscribe
            and leave a review. See you next week!
          </p>
        </div>
      </details>
    </div>
  </article>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [The Audio element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)
- **W3Schools**: [HTML Audio](https://www.w3schools.com/html/html5_audio.asp)
- **Can I Use**: [Audio format support](https://caniuse.com/audio)
- **Web.dev**: [Media and Source Tags](https://web.dev/media-source/)

---

**Previous Topic**: [Figure and Figcaption](./figure-figcaption.md)
**Next Topic**: [Video](./video.md)
**Category**: [Media Elements](./README.md)
