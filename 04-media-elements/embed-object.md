# Embed and Object Elements

## Overview
The `<embed>` and `<object>` elements allow you to embed external content and resources into HTML documents, including PDFs, Flash content (deprecated), plugins, and other media types. While historically used for Flash and Java applets, they're now primarily used for PDFs and specialized plugins.

## The Embed Element

### Basic Syntax

```html
<embed src="document.pdf" type="application/pdf" width="800" height="600">
```

**Key Points:**
- Self-closing (void) element
- No fallback content support
- Simple syntax for basic embedding
- Primarily used for PDFs

### Attributes

```html
<embed src="file.pdf"           <!-- Source URL (required) -->
       type="application/pdf"    <!-- MIME type -->
       width="800"               <!-- Width in pixels -->
       height="600">             <!-- Height in pixels -->
```

### Common Uses

#### Embedding PDF

```html
<embed src="whitepaper.pdf"
       type="application/pdf"
       width="100%"
       height="800px">
```

#### Embedding with Frame

```html
<div style="border: 2px solid #ddd; padding: 20px;">
  <h3>Product Manual (PDF)</h3>
  <embed src="manual.pdf"
         type="application/pdf"
         width="100%"
         height="600px"
         style="border: none;">
</div>
```

## The Object Element

### Basic Syntax

```html
<object data="document.pdf" type="application/pdf" width="800" height="600">
  <p>Your browser doesn't support PDFs. <a href="document.pdf">Download instead</a>.</p>
</object>
```

**Key Points:**
- Supports fallback content (text between tags)
- More flexible than `<embed>`
- Better for accessibility
- Can nest multiple objects as fallbacks

### Attributes

```html
<object data="file.pdf"              <!-- Source URL -->
        type="application/pdf"       <!-- MIME type -->
        width="800"                  <!-- Width -->
        height="600"                 <!-- Height -->
        name="pdfViewer"             <!-- Name for scripting -->
        usemap="#mapname"            <!-- Image map reference -->
        form="formid"                <!-- Associated form -->
        typemustmatch>               <!-- Type must match data -->
  Fallback content here
</object>
```

### Common Uses

#### PDF with Fallback

```html
<object data="report-2024.pdf"
        type="application/pdf"
        width="100%"
        height="800px">
  <p>
    Unable to display PDF.
    <a href="report-2024.pdf" download>Download the report (PDF, 2.3 MB)</a>
  </p>
</object>
```

#### Nested Objects (Progressive Enhancement)

```html
<object data="animation.svg" type="image/svg+xml" width="400" height="300">
  <object data="animation.png" type="image/png" width="400" height="300">
    <p>Animation not supported. <a href="animation.svg">View SVG</a></p>
  </object>
</object>
```

#### YouTube Video (Alternative to iframe)

```html
<object data="https://www.youtube.com/embed/VIDEO_ID"
        width="560"
        height="315">
  <param name="allowfullscreen" value="true">
  <p>Video cannot be displayed. <a href="https://www.youtube.com/watch?v=VIDEO_ID">Watch on YouTube</a>.</p>
</object>
```

**Note**: `<iframe>` is preferred for embedding YouTube videos in modern web development.

## Param Element (for Object)

The `<param>` element defines parameters for `<object>` elements.

```html
<object data="movie.swf" type="application/x-shockwave-flash" width="400" height="300">
  <param name="autoplay" value="false">
  <param name="loop" value="false">
  <param name="quality" value="high">
  <p>Flash is not supported.</p>
</object>
```

**Common parameters:**
- `autoplay`: Auto-start playback
- `loop`: Repeat content
- `quality`: Rendering quality
- `bgcolor`: Background color
- `allowfullscreen`: Enable fullscreen mode

## Embed vs Object vs Iframe

| Feature | `<embed>` | `<object>` | `<iframe>` |
|---------|-----------|-----------|-----------|
| Fallback content | ❌ No | ✅ Yes | ✅ Yes |
| Accessibility | ⚠️ Limited | ✅ Good | ✅ Best |
| PDF embedding | ✅ Good | ✅ Good | ✅ Better |
| External HTML | ❌ No | ⚠️ Limited | ✅ Yes |
| Plugin support | ✅ Yes | ✅ Yes | ❌ No |
| Modern use | ⚠️ Legacy | ⚠️ Legacy | ✅ Preferred |

