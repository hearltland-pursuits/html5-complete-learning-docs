---
title: Language and Direction Attributes
category: Global Attributes
order: 20
---

# Language and Direction Attributes

> **Quick Summary:** The `lang` attribute specifies the language of content (critical for SEO, accessibility, and browser features like spell-check). The `dir` attribute controls text direction for right-to-left languages (Arabic, Hebrew). Both improve internationalization (i18n) and user experience.

## Table of Contents
- [Introduction](#introduction)
- [Lang Attribute](#lang-attribute)
- [Dir Attribute](#dir-attribute)
- [Use Cases](#use-cases)
- [Examples](#examples)
- [Best Practices](#best-practices)
- [Related Topics](#related-topics)

---

## Introduction

The `lang` and `dir` attributes are global attributes that control language and text direction:

- **`lang`**: Declares the language of element content (English, Spanish, Arabic, etc.)
- **`dir`**: Sets text direction (left-to-right or right-to-left)

**Key points:**
- Both are global (work on any HTML element)
- `lang` is critical for SEO, accessibility, screen readers
- `dir` is essential for RTL languages (Arabic, Hebrew, Persian)
- Can be set on `<html>` for whole page or specific elements

**Key Concept:** `lang` tells browsers and assistive technologies what language content is written in. `dir` tells browsers which direction to display text. Both are essential for multilingual and international websites.

---

## Lang Attribute

### Basic Syntax

```html
<element lang="language-code">Content</element>
```

### Language Codes

Language codes follow **ISO 639-1** (2-letter) or **BCP 47** (language-region):

**Common language codes:**
```html
<html lang="en">          <!-- English (generic) -->
<html lang="en-US">       <!-- English (United States) -->
<html lang="en-GB">       <!-- English (United Kingdom) -->
<html lang="es">          <!-- Spanish (generic) -->
<html lang="es-MX">       <!-- Spanish (Mexico) -->
<html lang="es-ES">       <!-- Spanish (Spain) -->
<html lang="fr">          <!-- French (generic) -->
<html lang="fr-FR">       <!-- French (France) -->
<html lang="fr-CA">       <!-- French (Canada) -->
<html lang="de">          <!-- German -->
<html lang="zh">          <!-- Chinese (generic) -->
<html lang="zh-CN">       <!-- Chinese (Simplified) -->
<html lang="zh-TW">       <!-- Chinese (Traditional) -->
<html lang="ja">          <!-- Japanese -->
<html lang="ar">          <!-- Arabic -->
<html lang="ru">          <!-- Russian -->
<html lang="pt">          <!-- Portuguese (generic) -->
<html lang="pt-BR">       <!-- Portuguese (Brazil) -->
<html lang="pt-PT">       <!-- Portuguese (Portugal) -->
```

### Setting Page Language

**Always set `lang` on `<html>`:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Page Title</title>
</head>
<body>
  <!-- Content -->
</body>
</html>
```

### Why Lang Matters

**1. Screen Readers (Accessibility)**
- Pronounces text with correct accent/pronunciation
- Switches voices for different languages
- Critical for WCAG compliance

**2. Search Engines (SEO)**
- Google uses `lang` for regional search results
- Shows correct language version to users
- Helps with hreflang targeting

**3. Browser Features**
- Spell-check uses correct dictionary
- Hyphenation works correctly
- Translation prompts appear for foreign languages

**4. CSS Styling**
- Can style based on language: `:lang(en)`, `:lang(es)`

### Setting Language on Specific Elements

**Mixed-language content:**
```html
<html lang="en">
<body>
  <p>This paragraph is in English.</p>

  <!-- Quote in French -->
  <blockquote lang="fr">
    <p>Bonjour! Comment allez-vous?</p>
  </blockquote>

  <!-- Article in Spanish -->
  <article lang="es">
    <h2>Título en Español</h2>
    <p>Este artículo está en español.</p>
  </article>

  <p>Back to English.</p>
</body>
</html>
```

### CSS Styling by Language

```html
<style>
/* Style English content */
:lang(en) {
  font-family: Georgia, serif;
}

/* Style Spanish content */
:lang(es) {
  font-family: 'Times New Roman', serif;
}

/* Style Arabic content */
:lang(ar) {
  font-family: 'Arabic Typesetting', serif;
}

/* Different quotes for different languages */
:lang(en) q::before { content: '"'; }
:lang(en) q::after { content: '"'; }

:lang(fr) q::before { content: '«\00A0'; }
:lang(fr) q::after { content: '\00A0»'; }

:lang(de) q::before { content: '„'; }
:lang(de) q::after { content: '"'; }
</style>
```

---

## Dir Attribute

### Basic Syntax

```html
<element dir="direction">Content</element>
```

### Valid Values

| Value | Description | Use Case |
|-------|-------------|----------|
| `ltr` | Left-to-right | English, Spanish, French, German, most languages |
| `rtl` | Right-to-left | Arabic, Hebrew, Persian, Urdu |
| `auto` | Browser determines direction | Mixed content (automatically detects) |

### Setting Text Direction

**Right-to-left languages:**
```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>عنوان الصفحة</title>
</head>
<body>
  <h1>مرحبا بكم</h1>
  <p>هذا نص باللغة العربية</p>
</body>
</html>
```

**Hebrew example:**
```html
<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>כותרת העמוד</title>
</head>
<body>
  <h1>שלום</h1>
  <p>זהו טקסט בעברית</p>
</body>
</html>
```

### Mixed Direction Content

**English page with Arabic quote:**
```html
<html lang="en" dir="ltr">
<body>
  <p>This paragraph is left-to-right.</p>

  <blockquote lang="ar" dir="rtl">
    <p>هذا اقتباس باللغة العربية</p>
  </blockquote>

  <p>Back to left-to-right English.</p>
</body>
</html>
```

### Auto Direction

**Let browser detect direction:**
```html
<html lang="en" dir="ltr">
<body>
  <p>English text (LTR)</p>

  <!-- Auto-detect direction based on content -->
  <p dir="auto">مرحبا Hello שלום</p>

  <!-- User-generated content (unknown direction) -->
  <textarea dir="auto"></textarea>
</body>
</html>
```

### RTL Layout Impact

**What changes in RTL:**
- Text flows right-to-left
- UI elements flip (scrollbars, buttons)
- Margins/padding mirror
- Flexbox/Grid direction reverses

```html
<html lang="ar" dir="rtl">
<head>
  <style>
    .container {
      display: flex;
      /* In RTL, flex items start from right */
    }

    .sidebar {
      margin-left: 20px;
      /* In RTL, becomes margin-right automatically */
    }
  </style>
</head>
<body>
  <div class="container">
    <aside class="sidebar">الشريط الجانبي</aside>
    <main>المحتوى الرئيسي</main>
  </div>
</body>
</html>
```

---

## Use Cases

### 1. Multilingual Website

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Multilingual Site</title>
</head>
<body>
  <header>
    <nav>
      <a href="/en">English</a>
      <a href="/es">Español</a>
      <a href="/fr">Français</a>
      <a href="/ar">العربية</a>
    </nav>
  </header>

  <main>
    <section lang="en">
      <h2>Welcome</h2>
      <p>This is the English section.</p>
    </section>

    <section lang="es">
      <h2>Bienvenido</h2>
      <p>Esta es la sección en español.</p>
    </section>

    <section lang="fr">
      <h2>Bienvenue</h2>
      <p>Ceci est la section française.</p>
    </section>

    <section lang="ar" dir="rtl">
      <h2>مرحبا</h2>
      <p>هذا هو القسم العربي</p>
    </section>
  </main>
</body>
</html>
```

### 2. Blog with Foreign Quotes

```html
<html lang="en">
<body>
  <article>
    <h1>Understanding Multilingual Web Design</h1>

    <p>As the famous French saying goes:</p>

    <blockquote lang="fr">
      <p>« Plus ça change, plus c'est la même chose »</p>
      <footer>— Jean-Baptiste Alphonse Karr</footer>
    </blockquote>

    <p>Which translates to: "The more things change, the more they stay the same."</p>

    <p>Similarly, in Arabic:</p>

    <blockquote lang="ar" dir="rtl">
      <p>العلم نور والجهل ظلام</p>
      <footer>— مثل عربي</footer>
    </blockquote>

    <p>Meaning: "Knowledge is light, ignorance is darkness."</p>
  </article>
</body>
</html>
```

### 3. E-Commerce with RTL Support

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>متجر إلكتروني</title>
  <style>
    .product-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 20px;
      /* Grid automatically adjusts for RTL */
    }

    .product-card {
      border: 1px solid #ddd;
      padding: 20px;
      /* No need to manually flip margins/padding */
    }

    .price {
      font-weight: bold;
      color: #28a745;
    }

    /* Logical properties work in both LTR and RTL */
    .product-card {
      margin-inline-start: 10px; /* Left in LTR, right in RTL */
      padding-inline-end: 15px;  /* Right in LTR, left in RTL */
    }
  </style>
</head>
<body>
  <header>
    <h1>متجرنا الإلكتروني</h1>
    <nav>
      <a href="/">الرئيسية</a>
      <a href="/products">المنتجات</a>
      <a href="/cart">السلة</a>
    </nav>
  </header>

  <main>
    <div class="product-grid">
      <div class="product-card">
        <img src="product1.jpg" alt="منتج 1">
        <h3>سماعات لاسلكية</h3>
        <p class="price">٩٩٫٩٩ ريال</p>
        <button>إضافة إلى السلة</button>
      </div>

      <div class="product-card">
        <img src="product2.jpg" alt="منتج 2">
        <h3>ساعة ذكية</h3>
        <p class="price">١٩٩٫٩٩ ريال</p>
        <button>إضافة إلى السلة</button>
      </div>
    </div>
  </main>
</body>
</html>
```

### 4. Form with Mixed Directions

```html
<html lang="en" dir="ltr">
<body>
  <form>
    <h2>User Registration</h2>

    <!-- LTR fields -->
    <label for="email">Email:</label>
    <input type="email" id="email" name="email">

    <label for="password">Password:</label>
    <input type="password" id="password" name="password">

    <!-- User might enter Arabic name -->
    <label for="full-name">Full Name:</label>
    <input type="text" id="full-name" name="full-name" dir="auto">

    <!-- User might enter RTL address -->
    <label for="address">Address:</label>
    <textarea id="address" name="address" dir="auto"></textarea>

    <!-- Comments (unknown language) -->
    <label for="comments">Comments:</label>
    <textarea id="comments" name="comments" dir="auto"></textarea>

    <button type="submit">Submit</button>
  </form>
</body>
</html>
```

---

## Examples

### Example 1: Complete RTL Website (Arabic)

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>موقع عربي كامل</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Arabic Typesetting', 'Traditional Arabic', Arial, sans-serif;
      line-height: 1.6;
    }

    header {
      background: #333;
      color: white;
      padding: 20px;
    }

    nav {
      display: flex;
      gap: 20px;
      margin-top: 10px;
    }

    nav a {
      color: white;
      text-decoration: none;
    }

    main {
      max-width: 1200px;
      margin: 40px auto;
      padding: 0 20px;
    }

    .article-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 30px;
      margin-top: 30px;
    }

    article {
      border: 1px solid #ddd;
      padding: 20px;
      border-radius: 8px;
    }

    footer {
      background: #f8f9fa;
      padding: 40px 20px;
      text-align: center;
      margin-top: 60px;
    }
  </style>
</head>
<body>
  <header>
    <h1>موقع الأخبار العربية</h1>
    <nav>
      <a href="/">الرئيسية</a>
      <a href="/news">الأخبار</a>
      <a href="/sports">الرياضة</a>
      <a href="/tech">التقنية</a>
      <a href="/contact">اتصل بنا</a>
    </nav>
  </header>

  <main>
    <h2>آخر الأخبار</h2>

    <div class="article-grid">
      <article>
        <h3>عنوان الخبر الأول</h3>
        <p>هذا نص تجريبي للخبر الأول. يحتوي على معلومات مهمة حول الموضوع.</p>
        <a href="/article1">اقرأ المزيد ←</a>
      </article>

      <article>
        <h3>عنوان الخبر الثاني</h3>
        <p>هذا نص تجريبي للخبر الثاني. يتضمن تفاصيل إضافية عن الحدث.</p>
        <a href="/article2">اقرأ المزيد ←</a>
      </article>

      <article>
        <h3>عنوان الخبر الثالث</h3>
        <p>هذا نص تجريبي للخبر الثالث. يقدم رؤية شاملة حول القضية.</p>
        <a href="/article3">اقرأ المزيد ←</a>
      </article>
    </div>
  </main>

  <footer>
    <p>© ٢٠٢٥ موقع الأخبار العربية. جميع الحقوق محفوظة.</p>
  </footer>
</body>
</html>
```

### Example 2: Language Switcher

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8">
  <title>Language Switcher Demo</title>
  <style>
    .lang-switcher {
      position: fixed;
      top: 20px;
      right: 20px;
      display: flex;
      gap: 10px;
    }

    .lang-switcher button {
      padding: 8px 16px;
      border: 1px solid #ddd;
      background: white;
      cursor: pointer;
    }

    .lang-switcher button.active {
      background: #007bff;
      color: white;
      border-color: #007bff;
    }

    .content {
      max-width: 800px;
      margin: 80px auto 40px;
      padding: 0 20px;
    }

    [lang="ar"] {
      font-family: 'Arabic Typesetting', Arial, sans-serif;
    }

    [lang="he"] {
      font-family: 'David', 'Times New Roman', serif;
    }
  </style>
</head>
<body>
  <div class="lang-switcher">
    <button data-lang="en" data-dir="ltr" class="active">English</button>
    <button data-lang="es" data-dir="ltr">Español</button>
    <button data-lang="ar" data-dir="rtl">العربية</button>
    <button data-lang="he" data-dir="rtl">עברית</button>
  </div>

  <div class="content">
    <div class="lang-content" data-lang="en">
      <h1>Welcome to Our Website</h1>
      <p>This is a demonstration of multilingual content with different text directions.</p>
    </div>

    <div class="lang-content" data-lang="es" style="display:none;">
      <h1>Bienvenido a Nuestro Sitio Web</h1>
      <p>Esta es una demostración de contenido multilingüe con diferentes direcciones de texto.</p>
    </div>

    <div class="lang-content" data-lang="ar" style="display:none;">
      <h1>مرحبا بكم في موقعنا</h1>
      <p>هذا عرض توضيحي لمحتوى متعدد اللغات مع اتجاهات نصية مختلفة</p>
    </div>

    <div class="lang-content" data-lang="he" style="display:none;">
      <h1>ברוכים הבאים לאתר שלנו</h1>
      <p>זוהי הדגמה של תוכן רב לשוני עם כיווני טקסט שונים</p>
    </div>
  </div>

  <script>
    const buttons = document.querySelectorAll('.lang-switcher button');
    const html = document.documentElement;

    buttons.forEach(button => {
      button.addEventListener('click', function() {
        const lang = this.dataset.lang;
        const dir = this.dataset.dir;

        // Update HTML lang and dir
        html.setAttribute('lang', lang);
        html.setAttribute('dir', dir);

        // Update active button
        buttons.forEach(btn => btn.classList.remove('active'));
        this.classList.add('active');

        // Show corresponding content
        document.querySelectorAll('.lang-content').forEach(content => {
          content.style.display = content.dataset.lang === lang ? 'block' : 'none';
        });
      });
    });
  </script>
</body>
</html>
```

---

## Best Practices

### Do This

1. **Always Set Lang on HTML Element**
   ```html
   <!-- GOOD: Language declared at document level -->
   <!DOCTYPE html>
   <html lang="en">
   ```

2. **Use Regional Codes When Appropriate**
   ```html
   <!-- GOOD: Specific regional variant -->
   <html lang="en-US">  <!-- American English -->
   <html lang="en-GB">  <!-- British English -->
   <html lang="es-MX">  <!-- Mexican Spanish -->
   ```

3. **Set Lang on Mixed-Language Content**
   ```html
   <p>The French phrase <span lang="fr">c'est la vie</span> is commonly used.</p>
   ```

4. **Use dir="auto" for User Input**
   ```html
   <!-- User might enter any language -->
   <textarea dir="auto"></textarea>
   <input type="text" dir="auto">
   ```

5. **Use Logical CSS Properties for RTL**
   ```css
   /* GOOD: Works in both LTR and RTL */
   .element {
     margin-inline-start: 20px;  /* Left in LTR, right in RTL */
     padding-inline-end: 15px;   /* Right in LTR, left in RTL */
   }

   /* AVOID: Hard-coded direction */
   .element {
     margin-left: 20px;  /* Won't flip in RTL */
   }
   ```

### Avoid This

1. **Don't Omit Lang Attribute**
   ```html
   <!-- WRONG: No language specified -->
   <!DOCTYPE html>
   <html>

   <!-- CORRECT -->
   <!DOCTYPE html>
   <html lang="en">
   ```

2. **Don't Use Wrong Language Code**
   ```html
   <!-- WRONG: Invalid code -->
   <html lang="english">

   <!-- CORRECT: ISO 639-1 code -->
   <html lang="en">
   ```

3. **Don't Forget Dir for RTL Languages**
   ```html
   <!-- WRONG: Arabic without dir -->
   <html lang="ar">
     <p>النص العربي</p>
   </html>

   <!-- CORRECT -->
   <html lang="ar" dir="rtl">
     <p>النص العربي</p>
   </html>
   ```

---

## Quick Reference

### Language Codes (Common)

| Code | Language |
|------|----------|
| `en` | English |
| `es` | Spanish |
| `fr` | French |
| `de` | German |
| `it` | Italian |
| `pt` | Portuguese |
| `ru` | Russian |
| `zh` | Chinese |
| `ja` | Japanese |
| `ko` | Korean |
| `ar` | Arabic |
| `he` | Hebrew |
| `hi` | Hindi |
| `tr` | Turkish |

### Direction Values

| Value | Description |
|-------|-------------|
| `ltr` | Left-to-right (default) |
| `rtl` | Right-to-left (Arabic, Hebrew) |
| `auto` | Browser auto-detects |

---

## Browser Support

| Attribute | Chrome | Firefox | Safari | Edge | IE |
|-----------|--------|---------|--------|------|----|
| `lang` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `dir` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ All |
| `dir="auto"` | ✅ All | ✅ All | ✅ All | ✅ All | ✅ 11+ |

---

## Related Topics
- [Global Attributes](html5-attributes.md)
- [Meta Tags](../08-metadata-seo/meta-tags.md)
- [Accessibility](../13-accessibility/accessibility-overview.md)

---

**Last Updated:** November 17, 2025
**Category:** Global Attributes
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
