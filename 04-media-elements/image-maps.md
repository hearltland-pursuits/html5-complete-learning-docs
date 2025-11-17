# Image Maps

## Overview
Image maps allow you to define clickable areas (hotspots) within an image, where different regions link to different destinations. This is useful for interactive diagrams, floor plans, geographical maps, and infographics.

## Basic Syntax

```html
<img src="world-map.jpg" alt="World map" usemap="#worldmap">

<map name="worldmap">
  <area shape="rect" coords="0,0,100,100" href="north-america.html" alt="North America">
  <area shape="circle" coords="200,150,50" href="europe.html" alt="Europe">
  <area shape="poly" coords="300,50,400,100,350,200" href="asia.html" alt="Asia">
</map>
```

**Key Components:**
- `<img>` with `usemap` attribute references the map
- `<map>` container with `name` attribute
- Multiple `<area>` elements define clickable regions
- Each area has shape, coordinates, link, and alt text

## The Map Element

```html
<map name="mapname" id="mapname">
  <!-- Area elements go here -->
</map>
```

**Attributes:**
- `name` (required): Identifier referenced by `usemap`
- `id` (optional but recommended): For CSS/JS targeting

**Best practice**: Use same value for both `name` and `id`.

## The Area Element

### Shape Types

#### Rectangle (rect)

```html
<area shape="rect"
      coords="x1,y1,x2,y2"
      href="link.html"
      alt="Description">
```

**Coordinates**: Top-left corner (x1,y1) and bottom-right corner (x2,y2)

**Example**:
```html
<!-- Rectangle from (50,50) to (200,150) -->
<area shape="rect" coords="50,50,200,150" href="page1.html" alt="Region 1">
```

#### Circle (circle)

```html
<area shape="circle"
      coords="x,y,radius"
      href="link.html"
      alt="Description">
```

**Coordinates**: Center point (x,y) and radius

**Example**:
```html
<!-- Circle centered at (150,100) with radius 50px -->
<area shape="circle" coords="150,100,50" href="page2.html" alt="Region 2">
```

#### Polygon (poly)

```html
<area shape="poly"
      coords="x1,y1,x2,y2,x3,y3,..."
      href="link.html"
      alt="Description">
```

**Coordinates**: Series of x,y coordinate pairs defining vertices

**Example**:
```html
<!-- Triangle with 3 vertices -->
<area shape="poly" coords="100,50,150,150,50,150" href="page3.html" alt="Region 3">
```

#### Default

```html
<area shape="default" href="link.html" alt="Default region">
```

**Use**: Covers entire image (used for fallback clicks)

### Area Attributes

```html
<area shape="rect"
      coords="0,0,100,100"
      href="destination.html"
      alt="Description"
      target="_blank"
      download
      rel="noopener"
      hreflang="en"
      type="text/html"
      title="Tooltip text">
```

**Common attributes:**
- `shape`: rect, circle, poly, or default
- `coords`: Coordinate values (depends on shape)
- `href`: Link destination
- `alt`: Alternative text (required for accessibility)
- `target`: Where to open link (_blank, _self, _parent, _top)
- `download`: Trigger download instead of navigation
- `title`: Tooltip on hover
- `rel`: Relationship (e.g., noopener for _blank links)

## Complete Examples

