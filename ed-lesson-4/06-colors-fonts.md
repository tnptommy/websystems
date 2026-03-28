# 🎨 Topic 6 — Colors & Fonts

> **Control how text looks and what colours appear on your page.**

← [Prev: Box Model](./05-box-model.md) · [Next: Summary →](./07-summary.md)

---

## Colors

CSS supports several ways to write a colour value.

### Named colors

Plain English names — easy to read, limited selection:

```css
p { color: red; }
h1 { color: navy; }
div { background-color: lightgray; }
```

Common named colors:
`red` `blue` `green` `yellow` `orange` `purple` `pink` `black` `white` `gray` `navy` `teal` `coral` `salmon` `gold` `skyblue` `lightgray` `darkblue`

---

### Hex colors

A `#` followed by 6 hex digits — the most common format in real projects:

```css
p { color: #FF0000; }        /* red */
h1 { color: #0000FF; }       /* blue */
div { color: #333333; }      /* dark gray */
```

How hex works:
```
#  R  R  G  G  B  B
   ^     ^     ^
   red   green blue
   (00 to FF each)
```

| Value | Colour |
|-------|--------|
| `#000000` | Black |
| `#FFFFFF` | White |
| `#FF0000` | Red |
| `#00FF00` | Green |
| `#0000FF` | Blue |
| `#333333` | Dark gray |
| `#f5f5f5` | Off-white |

> 💡 Hex is **case-insensitive** — `#FF0000` and `#ff0000` are the same.  
> Short form: `#F00` is the same as `#FF0000`.

---

### RGB colors

Specify red, green, and blue values from 0 to 255:

```css
p { color: rgb(255, 0, 0); }         /* red */
h1 { color: rgb(0, 0, 255); }        /* blue */
div { color: rgb(100, 100, 100); }    /* gray */
```

### RGBA — with transparency

The `a` value goes from `0` (fully transparent) to `1` (fully opaque):

```css
div {
  background-color: rgba(0, 0, 255, 0.3);    /* blue, 30% opacity */
}
```

---

## Fonts

### `font-family` — choosing a font

```css
p {
  font-family: Arial, sans-serif;
}
```

Always list **multiple fonts** separated by commas — a fallback chain.  
The browser uses the first font it has installed. The last one should always be a generic family.

**Generic families:**

| Generic | Style |
|---------|-------|
| `serif` | Has small decorative strokes (Times New Roman) |
| `sans-serif` | Clean, no strokes (Arial, Helvetica) |
| `monospace` | Fixed-width — good for code (Courier, Consolas) |

**Common font stacks:**

```css
/* Clean, modern */
font-family: Arial, Helvetica, sans-serif;

/* Classic readable */
font-family: Georgia, "Times New Roman", serif;

/* Code / terminal */
font-family: "Courier New", Courier, monospace;

/* System default — fast loading */
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
```

---

### `font-size` — text size

```css
p {
  font-size: 16px;       /* pixels — most common */
  font-size: 1rem;       /* relative to root font size (usually 16px) */
  font-size: 1.2em;      /* relative to parent element's font size */
  font-size: large;      /* keyword */
}
```

---

### `font-weight` — bold or not

```css
p { font-weight: normal; }     /* default */
p { font-weight: bold; }       /* bold */
p { font-weight: 400; }        /* same as normal (100–900 scale) */
p { font-weight: 700; }        /* same as bold */
```

---

### `font-style` — italic

```css
p { font-style: normal; }
p { font-style: italic; }
```

---

### `line-height` — space between lines

```css
p {
  line-height: 1.6;     /* 1.6× the font size — good for readability */
  line-height: 24px;    /* fixed value */
}
```

---

### `text-align` — horizontal alignment

```css
p { text-align: left; }      /* default */
p { text-align: center; }
p { text-align: right; }
p { text-align: justify; }   /* stretches text to fill the line */
```

---

### `text-decoration` — underline etc.

```css
a { text-decoration: none; }          /* removes underline from links */
p { text-decoration: underline; }
p { text-decoration: line-through; }  /* strikethrough */
```

---

### `text-transform` — uppercase / lowercase

```css
h1 { text-transform: uppercase; }     /* ALL CAPS */
p  { text-transform: lowercase; }     /* all lowercase */
p  { text-transform: capitalize; }    /* First Letter Of Each Word */
```

---

## Full example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Colors and Fonts</title>
    <style>
      body {
        font-family: Arial, Helvetica, sans-serif;
        font-size: 16px;
        line-height: 1.6;
        background-color: #f5f5f5;
        color: #333;
      }

      h1 {
        color: #0D1B2A;
        text-align: center;
        font-size: 2rem;
        text-transform: uppercase;
        letter-spacing: 3px;
      }

      .highlight {
        color: #EE9B00;
        font-weight: bold;
      }

      .note {
        color: #888;
        font-style: italic;
        font-size: 14px;
      }

      a {
        color: #0A9396;
        text-decoration: none;
      }

      a:hover {
        text-decoration: underline;
      }

      code {
        font-family: "Courier New", monospace;
        background-color: #e8e8e8;
        padding: 2px 6px;
        border-radius: 4px;
        font-size: 14px;
      }
    </style>
  </head>
  <body>

    <h1>Colors and Fonts Demo</h1>

    <p>This body text uses Arial at 16px with a line-height of 1.6.</p>

    <p>This word is <span class="highlight">highlighted</span> using a class.</p>

    <p class="note">This is a note — smaller, grey, and italic.</p>

    <p>Visit <a href="#">this link</a> — it uses a teal colour with no underline.</p>

    <p>Use the <code>font-family</code> property to set fonts.</p>

  </body>
</html>
```

---

## Colors & fonts summary

| Property | What it does | Example |
|----------|-------------|---------|
| `color` | Text colour | `color: #333` |
| `background-color` | Background colour | `background-color: #f5f5f5` |
| `font-family` | Font typeface | `font-family: Arial, sans-serif` |
| `font-size` | Text size | `font-size: 16px` |
| `font-weight` | Bold or normal | `font-weight: bold` |
| `font-style` | Italic or normal | `font-style: italic` |
| `line-height` | Spacing between lines | `line-height: 1.6` |
| `text-align` | Horizontal alignment | `text-align: center` |
| `text-decoration` | Underline etc. | `text-decoration: none` |
| `text-transform` | Uppercase/lowercase | `text-transform: uppercase` |
| `letter-spacing` | Space between characters | `letter-spacing: 2px` |

---

← [Prev: Box Model](./05-box-model.md) · [Next: Summary →](./07-summary.md)
