# ✅ Topic 7 — Summary & Cheat Sheet

> **All HTML tags and CSS properties from Lesson 4 in one place.**

← [Prev: Colors & Fonts](./06-colors-fonts.md) · [Back to README](./README.md)

---

## Key concepts

| Concept | What it means |
|---------|--------------|
| HTML | Defines the structure and content of a page |
| CSS | Controls the appearance of HTML elements |
| Tag | An HTML label — e.g. `<p>`, `<h1>`, `<div>` |
| Attribute | Extra info inside a tag — e.g. `href`, `src`, `class` |
| Selector | The CSS rule that targets an element |
| Property | What CSS changes — e.g. `color`, `font-size` |
| Value | What it changes to — e.g. `red`, `16px` |
| Box model | Content + Padding + Border + Margin |

---

## HTML Cheat Sheet

```html
<!-- ── BOILERPLATE ────────────────────────────────────────── -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Page Title</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <!-- content here -->
  </body>
</html>

<!-- ── HEADINGS ───────────────────────────────────────────── -->
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>

<!-- ── TEXT ──────────────────────────────────────────────── -->
<p>Paragraph</p>
<strong>Bold</strong>
<em>Italic</em>
<br>                      <!-- line break -->
<hr>                      <!-- horizontal rule -->

<!-- ── CONTAINERS ────────────────────────────────────────── -->
<div>Block container</div>
<span>Inline container</span>

<!-- ── LINKS ─────────────────────────────────────────────── -->
<a href="https://example.com">Link text</a>
<a href="page.html" target="_blank">Opens in new tab</a>
<a href="#section-id">Jump to section</a>

<!-- ── IMAGES ────────────────────────────────────────────── -->
<img src="photo.jpg" alt="Description">
<img src="photo.jpg" alt="Description" width="300" height="200">

<!-- ── UNORDERED LIST ────────────────────────────────────── -->
<ul>
  <li>Item</li>
  <li>Item</li>
</ul>

<!-- ── ORDERED LIST ──────────────────────────────────────── -->
<ol>
  <li>First</li>
  <li>Second</li>
</ol>

<!-- ── TABLE ─────────────────────────────────────────────── -->
<table>
  <thead>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Cell</td>
      <td>Cell</td>
    </tr>
  </tbody>
</table>

<!-- ── COMMENTS ──────────────────────────────────────────── -->
<!-- This is a comment — not shown in the browser -->
```

---

## CSS Cheat Sheet

```css
/* ── SELECTORS ───────────────────────────────────────────── */
p { }               /* all <p> elements */
.classname { }      /* elements with class="classname" */
#idname { }         /* element with id="idname" */
h1, h2 { }          /* both h1 and h2 */
div p { }           /* <p> elements inside a <div> */

/* ── CSS METHODS ─────────────────────────────────────────── */
/* Inline:   <p style="color: red;">                          */
/* Internal: <style> in <head>                                */
/* External: <link rel="stylesheet" href="style.css">         */

/* ── COLORS ──────────────────────────────────────────────── */
color: red;
color: #FF0000;
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.5);   /* 50% transparent */
background-color: #f5f5f5;

/* ── FONTS ───────────────────────────────────────────────── */
font-family: Arial, Helvetica, sans-serif;
font-size: 16px;
font-weight: bold;              /* or normal, 400, 700 */
font-style: italic;             /* or normal */
line-height: 1.6;
letter-spacing: 2px;

/* ── TEXT ────────────────────────────────────────────────── */
text-align: center;             /* left / center / right */
text-decoration: none;          /* underline / none / line-through */
text-transform: uppercase;      /* uppercase / lowercase / capitalize */

/* ── BOX MODEL ───────────────────────────────────────────── */
width: 300px;
height: 200px;
max-width: 100%;

padding: 20px;                  /* all sides */
padding: 10px 20px;             /* top+bottom  left+right */
padding: 5px 10px 15px 20px;    /* top right bottom left */
padding-top: 10px;

margin: 20px;
margin: 0 auto;                 /* centre horizontally */
margin-top: 10px;

border: 2px solid black;
border-radius: 8px;
border-top: 1px dashed gray;

box-sizing: border-box;         /* include padding+border in width */

/* ── DISPLAY ─────────────────────────────────────────────── */
display: block;
display: inline;
display: none;                  /* hides element */
```

---

## Read the question → know what to do

| Question says | Use this |
|---------------|----------|
| *"create a link"* | `<a href="url">text</a>` |
| *"open link in new tab"* | `target="_blank"` |
| *"add an image"* | `<img src="file" alt="desc">` |
| *"bullet point list"* | `<ul><li>...</li></ul>` |
| *"numbered list"* | `<ol><li>...</li></ol>` |
| *"add a table"* | `<table><tr><th>/<td>` |
| *"style one element only"* | Inline: `style=""` or ID: `#id` |
| *"style many elements"* | Class: `.classname { }` |
| *"link an external CSS file"* | `<link rel="stylesheet" href="style.css">` |
| *"centre text"* | `text-align: center` |
| *"centre a block"* | `margin: 0 auto` + `width: Xpx` |
| *"make text bold"* | `font-weight: bold` or `<strong>` |
| *"make text italic"* | `font-style: italic` or `<em>` |
| *"remove underline from link"* | `text-decoration: none` |
| *"add space inside an element"* | `padding` |
| *"add space between elements"* | `margin` |
| *"add a border"* | `border: 2px solid black` |
| *"round the corners"* | `border-radius: 8px` |

---

## Check your work before submitting

```bash
# Open your HTML file in the browser
# Right-click → Inspect → check for errors in the Console tab

# Validate HTML structure
# Every opening tag should have a closing tag (except self-closing ones)
# Self-closing: <br> <hr> <img> <input> <meta> <link>

# Check your CSS is linked correctly
# The <link> tag must be inside <head>
# The href path must match the actual filename exactly
```

> 💡 If your CSS is not working — first check the browser Console for errors,  
> then check the `href` path in your `<link>` tag matches the actual `.css` filename.

---

← [Prev: Colors & Fonts](./06-colors-fonts.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
