---
title: History API
category: HTML5 APIs
order: 6
---

# History API

> **Quick Summary:** The History API allows JavaScript to manipulate the browser's session history, enabling single-page applications (SPAs) to update the URL without full page reloads and providing seamless navigation with the back/forward buttons.

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

The History API is a powerful HTML5 feature that gives developers control over the browser's navigation history. Before this API, changing the URL required a full page reload, making it impossible to create smooth, app-like experiences on the web.

**The Problem:** Traditional web apps reload the entire page on every navigation. This causes flickering, lost scroll positions, and slower experiences. Hash-based routing (`#page1`) works but creates ugly URLs and has SEO limitations.

**The Solution:** The History API provides `pushState()` and `replaceState()` to modify the URL without reloading, plus the `popstate` event to detect back/forward button clicks. This enables single-page applications (SPAs) with clean URLs and instant navigation.

**Key Concept:** The History API doesn't load pages—it only changes the URL and manages history. You're responsible for loading and displaying content based on the current state.

---

## Basic Syntax

### Key Methods

```javascript
// Add a new entry to the history stack
history.pushState(state, title, url);

// Replace the current history entry
history.replaceState(state, title, url);

// Navigate through history
history.back();    // Go back one page
history.forward(); // Go forward one page
history.go(-2);    // Go back 2 pages
history.go(1);     // Go forward 1 page

// Get current history length
console.log(history.length); // Number of entries in session history

// Access current state
console.log(history.state); // The state object for current page
```

### Listening for Navigation Events

```javascript
// Listen for back/forward button clicks
window.addEventListener('popstate', function(event) {
  console.log('State:', event.state);
  console.log('URL:', location.pathname);

  // Load content based on new URL
  loadContentForURL(location.pathname);
});
```

### Parameters Explained

| Method | Parameter | Description |
|--------|-----------|-------------|
| `pushState()` | `state` | JavaScript object (max ~640KB) with page data |
| | `title` | Currently ignored by all browsers (use `document.title` instead) |
| | `url` | New URL (must be same origin, can be relative) |
| `replaceState()` | Same as above | Replaces current entry instead of adding new one |
| `popstate` event | `event.state` | The state object saved with `pushState()` |

---

## Examples

### Example 1: Basic Single-Page Navigation

**Scenario:** Create a simple multi-page app that navigates without full page reloads

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SPA Example</title>
  <style>
    nav a {
      margin: 0 10px;
      padding: 10px 15px;
      text-decoration: none;
      background: #2196F3;
      color: white;
      border-radius: 5px;
    }
    nav a.active {
      background: #1976D2;
    }
    .page {
      display: none;
      padding: 20px;
      margin-top: 20px;
      border: 2px solid #ddd;
      border-radius: 5px;
    }
    .page.active {
      display: block;
    }
  </style>
</head>
<body>
  <nav>
    <a href="/" data-page="home">Home</a>
    <a href="/about" data-page="about">About</a>
    <a href="/contact" data-page="contact">Contact</a>
  </nav>

  <div id="content">
    <div class="page active" id="home">
      <h1>Home Page</h1>
      <p>Welcome to our single-page application!</p>
    </div>
    <div class="page" id="about">
      <h1>About Us</h1>
      <p>Learn more about our company.</p>
    </div>
    <div class="page" id="contact">
      <h1>Contact</h1>
      <p>Get in touch with us.</p>
    </div>
  </div>

  <script>
    // Handle navigation link clicks
    document.querySelectorAll('nav a').forEach(link => {
      link.addEventListener('click', function(e) {
        e.preventDefault();

        const url = this.getAttribute('href');
        const page = this.dataset.page;

        // Update history
        history.pushState({ page }, '', url);

        // Update content
        showPage(page);

        // Update active link
        updateActiveLink(this);
      });
    });

    // Handle back/forward buttons
    window.addEventListener('popstate', function(event) {
      if (event.state && event.state.page) {
        showPage(event.state.page);
        updateActiveLink(document.querySelector(`[data-page="${event.state.page}"]`));
      }
    });

    function showPage(pageId) {
      // Hide all pages
      document.querySelectorAll('.page').forEach(page => {
        page.classList.remove('active');
      });

      // Show target page
      const targetPage = document.getElementById(pageId);
      if (targetPage) {
        targetPage.classList.add('active');
        document.title = pageId.charAt(0).toUpperCase() + pageId.slice(1);
      }
    }

    function updateActiveLink(activeLink) {
      document.querySelectorAll('nav a').forEach(link => {
        link.classList.remove('active');
      });
      activeLink.classList.add('active');
    }

    // Set initial state (for when user lands directly on page)
    const currentPath = location.pathname;
    const initialPage = currentPath === '/' ? 'home' : currentPath.slice(1);
    history.replaceState({ page: initialPage }, '', currentPath);
  </script>
