# Figure and Figcaption Elements

## Overview
The `<figure>` element represents self-contained content (images, diagrams, code, quotes) that is referenced from the main flow but could be moved to another location without affecting the document's meaning. The `<figcaption>` element provides a caption or legend for its parent `<figure>`.

## Basic Syntax

```html
<figure>
  <img src="photo.jpg" alt="Description">
  <figcaption>Caption text here</figcaption>
</figure>
```

**Key Points:**
- `<figure>` wraps self-contained content
- `<figcaption>` is optional but recommended
- `<figcaption>` can appear before or after figure content
- Only one `<figcaption>` per `<figure>`
- Provides semantic meaning for screen readers

## Use Cases

### 1. Images with Captions

```html
<figure>
  <img src="grand-canyon.jpg"
       alt="Aerial view of the Grand Canyon"
       width="800"
       height="600">
  <figcaption>
    The Grand Canyon, photographed at sunset from Mather Point
  </figcaption>
</figure>
```

### 2. Multiple Images (Gallery Item)

```html
<figure>
  <img src="photo1.jpg" alt="Mountain peak at sunrise">
  <img src="photo2.jpg" alt="Forest trail in autumn">
  <img src="photo3.jpg" alt="Coastal sunset">
  <figcaption>
    Nature photography series by Jane Doe, 2024
  </figcaption>
</figure>
```

### 3. Code Examples

```html
<figure>
  <pre><code>
function greet(name) {
  return `Hello, ${name}!`;
}

console.log(greet('World'));
  </code></pre>
  <figcaption>
    Listing 1: JavaScript greeting function using template literals
  </figcaption>
</figure>
```

### 4. Blockquotes with Attribution

```html
<figure>
  <blockquote>
    <p>
      The only way to do great work is to love what you do.
    </p>
  </blockquote>
  <figcaption>
    — Steve Jobs, <cite>Stanford Commencement Address, 2005</cite>
  </figcaption>
</figure>
```

### 5. Tables with Descriptions

```html
<figure>
  <table>
    <thead>
      <tr>
        <th>Quarter</th>
        <th>Revenue</th>
        <th>Growth</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Q1 2024</td>
        <td>$2.5M</td>
        <td>+15%</td>
      </tr>
      <tr>
        <td>Q2 2024</td>
        <td>$3.1M</td>
        <td>+24%</td>
      </tr>
    </tbody>
  </table>
  <figcaption>
    Table 1: Quarterly revenue growth for fiscal year 2024
  </figcaption>
</figure>
```

### 6. Videos with Captions

```html
<figure>
  <video controls width="640" height="360">
    <source src="tutorial.mp4" type="video/mp4">
    <source src="tutorial.webm" type="video/webm">
    Your browser doesn't support video.
  </video>
  <figcaption>
    Video 1: Introduction to HTML5 semantic elements (5:32)
  </figcaption>
</figure>
```

### 7. Audio with Metadata

```html
<figure>
  <audio controls>
    <source src="podcast-episode-12.mp3" type="audio/mpeg">
    Your browser doesn't support audio.
  </audio>
  <figcaption>
    Podcast Episode 12: The Future of Web Development
    <br>
    <small>Duration: 45 minutes | Published: Jan 15, 2024</small>
  </figcaption>
</figure>
```

### 8. Diagrams and Illustrations

```html
<figure>
  <svg width="400" height="200" viewBox="0 0 400 200">
    <rect x="50" y="50" width="100" height="100" fill="#3498db"/>
    <circle cx="250" cy="100" r="50" fill="#e74c3c"/>
    <text x="200" y="180" text-anchor="middle">Process Flow</text>
  </svg>
  <figcaption>
    Figure 2: Simplified data processing workflow
  </figcaption>
</figure>
```

## Figcaption Positioning

### Caption Below (Most Common)

```html
<figure>
  <img src="chart.png" alt="Sales chart">
  <figcaption>Annual sales performance 2024</figcaption>
</figure>
```

### Caption Above

```html
<figure>
  <figcaption>Figure 3: Network architecture diagram</figcaption>
  <img src="network-diagram.png" alt="Three-tier network architecture">
</figure>
```

### Caption with Attribution and Credits

