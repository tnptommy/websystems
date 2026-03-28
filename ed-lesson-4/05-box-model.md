# 📦 Topic 5 — The Box Model

> **Every HTML element is a box. The box model controls its size and spacing.**

← [Prev: CSS Selectors](./04-css-selectors.md) · [Next: Colors & Fonts →](./06-colors-fonts.md)

---

## What is the box model?

In CSS, every element — every paragraph, heading, image, div — is treated as a **rectangular box**.

That box has four layers:

```
┌─────────────────────────────────┐
│            MARGIN               │  ← space outside the border
│   ┌─────────────────────────┐   │
│   │         BORDER          │   │  ← the visible edge
│   │   ┌─────────────────┐   │   │
│   │   │     PADDING     │   │   │  ← space inside the border
│   │   │   ┌─────────┐   │   │   │
│   │   │   │ CONTENT │   │   │   │  ← the actual text or image
│   │   │   └─────────┘   │   │   │
│   │   └─────────────────┘   │   │
│   └─────────────────────────┘   │
└─────────────────────────────────┘
```

From inside to outside:
1. **Content** — the text or image
2. **Padding** — space between content and border
3. **Border** — the visible line around the element
4. **Margin** — space between this element and other elements

---

## Padding

Padding adds space **inside** the element, between the content and the border.

```css
div {
  padding: 20px;                    /* same on all 4 sides */
  padding: 10px 20px;               /* top+bottom: 10px, left+right: 20px */
  padding: 5px 10px 15px 20px;      /* top right bottom left (clockwise) */
}

/* Or set each side individually */
div {
  padding-top: 10px;
  padding-right: 20px;
  padding-bottom: 10px;
  padding-left: 20px;
}
```

**Effect:** Makes the element feel more spacious inside.

```html
<style>
  .no-padding  { background: lightblue; }
  .has-padding { background: lightblue; padding: 20px; }
</style>

<p class="no-padding">No padding — text is right at the edge.</p>
<p class="has-padding">Padding — text has breathing room.</p>
```

---

## Border

Border draws a line **around** the element.

```css
div {
  border: 2px solid black;          /* width  style  colour */
}
```

Border styles:

| Style | Looks like |
|-------|-----------|
| `solid` | Solid line |
| `dashed` | Dashed line |
| `dotted` | Dotted line |
| `none` | No border |

```css
div {
  border: 1px solid #ccc;
  border: 3px dashed red;
  border: 2px dotted navy;

  /* Set each side individually */
  border-top: 2px solid black;
  border-bottom: 1px dashed gray;

  /* Rounded corners */
  border-radius: 8px;
  border-radius: 50%;               /* makes a circle if width = height */
}
```

---

## Margin

Margin adds space **outside** the element, pushing other elements away.

```css
div {
  margin: 20px;                     /* same on all 4 sides */
  margin: 10px 20px;                /* top+bottom: 10px, left+right: 20px */
  margin: 0 auto;                   /* centre horizontally (needs a width set) */
}

/* Or set each side individually */
div {
  margin-top: 10px;
  margin-right: 0;
  margin-bottom: 10px;
  margin-left: 0;
}
```

**Centering a block element:**
```css
div {
  width: 600px;
  margin: 0 auto;     /* 0 top/bottom, auto left/right = centred */
}
```

---

## Width and height

```css
div {
  width: 300px;
  height: 200px;
  max-width: 100%;      /* never wider than its container */
  min-height: 100px;    /* at least this tall */
}
```

> ⚠️ By default, `width` sets the content width only.  
> Padding and border are **added on top** of that.

### `box-sizing: border-box`

This property makes `width` include padding and border — much easier to work with:

```css
* {
  box-sizing: border-box;   /* apply to everything */
}

div {
  width: 300px;
  padding: 20px;
  border: 2px solid black;
  /* total width is still 300px — padding and border are inside */
}
```

> 💡 Add `box-sizing: border-box` to every project. It prevents a lot of sizing surprises.

---

## Full example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Box Model</title>
    <style>
      * {
        box-sizing: border-box;
      }

      body {
        font-family: Arial, sans-serif;
        padding: 20px;
      }

      .card {
        width: 300px;
        padding: 20px;
        margin: 10px auto;
        border: 2px solid #ccc;
        border-radius: 8px;
        background-color: white;
      }

      .card h2 {
        margin-top: 0;
      }

      .card p {
        margin-bottom: 0;
        color: #555;
      }
    </style>
  </head>
  <body>

    <div class="card">
      <h2>Card Title</h2>
      <p>This card uses padding, border, margin, and border-radius.</p>
    </div>

    <div class="card">
      <h2>Second Card</h2>
      <p>Same class — same style applied automatically.</p>
    </div>

  </body>
</html>
```

---

## Box model summary

| Property | What it does | Example |
|----------|-------------|---------|
| `padding` | Space inside, between content and border | `padding: 20px` |
| `border` | Visible line around the element | `border: 1px solid black` |
| `margin` | Space outside, between elements | `margin: 10px auto` |
| `width` | Width of the content area | `width: 300px` |
| `height` | Height of the content area | `height: 200px` |
| `border-radius` | Rounds the corners | `border-radius: 8px` |
| `box-sizing: border-box` | Width includes padding and border | `box-sizing: border-box` |

---

← [Prev: CSS Selectors](./04-css-selectors.md) · [Next: Colors & Fonts →](./06-colors-fonts.md)