</body>
</html>
```

**Result:** Clicking navigation links changes the URL and content instantly, and the back/forward buttons work perfectly. The URL updates cleanly without page reloads.

---

### Example 2: Tabbed Interface with URL Updates

**Scenario:** A tabbed interface where each tab has its own URL for sharing/bookmarking

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tab History Example</title>
  <style>
    .tabs {
      display: flex;
      gap: 5px;
      border-bottom: 2px solid #ddd;
    }
    .tab {
      padding: 10px 20px;
      background: #f0f0f0;
      border: none;
      cursor: pointer;
      border-radius: 5px 5px 0 0;
    }
    .tab.active {
      background: #2196F3;
      color: white;
    }
    .tab-content {
      display: none;
      padding: 20px;
    }
    .tab-content.active {
      display: block;
    }
  </style>
</head>
<body>
  <h1>Product Information</h1>

  <div class="tabs">
    <button class="tab active" data-tab="overview">Overview</button>
    <button class="tab" data-tab="specs">Specifications</button>
    <button class="tab" data-tab="reviews">Reviews</button>
  </div>

  <div class="tab-content active" id="overview">
    <h2>Overview</h2>
    <p>This product is amazing and will change your life!</p>
  </div>

  <div class="tab-content" id="specs">
    <h2>Specifications</h2>
    <ul>
      <li>Weight: 2.5 lbs</li>
      <li>Dimensions: 10" x 8" x 2"</li>
      <li>Battery Life: 24 hours</li>
    </ul>
  </div>

  <div class="tab-content" id="reviews">
    <h2>Customer Reviews</h2>
    <p>⭐⭐⭐⭐⭐ "Best purchase ever!" - John D.</p>
    <p>⭐⭐⭐⭐ "Great value for money." - Sarah M.</p>
  </div>

  <script>
    const tabs = document.querySelectorAll('.tab');

    tabs.forEach(tab => {
      tab.addEventListener('click', function() {
        const tabName = this.dataset.tab;

        // Update URL with tab name
        history.pushState(
          { tab: tabName },
          '',
          `/product?tab=${tabName}`
        );

        switchTab(tabName);
      });
    });

    // Handle back/forward
    window.addEventListener('popstate', function(event) {
      if (event.state && event.state.tab) {
        switchTab(event.state.tab);
      } else {
        // Default to overview if no state
        switchTab('overview');
      }
    });

    function switchTab(tabName) {
      // Update tabs
      document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
      document.querySelector(`[data-tab="${tabName}"]`).classList.add('active');

      // Update content
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      document.getElementById(tabName).classList.add('active');
    }

    // Initialize state on page load
    const urlParams = new URLSearchParams(window.location.search);
    const initialTab = urlParams.get('tab') || 'overview';
    history.replaceState({ tab: initialTab }, '', location.href);
    switchTab(initialTab);
  </script>
</body>
</html>
```

**Result:** Each tab has a unique, shareable URL. Users can bookmark specific tabs, and the back button cycles through tab history.

---

### Example 3: Infinite Scroll with History Management

**Scenario:** Load more content as users scroll, updating the URL to reflect the current page number

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Infinite Scroll History</title>
  <style>
    .item {
      padding: 20px;
      margin: 10px 0;
      background: #f5f5f5;
      border-radius: 5px;
    }
    .loading {
      text-align: center;
      padding: 20px;
      font-style: italic;
      color: #666;
    }
  </style>
