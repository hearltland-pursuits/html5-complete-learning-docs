---
title: Textarea & File Inputs
category: Forms & Input
order: 7
---

# Textarea & File Inputs

> **Quick Summary:** The `<textarea>` element handles multi-line text input (comments, descriptions, messages), while `<input type="file">` enables file uploads with support for multiple files, file type restrictions, and drag-and-drop functionality.

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

While `<input>` handles single-line text, **`<textarea>`** is designed for multi-line text entry—perfect for comments, messages, descriptions, code snippets, and long-form content. Unlike inputs, textareas are resizable (by default) and preserve line breaks and formatting.

The **`<input type="file">`** element enables file uploads from the user's device. HTML5 enhanced it with `multiple` (upload several files at once), `accept` (restrict file types like images or PDFs), and native drag-and-drop support. Combined with the `<form enctype="multipart/form-data">` attribute, file inputs power profile picture uploads, document submissions, and attachment features.

Both elements are essential for modern web applications: textarea for user-generated content and file input for media/document handling.

**Key Concept:** Use `<textarea>` for multi-line text (descriptions, comments). Use `<input type="file">` for file uploads (images, documents). Both require proper validation—textarea for max length, file input for size and type.

---

## Basic Syntax

```html
<!-- Textarea for multi-line text -->
<label for="message">Message:</label>
<textarea id="message" name="message" rows="5" cols="40"></textarea>

<!-- File input for uploads -->
<label for="avatar">Profile Picture:</label>
<input type="file" id="avatar" name="avatar" accept="image/*">
```

### Textarea Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `name` | Text string | Form field name |
| `id` | Text string | Associates with label |
| `rows` | Number | Visible lines (height) |
| `cols` | Number | Visible columns (width) |
| `maxlength` | Number | Maximum character limit |
| `minlength` | Number | Minimum character requirement |
| `placeholder` | Text | Hint text (disappears on input) |
| `required` | Boolean | Makes field mandatory |
| `readonly` | Boolean | Prevents editing |
| `disabled` | Boolean | Disables textarea |
| `wrap` | `soft`, `hard` | Text wrapping behavior |

### File Input Attributes

| Attribute | Values | Description |
|-----------|--------|-------------|
| `accept` | MIME types, file extensions | Restricts file types (e.g., `.pdf`, `image/*`) |
| `multiple` | Boolean | Allows selecting multiple files |
| `required` | Boolean | Makes file upload mandatory |
| `capture` | `user`, `environment` | Mobile: Opens camera directly |

---

## Examples

### Example 1: Contact Form with Message Textarea

**Scenario:** Contact form with multi-line message field.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Form</title>
</head>
<body>
  <form action="/contact" method="POST">
    <label for="name">Name: *</label>
    <input type="text" id="name" name="name" required>

    <label for="email">Email: *</label>
    <input type="email" id="email" name="email" required>

    <label for="message">Message: *</label>
    <textarea
      id="message"
      name="message"
      rows="8"
      cols="50"
      minlength="10"
      maxlength="1000"
      placeholder="Tell us what you're thinking..."
      required
      aria-describedby="message-hint"></textarea>

    <small id="message-hint">10-1000 characters. Line breaks preserved.</small>

    <button type="submit">Send Message</button>
  </form>
</body>
</html>
```

**Result:** 8-row textarea for messages. Validates 10-1000 characters. Placeholder disappears when typing. Line breaks are preserved when submitted.

---

### Example 2: Profile Picture Upload with Image Restriction

**Scenario:** User profile form with avatar upload (images only).

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Profile Upload</title>
</head>
<body>
  <form action="/profile" method="POST" enctype="multipart/form-data">
    <label for="username">Username: *</label>
    <input type="text" id="username" name="username" required>

    <label for="profile-pic">Profile Picture (JPG, PNG, max 5MB): *</label>
    <input
      type="file"
      id="profile-pic"
      name="avatar"
      accept="image/jpeg, image/png, image/gif"
      required
      aria-describedby="pic-hint">

    <small id="pic-hint">Accepted formats: JPEG, PNG, GIF. Maximum size: 5MB.</small>

    <button type="submit">Upload Profile</button>
  </form>
</body>
</html>
```

**Result:** File picker restricted to JPEG, PNG, GIF images. Form uses `enctype="multipart/form-data"` (required for file uploads). Browser shows only image files in picker.

