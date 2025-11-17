---
title: Text Direction and Language
category: Text Content
order: 7
---

# Text Direction and Language

> **Quick Summary:** HTML5 provides the lang and dir attributes to specify content language and text direction (left-to-right or right-to-left), enabling proper rendering of multilingual content and improving accessibility for assistive technologies and search engines.

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

The web is inherently international, serving content in hundreds of languages with different writing systems and directionality. HTML5 provides two critical global attributes—`lang` and `dir`—to properly handle multilingual and bidirectional content. These attributes ensure correct text rendering, improve accessibility, and help search engines understand content language for proper indexing.

The `lang` attribute specifies the natural language of content using standardized language codes (ISO 639-1 two-letter codes, optionally combined with ISO 3166-1 region codes). This information helps screen readers pronounce text correctly, enables browser translation features, and assists search engines with language-specific indexing. Setting `lang` on the `<html>` element establishes the document's primary language, while inline `lang` attributes mark sections in different languages.

The `dir` attribute controls text direction for languages written right-to-left (RTL) like Arabic, Hebrew, Persian, and Urdu, or left-to-right (LTR) like English, Spanish, and French. Proper directionality ensures text flows correctly, punctuation appears in the right position, and bidirectional content (mixing RTL and LTR) displays appropriately. Understanding text direction is essential for creating inclusive, globally accessible websites.

**Key Concept:** Use `lang` to specify content language (enabling correct pronunciation and indexing) and `dir` to control text flow direction (LTR or RTL). Both are global attributes applicable to any HTML element.

## Basic Syntax

### Language Attribute (lang)

**Set document language:**
```html
<!DOCTYPE html>
<html lang="en">
  <!-- English content -->
</html>
```

**Common language codes:**

| Code | Language | Region Example |
|------|----------|----------------|
| `en` | English | `en-US` (US), `en-GB` (British) |
| `es` | Spanish | `es-ES` (Spain), `es-MX` (Mexico) |
| `fr` | French | `fr-FR` (France), `fr-CA` (Canadian) |
| `de` | German | `de-DE` (Germany), `de-AT` (Austria) |
| `zh` | Chinese | `zh-CN` (Simplified), `zh-TW` (Traditional) |
| `ar` | Arabic | `ar-SA` (Saudi Arabia), `ar-EG` (Egypt) |
| `ja` | Japanese | `ja-JP` (Japan) |
| `ru` | Russian | `ru-RU` (Russia) |
| `pt` | Portuguese | `pt-BR` (Brazil), `pt-PT` (Portugal) |
| `hi` | Hindi | `hi-IN` (India) |
| `he` | Hebrew | `he-IL` (Israel) |

**Inline language switching:**
```html
<p>
  The French word for "hello" is <span lang="fr">bonjour</span>.
</p>
```

### Direction Attribute (dir)

**Possible values:**

| Value | Meaning | Use Case |
|-------|---------|----------|
| `ltr` | Left-to-right | English, Spanish, French, etc. |
| `rtl` | Right-to-left | Arabic, Hebrew, Persian, Urdu |
| `auto` | Automatic (based on content) | Mixed directional content |

**Set document direction:**
```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
  <!-- Arabic content flows right-to-left -->
</html>
```

**Inline direction switching:**
```html
<p dir="rtl">
  هذا النص بالعربية (This text is in Arabic)
</p>
```

**Automatic direction detection:**
```html
<p dir="auto">
  This automatically detects direction based on first strongly-typed character.
</p>
```

**Combined usage:**
```html
<html lang="ar" dir="rtl">
  <body>
    <p>محتوى عربي (Arabic content)</p>
    <p lang="en" dir="ltr">English content embedded in Arabic page</p>
  </body>
</html>
```

## Examples