### World Map with Continents

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive World Map</title>
  <style>
    .map-container {
      max-width: 800px;
      margin: 50px auto;
      text-align: center;
    }

    .map-container img {
      width: 100%;
      height: auto;
      border: 2px solid #ddd;
      border-radius: 8px;
    }

    .map-info {
      margin-top: 20px;
      padding: 15px;
      background: #f0f0f0;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <div class="map-container">
    <h1>Explore the World</h1>
    <p>Click on a continent to learn more</p>

    <img src="world-map.jpg"
         alt="Interactive world map - click regions to explore"
         usemap="#worldmap"
         width="800"
         height="450">

    <map name="worldmap">
      <!-- North America -->
      <area shape="poly"
            coords="50,100,150,80,200,150,180,250,100,220"
            href="north-america.html"
            alt="North America"
            title="Explore North America">

      <!-- South America -->
      <area shape="poly"
            coords="180,280,220,300,200,450,150,420"
            href="south-america.html"
            alt="South America"
            title="Explore South America">

      <!-- Europe -->
      <area shape="rect"
            coords="350,50,480,180"
            href="europe.html"
            alt="Europe"
            title="Explore Europe">

      <!-- Africa -->
      <area shape="circle"
            coords="420,320,80"
            href="africa.html"
            alt="Africa"
            title="Explore Africa">

      <!-- Asia -->
      <area shape="poly"
            coords="500,100,700,80,720,300,550,280"
            href="asia.html"
            alt="Asia"
            title="Explore Asia">

      <!-- Australia -->
      <area shape="rect"
            coords="630,380,750,450"
            href="australia.html"
            alt="Australia"
            title="Explore Australia">
    </map>

    <div class="map-info">
      <p><strong>Tip:</strong> Hover over continents to see clickable regions</p>
    </div>
  </div>
</body>
</html>
```

### Office Floor Plan

```html
<div style="max-width: 600px; margin: 0 auto;">
  <h2>Office Floor Plan</h2>
  <p>Click on rooms for more details</p>

  <img src="floor-plan.jpg"
       alt="Office floor plan - click rooms for details"
       usemap="#floorplan"
       style="width: 100%; border: 1px solid #ccc;">

  <map name="floorplan">
    <!-- Conference Room (rectangle) -->
    <area shape="rect"
          coords="50,50,200,150"
          href="#conference"
          alt="Conference Room A"
          title="Conference Room A - Capacity: 12 people">

    <!-- CEO Office (rectangle) -->
    <area shape="rect"
          coords="220,50,350,150"
          href="#ceo"
          alt="CEO Office"
          title="CEO Office">

    <!-- Open Workspace (polygon) -->
    <area shape="poly"
          coords="50,170,350,170,350,400,50,400"
          href="#workspace"
          alt="Open Workspace"
          title="Open Workspace - 24 desks">

    <!-- Kitchen (circle) -->
    <area shape="circle"
          coords="500,100,60"
          href="#kitchen"
          alt="Kitchen"
          title="Kitchen & Break Area">

    <!-- Restrooms (rectangle) -->
    <area shape="rect"
          coords="450,250,550,350"
          href="#restrooms"
          alt="Restrooms"
          title="Restrooms">
  </map>
</div>
```

### Product Diagram with Hotspots

```html
<figure>
  <img src="laptop-diagram.jpg"
       alt="Laptop diagram with interactive features"
       usemap="#laptopmap"
       width="800"
       height="600"
       style="border: 2px solid #ddd;">

  <map name="laptopmap">
    <!-- Screen -->
    <area shape="rect"
          coords="150,50,650,400"
          href="screen-specs.html"
          alt="15.6-inch Retina Display"
          title="4K Retina Display with True Tone">

    <!-- Keyboard -->
    <area shape="rect"
          coords="150,420,650,550"
          href="keyboard-specs.html"
          alt="Backlit Keyboard"
          title="Magic Keyboard with Touch ID">

    <!-- Trackpad -->
    <area shape="rect"
          coords="300,560,500,620"
          href="trackpad-specs.html"
          alt="Force Touch Trackpad"
          title="Large Force Touch Trackpad">

    <!-- USB-C Ports (left side) -->
    <area shape="circle"
          coords="100,300,20"
          href="ports-specs.html"
          alt="USB-C Ports"
          title="2x Thunderbolt 4 ports">

    <!-- USB-C Ports (right side) -->
    <area shape="circle"
          coords="700,300,20"
          href="ports-specs.html"
          alt="USB-C Ports"
          title="2x Thunderbolt 4 ports">
  </map>

  <figcaption>
    Interactive laptop diagram - click on features for specifications
  </figcaption>
</figure>
```

### Restaurant Seating Chart

```html
<div class="seating-chart">
  <h2>Reserve a Table</h2>
  <p>Click on a table to check availability</p>

  <img src="restaurant-layout.jpg"
       alt="Restaurant seating layout"
       usemap="#seatingmap"
       width="700"
       height="500">

  <map name="seatingmap">
    <!-- Table 1 (2-person) -->
    <area shape="circle"
          coords="150,100,40"
          href="reserve.php?table=1"
          alt="Table 1 - Seats 2"
          title="Table 1: Window seat for 2">

    <!-- Table 2 (4-person) -->
    <area shape="rect"
          coords="250,80,380,160"
          href="reserve.php?table=2"
          alt="Table 2 - Seats 4"
          title="Table 2: Family table for 4">

    <!-- Table 3 (6-person) -->
    <area shape="rect"
          coords="100,250,280,380"
          href="reserve.php?table=3"
          alt="Table 3 - Seats 6"
          title="Table 3: Large group table for 6">

    <!-- Bar Seating -->
    <area shape="poly"
          coords="450,100,650,100,650,250,450,250"
          href="reserve.php?area=bar"
          alt="Bar Seating"
          title="Bar seating - Walk-in only">

    <!-- Outdoor Patio -->
    <area shape="poly"
          coords="50,420,350,420,350,480,50,480"
          href="reserve.php?area=patio"
          alt="Outdoor Patio"
          title="Outdoor patio - Weather permitting">
  </map>
</div>
```

## Creating Coordinates

### Manual Method

1. Open image in image editor (Photoshop, GIMP, Paint.NET)
2. Use ruler/info panel to find pixel coordinates
3. Note down x,y positions for each corner/point
4. Write coordinates in HTML

### Using Online Tools

**Recommended tools:**
- **Image Map Generator**: https://www.image-map.net/
- **HTML Image Map Creator**: Various online tools available
- **Browser DevTools**: Inspect and measure elements

### Using JavaScript

```html
<img src="map.jpg" id="map" alt="Map">
<p id="coords">Click on image to get coordinates</p>

<script>
document.getElementById('map').addEventListener('click', function(e) {
  const rect = this.getBoundingClientRect();
  const x = Math.round(e.clientX - rect.left);
  const y = Math.round(e.clientY - rect.top);
  document.getElementById('coords').textContent = `Coordinates: ${x}, ${y}`;
});
</script>
```

## Responsive Image Maps

### Problem: Fixed Coordinates Don't Scale

Traditional image maps use absolute pixel coordinates that don't adapt to responsive images.

### Solution 1: JavaScript Library

**ImageMapster** (jQuery plugin):
```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="jquery.imagemapster.min.js"></script>

<script>
$('img[usemap]').mapster({
  fillOpacity: 0.4,
  fillColor: "00ff00"
});
</script>
```

**image-map** (Vanilla JS):
```html
<script src="imageMapResizer.min.js"></script>
<script>
imageMapResize();
</script>
```

### Solution 2: CSS Percentage-Based (Modern)

```html
<style>
  .map-wrapper {
    position: relative;
    width: 100%;
    max-width: 800px;
  }

  .map-wrapper img {
    width: 100%;
    height: auto;
    display: block;
  }

  .map-link {
    position: absolute;
    cursor: pointer;
  }

  .region-1 {
    top: 10%;
    left: 5%;
    width: 20%;
    height: 15%;
  }
</style>

<div class="map-wrapper">
  <img src="map.jpg" alt="Interactive map">
  <a href="page1.html" class="map-link region-1" title="Region 1"></a>
  <a href="page2.html" class="map-link region-2" title="Region 2"></a>
</div>
```

### Solution 3: SVG Alternative

```html
<svg viewBox="0 0 800 600" style="width: 100%; height: auto;">
  <image href="map.jpg" width="800" height="600" />

  <!-- Clickable rectangle -->
  <a href="north.html">
    <rect x="50" y="50" width="150" height="100"
          fill="transparent"
          stroke="blue"
          stroke-width="2" />
    <title>North Region</title>
  </a>

  <!-- Clickable circle -->
  <a href="central.html">
    <circle cx="400" cy="300" r="80"
            fill="rgba(255,0,0,0.3)"
            stroke="red"
            stroke-width="2" />
    <title>Central Region</title>
  </a>
</svg>
```

## Accessibility Considerations

### Always Include Alt Text

```html
<area shape="rect"
      coords="0,0,100,100"
      href="page.html"
      alt="Descriptive alt text"  <!-- Required! -->
      title="Additional hover info">
```

### Provide Text Alternative

```html
<img src="map.jpg" alt="World map" usemap="#worldmap">

<map name="worldmap">
  <area shape="rect" coords="..." href="europe.html" alt="Europe">
  <area shape="rect" coords="..." href="asia.html" alt="Asia">
</map>

<!-- Text alternative for accessibility -->
<div class="text-links">
  <h3>Map Regions:</h3>
  <ul>
    <li><a href="europe.html">Europe</a></li>
    <li><a href="asia.html">Asia</a></li>
    <li><a href="africa.html">Africa</a></li>
  </ul>
</div>
```

### Keyboard Navigation

Image maps are keyboard accessible by default:
- **Tab**: Navigate between areas
- **Enter**: Activate link

### ARIA Enhancement

```html
<img src="map.jpg"
     alt="Interactive office floor plan"
     usemap="#floorplan"
     role="img"
     aria-label="Interactive floor plan with clickable rooms">

<map name="floorplan">
  <area shape="rect"
        coords="..."
        href="#room1"
        alt="Conference Room"
        role="link"
        aria-label="Conference Room - Click for details">
</map>
```

## Browser Support

- **Image Maps**: Universal support (all browsers, including IE6+)
- **`<map>` and `<area>`**: Supported in all HTML versions
- **Responsive maps**: Requires JavaScript libraries or CSS workarounds

## Common Mistakes

❌ **Missing alt text**
```html
<area shape="rect" coords="0,0,100,100" href="page.html">
```

✅ **Include alt text**
```html
<area shape="rect" coords="0,0,100,100" href="page.html" alt="Description">
```

---

❌ **Mismatched usemap and name**
```html
<img usemap="#map1" ...>
<map name="map2"> <!-- Wrong name! -->
```

✅ **Matching references**
```html
<img usemap="#map1" ...>
<map name="map1">
```

---

❌ **Incorrect coordinate order**
```html
<!-- Wrong: x2,y2,x1,y1 -->
<area shape="rect" coords="200,150,50,50" href="...">
```

✅ **Correct: x1,y1,x2,y2**
```html
<area shape="rect" coords="50,50,200,150" href="...">
```

---

❌ **Non-responsive map on mobile**
```html
<img src="map.jpg" width="800" usemap="#map">
```

✅ **Responsive with JavaScript helper**
```html
<img src="map.jpg" style="width: 100%;" usemap="#map">
<script src="imageMapResizer.min.js"></script>
<script>imageMapResize();</script>
```

## Practice Exercise

Create an interactive infographic with:
1. Image with 4-5 clickable regions
2. Different shape types (rect, circle, poly)
3. Hover tooltips
4. Text link alternatives
5. Proper accessibility

### Solution

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Web Development Stack Infographic</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 50px auto;
      padding: 20px;
      background: #f5f5f5;
    }

    .infographic-container {
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    h1 {
      color: #2c3e50;
      text-align: center;
    }

    .map-image {
      width: 100%;
      height: auto;
      border: 2px solid #ddd;
      border-radius: 8px;
      display: block;
      margin: 20px 0;
    }

    .text-alternative {
      margin-top: 30px;
      padding: 20px;
      background: #ecf0f1;
      border-left: 4px solid #3498db;
      border-radius: 4px;
    }

    .text-alternative h2 {
      margin-top: 0;
      color: #2c3e50;
    }

    .text-alternative ul {
      list-style: none;
      padding: 0;
    }

    .text-alternative li {
      margin: 10px 0;
    }

    .text-alternative a {
      color: #3498db;
      text-decoration: none;
      font-weight: bold;
    }

    .text-alternative a:hover {
      text-decoration: underline;
    }

    .info-box {
      background: #fff3cd;
      border: 1px solid #ffc107;
      padding: 15px;
      border-radius: 5px;
      margin-bottom: 20px;
    }
  </style>
</head>
<body>
  <div class="infographic-container">
    <h1>🚀 Modern Web Development Stack</h1>

    <div class="info-box">
      <strong>Interactive Infographic:</strong> Click on each technology layer
      to learn more about it.
    </div>

    <img src="web-stack-diagram.jpg"
         alt="Web development stack showing frontend, backend, and database layers"
         usemap="#webstack"
         class="map-image"
         width="800"
         height="600">

    <map name="webstack" id="webstack">
      <!-- Frontend Layer (Rectangle at top) -->
      <area shape="rect"
            coords="100,50,700,180"
            href="frontend.html"
            alt="Frontend Technologies"
            title="Frontend: HTML5, CSS3, JavaScript, React">

      <!-- Backend Layer (Rectangle in middle) -->
      <area shape="rect"
            coords="100,220,700,350"
            href="backend.html"
            alt="Backend Technologies"
            title="Backend: Node.js, Python, Ruby, PHP">

      <!-- Database Layer (Rectangle at bottom) -->
      <area shape="rect"
            coords="100,390,700,520"
            href="database.html"
            alt="Database Technologies"
            title="Databases: PostgreSQL, MongoDB, Redis">

      <!-- DevOps Circle (right side) -->
      <area shape="circle"
            coords="750,300,60"
            href="devops.html"
            alt="DevOps & Deployment"
            title="DevOps: Docker, Kubernetes, CI/CD">

      <!-- API Gateway (Center polygon) -->
      <area shape="poly"
            coords="350,290,450,290,450,310,350,310"
            href="api.html"
            alt="API Layer"
            title="API Gateway & Microservices">
    </map>

    <!-- Text Alternative for Accessibility -->
    <div class="text-alternative">
      <h2>📋 Stack Layers (Text Navigation)</h2>
      <ul>
        <li>
          <strong>🎨 <a href="frontend.html">Frontend Layer</a></strong><br>
          HTML5, CSS3, JavaScript, React, Vue, Angular
        </li>
        <li>
          <strong>⚙️ <a href="backend.html">Backend Layer</a></strong><br>
          Node.js, Python, Ruby on Rails, PHP, Java
        </li>
        <li>
          <strong>💾 <a href="database.html">Database Layer</a></strong><br>
          PostgreSQL, MySQL, MongoDB, Redis, Elasticsearch
        </li>
        <li>
          <strong>🚢 <a href="devops.html">DevOps & Deployment</a></strong><br>
          Docker, Kubernetes, Jenkins, GitHub Actions, AWS
        </li>
        <li>
          <strong>🔌 <a href="api.html">API & Integration</a></strong><br>
          REST APIs, GraphQL, gRPC, WebSockets
        </li>
      </ul>
    </div>
  </div>
</body>
</html>
```

## Additional Resources

- **MDN Web Docs**: [Image Maps](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/map)
- **W3Schools**: [HTML Image Maps](https://www.w3schools.com/html/html_images_imagemap.asp)
- **Image Map Generator**: [Online Tool](https://www.image-map.net/)
- **imageMapResizer**: [Responsive Image Maps Library](https://github.com/davidjbradshaw/image-map-resizer)

---

**Previous Topic**: [Embed and Object](./embed-object.md)
**Next Topic**: [Lazy Loading](./lazy-loading.md)
**Category**: [Media Elements](./README.md)