</head>
<body>
  <h1>Article Feed - Page <span id="pageNumber">1</span></h1>
  <div id="feed"></div>
  <div class="loading" id="loading">Loading more...</div>

  <script>
    let currentPage = 1;
    let loading = false;

    function loadPage(page) {
      loading = true;
      document.getElementById('loading').style.display = 'block';

      // Simulate API call
      setTimeout(() => {
        const feed = document.getElementById('feed');

        for (let i = 1; i <= 5; i++) {
          const itemNumber = (page - 1) * 5 + i;
          const item = document.createElement('div');
          item.className = 'item';
          item.textContent = `Article ${itemNumber}: Lorem ipsum dolor sit amet...`;
          feed.appendChild(item);
        }

        loading = false;
        document.getElementById('loading').style.display = 'none';
      }, 1000);
    }

    // Infinite scroll detection
    window.addEventListener('scroll', function() {
      if (loading) return;

      const scrollHeight = document.documentElement.scrollHeight;
      const scrollTop = window.scrollY;
      const clientHeight = window.innerHeight;

      if (scrollTop + clientHeight >= scrollHeight - 100) {
        currentPage++;
        loadPage(currentPage);

        // Update URL without creating new history entry
        history.replaceState(
          { page: currentPage },
          '',
          `?page=${currentPage}`
        );

        document.getElementById('pageNumber').textContent = currentPage;
      }
    });

    // Handle back/forward navigation
    window.addEventListener('popstate', function(event) {
      if (event.state && event.state.page) {
        currentPage = event.state.page;
        document.getElementById('pageNumber').textContent = currentPage;

        // In real app: re-fetch data for this page
        console.log('Navigate to page:', currentPage);
      }
    });

    // Initialize first page
    const urlParams = new URLSearchParams(window.location.search);
    const initialPage = parseInt(urlParams.get('page')) || 1;
    currentPage = initialPage;
    history.replaceState({ page: initialPage }, '', `?page=${initialPage}`);
    loadPage(currentPage);
  </script>
</body>
</html>
```

**Result:** As users scroll, the URL updates to `?page=2`, `?page=3`, etc. The back button returns to previous scroll positions (in a real app, you'd save and restore scroll position).

**Notes:**
- Uses `replaceState()` instead of `pushState()` to avoid cluttering history with every scroll
- In production, you'd restore scroll position and re-fetch data when navigating back
- Consider saving scroll position in the state object

---

## Common Use Cases

### Use Case 1: Single-Page Applications (SPAs)
**When:** Building React, Vue, or vanilla JS apps with client-side routing
**How:**
```javascript
// When user clicks a link
function navigate(url, data) {
  history.pushState({ data }, '', url);
  renderPage(url, data);
}

// When user clicks back/forward
window.addEventListener('popstate', (e) => {
  renderPage(location.pathname, e.state?.data);
});
```
**Why:** Users expect the back button to work, and URLs should be shareable and bookmarkable.

---

### Use Case 2: Multi-Step Forms/Wizards
**When:** Forms with multiple steps where users might want to go back
**How:**
```javascript
function goToStep(stepNumber) {
  history.pushState({ step: stepNumber }, '', `/signup/step-${stepNumber}`);
  showStep(stepNumber);
}

window.addEventListener('popstate', (e) => {
  showStep(e.state?.step || 1);
});
```
**Why:** Allows users to use back button to correct mistakes without losing form data.

---

### Use Case 3: Modal Dialogs with URLs
**When:** Opening modals/lightboxes that should have their own URLs
**How:**
```javascript
function openModal(modalId) {
  history.pushState({ modal: modalId }, '', `/gallery/${modalId}`);
  showModal(modalId);
}