### When to Use Each

**Use `<iframe>`** (Recommended):
- Embedding external web pages
- YouTube/Vimeo videos
- Google Maps
- Social media embeds
- PDFs (modern approach)

**Use `<object>`**:
- PDFs with fallback content needed
- SVG with fallback images
- Specialized plugins (rare)

**Use `<embed>`**:
- Legacy browser support
- Simple PDF embedding without fallbacks
- Plugins requiring minimal configuration

## PDF Embedding Comparison

### Using Iframe (Recommended)

```html
<iframe src="document.pdf"
        width="100%"
        height="800px"
        style="border: none;">
  <p>Your browser doesn't support iframes. <a href="document.pdf">Download PDF</a>.</p>
</iframe>
```

### Using Object (Good Fallback)

```html
<object data="document.pdf"
        type="application/pdf"
        width="100%"
        height="800px">
  <p>
    PDF cannot be displayed.
    <a href="document.pdf" download>Download instead (PDF, 1.5 MB)</a>
  </p>
</object>
```

### Using Embed (Simple)

```html
<embed src="document.pdf"
       type="application/pdf"
       width="100%"
       height="800px">
```

### Best Practice: Progressive Enhancement

```html
<!-- Try iframe first -->
<iframe src="report.pdf"
        width="100%"
        height="800px"
        style="border: 1px solid #ddd;">

  <!-- Fallback to object if iframe fails -->
  <object data="report.pdf"
          type="application/pdf"
          width="100%"
          height="800px">

    <!-- Final fallback: download link -->
    <p>
      Cannot display PDF in your browser.
      <a href="report.pdf" download class="download-btn">
        📄 Download Report (PDF, 2.1 MB)
      </a>
    </p>
  </object>
</iframe>
```

## Accessibility Considerations

### Provide Text Alternatives

```html
<object data="infographic.pdf"
        type="application/pdf"
        width="100%"
        height="1000px"
        aria-label="Annual Report 2024 Infographic">
  <p>
    This document contains our 2024 annual report infographic showing
    revenue growth, customer metrics, and market expansion.
    <a href="infographic.pdf" download>Download PDF (1.8 MB)</a>
  </p>
</object>
```

### Include Download Links

```html
<figure>
  <object data="user-guide.pdf"
          type="application/pdf"
          width="100%"
          height="600px">
    <p>PDF viewer not available. <a href="user-guide.pdf">Download guide</a>.</p>
  </object>

  <figcaption>
    User Guide v2.3 (PDF, 3.4 MB)
    <a href="user-guide.pdf" download>Download</a> |
    <a href="user-guide.html">HTML version</a>
  </figcaption>
</figure>
```

### Keyboard Navigation

```html
<!-- Iframe with proper title for screen readers -->
<iframe src="document.pdf"
        title="Product Specification Document"
        width="100%"
        height="800px"
        tabindex="0">
  <a href="document.pdf">Download specification</a>
</iframe>
```

## Common Use Cases

### Technical Documentation

```html
<article>
  <h2>API Documentation</h2>
  <p>Complete reference guide for our REST API endpoints</p>

  <div style="margin: 20px 0; border: 2px solid #e0e0e0; border-radius: 8px; padding: 15px;">
    <object data="api-docs.pdf"
            type="application/pdf"
            width="100%"
            height="900px"
            style="display: block;">
      <p style="text-align: center; padding: 40px;">
        <strong>PDF Viewer Not Available</strong><br><br>
        <a href="api-docs.pdf" download style="display: inline-block; padding: 12px 30px; background: #007bff; color: white; text-decoration: none; border-radius: 5px;">
          📥 Download Documentation (PDF, 4.2 MB)
        </a>
      </p>
    </object>
  </div>
</article>
```

### Product Catalog

```html
<section class="product-catalog">
  <h2>2024 Product Catalog</h2>

  <object data="catalog-2024.pdf"
          type="application/pdf"
          width="100%"
          height="1000px">
    <div style="text-align: center; padding: 60px 20px; background: #f8f9fa;">
      <h3>View Our Product Catalog</h3>
      <p>Browse over 500 products across 12 categories</p>
      <a href="catalog-2024.pdf" download class="btn-primary">
        Download Catalog (PDF, 15 MB)
      </a>
      <br><br>
      <small>Or <a href="products.html">browse online version</a></small>
    </div>
  </object>
</section>
```