### Example 1: Multilingual Website with Language Switching
**Use Case:** International company website with multiple language versions

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Global Tech Solutions</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
    }
    .language-switcher {
      text-align: right;
      margin-bottom: 2em;
    }
    .language-switcher a {
      margin: 0 0.5em;
      padding: 0.5em 1em;
      background-color: #f0f0f0;
      text-decoration: none;
      color: #333;
      border-radius: 4px;
    }
    .language-switcher a:hover {
      background-color: #e0e0e0;
    }
    blockquote {
      border-left: 4px solid #0066cc;
      padding-left: 1em;
      font-style: italic;
      margin: 1.5em 0;
    }
    [lang="fr"] {
      quotes: "« " " »";
    }
    [lang="de"] {
      quotes: "„" """;
    }
  </style>
</head>
<body>
  <nav class="language-switcher" aria-label="Language Selector">
    <a href="/en" lang="en" hreflang="en">English</a>
    <a href="/es" lang="es" hreflang="es">Español</a>
    <a href="/fr" lang="fr" hreflang="fr">Français</a>
    <a href="/de" lang="de" hreflang="de">Deutsch</a>
  </nav>

  <article>
    <h1>Welcome to Global Tech Solutions</h1>

    <section>
      <h2>Our Mission</h2>
      <p>
        We deliver innovative technology solutions to businesses worldwide.
        Our team speaks your language and understands your market.
      </p>

      <h3>Testimonials</h3>

      <blockquote lang="fr">
        <p>
          Une entreprise exceptionnelle qui comprend vraiment les besoins
          internationaux. Leur service client est remarquable.
        </p>
        <footer>— Marie Dupont, <span lang="en">CEO, Acme France</span></footer>
      </blockquote>

      <blockquote lang="es">
        <p>
          La mejor experiencia que hemos tenido con un proveedor de tecnología.
          Altamente recomendado para empresas en América Latina.
        </p>
        <footer>— Carlos Rodríguez, <span lang="en">CTO, Tech México</span></footer>
      </blockquote>

      <blockquote lang="de">
        <p>
          Hervorragende technische Expertise und ausgezeichneter Support.
          Wir arbeiten seit drei Jahren zusammen.
        </p>
        <footer>— Hans Müller, <span lang="en">Director, Berlin Systems</span></footer>
      </blockquote>
    </section>

    <section>
      <h2>Contact Us</h2>
      <p>Our offices:</p>
      <address>
        <strong lang="en">USA:</strong> 123 Tech Drive, San Francisco, CA 94102<br>
        <strong lang="es">México:</strong> Av. Reforma 456, Ciudad de México<br>
        <strong lang="fr">France:</strong> 78 Rue de la Tech, 75001 Paris<br>
        <strong lang="de">Deutschland:</strong> Technologiestraße 90, 10115 Berlin
      </address>
    </section>
  </article>
</body>
</html>
```

### Example 2: Right-to-Left (RTL) Language Support
**Use Case:** Arabic website with embedded English content

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>الأخبار التقنية</title>
  <style>
    body {
      font-family: 'Arial', 'Tahoma', sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.8;
    }
    h1, h2 {
      color: #2c3e50;
      border-bottom: 2px solid #3498db;
      padding-bottom: 0.5em;
    }
    .english-content {
      direction: ltr;
      text-align: left;
      background-color: #f9f9f9;
      padding: 1em;
      border-left: 4px solid #e74c3c;
      margin: 1.5em 0;
    }
    .date {
      color: #7f8c8d;
      font-size: 0.9em;
    }
    code {
      font-family: 'Courier New', monospace;
      background-color: #ecf0f1;
      padding: 2px 6px;
      border-radius: 3px;
      direction: ltr;
      display: inline-block;
    }
  </style>
</head>
<body>
  <article>
    <header>
      <h1>تطورات التكنولوجيا الحديثة</h1>
      <p class="date">١٧ نوفمبر ٢٠٢٥</p>
    </header>

    <section>
      <h2>الذكاء الاصطناعي في التعليم</h2>
      <p>
        يشهد مجال التعليم ثورة كبيرة بفضل تقنيات الذكاء الاصطناعي.
        المدارس والجامعات في جميع أنحاء العالم تتبنى هذه التقنيات
        لتحسين تجربة التعلم.
      </p>

      <p>
        وفقًا لتقرير منظمة اليونسكو، فإن استخدام أدوات الذكاء الاصطناعي
        في الفصول الدراسية قد زاد بنسبة ٤٠٪ في السنوات الثلاث الماضية.
      </p>

      <div class="english-content" lang="en" dir="ltr">
        <h3>UNESCO Report Summary (English)</h3>
        <p>
          Artificial Intelligence in education has grown by 40% over the past
          three years. Schools are adopting AI-powered tools for personalized
          learning experiences and automated assessment systems.
        </p>
        <p>
          Key technologies include: natural language processing (NLP),
          machine learning algorithms, and adaptive learning platforms.
        </p>
      </div>

      <p>
        التقنيات الرئيسية تشمل معالجة اللغة الطبيعية، وخوارزميات
        التعلم الآلي، ومنصات التعلم التكيفي.
      </p>
    </section>

    <section>
      <h2>البرمجة وتطوير الويب</h2>
      <p>
        لغات البرمجة الأكثر شعبية في عام ٢٠٢٥ تشمل:
      </p>

      <ul>
        <li>
          <span lang="en">Python</span> - لتحليل البيانات والذكاء الاصطناعي
        </li>
        <li>
          <span lang="en">JavaScript</span> - لتطوير تطبيقات الويب
        </li>
        <li>
          <span lang="en">Go</span> - للخدمات السحابية
        </li>
      </ul>

      <p>
        مثال على كود <span lang="en">Python</span> بسيط:
        <code lang="en">print("Hello World")</code>
      </p>

      <p>
        في اللغة العربية، يمكننا كتابة:
        <code lang="en">print("مرحبا بالعالم")</code>
      </p>
    </section>

    <section>
      <h2>الأمن السيبراني</h2>
      <p>
        مع تزايد التهديدات الإلكترونية، أصبح الأمن السيبراني أولوية
        قصوى للشركات والمؤسسات. الخبراء ينصحون باستخدام:
      </p>

      <ol>
        <li>المصادقة الثنائية (<abbr title="Two-Factor Authentication" lang="en">2FA</abbr>)</li>
        <li>تشفير البيانات باستخدام <abbr title="Secure Sockets Layer" lang="en">SSL</abbr>/
            <abbr title="Transport Layer Security" lang="en">TLS</abbr></li>
        <li>جدران الحماية المتقدمة</li>
      </ol>
    </section>

    <footer>
      <p>
        <small>
          جميع الحقوق محفوظة © ٢٠٢٥ الأخبار التقنية
        </small>
      </p>
    </footer>
  </article>
</body>
</html>
```

### Example 3: Bidirectional Text (Bidi) with Mixed Content
**Use Case:** Educational content mixing English and Hebrew

```html
<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>לימוד תכנות</title>
  <style>
    body {
      font-family: 'Arial', 'David', sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.8;
    }
    h1 {
      color: #2c3e50;
      border-bottom: 3px solid #9b59b6;
      padding-bottom: 0.5em;
    }
    .code-example {
      background-color: #2d2d2d;
      color: #f8f8f2;
      padding: 1.5em;
      border-radius: 6px;
      direction: ltr;
      text-align: left;
      font-family: 'Consolas', 'Courier New', monospace;
      margin: 1.5em 0;
      overflow-x: auto;
    }
    .english-term {
      direction: ltr;
      display: inline-block;
      font-family: 'Consolas', monospace;
      background-color: #ecf0f1;
      padding: 2px 6px;
      border-radius: 3px;
    }
    .bidi-warning {
      background-color: #fff3cd;
      border-left: 4px solid #ffc107;
      padding: 1em;
      margin: 1.5em 0;
    }
  </style>
</head>
<body>
  <article>
    <h1>מדריך ללימוד HTML5</h1>

    <section>
      <h2>מבוא</h2>
      <p>
        <span lang="en" class="english-term">HTML5</span> היא שפת סימון המשמשת
        ליצירת דפי אינטרנט. המילה
        <span lang="en" class="english-term">HTML</span> היא ראשי תיבות של
        <span lang="en">HyperText Markup Language</span>.
      </p>

      <p>
        האלמנטים הבסיסיים ב-<span lang="en" class="english-term">HTML</span> כוללים:
      </p>

      <ul>
        <li><code lang="en" dir="ltr">&lt;html&gt;</code> - אלמנט השורש</li>
        <li><code lang="en" dir="ltr">&lt;head&gt;</code> - מידע על המסמך</li>
        <li><code lang="en" dir="ltr">&lt;body&gt;</code> - תוכן הדף</li>
      </ul>
    </section>

    <section>
      <h2>דוגמה לקוד HTML</h2>
      <p>
        הנה דוגמה פשוטה של מסמך <span lang="en" class="english-term">HTML5</span>:
      </p>

      <div class="code-example" lang="en">
<pre>&lt;!DOCTYPE html&gt;
&lt;html lang="he" dir="rtl"&gt;
&lt;head&gt;
  &lt;meta charset="UTF-8"&gt;
  &lt;title&gt;דף לדוגמה&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;שלום עולם&lt;/h1&gt;
  &lt;p&gt;זהו מסמך HTML בעברית.&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
      </div>

      <div class="bidi-warning">
        <p>
          <strong>שימו לב:</strong> כאשר כותבים קוד שמכיל טקסט בעברית,
          חשוב להגדיר את תכונות
          <code lang="en" dir="ltr">lang="he"</code> ו-
          <code lang="en" dir="ltr">dir="rtl"</code> באלמנט
          <code lang="en" dir="ltr">&lt;html&gt;</code>.
        </p>
      </div>
    </section>

    <section>
      <h2>טיפים לעבודה עם טקסט דו-כיווני</h2>
      <p>
        כאשר משלבים טקסט בעברית עם מונחים באנגלית, חשוב להשתמש ב-
        <span lang="en" class="english-term">bidi</span> (bidirectional) באופן נכון:
      </p>

      <ol>
        <li>
          השתמשו ב-<code lang="en" dir="ltr">lang</code> לציון שפה:
          <code lang="en" dir="ltr">&lt;span lang="en"&gt;English&lt;/span&gt;</code>
        </li>
        <li>
          השתמשו ב-<code lang="en" dir="ltr">dir</code> לשינוי כיווניות:
          <code lang="en" dir="ltr">dir="ltr"</code> או
          <code lang="en" dir="ltr">dir="rtl"</code>
        </li>
        <li>
          השתמשו ב-<code lang="en" dir="ltr">dir="auto"</code> לזיהוי אוטומטי
        </li>
      </ol>
    </section>

    <footer>
      <p>
        <small>
          כל הזכויות שמורות © 2025 | נוצר בעזרת
          <span lang="en" class="english-term">HTML5</span>
        </small>
      </p>
    </footer>
  </article>
</body>
</html>
```

## Common Use Cases

### 1. Multilingual Websites
Mark language changes for proper screen reader pronunciation and search engine indexing:

```html
<p>
  The German word for "thank you" is <span lang="de">danke</span>.
  In Japanese, you say <span lang="ja">ありがとう</span> (arigatou).
</p>
```

**When to use:** Educational content, language learning sites, translation services, international business sites

### 2. Right-to-Left Language Support
Create websites for RTL languages like Arabic, Hebrew, Persian, or Urdu:

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <title>موقع عربي</title>
</head>
<body>
  <h1>مرحبا بكم</h1>
  <p>هذا محتوى عربي يتدفق من اليمين إلى اليسار.</p>
</body>
</html>
```

**When to use:** Content targeting Middle East, North Africa, Israel, Pakistan, or other RTL language regions

### 3. User-Generated Content with Unknown Direction
Use `dir="auto"` for content where directionality isn't known in advance:

```html
<form>
  <label for="comment">Comment:</label>
  <textarea id="comment" dir="auto"></textarea>
</form>
```

**When to use:** Comment systems, social media posts, user reviews, multilingual forums

## Browser Support

| Attribute | Chrome | Firefox | Safari | Edge | Mobile Safari | Mobile Chrome |
|-----------|--------|---------|--------|------|---------------|---------------|
| `lang` | All | All | All | All | All | All |
| `dir="ltr"` | All | All | All | All | All | All |
| `dir="rtl"` | All | All | All | All | All | All |
| `dir="auto"` | 16+ | 10+ | 6+ | 79+ | 6+ | 18+ |

**Browser Support:** Universal for `lang`, `dir="ltr"`, and `dir="rtl"`

The `lang` and `dir` attributes have been part of HTML since HTML 4.01 (1999) and are supported universally. The `dir="auto"` value was introduced in HTML5 and has excellent modern browser support (98%+ as of 2025).

**Default Behavior:**
- Without `lang`: Browsers assume document language based on system/browser settings
- Without `dir`: Browsers default to LTR (left-to-right)
- `dir="auto"`: Detects direction from first strongly-typed character (Unicode bidi algorithm)

**Resources:**
- [MDN: lang attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang)
- [MDN: dir attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/dir)
- [WHATWG HTML Living Standard: lang and dir](https://html.spec.whatwg.org/multipage/dom.html#the-lang-and-xml:lang-attributes)
- [W3C: Language Tags](https://www.w3.org/International/articles/language-tags/)
- [W3C: Creating HTML Pages in Arabic, Hebrew and Other Right-to-left Scripts](https://www.w3.org/International/questions/qa-html-dir)

## Accessibility Considerations

### WCAG 2.1 Compliance

**Level A Requirements (3.1.1):**
- **Language of Page:** Set `lang` attribute on `<html>` element to specify default language
- Required for WCAG Level A compliance

**Level AA Requirements (3.1.2):**
- **Language of Parts:** Mark inline language changes with `lang` attribute on containing element
- Required for WCAG Level AA compliance

### Screen Reader Behavior

**lang attribute:**
- Screen readers use `lang` to select correct pronunciation rules
- Example: "Paris" pronounced differently in English vs. French
- Without `lang`, screen readers guess based on system settings (often incorrect)

**dir attribute:**
- Screen readers announce RTL content correctly when `dir="rtl"` is set
- Reading order follows directionality (right-to-left for Arabic/Hebrew)
- Punctuation placement adjusts based on direction

**Impact of missing lang/dir:**
```html
<!-- BAD: No language specified -->
<p>Bonjour</p>  <!-- Screen reader may pronounce as English "BON-joor" -->

<!-- GOOD: French language specified -->
<p lang="fr">Bonjour</p>  <!-- Screen reader pronounces correctly "bon-ZHOOR" -->
```

### Best Practices for Screen Readers

1. **Always set lang on html element:**
```html
<!DOCTYPE html>
<html lang="en">
  <!-- Sets default language for entire document -->
</html>
```

2. **Mark all language changes inline:**
```html
<p>
  The Spanish word is <span lang="es">hola</span>.
</p>
```

3. **Set dir for RTL content:**
```html
<p lang="ar" dir="rtl">
  مرحبا
</p>
```

4. **Use dir="auto" for user input:**
```html
<input type="text" dir="auto" placeholder="Enter text in any language">
```

**Resources:**
- [WCAG 2.1: Language of Page (3.1.1)](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
- [WCAG 2.1: Language of Parts (3.1.2)](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
- [WebAIM: Document Language](https://webaim.org/techniques/screenreader/#language)

## Best Practices

### Do This ✓

1. **Always declare document language:**
```html
<!-- Correct: Explicit language declaration -->
<!DOCTYPE html>
<html lang="en">
```

2. **Mark inline language changes:**
```html
<!-- Correct: Language switching for proper pronunciation -->
<p>
  In French, "hello" is <span lang="fr">bonjour</span>,
  and in Spanish it's <span lang="es">hola</span>.
</p>
```

3. **Use region codes when relevant:**
```html
<!-- Correct: Specifying regional variant -->
<html lang="en-GB">  <!-- British English -->
<html lang="pt-BR">  <!-- Brazilian Portuguese -->
```

4. **Set dir for RTL languages:**
```html
<!-- Correct: Arabic content with RTL direction -->
<html lang="ar" dir="rtl">
```

5. **Use dir="auto" for user-generated content:**
```html
<!-- Correct: Automatic direction detection -->
<textarea dir="auto" placeholder="Enter comment..."></textarea>
```

### Avoid This ✗

1. **Don't omit lang attribute:**
```html
<!-- WRONG: No language declaration -->
<!DOCTYPE html>
<html>

<!-- CORRECT: Always declare language -->
<!DOCTYPE html>
<html lang="en">
```

2. **Don't use incorrect language codes:**
```html
<!-- WRONG: Invalid language code -->
<html lang="english">

<!-- CORRECT: Use ISO 639-1 two-letter codes -->
<html lang="en">
```

3. **Don't forget to mark embedded language changes:**
```html
<!-- WRONG: No lang attribute for French -->
<p>The word "bonjour" means hello in French.</p>

<!-- CORRECT: Mark language change -->
<p>The word <span lang="fr">bonjour</span> means hello in French.</p>
```

4. **Don't use CSS for text direction:**
```html
<!-- WRONG: Using CSS instead of dir attribute -->
<p style="direction: rtl;">النص العربي</p>

<!-- CORRECT: Use dir attribute -->
<p lang="ar" dir="rtl">النص العربي</p>
```

5. **Don't assume LTR is default everywhere:**
```html
<!-- WRONG: Embedding English in Arabic page without dir -->
<html lang="ar" dir="rtl">
  <p>محتوى عربي</p>
  <p>English content</p>  <!-- Will display RTL! -->
</html>

<!-- CORRECT: Specify LTR for embedded English -->
<html lang="ar" dir="rtl">
  <p>محتوى عربي</p>
  <p lang="en" dir="ltr">English content</p>
</html>
```

## Related Topics

### Prerequisites
- [HTML Syntax](../01-fundamentals/syntax.md) - Attributes and element structure
- [Character Encoding](../01-fundamentals/character-encoding.md) - UTF-8 for international characters
- [Document Structure](../01-fundamentals/document-structure.md) - html element and attributes

### Related Topics
- [Global Attributes](../09-global-attributes/lang-dir.md) - Complete lang and dir reference
- [Accessibility Overview](../13-accessibility/accessibility-overview.md) - International accessibility
- [Meta Tags](../08-metadata-seo/meta-tags.md) - Internationalization metadata

### Next Steps
- [Anchor Links](../03-links-navigation/anchor-links.md) - Creating hyperlinks
- [Semantic HTML5](../07-semantic-html5/semantic-overview.md) - Semantic markup principles
- [Accessibility Best Practices](../13-accessibility/accessibility-overview.md) - Creating accessible content

## Practice Exercise

### Requirements
Create a **"Multilingual Language Learning Page"** that demonstrates proper use of lang and dir attributes. Your HTML document should include:

1. A main heading and introduction in English
2. At least 3 sections, each featuring:
   - Content in a different language (French, Spanish, German, Arabic, Hebrew, or Japanese)
   - Proper `lang` attributes for all language changes
   - Proper `dir` attributes for RTL languages (if using Arabic/Hebrew)
3. At least one bidirectional section mixing English with RTL language
4. A form input with `dir="auto"` for user-generated content
5. CSS styling that:
   - Respects text direction (padding/margins adjust for RTL)
   - Quotes styled appropriately per language
   - Code examples maintain LTR direction regardless of page direction

**Accessibility Requirements:**
- Set `lang` on `<html>` element (WCAG 3.1.1 Level A)
- Mark all inline language changes with `lang` (WCAG 3.1.2 Level AA)
- Use `dir="rtl"` for Arabic or Hebrew content
- Provide translations or context for non-English phrases

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Multilingual Language Learning</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.6;
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
  <title>Common Greetings Around the World</title>
  <style>
    body {
      font-family: Arial, Helvetica, sans-serif;
      max-width: 900px;
      margin: 0 auto;
      padding: 20px;
      line-height: 1.8;
      background-color: #f5f5f5;
    }
    h1 {
      color: #2c3e50;
      text-align: center;
      border-bottom: 3px solid #3498db;
      padding-bottom: 0.5em;
    }
    h2 {
      color: #34495e;
      margin-top: 2em;
    }
    .language-section {
      background-color: white;
      padding: 1.5em;
      margin: 1.5em 0;
      border-radius: 8px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .language-section[dir="rtl"] {
      border-right: 5px solid #9b59b6;
      border-left: none;
    }
    .language-section[dir="ltr"] {
      border-left: 5px solid #3498db;
    }
    .phrase {
      font-size: 1.3em;
      font-weight: bold;
      color: #2980b9;
      margin: 0.5em 0;
    }
    .translation {
      font-style: italic;
      color: #7f8c8d;
    }
    .pronunciation {
      background-color: #ecf0f1;
      padding: 0.5em;
      border-radius: 4px;
      font-family: 'Courier New', monospace;
      margin: 0.5em 0;
    }
    [lang="fr"] {
      quotes: "« " " »";
    }
    [lang="de"] {
      quotes: "„" """;
    }
    [lang="ar"], [lang="he"] {
      font-size: 1.1em;
    }
    code {
      direction: ltr !important;
      display: inline-block;
      font-family: 'Consolas', monospace;
      background-color: #2d2d2d;
      color: #f8f8f2;
      padding: 2px 6px;
      border-radius: 3px;
    }
    .comment-form {
      background-color: white;
      padding: 1.5em;
      border-radius: 8px;
      margin-top: 2em;
    }
    textarea {
      width: 100%;
      padding: 0.75em;
      border: 1px solid #bdc3c7;
      border-radius: 4px;
      font-size: 1em;
      font-family: Arial, sans-serif;
      resize: vertical;
    }
    .info-box {
      background-color: #d1ecf1;
      border-left: 4px solid #0c5460;
      padding: 1em;
      margin: 1.5em 0;
    }
    .info-box[dir="rtl"] {
      border-left: none;
      border-right: 4px solid #0c5460;
    }
  </style>
