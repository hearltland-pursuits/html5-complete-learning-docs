---
title: Download Links
category: Links and Navigation
order: 5
---

# Download Links

> **Quick Summary:** The download attribute instructs browsers to download linked resources instead of navigating to them, enabling users to save files like PDFs, images, documents, and media with custom filenames directly from web pages.

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

## Introduction

The `download` attribute transforms regular hyperlinks into download triggers, prompting browsers to save the linked resource to the user's device rather than navigating to or displaying it. This attribute is essential for providing downloadable content like PDFs, images, documents, software installers, and data exports.

When a user clicks a link with the `download` attribute, the browser initiates a file download dialog (or automatic download, depending on browser settings) with either the original filename or a custom filename specified in the attribute value. This simple addition significantly improves user experience by eliminating the need for users to right-click and select "Save As" or navigate away from the current page.

The download attribute works best with same-origin resources (files hosted on your domain). Cross-origin downloads (files from different domains) may not work due to browser security restrictions and CORS policies. Understanding these limitations and providing appropriate fallbacks ensures a smooth experience for all users across different browsers and configurations.

**Key Concept:** Adding `download` to a link triggers file download instead of navigation. Specify custom filenames with `download="filename.ext"`. Works best for same-origin resources due to CORS restrictions.

## Basic Syntax

**Basic download link (uses original filename):**
```html
<a href="/files/report.pdf" download>Download Report</a>
```

**Download with custom filename:**
```html
<a href="/files/q4-2025-report.pdf" download="Q4-Financial-Report.pdf">
  Download Q4 Report
</a>
```

**Download attribute syntax:**

| Syntax | Behavior | Example |
|--------|----------|---------|
| `download` | Download with original filename | `<a href="file.pdf" download>` |
| `download="newname.pdf"` | Download with custom filename | `<a href="old.pdf" download="new.pdf">` |
| `download=""` | Download with original filename | `<a href="file.pdf" download="">` |

**File types commonly used with download:**

| File Type | Extension | MIME Type | Use Case |
|-----------|-----------|-----------|----------|
| PDF | `.pdf` | `application/pdf` | Documents, reports, forms |
| Word | `.docx` | `application/vnd.openxmlformats-officedocument.wordprocessingml.document` | Editable documents |
| Excel | `.xlsx` | `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet` | Spreadsheets, data |
| Image | `.jpg`, `.png` | `image/jpeg`, `image/png` | Photos, graphics |
| ZIP | `.zip` | `application/zip` | Compressed archives |
| CSV | `.csv` | `text/csv` | Data exports |
| MP3 | `.mp3` | `audio/mpeg` | Audio files |
| MP4 | `.mp4` | `video/mp4` | Video files |

**Important:** The `type` attribute (MIME type) is optional but recommended for clarity:

```html
<a href="/files/data.csv" download="export.csv" type="text/csv">
  Download CSV Data
</a>
```

## Examples

### Example 1: Document Downloads with File Info
**Use Case:** Resource library with downloadable PDFs

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Resource Library</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 40px 20px;
      line-height: 1.7;
    }
    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #3498db;
      padding-bottom: 0.5em;
    }
    .resource-list {
      list-style: none;
      padding: 0;
    }
    .resource-item {
      background-color: #ecf0f1;
      margin: 1.5em 0;
      padding: 1.5em;
      border-radius: 8px;
      border-left: 4px solid #3498db;
    }
    .resource-item h3 {
      color: #34495e;
      margin-bottom: 0.5em;
    }
    .resource-meta {
      color: #7f8c8d;
      font-size: 0.9em;
      margin: 0.5em 0;
    }
    .download-btn {
      display: inline-block;
      background-color: #27ae60;
      color: white;
      padding: 0.75em 1.5em;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      margin-top: 1em;
      transition: background-color 0.3s;
    }
    .download-btn:hover,
    .download-btn:focus {
      background-color: #229954;
    }
    .download-btn:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }
    .download-btn::before {
      content: "⬇ ";
      font-size: 1.2em;
    }
  </style>