window.addEventListener('popstate', (e) => {
  if (e.state?.modal) {
    showModal(e.state.modal);
  } else {
    closeAllModals();
  }
});
```
**Why:** Users can share links to specific modals, and the back button closes modals intuitively.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | 5+      | Full Support  | Since 2010 |
| Firefox | 4+      | Full Support  | Excellent support |
| Safari  | 5+      | Full Support  | iOS Safari 4.2+ |
| Edge    | All     | Full Support  | Including legacy Edge |
| IE      | 10+     | Full Support  | IE 10-11 only |

**Fallback Strategy:**
```javascript
if (history.pushState) {
  // Use History API
  history.pushState(state, '', url);
} else {
  // Fallback to hash-based routing for older browsers
  window.location.hash = '#' + url;
}
```

**Can I Use Link:** [https://caniuse.com/history](https://caniuse.com/history)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Announce page changes to screen readers when using History API
- Ensure focus management when content changes

**Level AA Requirements:**
- Provide skip links for navigated content
- Maintain logical tab order after navigation

### Screen Reader Support

```javascript
// Announce page changes to screen readers
function navigate(url, title) {
  history.pushState({}, '', url);
  document.title = title;

  // Update live region for screen readers
  const announcer = document.getElementById('route-announcer');
  announcer.textContent = `Navigated to ${title}`;

  // Reset focus to main content
  document.querySelector('main').focus();
}
```

```html
<!-- Add this to your HTML -->
<div id="route-announcer" aria-live="polite" aria-atomic="true" class="sr-only"></div>
```

**Key Points:**
- Always update `document.title` when URL changes
- Use ARIA live regions to announce navigation
- Manage focus appropriately (e.g., focus main heading after navigation)
- Provide "Skip to content" links on every virtual page

### Keyboard Navigation

- **Tab:** Must work correctly after navigation
- **Enter/Space:** Trigger navigation on interactive elements
- **Focus Management:** Reset focus to main heading or content area after navigation

```javascript
function navigate(url) {
  history.pushState({}, '', url);
  renderContent(url);

  // Move focus to main heading
  const mainHeading = document.querySelector('h1');
  mainHeading.setAttribute('tabindex', '-1');
  mainHeading.focus();
}
```

---

## Best Practices

### Do This

1. **Always Update Document Title**
   ```javascript
   history.pushState({ page: 'about' }, '', '/about');
   document.title = 'About Us - MySite';
   ```
   **Why:** Screen readers announce the title, and it appears in browser tabs/bookmarks.

2. **Store Meaningful State Data**
   ```javascript
   history.pushState({
     scrollY: window.scrollY,
     filters: currentFilters,
     timestamp: Date.now()
   }, '', '/search?q=javascript');
   ```
   **Why:** Allows you to restore exact page state when user navigates back.

3. **Use replaceState for Non-Navigation Updates**
   ```javascript
   // User types in search box
   searchInput.addEventListener('input', (e) => {
     const query = e.target.value;
     history.replaceState({ query }, '', `/search?q=${query}`);
   });
   ```
   **Why:** Avoids cluttering history with every keystroke.

4. **Handle Initial Page Load**
   ```javascript
   // On page load, check URL and render appropriate content
   window.addEventListener('DOMContentLoaded', () => {
     const path = location.pathname;
     renderPage(path);

     // Set initial state
     history.replaceState({ path }, '', path);
   });
   ```
   **Why:** Ensures the app works when users land directly on deep URLs.

---

### Avoid This

1. **Don't Change Origin**
   ```javascript
   // ❌ WRONG - Different origin
   history.pushState({}, '', 'https://different-site.com/page');
   ```
   **Why Not:** Throws a SecurityError. URLs must be same-origin.
   **Instead:** Only change path, query, or hash: `/page`, `?tab=2`, `#section`

2. **Don't Rely on the `title` Parameter**
   ```javascript
   // ❌ WRONG - Title parameter is ignored by browsers
   history.pushState({}, 'My Page Title', '/page');
   ```
   **Why Not:** No browser uses this parameter. It was meant for future use.
   **Instead:** Manually update `document.title` yourself.

3. **Don't Forget to Handle popstate**
   ```javascript
   // ❌ WRONG - pushState without popstate handler
   history.pushState({}, '', '/page');
   renderPage('/page');
   // Now back button breaks!
   ```
   **Why Not:** Back/forward buttons won't work correctly.
   **Instead:** Always add a `popstate` listener to handle navigation.