</head>
<body>
  <article>
    <h1>Common Greetings Around the World</h1>

    <p>
      Learning to greet people in their native language shows respect and
      opens doors to meaningful connections. Here are some common greetings
      from different languages and cultures.
    </p>

    <section class="language-section" dir="ltr">
      <h2 lang="fr">French (Français)</h2>
      <p class="phrase" lang="fr">Bonjour!</p>
      <p class="translation">Translation: Good day / Hello</p>
      <p class="pronunciation">Pronunciation: bon-ZHOOR</p>
      <p>
        In French culture, <span lang="fr">bonjour</span> is used until
        late afternoon, when it's replaced by <span lang="fr">bonsoir</span>
        (good evening). The French take greetings seriously—entering a shop
        without saying <span lang="fr">bonjour</span> is considered rude!
      </p>
      <p>
        To mark French text in HTML, use:
        <code>&lt;span lang="fr"&gt;bonjour&lt;/span&gt;</code>
      </p>
    </section>

    <section class="language-section" dir="ltr">
      <h2 lang="es">Spanish (Español)</h2>
      <p class="phrase" lang="es">¡Hola!</p>
      <p class="translation">Translation: Hello</p>
      <p class="pronunciation">Pronunciation: OH-lah</p>
      <p>
        <span lang="es">Hola</span> is the universal greeting in Spanish,
        used at any time of day. For a more formal greeting, you might say
        <span lang="es">Buenos días</span> (good morning),
        <span lang="es">Buenas tardes</span> (good afternoon), or
        <span lang="es">Buenas noches</span> (good evening/night).
      </p>
      <p>
        Spanish from Spain uses <code lang="es">es-ES</code>, while
        Mexican Spanish uses <code lang="es">es-MX</code>.
      </p>
    </section>

    <section class="language-section" dir="rtl" lang="ar">
      <h2>Arabic (العربية)</h2>
      <p class="phrase">السلام عليكم</p>
      <p class="translation" dir="ltr">Translation: Peace be upon you</p>
      <p class="pronunciation" dir="ltr">Pronunciation: as-sa-LAM a-LAY-kum</p>
      <p>
        السلام عليكم هي التحية الإسلامية التقليدية المستخدمة في جميع
        أنحاء العالم العربي. الرد المناسب هو: وعليكم السلام
        (wa a-LAY-kum as-sa-LAM).
      </p>

      <div class="info-box" dir="rtl">
        <p>
          <strong>ملاحظة:</strong> النص العربي يتطلب استخدام التوجيه من
          اليمين إلى اليسار. في HTML، نستخدم:
        </p>
        <p dir="ltr">
          <code>&lt;p lang="ar" dir="rtl"&gt;النص العربي&lt;/p&gt;</code>
        </p>
      </div>
    </section>

    <section class="language-section" dir="ltr">
      <h2 lang="ja">Japanese (日本語)</h2>
      <p class="phrase" lang="ja">こんにちは</p>
      <p class="translation">Translation: Hello / Good afternoon</p>
      <p class="pronunciation">Pronunciation: kon-nee-chee-WAH</p>
      <p>
        <span lang="ja">こんにちは</span> (konnichiwa) is used during the
        daytime. In the morning, Japanese speakers say
        <span lang="ja">おはようございます</span> (ohayou gozaimasu),
        and in the evening, <span lang="ja">こんばんは</span> (konbanwa).
      </p>
      <p>
        Japanese uses three writing systems: hiragana (ひらがな), katakana (カタカナ),
        and kanji (漢字). The HTML language code is:
        <code lang="ja">ja-JP</code>
      </p>
    </section>

    <section class="language-section" dir="rtl" lang="he">
      <h2>Hebrew (עברית)</h2>
      <p class="phrase">שלום</p>
      <p class="translation" dir="ltr">Translation: Hello / Peace</p>
      <p class="pronunciation" dir="ltr">Pronunciation: sha-LOHM</p>
      <p>
        שלום היא המילה הנפוצה ביותר לאמירת "שלום" בעברית.
        המילה שלום משמעה גם "שלום" (peace) וגם "להתראות" (goodbye).
      </p>

      <div class="info-box" dir="rtl">
        <p>
          <strong>טיפ:</strong> עברית, כמו ערבית, נכתבת מימין לשמאל.
          בHTML משתמשים ב:
        </p>
        <p dir="ltr">
          <code>&lt;html lang="he" dir="rtl"&gt;</code>
        </p>
      </div>

      <p dir="ltr" lang="en">
        <strong>Bidirectional Note (English):</strong> Hebrew text flows
        right-to-left, but code examples and English words maintain
        left-to-right direction. This is called bidirectional (bidi) text.
      </p>
    </section>

    <section class="language-section" dir="ltr">
      <h2 lang="de">German (Deutsch)</h2>
      <p class="phrase" lang="de">Guten Tag!</p>
      <p class="translation">Translation: Good day</p>
      <p class="pronunciation">Pronunciation: GOO-ten TAHG</p>
      <p>
        <span lang="de">Guten Tag</span> is a formal greeting used during
        the day. Informally, Germans say <span lang="de">Hallo</span> or
        <span lang="de">Hi</span>. In southern Germany and Austria, you'll
        often hear <span lang="de">Grüß Gott</span> (greet God).
      </p>
      <p>
        German uses regional variants: <code lang="de">de-DE</code> (Germany),
        <code lang="de">de-AT</code> (Austria), <code lang="de">de-CH</code>
        (Switzerland).
      </p>
    </section>

    <section class="comment-form">
      <h2>Share Your Greeting</h2>
      <p>
        Do you know a greeting in another language? Share it below!
        Our form automatically detects text direction.
      </p>

      <form>
        <label for="language">Language:</label><br>
        <input type="text" id="language" name="language" dir="auto"
               placeholder="e.g., Swahili, Hindi, Russian" required><br><br>

        <label for="greeting">Greeting in that language:</label><br>
        <textarea id="greeting" name="greeting" rows="3" dir="auto"
                  placeholder="Enter greeting text here..." required></textarea><br><br>

        <label for="translation">English translation:</label><br>
        <input type="text" id="translation" name="translation"
               placeholder="What does it mean?" required><br><br>

        <button type="submit">Submit Greeting</button>
      </form>

      <p>
        <small>
          <strong>Note:</strong> The form uses <code>dir="auto"</code> to
          automatically detect text direction based on your input. Try typing
          in Arabic (مرحبا) or Hebrew (שלום) to see it work!
        </small>
      </p>
    </section>

    <footer>
      <p>
        <small>
          Learn more about language codes at the
          <a href="https://www.w3.org/International/questions/qa-choosing-language-tags">
          W3C Internationalization documentation</a>.
        </small>
      </p>
    </footer>
  </article>
