# 🏗️ Topic 1 — HTML Structure & Basic Tags

> **Every webpage starts with the same skeleton. Learn it once, use it everywhere.**

← [Back to README](./README.md) · [Next: Links, Images, Lists & Tables →](./02-html-elements.md)

---

## What is HTML?

HTML stands for **HyperText Markup Language**.

It uses **tags** to label pieces of content so the browser knows what each thing is.

```html
<p>This is a paragraph.</p>
^                        ^
opening tag              closing tag
```

Tags usually come in pairs — an opening tag and a closing tag.  
The closing tag has a `/` before the tag name.

---

## The HTML boilerplate

Every HTML file starts with the same basic structure:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Page</title>
  </head>
  <body>

    <!-- Your content goes here -->

  </body>
</html>
```

What each part does:

| Part | What it does |
|------|-------------|
| `<!DOCTYPE html>` | Tells the browser this is an HTML5 file |
| `<html>` | The root element — wraps everything |
| `<head>` | Contains metadata — not shown on the page |
| `<meta charset="UTF-8">` | Supports special characters |
| `<title>` | Text shown in the browser tab |
| `<body>` | Everything the user sees goes here |
| `<!-- comment -->` | A comment — ignored by the browser |

> 💡 **Try it now:** Create `~/index.html`, paste the boilerplate, save, and open in your browser.

---

## Headings

HTML has 6 heading levels — `<h1>` is the biggest, `<h6>` is the smallest.

```html
<h1>Main Heading</h1>
<h2>Section Heading</h2>
<h3>Subsection</h3>
<h4>Smaller heading</h4>
<h5>Even smaller</h5>
<h6>Smallest heading</h6>
```

> 💡 Use only **one `<h1>`** per page — it is the main title.

---

## Paragraphs

```html
<p>This is a paragraph of text.</p>

<p>This is a second paragraph. Each one gets its own block of space.</p>
```

---

## Line break and horizontal rule

```html
<p>Line one.<br>Line two in the same paragraph.</p>

<hr>
```

`<br>` and `<hr>` are **self-closing tags** — no closing tag needed.

---

## Bold and italic

```html
<strong>This text is bold.</strong>
<em>This text is italic.</em>
```

---

## `<div>` and `<span>`

These have **no visual effect on their own** — they group content so CSS can target it.

| Tag | Type | Used for |
|-----|------|---------|
| `<div>` | Block — full line | Grouping sections |
| `<span>` | Inline — within a line | Styling part of a sentence |

```html
<div>
  <p>This paragraph is inside a div.</p>
  <p>So is this one.</p>
</div>

<p>The word <span>important</span> is inside a span.</p>
```

---

## Full example — put it all together

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>My First Page</title>
  </head>
  <body>

    <h1>Welcome to My Page</h1>

    <p>This is my first paragraph. HTML is not that hard.</p>

    <h2>About Me</h2>

    <p>
      My name is <strong>Tommy</strong> and I am learning
      <em>web development</em>.
    </p>

    <hr>

    <p>That line above is a horizontal rule.</p>

  </body>
</html>
```

---

## Tags summary

| Tag | What it does |
|-----|-------------|
| `<h1>` – `<h6>` | Headings, largest to smallest |
| `<p>` | Paragraph |
| `<br>` | Line break (self-closing) |
| `<hr>` | Horizontal rule (self-closing) |
| `<strong>` | Bold |
| `<em>` | Italic |
| `<div>` | Block container |
| `<span>` | Inline container |
| `<!-- -->` | Comment |

---

← [Back to README](./README.md) · [Next: Links, Images, Lists & Tables →](./02-html-elements.md)