```html
<figure>
  <img src="wildlife-photo.jpg" alt="Lion in savanna">
  <figcaption>
    African lion resting in the Serengeti
    <br>
    <small>Photo by John Smith | License: CC BY-NC 4.0</small>
  </figcaption>
</figure>
```

## Styling Figures

### Basic Styling

```html
<style>
  figure {
    margin: 20px 0;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 8px;
    background: #f9f9f9;
  }

  figure img {
    width: 100%;
    height: auto;
    display: block;
    border-radius: 4px;
  }

  figcaption {
    margin-top: 10px;
    text-align: center;
    color: #555;
    font-size: 0.9rem;
    font-style: italic;
  }
</style>

<figure>
  <img src="landscape.jpg" alt="Mountain landscape">
  <figcaption>Sunset in the Rocky Mountains</figcaption>
</figure>
```

### Floating Figures

```html
<style>
  .float-right {
    float: right;
    margin: 0 0 20px 20px;
    max-width: 400px;
  }

  .float-left {
    float: left;
    margin: 0 20px 20px 0;
    max-width: 400px;
  }

  figure img {
    width: 100%;
    height: auto;
  }

  figcaption {
    font-size: 0.85rem;
    color: #666;
    padding: 8px;
    background: #f5f5f5;
  }
</style>

<article>
  <h2>Article Title</h2>

  <figure class="float-right">
    <img src="illustration.jpg" alt="Diagram">
    <figcaption>Figure 1: Process overview</figcaption>
  </figure>

  <p>Main article text flows around the figure...</p>
  <p>More content here...</p>
</article>
```

### Gallery Grid with Figures

```html
<style>
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
  }

  .gallery figure {
    margin: 0;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.3s;
  }

  .gallery figure:hover {
    transform: translateY(-5px);
  }

  .gallery img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    display: block;
  }

  .gallery figcaption {
    padding: 12px;
    text-align: center;
    background: white;
    font-size: 0.9rem;
  }
</style>

<div class="gallery">
  <figure>
    <img src="photo1.jpg" alt="Beach sunset">
    <figcaption>Coastal Sunset</figcaption>
  </figure>

  <figure>
    <img src="photo2.jpg" alt="Mountain lake">
    <figcaption>Alpine Lake</figcaption>
  </figure>

  <figure>
    <img src="photo3.jpg" alt="Forest path">
    <figcaption>Forest Trail</figcaption>
  </figure>
</div>
```

## Accessibility Considerations

### Proper Alt Text

```html
<!-- Image alt describes the image content -->
<!-- Figcaption provides context, credit, or additional information -->

<figure>
  <img src="chart.png"
       alt="Bar chart showing 30% increase in sales from 2023 to 2024">
  <figcaption>
    Figure 5: Annual sales comparison (Data source: Internal Q4 report)
  </figcaption>
</figure>
```

**Key principle**: Alt text describes WHAT is in the image. Figcaption provides context, attribution, or supplementary information.

### Screen Reader Announcement

```html
<figure aria-labelledby="fig-caption-1">
  <img src="diagram.png" alt="Three-layer network architecture">
  <figcaption id="fig-caption-1">
    Figure 1: Typical three-tier web application architecture
  </figcaption>
</figure>
```

### Complex Figures

```html
<figure>
  <img src="complex-chart.png"
       alt="Line graph showing temperature trends"
       aria-describedby="chart-description">
  <figcaption>
    Temperature trends 2020-2024
  </figcaption>
  <div id="chart-description" class="sr-only">
    The chart shows average monthly temperatures from 2020 to 2024.
    Temperatures ranged from 45°F in winter to 85°F in summer,
    with a noticeable 3°F increase in average temperatures over the period.
  </div>
</figure>

<style>
  .sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0,0,0,0);
    white-space: nowrap;
    border: 0;
  }
</style>
```

## Common Patterns

### Article with Inline Figures

```html
<article>
  <h1>Understanding Climate Change</h1>

  <p>Introduction paragraph...</p>

  <figure>
    <img src="temperature-graph.png"
         alt="Global temperature increase graph 1900-2024">
    <figcaption>
      Figure 1: Global average temperature anomaly (base period: 1951-1980)
    </figcaption>
  </figure>

  <p>As shown in Figure 1, temperatures have risen significantly...</p>

  <figure>
    <blockquote>
      <p>Climate change is the defining issue of our time.</p>
    </blockquote>
    <figcaption>
      — United Nations Secretary-General, 2019
    </figcaption>
  </figure>

  <p>Conclusion paragraph...</p>
</article>
```