</body>
</html>
```

**Key Features of Solution:**
- Sets `lang="en"` on `<html>` element (WCAG 3.1.1 Level A)
- Marks all inline language changes with `lang` attribute (WCAG 3.1.2 Level AA)
- Includes 6 different languages: English, French, Spanish, Arabic, Japanese, Hebrew, German
- Uses `dir="rtl"` for Arabic and Hebrew sections
- Demonstrates bidirectional text mixing English and Hebrew/Arabic
- Form inputs use `dir="auto"` for automatic direction detection
- CSS respects text direction (border-left for LTR, border-right for RTL)
- Code examples maintain LTR direction with `direction: ltr !important`
- Language-specific quote styling (French guillemets, German quotes)
- Provides translations and pronunciations for all phrases
- Shows proper HTML code examples for implementing lang/dir attributes
- Accessible structure with semantic headings and labels

---

## Navigation

- **Previous:** [Abbreviations](abbreviations.md)
- **Next:** [Anchor Links](../03-links-navigation/anchor-links.md)
- **Up:** [Text Content](README.md)
- **Home:** [HTML5 Complete Learning Documentation](../README.md)

---

**Document Information:**
- **Created:** 2025-11-17
- **Category:** Text Content
- **Difficulty:** Intermediate
- **Author:** Joshua P. Hickman
- **Copyright:** © 2025 Joshua P. Hickman. All rights reserved.
- **Development:** Created with assistance from Claude Code
