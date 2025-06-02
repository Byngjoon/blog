+++
date = '2025-05-29T14:20:15+09:00'
title = '[Web Programming] [02] Frontend - HTML Part 02'
description = "Learn about HTML5"
categories = ["Information Technology/Application Software Development/Web Programming"]
tags = ["Frontend"]
slug = "html-part-02"
math = true
draft = false
+++

# Chapter 01. Frontend – HTML (Part 02)

---

## Contents

- [1.1. What is HTML]({{< relref "posts/web-programming-01.md" >}})
- [1.2. What is a Markup Language]({{< relref "posts/web-programming-01.md" >}})
- [1.3. Core Concepts of HTML]({{< relref "posts/web-programming-01.md" >}})
- [1.4. Basic HTML Document Structure]({{< relref "posts/web-programming-01.md" >}})
- [1.5. Common HTML Tags]({{< relref "posts/web-programming-01.md" >}})
- [1.6. Forms and Input Elements](#section-16-forms-and-input-elements)
- [1.7. Semantic HTML Tags](#section-17-semantic-html-tags)
- [1.8. HTML Entities & Special Characters](#section-18-html-entities--special-characters)
- [1.9. HTML Accessibility (ARIA Basics)](#section-19-html-accessibility-aria-basics)
- [1.10. SEO and HTML Structure *(Optional)*](#section-110-seo-and-html-structure-optional)

---

## Section 1.6. Forms and Input Elements

### 1. What is a Form?

An HTML `<form>` element is used to **collect user input** and **submit it to a server**.

```html
<form action="/submit" method="post">
  <label for="username">Name:</label>
  <input type="text" id="username" name="username">
  <input type="submit" value="Send">
</form>
```

---

### 2. Do Input Elements Have to Be Inside a `<form>`?

> **No**, an `<input>` element does **not** have to be placed inside a `<form>`.  
> However, using it within a `<form>` is **recommended** for proper data submission, validation, and accessibility.

---

#### Using `<input>` Without a `<form>`

```html
<input type="text" placeholder="Standalone input">
```

- This input will appear and accept user input.
- But it **won’t submit any data** or trigger form behavior.

---

#### Why Use a `<form>`?

| Reason              | Benefit                                                                 |
|---------------------|-------------------------------------------------------------------------|
| `action`, `method`  | Submits data to a server                                                |
| Submit behavior     | Pressing **Enter** triggers submission automatically                   |
| HTML5 validation    | Fields like `required`, `type="email"` work only within a `<form>`      |
| Accessibility       | Assistive tech recognizes the grouped structure of form-related inputs |

---

#### Using Inputs Without `<form>` via JavaScript

You can manually retrieve and handle input values like this:

```html
<input id="data">
<button onclick="alert(document.getElementById('data').value)">Show</button>
```

- This works **without a form**, using JavaScript to handle logic.

---

#### Summary

| Situation                        | Allowed?| Notes                                    |
|----------------------------------|:-------:|------------------------------------------|
| `<input>` alone                  | O       | Input works but no submit functionality  |
| `<input>` inside `<form>`        | O       | Enables full form behavior               |
| JS-handled input (no `<form>`)   | O       | Requires manual scripting                |

> **Conclusion:**  
> If you want to collect and submit user input using built-in browser behavior (like pressing Enter or validating fields), use a `<form>`.  
> For quick, local interaction (like showing alerts or changing the UI), `<input>` can stand alone with JavaScript.

---

### 3. Key Form Attributes

The `<form>` element supports several important attributes that control how form data is submitted and interpreted by the server.

---

#### `action`

- **Definition**: Specifies the URL where the form data should be sent after submission.
- **If omitted**: The form submits to the **same URL** as the page it’s on.
- **Examples**:
  ```html
  <form action="/submit">...</form>
  <form action="/login">...</form>
  <form action="/api/feedback">...</form>
  <form action="https://api.example.com/data">...</form>
  ```

> `/submit` - This means: "Send the form data to the `/submit` route on the current server."
> If the HTML page is hosted at `https://example.com/form.html`, then will send data to `https://example.com/submit`.
> The server should have backend code ready to receive and handle this request at `/submit`.
> Like this, `action="/path"` declares the receiving location on the server.

---

#### `method`

- **Definition**: Specifies the HTTP method to use when sending form data.
- **Allowed values**:
  - `get`: Appends data to the URL (visible in address bar)
  - `post`: Sends data in the request body (hidden from URL)
- **When to use**:
  - Use `get` for simple queries/searches (no sensitive data)
  - Use `post` for login forms, file uploads, sensitive info

```html
<form method="get">      <!-- example.com?name=jong -->
<form method="post">     <!-- Data in body -->
```

---

#### `enctype`

- **Definition**: Specifies how the form data should be encoded when submitted to the server.
- **Relevant when**: `method="post"` is used.
- **Common values**:
  - `application/x-www-form-urlencoded` (default)
  - `multipart/form-data` → for **file uploads**
  - `text/plain` → rarely used, sends raw text (no encoding)

```html
<form method="post" enctype="multipart/form-data">
  <input type="file">
</form>
```

---

#### `autocomplete`

- **Definition**: Controls whether the browser should auto-fill the form based on past input.
- **Values**:
  - `on` (default)
  - `off` (useful for login, credit card forms)

```html
<form autocomplete="off">
```

---

#### `novalidate`

- **Definition**: Disables built-in HTML5 validation (ignores `required`, `type="email"`, etc.)
- **Usage**: Often used when validation is handled fully via JavaScript.

```html
<form novalidate>
```

---

#### `target`

- **Definition**: Specifies where to display the response after form submission.
- **Values**:
  - `_self`: current tab (default)
  - `_blank`: new tab
  - `_parent`, `_top`: for frames

```html
<form target="_blank">
```

---

#### Summary

| Attribute     | Description                                 | Common Values                        |
|---------------|---------------------------------------------|--------------------------------------|
| `action`      | Destination URL for form data               | `/submit`, `https://...`             |
| `method`      | HTTP method to use                          | `get`, `post`                        |
| `enctype`     | Data encoding type                          | `application/x-www-form-urlencoded`, `multipart/form-data` |
| `autocomplete`| Browser autofill setting                    | `on`, `off`                          |
| `novalidate`  | Skips HTML5 built-in validation             | -                                    |
| `target`      | Where to display server response            | `_self`, `_blank`, `_parent`, `_top` |

---

### 4. Common Input Elements

| Tag           | Type/Role           | Example                                  |
|---------------|---------------------|------------------------------------------|
| `<input>`     | Single-line input   | `<input type="text">`                    |
| `<textarea>`  | Multi-line text     | `<textarea rows="4"></textarea>`         |
| `<select>`    | Drop-down list      | `<select><option>One</option></select>` |
| `<option>`    | Option in `<select>`| `<option value="1">One</option>`        |
| `<button>`    | Clickable button    | `<button>Click</button>`                 |
| `<label>`     | Describes input     | `<label for="email">Email</label>`      |
| `<fieldset>`  | Groups inputs       | `<fieldset><legend>Info</legend></fieldset>`|
| `<legend>`    | Title of fieldset   | `<legend>Personal Info</legend>`        |

---

### 5. Input `type` Values

| `type` Value | Description              |
|--------------|--------------------------|
| `text`       | Single-line text input   |
| `password`   | Hidden input             |
| `email`      | Validated email field    |
| `number`     | Numeric input            |
| `checkbox`   | Toggle on/off            |
| `radio`      | Multiple choice options  |
| `date`       | Date picker              |
| `file`       | File upload              |
| `submit`     | Submit the form          |
| `reset`      | Reset form fields        |
| `button`     | General-purpose button   |
| `hidden`     | Invisible value input    |

---

### 6. Input Attributes

| Attribute   | Description                           | Example                              |
|-------------|---------------------------------------|--------------------------------------|
| `name`      | Key used when submitting data         | `name="email"`                       |
| `value`     | Default or submitted value            | `value="default"`                    |
| `placeholder` | Hint shown in empty input           | `placeholder="Enter name"`          |
| `required`  | Field must be filled                  | `<input required>`                   |
| `readonly`  | Cannot be edited                      | `<input readonly>`                   |
| `disabled`  | Grayed out and skipped from submit    | `<input disabled>`                   |
| `checked`   | Checked by default (radio/checkbox)   | `<input type="checkbox" checked>`    |
| `min`, `max`, `step` | Validation for number/date inputs | `<input type="number" min="1" max="10" step="1">` |

---

### 7. Notes

- Always pair `<label>` with `for` matching the `id` of the input for accessibility.
- Use `name` to ensure input values are submitted.
- Use `fieldset` and `legend` to improve form structure and semantics.

---

## Section 1.7. Semantic HTML Tags
- `<header>`, `<footer>`, `<nav>`, `<main>`, `<section>`, `<article>`

## Section 1.8. HTML Entities & Special Characters

## Section 1.9. HTML Accessibility (ARIA Basics)

## Section 1.10. SEO and HTML Structure *(Optional)*