**Note:** Client-side `accept` is a UX convenience but not security. Always validate file type and size on server.

---

### Example 3: Multiple Document Upload

**Scenario:** Job application form allowing multiple resume/portfolio files.

**HTML:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Job Application</title>
</head>
<body>
  <form action="/apply" method="POST" enctype="multipart/form-data">
    <label for="applicant-name">Full Name: *</label>
    <input type="text" id="applicant-name" name="name" required>

    <label for="cover-letter">Cover Letter: *</label>
    <textarea
      id="cover-letter"
      name="cover_letter"
      rows="10"
      cols="60"
      maxlength="2000"
      required
      placeholder="Introduce yourself and explain why you're a great fit..."></textarea>

    <label for="documents">Upload Resume & Portfolio (PDF, DOC, DOCX): *</label>
    <input
      type="file"
      id="documents"
      name="documents[]"
      accept=".pdf, .doc, .docx"
      multiple
      required
      aria-describedby="doc-hint">

    <small id="doc-hint">Select multiple files using Ctrl/Cmd+click. Max 10MB per file.</small>

    <button type="submit">Submit Application</button>
  </form>
</body>
</html>
```

**Result:** Users can select multiple files at once. `accept=".pdf, .doc, .docx"` shows only document files. Server receives array of files via `documents[]`.

---

## Common Use Cases

### Use Case 1: Blog Post Editor
**When:** CMS where users write blog posts or articles.
**How:**
```html
<label for="post-content">Post Content:</label>
<textarea
  id="post-content"
  name="content"
  rows="20"
  cols="80"
  maxlength="50000"
  required
  wrap="soft"></textarea>
```
**Why:** Large textarea for long-form content. `wrap="soft"` preserves line breaks visually but doesn't insert hard returns.

---

### Use Case 2: Mobile Camera Upload
**When:** Mobile app where users upload photos directly from camera.
**How:**
```html
<label for="photo">Take Photo:</label>
<input
  type="file"
  id="photo"
  name="photo"
  accept="image/*"
  capture="environment"
  required>
```
**Why:** `capture="environment"` opens rear camera on mobile devices. `accept="image/*"` ensures only images.

---

### Use Case 3: Code Snippet Submission
**When:** Developer platform where users submit code examples.
**How:**
```html
<label for="code">Code Snippet:</label>
<textarea
  id="code"
  name="code_snippet"
  rows="15"
  cols="70"
  spellcheck="false"
  autocomplete="off"
  wrap="off"
  placeholder="Paste your code here..."
  required></textarea>
```
**Why:** `spellcheck="false"` prevents red underlines in code. `wrap="off"` disables auto line wrapping. `autocomplete="off"` prevents browser suggestions.

---

## Browser Support

| Browser | Version | Support Level | Notes |
|---------|---------|---------------|-------|
| Chrome  | All     | Full Support  | Full textarea and file input support |
| Firefox | All     | Full Support  | Full support including `multiple`, `accept` |
| Safari  | All     | Full Support  | Full support (mobile `capture` since iOS 6) |
| Edge    | All     | Full Support  | Full support (all versions) |
| IE 11   | 11      | Partial Support | Textarea works; file input `multiple` supported |

**Fallback Strategy:**
```html
<!-- No fallback needed - universal support -->
<!-- For multiple file upload in IE9 and older, use JavaScript polyfill -->
```

**Can I Use Links:**
- [Textarea Element](https://caniuse.com/textarea) (universal)
- [File Input Multiple](https://caniuse.com/input-file-multiple)

---

## Accessibility Considerations

### WCAG Compliance

**Level A Requirements:**
- Textareas and file inputs must have associated `<label>` elements
- Keyboard navigation must work (Tab, arrow keys for textarea)
- Required fields must be clearly indicated

**Level AA Requirements:**
- Labels must have sufficient color contrast
- Character limit hints should be programmatically associated
- Error messages must be clear and associated with inputs

### Screen Reader Support

```html
<!-- Accessible textarea -->
<label for="feedback">
  Feedback <span aria-label="required">*</span>
</label>
<textarea
  id="feedback"
  name="feedback"
  rows="6"
  maxlength="500"
  required
  aria-required="true"
  aria-describedby="feedback-hint"></textarea>