### Product Showcase

```html
<figure class="product-showcase">
  <picture>
    <source srcset="product.avif" type="image/avif">
    <source srcset="product.webp" type="image/webp">
    <img src="product.jpg"
         alt="Wireless noise-canceling headphones in matte black"
         width="600"
         height="600">
  </picture>
  <figcaption>
    <h3>Premium Wireless Headphones</h3>
    <p>Active noise cancellation | 30-hour battery | Bluetooth 5.3</p>
    <p><strong>$299.99</strong></p>
  </figcaption>
</figure>
```

### Technical Documentation

```html
<section>
  <h2>3.2 Installation Process</h2>

  <p>Follow these steps to install the software:</p>

  <figure>
    <pre><code>$ npm install @example/package
$ npm run setup
$ npm start</code></pre>
    <figcaption>
      Listing 3.1: Installation commands for Unix-based systems
    </figcaption>
  </figure>

  <p>The installation process typically takes 2-3 minutes...</p>
</section>
```

## Figure vs img Alone

### When to use `<figure>`:
- ✅ Content needs a caption
- ✅ Self-contained reference (chart, diagram, example)
- ✅ Could be moved without disrupting flow
- ✅ Numbered figures in documentation

### When to use `<img>` alone:
- ✅ Inline images in paragraphs
- ✅ Icons and logos
- ✅ Background/decorative images
- ✅ No caption needed

**Example comparison:**

```html
<!-- Use img alone for inline images -->
<p>
  Click the <img src="save-icon.png" alt="Save" width="20" height="20"> icon
  to save your work.
</p>

<!-- Use figure for referenced content -->
<figure>
  <img src="workflow-diagram.png" alt="Five-step workflow diagram">
  <figcaption>Figure 2: Standard approval workflow</figcaption>
</figure>
<p>As illustrated in Figure 2, the workflow consists of five stages...</p>
```

## Browser Support

- **`<figure>` and `<figcaption>`**: Universal support in all modern browsers
- Supported since: IE 9+, Chrome 8+, Firefox 4+, Safari 5.1+, Edge (all versions)

## Common Mistakes

❌ **Multiple figcaptions**
```html
<figure>
  <img src="photo.jpg" alt="Photo">
  <figcaption>Caption 1</figcaption>
  <figcaption>Caption 2</figcaption> <!-- Invalid! -->
</figure>
```

✅ **Single figcaption**
```html
<figure>
  <img src="photo.jpg" alt="Photo">
  <figcaption>Combined caption with all information</figcaption>
</figure>
```

---

❌ **Figcaption outside figure**
```html
<img src="photo.jpg" alt="Photo">
<figcaption>This won't work</figcaption> <!-- Invalid! -->
```

✅ **Figcaption inside figure**
```html
<figure>
  <img src="photo.jpg" alt="Photo">
  <figcaption>This is correct</figcaption>
</figure>
```

---

❌ **Redundant alt and figcaption**
```html
<figure>
  <img src="sunset.jpg" alt="Beautiful sunset over the ocean">
  <figcaption>Beautiful sunset over the ocean</figcaption> <!-- Redundant! -->
</figure>
```

✅ **Complementary alt and figcaption**
```html
<figure>
  <img src="sunset.jpg" alt="Orange and purple sky reflected on calm ocean water">
  <figcaption>Sunset at Malibu Beach, California - July 2024</figcaption>
</figure>
```

---

❌ **Using figure for layout only**
```html
<!-- Don't use figure just for styling -->
<figure class="sidebar-box">
  <h3>Related Links</h3>
  <ul><li>Link 1</li></ul>
</figure>
```

✅ **Use figure for semantic content**
```html
<!-- Use div for layout, figure for self-contained content -->
<aside class="sidebar-box">
  <h3>Related Links</h3>
  <ul><li>Link 1</li></ul>
</aside>
```

## Practice Exercise