</head>
<body>
  <article>
    <h1>Resource Library</h1>

    <ul class="resource-list">
      <li class="resource-item">
        <h3>2025 Marketing Strategy Guide</h3>
        <p>
          Comprehensive guide to digital marketing strategies for small
          businesses. Includes SEO, social media, and content marketing tactics.
        </p>
        <p class="resource-meta">
          <strong>Format:</strong> PDF |
          <strong>Size:</strong> 2.4 MB |
          <strong>Pages:</strong> 45
        </p>
        <a href="/files/marketing-guide-2025.pdf"
           download="Marketing-Strategy-Guide-2025.pdf"
           class="download-btn">
          Download PDF (2.4 MB)
        </a>
      </li>

      <li class="resource-item">
        <h3>Financial Planning Template</h3>
        <p>
          Excel spreadsheet with formulas for budgeting, expense tracking,
          and financial forecasting. Ready to customize for your business.
        </p>
        <p class="resource-meta">
          <strong>Format:</strong> Excel (.xlsx) |
          <strong>Size:</strong> 156 KB
        </p>
        <a href="/files/financial-template.xlsx"
           download="Financial-Planning-Template.xlsx"
           type="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
           class="download-btn">
          Download Excel Template (156 KB)
        </a>
      </li>

      <li class="resource-item">
        <h3>Brand Assets Package</h3>
        <p>
          Complete branding package including logos, color palettes, typography
          guidelines, and usage examples. Available in multiple formats.
        </p>
        <p class="resource-meta">
          <strong>Format:</strong> ZIP archive |
          <strong>Size:</strong> 8.7 MB |
          <strong>Contents:</strong> PSD, AI, SVG, PNG files
        </p>
        <a href="/files/brand-assets.zip"
           download="Brand-Assets-Package.zip"
           type="application/zip"
           class="download-btn">
          Download ZIP Archive (8.7 MB)
        </a>
      </li>
    </ul>
  </article>
</body>
</html>
```

### Example 2: Image Downloads with Preview
**Use Case:** Stock photo library with downloadable images

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Stock Photos</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 1200px;
      margin: 0 auto;
      padding: 40px 20px;
    }
    h1 {
      text-align: center;
      color: #2c3e50;
    }
    .photo-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 2em;
      margin: 3em 0;
    }
    .photo-card {
      background-color: white;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s;
    }
    .photo-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
    }
    .photo-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      display: block;
    }
    .photo-info {
      padding: 1.5em;
    }
    .photo-title {
      color: #2c3e50;
      font-size: 1.2em;
      margin-bottom: 0.5em;
    }
    .photo-meta {
      color: #7f8c8d;
      font-size: 0.9em;
      margin-bottom: 1em;
    }
    .download-options {
      display: flex;
      gap: 0.75em;
    }
    .download-link {
      flex: 1;
      background-color: #3498db;
      color: white;
      padding: 0.75em;
      text-align: center;
      text-decoration: none;
      border-radius: 6px;
      font-weight: bold;
      transition: background-color 0.3s;
    }
    .download-link:hover,
    .download-link:focus {
      background-color: #2980b9;
    }
    .download-link:focus {
      outline: 2px solid #FFD700;
      outline-offset: 2px;
    }
  </style>
</head>
<body>
  <h1>Free Stock Photos</h1>

  <div class="photo-grid">
    <article class="photo-card">
      <img src="mountain-landscape.jpg" alt="Mountain landscape at sunset">
      <div class="photo-info">
        <h3 class="photo-title">Mountain Sunset</h3>
        <p class="photo-meta">
          4000 × 3000 px | JPEG | 2.1 MB
        </p>
        <div class="download-options">
          <a href="mountain-landscape.jpg"
             download="mountain-sunset-4k.jpg"
             class="download-link">
            Download Original
          </a>
        </div>
      </div>
    </article>

    <article class="photo-card">
      <img src="city-skyline.jpg" alt="City skyline at night">
      <div class="photo-info">
        <h3 class="photo-title">City Lights</h3>
        <p class="photo-meta">
          5000 × 3333 px | JPEG | 3.8 MB
        </p>
        <div class="download-options">
          <a href="city-skyline.jpg"
             download="city-lights-5k.jpg"
             class="download-link">
            Download Original
          </a>
        </div>
      </div>
    </article>

    <article class="photo-card">
      <img src="forest-path.jpg" alt="Forest path with sunlight filtering through trees">
      <div class="photo-info">
        <h3 class="photo-title">Forest Path</h3>
        <p class="photo-meta">
          3840 × 2160 px | JPEG | 1.9 MB
        </p>
        <div class="download-options">
          <a href="forest-path.jpg"
             download="forest-path-4k.jpg"
             class="download-link">
            Download Original
          </a>
        </div>
      </div>
    </article>
  </div>
</body>
</html>
```