<small id="feedback-hint">Maximum 500 characters. <span id="char-count">0/500</span></small>

<!-- Accessible file input -->
<label for="attachment">
  Attachment <span aria-label="required">*</span>
</label>
<input
  type="file"
  id="attachment"
  name="file"
  accept=".pdf"
  required
  aria-required="true"
  aria-describedby="file-hint">

<small id="file-hint">PDF files only, max 5MB.</small>
```

**Key Points:**
- `aria-required="true"` announces required fields
- `aria-describedby` links character limits and file restrictions
- Provide clear file type/size instructions

### Keyboard Navigation

**Textarea:**
- **Tab:** Moves focus to/from textarea
- **Enter:** Inserts new line (doesn't submit form)
- **Arrow Keys:** Moves cursor within text
- **Ctrl/Cmd + A:** Selects all text

**File Input:**
- **Tab:** Moves focus to file input
- **Spacebar/Enter:** Opens file picker dialog
- **Escape:** Closes file picker

---

## Best Practices

### Do This

1. **Set Appropriate Rows and Cols**
   ```html
   <!-- GOOD: Visible size matches expected content -->
   <textarea rows="10" cols="60" name="bio"></textarea>
   ```
   **Why:** Users see most of their content without scrolling. `rows` sets height, `cols` sets width.

2. **Use maxlength for Textareas**
   ```html
   <!-- GOOD: Prevents database overflow -->
   <textarea maxlength="1000" name="comment"></textarea>
   <small>Maximum 1000 characters</small>
   ```
   **Why:** Validates length client-side. Always validate server-side too.

3. **Restrict File Types with Accept**
   ```html
   <!-- GOOD: Guides user to correct file type -->
   <input type="file" accept="image/*" name="photo">
   ```
   **Why:** Shows only relevant files in picker. Improves UX.

---

### Avoid This

1. **Using Placeholder Instead of Label**
   ```html
   <!-- WRONG: No label, only placeholder -->
   <textarea placeholder="Enter message"></textarea>
   ```
   **Why Not:** Placeholder disappears when typing. Screen readers may not announce it. Fails WCAG.
   **Instead:**
   ```html
   <label for="msg">Message:</label>
   <textarea id="msg" placeholder="Optional hint..."></textarea>
   ```

2. **Forgetting enctype for File Uploads**
   ```html
   <!-- WRONG: File upload won't work -->
   <form action="/upload" method="POST">
     <input type="file" name="document">
   </form>
   ```
   **Why Not:** Without `enctype="multipart/form-data"`, file data isn't sent. Most common file upload mistake.
   **Instead:**
   ```html
   <form action="/upload" method="POST" enctype="multipart/form-data">
     <input type="file" name="document">
   </form>
   ```

3. **No File Type/Size Guidance**
   ```html
   <!-- WRONG: User doesn't know what files are allowed -->
   <input type="file" name="upload">
   ```
   **Why Not:** Users waste time uploading wrong file types or oversized files.
   **Instead:**
   ```html
   <label for="doc">Document (PDF, max 5MB):</label>
   <input type="file" id="doc" accept=".pdf" aria-describedby="doc-hint">
   <small id="doc-hint">PDF files only. Maximum size: 5MB.</small>
   ```

---

## Related Topics

**Prerequisites:**
- [Form Element](form-element.md) - Form structure and enctype
- [Text Inputs](text-inputs.md) - Basic input concepts

**Related Concepts:**
- [Form Validation](form-validation.md) - Validating text length and file types
- [Form Attributes](form-attributes.md) - Additional HTML5 attributes
- [Form Accessibility](form-accessibility.md) - Accessible forms

**Next Steps:**
- [Form Validation](form-validation.md) - HTML5 validation
- [Form Buttons](form-buttons.md) - Submit and reset buttons

**External Resources:**
- [MDN - Textarea Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)
- [MDN - File Input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file)
- [W3Schools - HTML Textarea](https://www.w3schools.com/tags/tag_textarea.asp)

---

## Practice Exercise

### Challenge: Build a Support Ticket Form

**Objective:** Create a support ticket form with textarea for issue description and file upload for screenshots/attachments.

**Requirements:**
- [ ] Subject line (text input, max 100 chars)
- [ ] Issue description (textarea, 20-2000 chars)
- [ ] Attachment upload (images and PDFs, multiple files)
- [ ] Show character count for description
- [ ] Bonus: Add priority selector (dropdown: Low, Medium, High)

---

### Starter Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Support Ticket</title>
</head>
<body>
  <h1>Submit Support Ticket</h1>
  <form action="/support" method="POST" enctype="multipart/form-data">
    <!-- Add your form fields here -->
    <button type="submit">Submit Ticket</button>
  </form>
</body>
</html>
```