4. **Don't Use for External Links**
   ```javascript
   // ❌ WRONG - Using History API for external sites
   externalLink.addEventListener('click', (e) => {
     e.preventDefault();
     history.pushState({}, '', 'https://external.com');
   });
   ```
   **Why Not:** Security violation and makes no sense.
   **Instead:** Let external links navigate normally.

---

## Related Topics

**Prerequisites (Learn These First):**
- [JavaScript Events](../01-fundamentals/javascript-basics.md) - Event listeners
- [Links and Navigation](../03-links-navigation/anchor-links.md) - Traditional navigation

**Related Concepts:**
- [Page Visibility API](page-visibility.md) - Detect when user switches tabs
- [Online/Offline Detection](online-offline.md) - Handle navigation while offline

**Next Steps (Learn These Next):**
- [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) - Advanced offline caching for SPAs
- [URL API](https://developer.mozilla.org/en-US/docs/Web/API/URL) - Parse and manipulate URLs

**External Resources:**
- [MDN Web Docs - History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)
- [HTML Living Standard - Session History](https://html.spec.whatwg.org/multipage/history.html)
- [Manipulating Browser History (Mozilla)](https://developer.mozilla.org/en-US/docs/Web/API/History_API/Working_with_the_History_API)

---

## Practice Exercise

### Challenge: Build a Simple Blog SPA

**Objective:** Create a single-page blog with multiple articles where each article has its own URL and the back button works correctly.

**Requirements:**
- [ ] Display a list of blog post titles
- [ ] Clicking a title loads the full article without page reload
- [ ] Each article has a unique URL (e.g., `/blog/article-1`)
- [ ] Back button returns to article list
- [ ] Browser's forward button works correctly
- [ ] Bonus: Add URL for scrolling within an article (e.g., `#comments`)

---

### Starter Code

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog SPA</title>
  <style>
    .container { max-width: 800px; margin: 0 auto; padding: 20px; }
    .post-list { list-style: none; padding: 0; }
    .post-list li {
      padding: 15px;
      margin: 10px 0;
      background: #f5f5f5;
      border-radius: 5px;
      cursor: pointer;
    }
    .post-list li:hover { background: #e0e0e0; }
    .article { display: none; }
    .article.active { display: block; }
    .back-btn {
      padding: 10px 15px;
      background: #2196F3;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="container">
    <div id="postList" class="active">
      <h1>My Blog</h1>
      <ul class="post-list">
        <li data-article="article-1">Article 1: Introduction to Web Development</li>
        <li data-article="article-2">Article 2: Understanding the DOM</li>
        <li data-article="article-3">Article 3: Modern JavaScript Features</li>
      </ul>
    </div>

    <div id="article-1" class="article">
      <button class="back-btn">← Back to Posts</button>
      <h1>Introduction to Web Development</h1>
      <p>This is the content of article 1...</p>
    </div>

    <div id="article-2" class="article">
      <button class="back-btn">← Back to Posts</button>
      <h1>Understanding the DOM</h1>
      <p>This is the content of article 2...</p>
    </div>

    <div id="article-3" class="article">
      <button class="back-btn">← Back to Posts</button>
      <h1>Modern JavaScript Features</h1>
      <p>This is the content of article 3...</p>
    </div>
  </div>

  <!-- Add your JavaScript here -->
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

**Complete Solution:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Blog SPA</title>
  <style>
    .container { max-width: 800px; margin: 0 auto; padding: 20px; }
    .post-list { list-style: none; padding: 0; }
    .post-list li {
      padding: 15px;
      margin: 10px 0;
      background: #f5f5f5;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.2s;
    }
    .post-list li:hover { background: #e0e0e0; }
    .article { display: none; }
    .article.active { display: block; }
    .back-btn {
      padding: 10px 15px;
      background: #2196F3;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-bottom: 20px;
    }
    .back-btn:hover { background: #1976D2; }
  </style>
</head>
<body>
  <div class="container">
    <div id="postList">
      <h1>My Blog</h1>
      <ul class="post-list">
        <li data-article="article-1">Article 1: Introduction to Web Development</li>
        <li data-article="article-2">Article 2: Understanding the DOM</li>
        <li data-article="article-3">Article 3: Modern JavaScript Features</li>
      </ul>
    </div>

    <div id="article-1" class="article">
      <button class="back-btn">← Back to Posts</button>
      <h1>Introduction to Web Development</h1>
      <p>Web development is the art and science of building websites and web applications...</p>
    </div>

    <div id="article-2" class="article">
      <button class="back-btn">← Back to Posts</button>
      <h1>Understanding the DOM</h1>
      <p>The Document Object Model (DOM) is a programming interface for web documents...</p>
    </div>

    <div id="article-3" class="article">
      <button class="back-btn">← Back to Posts</button>
      <h1>Modern JavaScript Features</h1>
      <p>ES6 and beyond have introduced powerful features like arrow functions, destructuring...</p>
    </div>
  </div>

  <script>
    const postList = document.getElementById('postList');
    const articles = document.querySelectorAll('.article');
    const backButtons = document.querySelectorAll('.back-btn');

    // Handle article clicks
    document.querySelectorAll('.post-list li').forEach(item => {
      item.addEventListener('click', function() {
        const articleId = this.dataset.article;
        navigateToArticle(articleId);
      });
    });

    // Handle back button clicks
    backButtons.forEach(btn => {
      btn.addEventListener('click', () => {
        navigateToHome();
      });
    });

    // Navigate to article
    function navigateToArticle(articleId) {
      const url = `/blog/${articleId}`;
      history.pushState({ view: 'article', articleId }, '', url);
      showArticle(articleId);
    }

    // Navigate to home
    function navigateToHome() {
      history.pushState({ view: 'home' }, '', '/blog');
      showHome();
    }

    // Show specific article
    function showArticle(articleId) {
      postList.style.display = 'none';
      articles.forEach(article => article.classList.remove('active'));

      const targetArticle = document.getElementById(articleId);
      if (targetArticle) {
        targetArticle.classList.add('active');
        document.title = targetArticle.querySelector('h1').textContent;
      }
    }

    // Show home (post list)
    function showHome() {
      postList.style.display = 'block';
      articles.forEach(article => article.classList.remove('active'));
      document.title = 'My Blog';
    }

    // Handle browser back/forward
    window.addEventListener('popstate', function(event) {
      if (event.state) {
        if (event.state.view === 'article') {
          showArticle(event.state.articleId);
        } else if (event.state.view === 'home') {
          showHome();
        }
      } else {
        // No state = initial load or external navigation
        showHome();
      }
    });

    // Initialize on page load
    window.addEventListener('DOMContentLoaded', function() {
      const path = location.pathname;

      if (path === '/blog' || path === '/') {
        history.replaceState({ view: 'home' }, '', '/blog');
        showHome();
      } else {
        // Handle direct navigation to article (e.g., /blog/article-1)
        const match = path.match(/\/blog\/(article-\d+)/);
        if (match) {
          const articleId = match[1];
          history.replaceState({ view: 'article', articleId }, '', path);
          showArticle(articleId);
        } else {
          showHome();
        }
      }
    });
  </script>
</body>
</html>
```

**Explanation:**
This SPA uses `pushState()` to create separate URLs for each article (`/blog/article-1`, etc.). The `popstate` event handler ensures the back/forward buttons work correctly by checking the state object. The app also handles direct navigation (when users land directly on an article URL) by parsing the path on initial load.

</details>

---

### Expected Result

**Visual Outcome:**
- Clicking an article title instantly shows the article and updates the URL
- The browser's back button returns to the post list
- The forward button re-opens the article
- Direct navigation to `/blog/article-2` shows that article immediately
- Document title updates for each page

**Key Learnings:**
- How to use `pushState()` and `replaceState()` effectively
- Implementing `popstate` event handlers for back/forward navigation
- Managing application state and URL synchronization
- Real-world SPA navigation patterns

---

## Navigation

**Previous:** [Server-Sent Events](server-sent-events.md)
**Next:** [Fullscreen API](fullscreen.md)
**Up:** [Back to HTML5 APIs](../)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 18, 2025
**Category:** HTML5 APIs
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