### Example 3: Data Export with Multiple Formats
**Use Case:** Analytics dashboard with data export options

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Analytics Dashboard</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 800px;
      margin: 0 auto;
      padding: 40px 20px;
    }
    .export-section {
      background-color: #ecf0f1;
      padding: 2em;
      border-radius: 12px;
      margin: 2em 0;
    }
    .export-section h2 {
      color: #2c3e50;
      margin-bottom: 1em;
    }
    .export-options {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1em;
    }
    .export-btn {
      display: flex;
      flex-direction: column;
      align-items: center;
      background-color: white;
      padding: 1.5em;
      text-decoration: none;
      border-radius: 8px;
      border: 2px solid #3498db;
      color: #2c3e50;
      transition: all 0.3s;
    }
    .export-btn:hover,
    .export-btn:focus {
      background-color: #3498db;
      color: white;
      transform: scale(1.05);
    }
    .export-btn:focus {
      outline: 3px solid #FFD700;
      outline-offset: 2px;
    }
    .export-icon {
      font-size: 2.5em;
      margin-bottom: 0.5em;
    }
    .export-format {
      font-weight: bold;
      font-size: 1.1em;
      margin-bottom: 0.25em;
    }
    .export-desc {
      font-size: 0.85em;
      color: #7f8c8d;
      text-align: center;
    }
    .export-btn:hover .export-desc,
    .export-btn:focus .export-desc {
      color: #ecf0f1;
    }
  </style>
</head>
<body>
  <h1>Analytics Dashboard</h1>

  <section class="export-section">
    <h2>Export Your Data</h2>
    <p>
      Download your analytics data in your preferred format. All exports
      include the last 30 days of data.
    </p>

    <div class="export-options">
      <a href="/api/export/csv"
         download="analytics-data.csv"
         type="text/csv"
         class="export-btn">
        <span class="export-icon" aria-hidden="true">📊</span>
        <span class="export-format">CSV</span>
        <span class="export-desc">Spreadsheet format</span>
      </a>

      <a href="/api/export/json"
         download="analytics-data.json"
         type="application/json"
         class="export-btn">
        <span class="export-icon" aria-hidden="true">{ }</span>
        <span class="export-format">JSON</span>
        <span class="export-desc">Developer friendly</span>
      </a>

      <a href="/api/export/pdf"
         download="analytics-report.pdf"
         type="application/pdf"
         class="export-btn">
        <span class="export-icon" aria-hidden="true">📄</span>
        <span class="export-format">PDF</span>
        <span class="export-desc">Print-ready report</span>
      </a>

      <a href="/api/export/xlsx"
         download="analytics-data.xlsx"
         type="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
         class="export-btn">
        <span class="export-icon" aria-hidden="true">📈</span>
        <span class="export-format">Excel</span>
        <span class="export-desc">Advanced analysis</span>
      </a>
    </div>
  </section>
</body>
</html>
```

## Common Use Cases

### 1. Document Downloads
Provide downloadable PDFs, Word documents, presentations:

```html
<a href="/files/whitepaper.pdf" download="Company-Whitepaper-2025.pdf">
  Download Whitepaper (PDF, 3.2 MB)
</a>
```

**When to use:** Reports, ebooks, whitepapers, forms, templates

### 2. Image Downloads
Allow users to save images, graphics, photos:

```html
<a href="/images/high-res-logo.png" download="Company-Logo-HighRes.png">
  Download High-Resolution Logo
</a>
```

**When to use:** Stock photos, logos, graphics, wallpapers

### 3. Data Exports
Export user data, reports, analytics:

```html
<a href="/api/export/csv" download="user-data-export.csv">
  Export Data as CSV
