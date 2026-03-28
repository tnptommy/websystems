# 🎯 Topic 4 — CSS Selectors & Properties

> **Selectors tell CSS which elements to style. Properties tell it what to change.**

← [Prev: CSS Methods](./03-css-methods.md) · [Next: Box Model →](./05-box-model.md)

---

## CSS syntax

Every CSS rule follows the same pattern:

```css
selector {
  property: value;
  property: value;
}
```

Example:
```css
p {
  color: red;
  font-size: 18px;
}
```

- `p` = the selector (target all `<p>` elements)
- `color` = the property
- `red` = the value
- Each line ends with a `;`

---

## Selector 1 — Element selector

Targets **every element** of that type on the page.

```css
p {
  color: navy;
}

h1 {
  color: teal;
}

a {
  text-decoration: none;
}
```

```html
<p>This is navy.</p>
<p>This is also navy.</p>
<h1>This is teal.</h1>
```

---

## Selector 2 — Class selector

Targets elements with a specific `class` attribute.  
Use a `.` before the class name in CSS.

```css
.highlight {
  background-color: yellow;
  font-weight: bold;
}

.warning {
  color: red;
}
```

```html
<p class="highlight">This paragraph is highlighted.</p>
<p>This one is not.</p>
<p class="warning">This one is red.</p>
<p class="highlight warning">This one is both.</p>
```

> 💡 An element can have **multiple classes** — just separate them with a space.

---

## Selector 3 — ID selector

Targets **one specific element** with a matching `id` attribute.  
Use a `#` before the id name in CSS.

```css
#main-title {
  font-size: 48px;
  color: darkblue;
}
```

```html
<h1 id="main-title">This is the main title.</h1>
```

> ⚠️ Each `id` must be **unique** on the page — only one element can have each id.

---

## Class vs ID — when to use which

| | Class | ID |
|--|-------|----|
| Symbol in CSS | `.classname` | `#idname` |
| Can be used on | Many elements | One element only |
| Use for | Reusable styles | Unique elements |

---

## Combining selectors

```css
/* All paragraphs inside a div */
div p {
  color: gray;
}

/* Elements with both classes */
.card.featured {
  border: 2px solid gold;
}

/* Multiple selectors — same style */
h1, h2, h3 {
  font-family: Arial, sans-serif;
}
```

---

## Common CSS properties

### Text

```css
p {
  color: navy;                  /* text colour */
  font-size: 16px;              /* text size */
  font-weight: bold;            /* bold / normal */
  font-style: italic;           /* italic / normal */
  text-align: center;           /* left / center / right */
  text-decoration: underline;   /* underline / none */
  line-height: 1.6;             /* space between lines */
  letter-spacing: 2px;          /* space between characters */
}
```

### Background

```css
div {
  background-color: lightblue;
  background-image: url("bg.jpg");
}
```

### Dimensions

```css
div {
  width: 300px;
  height: 200px;
  max-width: 100%;
}
```

### Display

```css
span {
  display: block;        /* acts like a div */
}

div {
  display: inline;       /* acts like a span */
}

.hidden {
  display: none;         /* hides the element completely */
}
```

---

## Full example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Selectors Practice</title>
    <style>
      /* Element selector */
      body {
        font-family: Arial, sans-serif;
        background-color: #f5f5f5;
      }

      h1 {
        color: darkblue;
        text-align: center;
      }

      p {
        color: #333;
        line-height: 1.6;
      }

      /* Class selector */
      .highlight {
        background-color: yellow;
        font-weight: bold;
      }

      .note {
        color: gray;
        font-style: italic;
      }

      /* ID selector */
      #intro {
        font-size: 20px;
        color: teal;
      }
    </style>
  </head>
  <body>

    <h1>Selectors Demo</h1>

    <p id="intro">This paragraph has a unique id — it is larger and teal.</p>

    <p>This is a normal paragraph.</p>

    <p class="highlight">This one is highlighted with a class.</p>

    <p class="note">This one uses the note class — grey and italic.</p>

    <p class="highlight note">This one has both classes applied.</p>

  </body>
</html>
```

---

## Selectors summary

| Selector | Syntax | Targets |
|----------|--------|---------|
| Element | `p { }` | All `<p>` tags |
| Class | `.name { }` | All elements with `class="name"` |
| ID | `#name { }` | The one element with `id="name"` |
| Multiple | `h1, h2 { }` | Both `<h1>` and `<h2>` |
| Descendant | `div p { }` | `<p>` elements inside a `<div>` |

---

← [Prev: CSS Methods](./03-css-methods.md) · [Next: Box Model →](./05-box-model.md)