Create a blog post about web development with:
1. Article heading
2. Introduction paragraph
3. Figure with code example
4. Explanatory text
5. Figure with diagram/image
6. Conclusion
7. Proper styling for figures

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Understanding CSS Grid - Blog Post</title>
  <style>
    body {
      font-family: Georgia, serif;
      line-height: 1.6;
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
      color: #333;
    }

    article {
      background: white;
    }

    h1 {
      color: #2c3e50;
      font-size: 2.5rem;
      margin-bottom: 10px;
    }

    .meta {
      color: #7f8c8d;
      font-size: 0.9rem;
      margin-bottom: 30px;
    }

    figure {
      margin: 30px 0;
      padding: 20px;
      background: #f8f9fa;
      border-left: 4px solid #3498db;
      border-radius: 4px;
    }

    figure img {
      width: 100%;
      height: auto;
      border-radius: 4px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    figure pre {
      background: #2c3e50;
      color: #ecf0f1;
      padding: 15px;
      border-radius: 4px;
      overflow-x: auto;
    }

    figure code {
      font-family: 'Courier New', monospace;
      font-size: 0.9rem;
    }

    figcaption {
      margin-top: 15px;
      color: #555;
      font-style: italic;
      font-size: 0.95rem;
      text-align: center;
    }

    figcaption strong {
      font-style: normal;
      color: #2c3e50;
    }

    p {
      margin: 20px 0;
    }

    .conclusion {
      margin-top: 40px;
      padding-top: 20px;
      border-top: 2px solid #ecf0f1;
    }
  </style>
</head>
<body>
  <article>
    <h1>Understanding CSS Grid Layout</h1>
    <p class="meta">
      Published on January 15, 2024 | By Sarah Johnson | 5 min read
    </p>

    <p>
      CSS Grid is a powerful layout system that allows you to create complex,
      responsive web layouts with ease. Unlike traditional methods like floats
      or flexbox, Grid gives you complete control over both rows and columns
      simultaneously.
    </p>

    <figure>
      <pre><code>.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
  padding: 20px;
}

.item {
  background: #3498db;
  padding: 20px;
  color: white;
  text-align: center;
}</code></pre>
      <figcaption>
        <strong>Listing 1:</strong> Basic CSS Grid setup with three equal columns
      </figcaption>
    </figure>

    <p>
      The code above creates a simple three-column grid layout. The
      <code>repeat(3, 1fr)</code> function creates three columns of equal width,
      where "1fr" represents one fraction of the available space. The
      <code>grid-gap</code> property adds consistent spacing between grid items.
    </p>

    <figure>
      <img src="https://via.placeholder.com/800x400/3498db/ffffff?text=CSS+Grid+Layout+Example"
           alt="Visual diagram showing a three-column CSS grid with labeled areas"
           width="800"
           height="400">
      <figcaption>
        <strong>Figure 1:</strong> Visual representation of the three-column grid layout
        with items automatically placed in available cells
      </figcaption>
    </figure>

    <p>
      As shown in Figure 1, CSS Grid automatically positions items in the available
      cells. You can also explicitly control placement using properties like
      <code>grid-column</code> and <code>grid-row</code>, giving you precise control
      over your layout.
    </p>

    <figure>
      <blockquote>
        <p>
          "CSS Grid Layout is the most powerful layout system available in CSS.
          It's a two-dimensional system, meaning it can handle both columns and rows."
        </p>
      </blockquote>
      <figcaption>
        — CSS-Tricks, <cite>A Complete Guide to Grid</cite>
      </figcaption>
    </figure>

    <div class="conclusion">
      <p>
        CSS Grid revolutionizes web layout by providing an intuitive, powerful
        system for creating responsive designs. Whether you're building a simple
        photo gallery or a complex application interface, Grid offers the
        flexibility and control you need.
      </p>

      <p>
        Start experimenting with Grid in your next project – you'll quickly
        discover how much easier it makes layout design compared to traditional
        methods.
      </p>
    </div>
  </article>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [The Figure element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure)
- **MDN Web Docs**: [The Figcaption element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figcaption)
- **W3Schools**: [HTML figure Tag](https://www.w3schools.com/tags/tag_figure.asp)
- **HTML5 Doctor**: [The figure & figcaption elements](http://html5doctor.com/the-figure-figcaption-elements/)

---

**Previous Topic**: [Picture Element](./picture-element.md)
**Next Topic**: [Audio](./audio.md)
**Category**: [Media Elements](./README.md)