</a>
```

**When to use:** Dashboard exports, data backups, user data portability

## Browser Support

| Feature | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|---------|--------|---------|--------|------|---------------|---------------|
| `download` attribute | 14+ | 20+ | 10.1+ | 18+ | 13+ | 18+ |
| Custom filename | 14+ | 20+ | 10.1+ | 18+ | 13+ | 18+ |
| Cross-origin download | Limited | Limited | Limited | Limited | Limited | Limited |

**Browser Support:** Excellent (98%+)

The `download` attribute was introduced in HTML5 and has broad support in modern browsers. Older browsers (IE11 and earlier) ignore the attribute and navigate to the file instead.

**Cross-Origin Restrictions:**
- Same-origin downloads: ✅ Full support
- Cross-origin downloads: ⚠️ May not work due to CORS
- Workaround: Serve files from your domain or use server-side proxy

**Fallback for older browsers:**

```html
<a href="/files/document.pdf" download>
  Download PDF
</a>
<!-- In IE11 and older: Opens PDF in browser instead of downloading -->
```

**Resources:**
- [MDN: download attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#download)
- [Can I Use: download attribute](https://caniuse.com/download)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements:**
- **Link Purpose (2.4.4):** Link text must describe what will be downloaded
- **Non-text Content (1.1.1):** Provide file type and size information

**Level AA Requirements:**
- **Link Purpose in Context (2.4.4):** Make download intent clear from link text alone

### Best Practices

1. **Include file type and size in link text:**

```html
<!-- GOOD: Clear information -->
<a href="/files/report.pdf" download>
  Download Annual Report (PDF, 2.3 MB)
</a>

<!-- BAD: Missing information -->
<a href="/files/report.pdf" download>
  Download Report
</a>
```

2. **Use descriptive link text:**

```html
<!-- GOOD: Descriptive -->
<a href="/files/guide.pdf" download="SEO-Guide-2025.pdf">
  Download SEO Best Practices Guide (PDF, 1.8 MB)
</a>

<!-- BAD: Generic -->
<a href="/files/guide.pdf" download>
  Click here
</a>
```

3. **Warn about file downloads:**

```html
<!-- Visual indicator -->
<a href="/files/large-dataset.zip" download>
  ⬇ Download Dataset (ZIP, 45 MB)
</a>
```

4. **Provide alternative formats:**

```html
<p>
  Download in your preferred format:
  <a href="/files/data.csv" download>CSV</a> |
  <a href="/files/data.xlsx" download>Excel</a> |
  <a href="/files/data.json" download>JSON</a>
</p>
```

**Resources:**
- [WCAG 2.1: Link Purpose (2.4.4)](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
- [WebAIM: Links and Hypertext](https://webaim.org/techniques/hypertext/)

## Best Practices

### Do This ✓

1. **Include file type and size:**
```html
<a href="/files/report.pdf" download="Q4-Report.pdf">
  Download Q4 Report (PDF, 2.3 MB)
</a>
```

2. **Use descriptive custom filenames:**
```html
<a href="/uploads/doc123.pdf" download="2025-Marketing-Strategy.pdf">
  Download Marketing Strategy
</a>
```

3. **Add type attribute for clarity:**
```html
<a href="/files/data.csv"
   download="export.csv"
   type="text/csv">
  Download CSV
</a>
```

4. **Style download links distinctively:**
```css
a[download] {
  background-color: #27ae60;
  color: white;
  padding: 0.75em 1.5em;
  text-decoration: none;
}
a[download]::before {
  content: "⬇ ";
}
```

5. **Provide multiple format options:**
```html
<p>
  Download report:
  <a href="/report.pdf" download>PDF</a> |
  <a href="/report.docx" download>Word</a> |
  <a href="/report.txt" download>Text</a>
</p>
```

### Avoid This ✗

1. **Don't omit file information:**
```html
<!-- WRONG: No file type or size -->
<a href="/files/document.pdf" download>Download</a>

<!-- CORRECT: Clear information -->
<a href="/files/document.pdf" download>
  Download Document (PDF, 1.5 MB)
</a>
```

2. **Don't use generic filenames:**
```html
<!-- WRONG: Generic filename -->
<a href="/doc.pdf" download="download.pdf">Download</a>

<!-- CORRECT: Descriptive filename -->
<a href="/doc.pdf" download="Annual-Report-2025.pdf">
  Download Annual Report
</a>
```

3. **Don't rely on cross-origin downloads:**
```html
<!-- WRONG: May not work (CORS) -->
<a href="https://example.com/file.pdf" download>Download</a>

<!-- CORRECT: Use same-origin or proxy -->
<a href="/files/file.pdf" download>Download</a>
```

4. **Don't use download for navigation:**
```html
<!-- WRONG: Should navigate, not download -->
<a href="/about.html" download>About Us</a>