### Embedded SVG with PNG Fallback

```html
<object data="logo-animated.svg"
        type="image/svg+xml"
        width="300"
        height="100"
        aria-label="Company logo">
  <img src="logo-static.png" alt="Company logo" width="300" height="100">
</object>
```

### Legal Documents

```html
<div class="legal-document">
  <h3>Terms of Service</h3>
  <p>Last updated: January 15, 2024</p>

  <object data="terms-of-service.pdf"
          type="application/pdf"
          width="100%"
          height="700px">
    <p>
      Terms of Service document (PDF format)
      <br><br>
      <a href="terms-of-service.pdf" download>📄 Download PDF (850 KB)</a>
      <br>
      <a href="terms.html">📖 Read HTML version</a>
    </p>
  </object>
</div>
```

## Security Considerations

### Same-Origin Policy

```html
<!-- ⚠️ External PDFs may not display due to CORS -->
<object data="https://external-site.com/document.pdf"
        type="application/pdf"
        width="100%"
        height="800px">
  <p>External PDF may not display. <a href="https://external-site.com/document.pdf">View directly</a>.</p>
</object>
```

### Sandboxing

```html
<!-- Use iframe with sandbox for untrusted content -->
<iframe src="untrusted.pdf"
        sandbox="allow-same-origin allow-scripts"
        width="100%"
        height="800px">
</iframe>
```

### Content Security Policy

```html
<!-- Set CSP headers to control what can be embedded -->
<meta http-equiv="Content-Security-Policy"
      content="object-src 'self' https://trusted-cdn.com;">
```

## Browser Support

| Element | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| `<embed>` | ✅ All | ✅ All | ✅ All | ✅ All |
| `<object>` | ✅ All | ✅ All | ✅ All | ✅ All |
| PDF embedding | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| Flash (.swf) | ❌ Removed | ❌ Removed | ❌ Removed | ❌ Removed |

**Note**: Flash support was removed from all major browsers by end of 2020.

## Common Mistakes

❌ **Using Flash content**
```html
<object data="animation.swf" type="application/x-shockwave-flash">
  <!-- Flash is dead! Don't use this -->
</object>
```

✅ **Use HTML5 alternatives**
```html
<video controls>
  <source src="animation.mp4" type="video/mp4">
</video>
<!-- Or use Canvas, SVG, CSS animations -->
```

---

❌ **No fallback content**
```html
<object data="document.pdf" type="application/pdf" width="800" height="600">
</object>
```

✅ **Always provide fallback**
```html
<object data="document.pdf" type="application/pdf" width="800" height="600">
  <p>PDF not supported. <a href="document.pdf">Download instead</a>.</p>
</object>
```

---

❌ **Using object for modern video**
```html
<object data="video.mp4" width="640" height="360"></object>
```

✅ **Use video element**
```html
<video controls width="640" height="360">
  <source src="video.mp4" type="video/mp4">
</video>
```

## Modern Alternatives

### Instead of Flash Animations
- **HTML5 Video**: For video content
- **Canvas/WebGL**: For interactive graphics
- **CSS Animations**: For simple animations
- **SVG**: For vector animations
- **JavaScript libraries**: Three.js, Pixi.js

### Instead of Java Applets
- **WebAssembly**: For performance-critical code
- **JavaScript**: For most application logic
- **Web APIs**: Geolocation, WebRTC, etc.

### Instead of PDF Embedding
- **PDF.js**: JavaScript PDF viewer library
- **Native HTML**: Convert PDFs to HTML content
- **Google Docs Viewer**: External service
- **Cloud document viewers**: Microsoft Office Online, etc.

## Practice Exercise

