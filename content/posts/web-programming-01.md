+++
date = '2025-05-22T14:19:11+09:00'
title = '[Web Programming] [01] Frontend - HTML Part 01'
description = "Learn about HTML5"
categories = ["Information Technology/Application Software Development/Web Programming"]
tags = ["Frontend"]
slug = "html-part-01"
math = true
draft = false
+++

# Chapter 01. Frontend – HTML (Part 01)

> **Outline:** Introduction to the foundational language of the web. This chapter covers the structure, syntax, and semantics of HTML, the language used to build the backbone of every website. In this part, we describe core concepts, basic structure, and commonly used tags of HTML5.

---

## Contents

- [1.1. What is HTML](#section-11-what-is-html)
- [1.2. What is a Markup Language](#section-12-what-is-a-markup-language)
- [1.3. Core Concepts of HTML](#section-13-core-concepts-of-html)
- [1.4. Basic HTML Document Structure](#section-14-basic-html-document-structure)
- [1.5. Common HTML Tags](#section-15-common-html-tags)
- [1.6. Forms and Input Elements]({{< relref "posts/web-programming-02.md" >}})
- [1.7. Semantic HTML Tags]({{< relref "posts/web-programming-02.md" >}})
- [1.8. HTML Entities & Special Characters]({{< relref "posts/web-programming-02.md" >}})
- [1.9. HTML Accessibility (ARIA Basics)]({{< relref "posts/web-programming-02.md" >}})
- [1.10. SEO and HTML Structure *(Optional)*]({{< relref "posts/web-programming-02.md" >}})

---

## Section 1.1. What is HTML?

### 1. Definition

**HTML (HyperText Markup Language)** is the standard **markup language** used to define the **structure** of web pages.

> Every website you see in a browser starts with HTML.

---

### 2. Not a Programming Language

- HTML is **not** a programming language; it's a **markup language**.
- It doesn't have logic features like loops or conditionals.
- Its main purpose is to **describe content structure and meaning**, not behavior.

---

### 3. Key Features

| Feature            | Description                                         |
|--------------------|-----------------------------------------------------|
| **Structure**       | Defines the layout of the page (header, body, etc.)|
| **Tag-based Syntax**| Uses tags like `<p>`, `<h1>`, `<div>`, etc.         |
| **Hypertext Support**| Enables linking between pages using `<a>`          |
| **Human/Machine Readable**| Easy for browsers and developers to interpret  |

---

### 4. Role of HTML

- Expresses **content structure and meaning** (headings, paragraphs, lists, images, links)
- Acts as the **foundation for CSS and JavaScript**
- Important for **web accessibility** and **SEO (search engine optimization)**

---

### 5. Basic Example

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example Page</title>
  </head>
  <body>
    <h1>Hello, world!</h1>
    <p>This is example page for HTML.</p>
  </body>
</html>
```

---

## Section 1.2. What is a Markup Language?

### 1. Definition

A **markup language** is a system for **annotating text** so that the structure and semantics of the content can be understood and interpreted by computers.

> It tells the browser what each piece of content means, not just how it looks.

---

### 2. Purpose of a Markup Language

- **Structure**: Defines document layout and sections
- **Semantics**: Gives meaning to different parts of content
- **Foundation for Rendering**: Provides base instructions for how the content should be displayed

---

### 3. Example in HTML

```html
<h1>My Blog</h1>
<p>Welcome to my blog!</p>
```
> `<h1>`: Indicates a top-level heading
> `<p>`: Defines a paragraph
> This is how tags are used to “mark up” content with meaning.

---

### 4. Markup Language vs. Programming Language
|Feature              |Markup Language            |Programming Language    |
|---------------------|---------------------------|------------------------|
|Main Purpose         |Define structure & meaning |Control logic & behavior|
|Examples             |HTML, XML, Markdown        |Python, JavaScript, C   |
|Logic or Flow Control|Not possible               |Fully supported         |

---

### 5. Other Common Markup Languages
- HTML – Builds structure of web pages
- XML – Represents structured data
- Markdown – Lightweight syntax for formatting text
- LaTeX – Used for typesetting scientific documents

---

## Section 1.3. Core Concepts of HTML

### 1. Tag

- A **tag** is a keyword enclosed in angle brackets (`< >`) that defines the type or role of content.
- Most tags come in pairs: an **opening tag** and a **closing tag**.

```html
<p>Hello, world!</p>
```

- `<p>` is the opening tag, and `</p>` is the closing tag.
- Some tags are self-closing, like `<br>` or `<img>`. These do not require a closing tag.

---

### 2. Attribute

- An **attribute** provides additional information about an element.
- It appears inside the opening tag and uses the format `name="value"`.

```html
<img src="logo.png" alt="Company Logo">
```

- `src`: specifies the image source path.
- `alt`: provides alternative text if the image fails to load.

---

### 3. Content

- **Content** is the part between the opening and closing tags of an element.
- It can be plain text or **nested HTML elements**, and is what users actually see in the browser.

```html
<h1>Welcome</h1>
```

- `Welcome`: is the content of the `<h1>` element.

---

### 4. Element

- An **element** consists of the entire HTML unit:
  - Opening tag
  - Attributes (optional)
  - Content (optional)
  - Closing tag

```html
<tagname attribute1 = "value1" attribute2 = "value2">content</tagname>
```

```html
<a href="https://example.com">Visit</a>
```

- This is a full `<a>` element:
  - `<a>` is the opening tag
  - `href="https://example.com"` is the attribute
  - `Visit` is the content
  - `</a>` is the closing tag

---

### Summary Table

| Concept   | Description                                 | Example                                     |
|-----------|---------------------------------------------|---------------------------------------------|
| Tag       | Symbol that defines the element type        | `<p>`, `</p>`, `<img>`                      |
| Attribute | Key-value pair that adds info to a tag      | `href="..."`, `src="..."`, `alt="..."`      |
| Content   | What is displayed between tags              | `Hello`, `Link`, `Welcome`                  |
| Element   | Full HTML unit including tag(s) and content | `<p>Hello</p>`, `<a href="#">Link</a>`      |

---

## Section 1.4. Basic HTML Document Structure

### 1. Overview

Every HTML page starts with a **standard document structure** that browsers can recognize and render properly.  
This structure includes essential tags like `<!DOCTYPE>`, `<html>`, `<head>`, and `<body>`.

---

### 2. Basic Structure Template

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Page Title</title>
  </head>
  <body>
    <h1>Hello, world!</h1>
    <p>This is a paragraph.</p>
  </body>
</html>
```

---

### 3. Explanation of Each Part

| Part               | Purpose                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `<!DOCTYPE html>`  | Declares the document as HTML5                                          |
| `<html>`           | Root element of the page                                                |
| `<head>`           | Metadata (not visible): title, charset, styles, scripts, etc.           |
| `<body>`           | Visible content shown in the browser                                    |
| `<title>`          | Page title shown in the browser tab                                     |
| `<meta charset="">`| Declares character encoding (e.g., UTF-8 for Unicode support)           |

---

### 4. Notes

- Only **one `<html>`, `<head>`, and `<body>`** tag should appear per document.
- The `lang` attribute in `<html>` improves accessibility and SEO.
- Without `<!DOCTYPE html>`, browsers may enter **quirks mode** (inconsistent rendering).
- **Quirks Mode** is a non-standard rendering mode. In this mode, the browser does **not follow modern HTML and CSS standards**.
- `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN""http://www.w3.org/TR/html4/loose.dtd">` declares the document as HTML 4.01, instead of HTML5.

---

## Section 1.5. Common HTML Tags

### 1. Text Tags

| Tag         | Description                                      | Example                                |
|-------------|--------------------------------------------------|----------------------------------------|
| `<h1>`~`<h6>` | Headings from largest (`<h1>`) to smallest (`<h6>`) | `<h2>Subheading</h2>`                  |
| `<p>`       | Paragraph (block of text)                        | `<p>This is a paragraph.</p>`          |
| `<br>`      | Line break (new line)                            | `Line 1<br>Line 2`                      |
| `<hr>`      | Horizontal rule (divider line)                   | `<hr>`                                 |
| `<pre>`     | Preformatted text (preserves spaces, line breaks)| `<pre>  line 1\n  line 2</pre>`        |
| `<code>`    | Inline code snippet                              | `<code>print()</code>`                 |
| `<kbd>`     | Keyboard input                                   | `<kbd>Ctrl + C</kbd>`                  |
| `<samp>`    | Sample output (usually from a program)           | `<samp>404 Not Found</samp>`           |
| `<var>`     | Variable name (usually italic)                   | `<var>x</var> = 10`                    |

---

#### Notes

- Use heading tags (`<h1>`~`<h6>`) for structured titles and subtitles.
- `<pre>` keeps original spacing and line breaks—often used with `<code>`.
- `<kbd>`, `<samp>`, and `<var>` are useful in technical or educational content.

---

### 2. Formatting Tags

| Tag             | Description                                          | Example                              |
|------------------|------------------------------------------------------|--------------------------------------|
| `<strong>`       | Important/strong emphasis (usually bold)            | `<strong>Important</strong>`         |
| `<em>`           | Emphasized text (usually italic)                    | `<em>Note</em>`                      |
| `<mark>`         | Highlighted or marked text                          | `<mark>Highlight</mark>`            |
| `<small>`        | Smaller-sized text                                  | `<small>Footnote</small>`           |
| `<del>`          | Deleted text (strikethrough)                        | `<del>Removed</del>`                |
| `<ins>`          | Inserted text (usually underlined)                  | `<ins>New</ins>`                    |
| `<b>`            | Bold text without semantic meaning                  | `<b>Bold</b>`                        |
| `<i>`            | Italic text without semantic meaning                | `<i>Italic</i>`                      |
| `<u>`            | Underlined text                                     | `<u>Underline</u>`                   |
| `<sup>`          | Superscript (above baseline)                        | `x<sup>2</sup>` → x²                 |
| `<sub>`          | Subscript (below baseline)                          | `H<sub>2</sub>O` → H₂O               |
| `<abbr>`         | Abbreviation with tooltip                           | `<abbr title="HyperText Markup Language">HTML</abbr>` |
| `<cite>`         | Citation of a source (book, article, etc.)          | `<cite>The Republic</cite>`         |
| `<q>`            | Short inline quotation                              | `<q>This is quoted</q>`             |
| `<blockquote>`   | Block-level quotation                               | `<blockquote>This is a block quote</blockquote>` |

---

#### Notes

- `<strong>` and `<em>` carry semantic meaning and should be used for accessibility.
- `<b>` and `<i>` are purely visual and less preferred in semantic HTML.
- `<abbr>` is useful for accessibility and UX with screen readers.

---

### 3. List Tags

| Tag       | Description                            | Example                             |
|-----------|----------------------------------------|-------------------------------------|
| `<ul>`    | Unordered list (bulleted)              | `<ul><li>Item</li></ul>`            |
| `<ol>`    | Ordered list (numbered)                | `<ol><li>Item</li></ol>`            |
| `<li>`    | List item                              | `<li>Item</li>`                     |
| `<dl>`    | Description list (term + description)  | `<dl><dt>HTML</dt><dd>Markup</dd></dl>` |
| `<dt>`    | Term in description list               | `<dt>HTML</dt>`                     |
| `<dd>`    | Definition in description list         | `<dd>HyperText Markup Language</dd>` |

---

#### Common Attributes with List Tags

| Tag    | Attribute     | Description                                      | Example                                  |
|--------|---------------|--------------------------------------------------|------------------------------------------|
| `<ol>` | `type`        | Numbering style: `"1"`, `"a"`, `"A"`, `"i"`, `"I"` | `<ol type="A">` → A, B, C...             |
| `<ol>` | `start`       | Starting number for ordered list                | `<ol start="5">` → 5, 6, 7...             |
| `<li>` | `value`       | Custom numbering value (for `<ol>`)             | `<li value="10">Item</li>` → starts at 10|
| `<ul>` | `type` *(deprecated)* | Bullet style: `"disc"`, `"circle"`, `"square"` | `<ul type="circle">` *(not recommended)* |

---

#### Notes

- `type` and `start` are valid only on `<ol>`.
- `value` on `<li>` allows **non-sequential** numbering inside ordered lists.
- The `type` attribute on `<ul>` is deprecated in HTML5—use CSS instead:
  
```css
ul {
  list-style-type: square;
}
```

---

### 4. Link & Image Tags

| Tag       | Description                   | Example                                          |
|-----------|-------------------------------|--------------------------------------------------|
| `<a>`     | Hyperlink (anchor element)    | `<a href="https://example.com">Visit</a>`       |
| `<img>`   | Embeds an image               | `<img src="img.jpg" alt="description">`         |

---

#### Common Attributes for `<a>`

| Attribute   | Description                                              | Example                                       |
|-------------|----------------------------------------------------------|-----------------------------------------------|
| `href`      | Destination URL                                          | `<a href="https://example.com">Link</a>`      |
| `target`    | Where to open the link: `_blank`, `_self`, `_parent`, `_top` | `<a target="_blank">` → open in new tab |
| `title`     | Tooltip text on hover                                    | `<a title="Click to visit">`                  |
| `rel`       | Relationship between current and linked document         | `<a rel="noopener noreferrer">`               |
| `download`  | Suggests the browser to download rather than navigate    | `<a href="file.pdf" download>Download PDF</a>`|

---

#### Common Attributes for `<img>`

| Attribute   | Description                                               | Example                                          |
|-------------|-----------------------------------------------------------|--------------------------------------------------|
| `src`       | Path or URL to the image file                             | `<img src="logo.png">`                           |
| `alt`       | Alternative text if the image fails to load (required)    | `<img alt="Company logo">`                       |
| `title`     | Tooltip shown on hover                                    | `<img title="Hover text">`                       |
| `width`     | Image width in pixels or %                                | `<img width="200">`                              |
| `height`    | Image height in pixels or %                               | `<img height="150">`                             |
| `loading`   | Lazy loading setting: `"lazy"` or `"eager"`               | `<img loading="lazy">`                           |

---

#### Notes

- Always provide an `alt` attribute for images for accessibility and SEO.
- Use `target="_blank"` with `rel="noopener noreferrer"` for external links to enhance security.
- The `download` attribute in `<a>` helps with direct file downloads instead of opening them.

---

### 5. Table Tags

| Tag         | Description                          | Example                          |
|-------------|--------------------------------------|----------------------------------|
| `<table>`   | Table container                      | `<table>...</table>`            |
| `<tr>`      | Table row                            | `<tr>...</tr>`                  |
| `<th>`      | Table header cell                    | `<th>Header</th>`               |
| `<td>`      | Table data cell                      | `<td>Data</td>`                 |
| `<thead>`   | Table header section                 | `<thead>...</thead>`            |
| `<tbody>`   | Table body section                   | `<tbody>...</tbody>`            |
| `<tfoot>`   | Table footer section                 | `<tfoot>...</tfoot>`            |

---

### 6. Other Frequently Used Tags

| Tag         | Description                          | Example                          |
|-------------|--------------------------------------|----------------------------------|
| `<div>`     | Generic block-level container        | `<div>Block</div>`              |
| `<span>`    | Generic inline container             | `<span>Inline</span>`           |

---

#### Differences between `<div>` and `<span>`

| Feature         | `<div>`                         | `<span>`                         |
|------------------|----------------------------------|-----------------------------------|
| Display type     | Block-level                     | Inline                            |
| Default behavior | Occupies full width             | Fits content width                |
| Usage            | Grouping sections or layout     | Styling small inline text pieces  |
| Common use cases | Layouts, containers, wrappers   | Styling words, letters, or phrases|

---

#### Common Attributes

These apply to both `<div>` and `<span>`:

| Attribute   | Description                            | Example                                |
|-------------|----------------------------------------|----------------------------------------|
| `id`        | Unique identifier                      | `<div id="header">`                    |
| `class`     | Class name(s) for CSS or JS            | `<span class="highlight">`             |
| `style`     | Inline CSS styling                     | `<div style="color: red;">`            |
| `title`     | Tooltip shown on hover                 | `<span title="tooltip">`               |
| `hidden`    | Hides the element from display         | `<div hidden>Invisible</div>`          |

---

#### Notes

- `<div>` is often used to create layout sections (e.g., header, footer, sidebar).
- `<span>` is used to apply inline styles or behavior to part of the text.
- Prefer using **semantic HTML tags** (e.g., `<header>`, `<section>`, `<article>`) instead of `<div>` when appropriate.
- Avoid excessive use of `<div>` and `<span>` without meaningful structure—this leads to "**div soup**".
- `<div>` and `<span>` are non-semantic HTML elements used to group content. They are often styled with CSS to define layout or appearance. If you want to know more, <!--[click here]().-->

---

[To the part 02...]({{< relref "posts/web-programming-02.md" >}})