---

### Solution

<details>
<summary>Click to reveal solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Support Ticket</title>
  <style>
    body { font-family: Arial, sans-serif; max-width: 700px; margin: 2rem auto; padding: 0 1rem; }
    label { display: block; margin-top: 1.5rem; font-weight: bold; }
    input, textarea, select { width: 100%; padding: 0.5rem; margin-top: 0.5rem; }
    textarea { resize: vertical; font-family: Arial, sans-serif; }
    small { display: block; color: #666; margin-top: 0.25rem; }
    #char-count { font-weight: bold; color: #0066cc; }
    button { margin-top: 2rem; padding: 0.75rem 1.5rem; }
  </style>
</head>
<body>
  <h1>Submit Support Ticket</h1>
  <form action="/support" method="POST" enctype="multipart/form-data">
    <!-- Subject -->
    <label for="subject">Subject: <span aria-label="required">*</span></label>
    <input
      type="text"
      id="subject"
      name="subject"
      maxlength="100"
      required
      placeholder="Brief description of issue">

    <!-- Issue description -->
    <label for="description">Issue Description: <span aria-label="required">*</span></label>
    <textarea
      id="description"
      name="description"
      rows="10"
      minlength="20"
      maxlength="2000"
      required
      aria-describedby="desc-hint"
      placeholder="Describe the issue in detail..."></textarea>

    <small id="desc-hint">
      Minimum 20 characters, maximum 2000.
      <span id="char-count">0/2000</span>
    </small>

    <!-- File attachments -->
    <label for="attachments">Attachments (optional):</label>
    <input
      type="file"
      id="attachments"
      name="attachments[]"
      accept="image/*, .pdf"
      multiple
      aria-describedby="file-hint">

    <small id="file-hint">
      Upload screenshots or documents (PNG, JPG, PDF). Multiple files allowed.
    </small>

    <!-- Bonus: Priority -->
    <label for="priority">Priority: <span aria-label="required">*</span></label>
    <select id="priority" name="priority" required>
      <option value="">--Select priority--</option>
      <option value="low">Low</option>
      <option value="medium" selected>Medium</option>
      <option value="high">High</option>
      <option value="critical">Critical</option>
    </select>

    <button type="submit">Submit Ticket</button>
  </form>

  <script>
    // Character counter
    const textarea = document.getElementById('description');
    const charCount = document.getElementById('char-count');

    textarea.addEventListener('input', function() {
      const length = this.value.length;
      charCount.textContent = `${length}/2000`;

      if (length > 2000) {
        charCount.style.color = '#cc0000';
      } else if (length < 20) {
        charCount.style.color = '#cc6600';
      } else {
        charCount.style.color = '#006600';
      }
    });
  </script>
</body>
</html>
```

**Explanation:** This support ticket form uses a text input for subject (max 100 chars), textarea for detailed description (20-2000 chars with live counter), file upload for multiple attachments (images/PDFs), and priority selector. JavaScript tracks character count and changes color based on validation status. Form uses `enctype="multipart/form-data"` for file uploads.

</details>

---

### Expected Result

A functional support ticket form with subject input, resizable description textarea showing live character count, multiple file upload for screenshots/docs, and priority dropdown. Character counter changes color (red if over limit, orange if under minimum, green if valid).

**Key Learnings:**
- Using textarea for multi-line input with length validation
- File upload with multiple files and type restrictions
- Importance of `enctype="multipart/form-data"` for file uploads
- Enhancing UX with JavaScript character counter
- Providing clear guidance for file types and sizes

---

## Navigation

**Previous:** [Select & Datalist](select-datalist.md)
**Next:** [Form Validation](form-validation.md)
**Up:** [Back to Forms & Input](.)
**Home:** [Documentation Home](../README.md)

---

**Last Updated:** November 17, 2025
**Category:** Forms & Input
**Difficulty:** Intermediate
**Author:** Joshua P. Hickman | Created with assistance from Claude Code
