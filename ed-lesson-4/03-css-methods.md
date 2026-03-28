# 🎨 Topic 3 — Inline, Internal & External CSS

> **Three ways to add CSS to a page — and when to use each one.**

← [Prev: HTML Elements](./02-html-elements.md) · [Next: CSS Selectors →](./04-css-selectors.md)

---

## What is CSS?

CSS stands for **Cascading Style Sheets**.

It controls how HTML elements look — colour, size, spacing, font, layout.

Without CSS:
```
Black text, white background, default font, no spacing control.
```

With CSS:
```
Custom colours, fonts, layouts — every website looks different.
```

---

## Method 1 — Inline CSS

Inline CSS is written **directly on the HTML tag** using the `style` attribute.

```html
<p style="color: red; font-size: 20px;">This paragraph is red and large.</p>

<h1 style="color: blue;">This heading is blue.</h1>
```

### When to use it

✅ Quick one-off styling for a single element  
❌ Not good for whole pages — hard to maintain, no reuse

---

## Method 2 — Internal CSS

Internal CSS is written inside a `<style>` tag in the `<head>` section.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Internal CSS</title>
    <style>
      p {
        color: red;
        font-size: 18px;
      }

      h1 {
        color: blue;
      }
    </style>
  </head>
  <body>
    <h1>This heading is blue.</h1>
    <p>This paragraph is red.</p>
    <p>This one too — the style applies to all p tags.</p>
  </body>
</html>
```

### When to use it

✅ Good for single-page sites or quick testing  
❌ If you have multiple HTML files, you have to copy the CSS into each one

---

## Method 3 — External CSS

External CSS is written in a **separate `.css` file** and linked to the HTML file.

**style.css:**
```css
p {
  color: red;
  font-size: 18px;
}

h1 {
  color: blue;
}
```

**index.html:**
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>External CSS</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>This heading is blue.</h1>
    <p>This paragraph is red.</p>
  </body>
</html>
```

The `<link>` tag connects the HTML file to the CSS file.

### When to use it

✅ The correct approach for real projects  
✅ One CSS file controls the style of many HTML pages  
✅ Easy to update — change the CSS once, all pages update

---

## Comparison

| Method | Where CSS is written | Best for |
|--------|---------------------|---------|
| Inline | Inside the HTML tag (`style=""`) | One single element |
| Internal | Inside `<style>` in `<head>` | Single page, quick testing |
| External | Separate `.css` file, linked with `<link>` | Real projects, multiple pages |

---

## The cascade — order matters

"Cascading" in CSS means styles can come from multiple places at once.  
When there is a conflict, **more specific styles win**.

```html
<!-- External CSS says: p { color: blue; } -->
<!-- Internal CSS says: p { color: green; } -->
<!-- Inline CSS says:   style="color: red;" -->

<p style="color: red;">What colour am I?</p>
<!-- Answer: red — inline wins over internal, which wins over external -->
```

Priority (highest to lowest):
```
Inline > Internal > External
```

> 💡 **Try it now:**
> 1. Create `~/style.css` with `p { color: teal; }`
> 2. Link it to your `index.html` with `<link rel="stylesheet" href="style.css">`
> 3. Open the page and see the paragraph colour change

---

← [Prev: HTML Elements](./02-html-elements.md) · [Next: CSS Selectors →](./04-css-selectors.md)