<!-- CORRECT: Regular link for navigation -->
<a href="/about.html">About Us</a>
```

5. **Don't forget virus scanning for uploads:**
```html
<!-- If allowing user uploads, scan for malware before serving -->
<!-- Server-side validation and scanning required -->
```

## Related Topics

### Prerequisites
- [Anchor Links](anchor-links.md) - Basic hyperlink syntax
- [Link States](link-states.md) - Styling download links

### Related Topics
- [Email and Telephone Links](email-telephone-links.md) - Other special link types
- [Forms](../06-forms-input/form-element.md) - File upload functionality
- [Global Attributes](../09-global-attributes/id-class.md) - HTML attributes

### Next Steps
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Document structure
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - Accessible downloads
- [Security](../14-modern-html5/html5-security.md) - Secure file serving

## Practice Exercise

### Requirements
Create a **"Resource Downloads Page"** demonstrating download links with:

1. At least 3 downloadable resources (different file types)
2. File type and size displayed for each download
3. Custom filenames for all downloads
4. Styled download buttons with visual indicators
5. CSS that distinguishes download links from regular links

**Accessibility Requirements:**
- Descriptive link text (includes file type and size)
- Visible download icon or indicator
- Keyboard accessible with focus states
- Clear purpose from link text alone

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Resources</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
    }
    /* Add your styling here */
  </style>
</head>
<body>
  <!-- Add your content here -->
</body>
</html>
```

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Free Resources - Marketing Templates</title>
  <style>
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      max-width: 1000px;
      margin: 0 auto;
      padding: 40px 20px;
      line-height: 1.7;
      background-color: #f4f4f4;
    }
    h1 {
      color: #2c3e50;
      text-align: center;
      margin-bottom: 0.5em;
    }
    .intro {
      text-align: center;
      color: #7f8c8d;
      margin-bottom: 3em;
    }
    .resources-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2em;
    }
    .resource-card {
      background-color: white;
      padding: 2em;
      border-radius: 12px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s;
    }
    .resource-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 8px 12px rgba(0, 0, 0, 0.15);
    }
    .resource-card h2 {
      color: #34495e;
      margin-bottom: 0.75em;
      font-size: 1.5em;
    }
    .resource-description {
      color: #555;
      margin-bottom: 1.5em;
    }
    .resource-meta {
      display: flex;
      gap: 1.5em;
      margin-bottom: 1.5em;
      font-size: 0.9em;
      color: #7f8c8d;
    }
    .meta-item {
      display: flex;
      align-items: center;
      gap: 0.5em;
    }
    .download-btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      background-color: #27ae60;
      color: white;
      padding: 1em 1.5em;
      text-decoration: none;
      border-radius: 8px;
      font-weight: bold;
      font-size: 1.05em;
      transition: all 0.3s;
      border: none;
    }
    .download-btn::before {
      content: "⬇";
      font-size: 1.3em;
      margin-right: 0.5em;
    }
    .download-btn:hover,
    .download-btn:focus {
      background-color: #229954;
      transform: scale(1.02);
    }
    .download-btn:focus {
      outline: 3px solid #FFD700;
      outline-offset: 3px;
    }
    .download-btn:active {
      transform: scale(0.98);
    }
    .icon {
      font-size: 1.2em;
    }
  </style>