Create a documentation page with:
1. Embedded PDF using iframe (primary method)
2. Object fallback with download link
3. Responsive container
4. Accessibility features
5. Download and HTML view options

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Technical Documentation</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
      background: #f5f5f5;
    }

    .doc-container {
      background: white;
      border-radius: 10px;
      padding: 30px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    h1 {
      color: #2c3e50;
      margin-bottom: 10px;
    }

    .meta {
      color: #7f8c8d;
      margin-bottom: 20px;
      padding-bottom: 20px;
      border-bottom: 2px solid #ecf0f1;
    }

    .doc-actions {
      display: flex;
      gap: 15px;
      margin-bottom: 25px;
      flex-wrap: wrap;
    }

    .btn {
      display: inline-block;
      padding: 12px 25px;
      border-radius: 5px;
      text-decoration: none;
      font-weight: bold;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    }

    .btn-primary {
      background: #3498db;
      color: white;
    }

    .btn-secondary {
      background: #95a5a6;
      color: white;
    }

    .btn-success {
      background: #2ecc71;
      color: white;
    }

    .pdf-viewer {
      width: 100%;
      border: 2px solid #e0e0e0;
      border-radius: 8px;
      overflow: hidden;
      background: #fafafa;
    }

    .pdf-viewer iframe,
    .pdf-viewer object {
      width: 100%;
      height: 800px;
      display: block;
      border: none;
    }

    .fallback-content {
      text-align: center;
      padding: 60px 20px;
      background: #f8f9fa;
    }

    .fallback-content h3 {
      color: #2c3e50;
      margin-bottom: 15px;
    }

    .fallback-content p {
      color: #7f8c8d;
      margin-bottom: 25px;
    }

    @media (max-width: 768px) {
      .doc-container {
        padding: 15px;
      }

      .pdf-viewer iframe,
      .pdf-viewer object {
        height: 500px;
      }

      .doc-actions {
        flex-direction: column;
      }

      .btn {
        text-align: center;
      }
    }
  </style>
</head>
<body>
  <div class="doc-container">
    <h1>API Reference Guide v3.2</h1>

    <div class="meta">
      <p>
        <strong>Version:</strong> 3.2.1 |
        <strong>Published:</strong> January 15, 2024 |
        <strong>File Size:</strong> 3.4 MB
      </p>
    </div>

    <div class="doc-actions">
      <a href="api-reference.pdf" download class="btn btn-primary">
        📥 Download PDF
      </a>
      <a href="api-reference.html" class="btn btn-secondary">
        📖 HTML Version
      </a>
      <a href="javascript:window.print()" class="btn btn-success">
        🖨️ Print
      </a>
    </div>

    <div class="pdf-viewer">
      <!-- Primary: iframe -->
      <iframe src="api-reference.pdf"
              title="API Reference Guide"
              width="100%"
              height="800"
              loading="lazy">

        <!-- Fallback: object -->
        <object data="api-reference.pdf"
                type="application/pdf"
                width="100%"
                height="800">

          <!-- Final fallback: message and links -->
          <div class="fallback-content">
            <h3>📄 PDF Viewer Not Available</h3>
            <p>
              Your browser cannot display PDF files inline.
              Please download the document or view the HTML version.
            </p>

            <div style="display: flex; gap: 15px; justify-content: center; flex-wrap: wrap;">
              <a href="api-reference.pdf" download class="btn btn-primary">
                Download PDF (3.4 MB)
              </a>
              <a href="api-reference.html" class="btn btn-secondary">
                View HTML Version
              </a>
            </div>

            <p style="margin-top: 30px; font-size: 0.9rem;">
              <strong>Document Contents:</strong><br>
              Introduction • Authentication • Endpoints • Response Formats •
              Error Handling • Rate Limiting • Examples • Changelog
            </p>
          </div>
        </object>
      </iframe>
    </div>

    <div style="margin-top: 30px; padding: 20px; background: #f8f9fa; border-left: 4px solid #3498db; border-radius: 4px;">
      <h3 style="margin-top: 0;">📚 Additional Resources</h3>
      <ul style="line-height: 2;">
        <li><a href="quickstart.html">Quick Start Guide</a></li>
        <li><a href="tutorials.html">Video Tutorials</a></li>
        <li><a href="changelog.html">Changelog</a></li>
        <li><a href="support.html">Support Portal</a></li>
      </ul>
    </div>
  </div>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [The Embed element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/embed)
- **MDN Web Docs**: [The Object element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/object)
- **W3Schools**: [HTML embed Tag](https://www.w3schools.com/tags/tag_embed.asp)
- **W3Schools**: [HTML object Tag](https://www.w3schools.com/tags/tag_object.asp)

---

**Previous Topic**: [Video](./video.md)
**Next Topic**: [Image Maps](./image-maps.md)
**Category**: [Media Elements](./README.md)