</head>
<body>
  <header>
    <h1>Free Marketing Resources</h1>
    <p class="intro">
      Download professional templates and guides to jumpstart your marketing efforts.
      All resources are free for personal and commercial use.
    </p>
  </header>

  <main class="resources-grid">
    <article class="resource-card">
      <h2>Social Media Content Calendar</h2>
      <p class="resource-description">
        Plan your social media posts for the entire month with this
        comprehensive Excel template. Includes tabs for Facebook, Instagram,
        Twitter, and LinkedIn.
      </p>
      <div class="resource-meta">
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📄</span>
          <span>Excel (.xlsx)</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">💾</span>
          <span>247 KB</span>
        </span>
      </div>
      <a href="/files/social-media-calendar.xlsx"
         download="Social-Media-Content-Calendar-2025.xlsx"
         type="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
         class="download-btn">
        Download Excel Template
      </a>
    </article>

    <article class="resource-card">
      <h2>SEO Checklist Guide</h2>
      <p class="resource-description">
        Complete 50-point SEO checklist covering technical SEO, on-page
        optimization, content strategy, and link building. Perfect for
        beginners and professionals.
      </p>
      <div class="resource-meta">
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📄</span>
          <span>PDF</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">💾</span>
          <span>1.8 MB</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📖</span>
          <span>32 pages</span>
        </span>
      </div>
      <a href="/files/seo-checklist.pdf"
         download="Complete-SEO-Checklist-2025.pdf"
         type="application/pdf"
         class="download-btn">
        Download PDF Guide
      </a>
    </article>

    <article class="resource-card">
      <h2>Email Marketing Templates</h2>
      <p class="resource-description">
        Collection of 10 responsive email templates for newsletters, promotions,
        and announcements. Fully customizable HTML/CSS files ready to use with
        any email service provider.
      </p>
      <div class="resource-meta">
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📄</span>
          <span>ZIP Archive</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">💾</span>
          <span>3.2 MB</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📧</span>
          <span>10 templates</span>
        </span>
      </div>
      <a href="/files/email-templates.zip"
         download="Email-Marketing-Templates-Pack.zip"
         type="application/zip"
         class="download-btn">
        Download ZIP Archive
      </a>
    </article>

    <article class="resource-card">
      <h2>Brand Identity Worksheet</h2>
      <p class="resource-description">
        Interactive PDF workbook to define your brand voice, values, target
        audience, and visual identity. Includes exercises and examples from
        successful brands.
      </p>
      <div class="resource-meta">
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📄</span>
          <span>PDF</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">💾</span>
          <span>2.1 MB</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📖</span>
          <span>24 pages</span>
        </span>
      </div>
      <a href="/files/brand-worksheet.pdf"
         download="Brand-Identity-Worksheet.pdf"
         type="application/pdf"
         class="download-btn">
        Download PDF Workbook
      </a>
    </article>

    <article class="resource-card">
      <h2>Marketing Budget Calculator</h2>
      <p class="resource-description">
        Excel spreadsheet with formulas to plan and track your marketing
        budget across channels. Includes ROI tracking, monthly breakdowns,
        and visual charts.
      </p>
      <div class="resource-meta">
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📄</span>
          <span>Excel (.xlsx)</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">💾</span>
          <span>189 KB</span>
        </span>
      </div>
      <a href="/files/marketing-budget.xlsx"
         download="Marketing-Budget-Calculator-2025.xlsx"
         type="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
         class="download-btn">
        Download Excel Calculator
      </a>
    </article>

    <article class="resource-card">
      <h2>Content Marketing Playbook</h2>
      <p class="resource-description">
        Comprehensive guide to content marketing strategy, including content
        planning, creation workflows, distribution tactics, and performance
        measurement frameworks.
      </p>
      <div class="resource-meta">
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📄</span>
          <span>PDF</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">💾</span>
          <span>4.7 MB</span>
        </span>
        <span class="meta-item">
          <span class="icon" aria-hidden="true">📖</span>
          <span>68 pages</span>
        </span>
      </div>
      <a href="/files/content-playbook.pdf"
         download="Content-Marketing-Playbook-2025.pdf"
         type="application/pdf"
         class="download-btn">
        Download PDF Playbook
      </a>
    </article>
  </main>

  <footer style="margin-top: 4em; text-align: center; color: #7f8c8d;">
    <p>
      <small>
        All resources are provided free of charge under Creative Commons license.
        No signup required.
      </small>
    </p>
  </footer>
</body>
</html>
```

**Key Features:**
- 6 downloadable resources with different file types (Excel, PDF, ZIP)
- File type, size, and additional metadata displayed
- Custom descriptive filenames for all downloads
- Green download buttons with download icon (⬇)
- MIME type specified with `type` attribute
- Hover and focus states with transform effects
- Grid layout responsive to screen size
- WCAG AA compliant (descriptive text, sufficient contrast, keyboard accessible)
- Clear visual distinction between download links and regular links

---

## Navigation

- **Previous:** [Bookmark Links](bookmark-links.md)
- **Next:** [Semantic HTML Overview](../07-semantic-html5/semantic-overview.md)
- **Up:** [Links and Navigation](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Links and Navigation
- **Difficulty:** Beginner
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
