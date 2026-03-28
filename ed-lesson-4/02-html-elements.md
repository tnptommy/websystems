# 🔗 Topic 2 — Links, Images, Lists & Tables

> **The four most common HTML elements you will use on every page.**

← [Prev: HTML Structure](./01-html-structure.md) · [Next: CSS Methods →](./03-css-methods.md)

---

## Links — `<a>`

`<a>` stands for **anchor**. It creates a clickable link.

```html
<a href="https://www.google.com">Go to Google</a>
```

| Attribute | What it does |
|-----------|-------------|
| `href` | The URL to go to when clicked |

### Open in a new tab

```html
<a href="https://www.google.com" target="_blank">Open Google in new tab</a>
```

### Link to another page in your site

```html
<a href="about.html">About page</a>
```

### Link to a section on the same page

```html
<!-- The link -->
<a href="#contact">Go to Contact section</a>

<!-- The target section -->
<h2 id="contact">Contact</h2>
```

> 💡 **Try it now:** Add a link to your `index.html` and open in a browser to test it.

---

## Images — `<img>`

`<img>` is self-closing — no closing tag needed.

```html
<img src="photo.jpg" alt="A photo of a cat">
```

| Attribute | What it does |
|-----------|-------------|
| `src` | The path or URL to the image file |
| `alt` | Text shown if the image cannot load — also used by screen readers |

### Image from the web

```html
<img src="https://example.com/image.png" alt="Example image">
```

### Set the size

```html
<img src="photo.jpg" alt="Photo" width="300" height="200">
```

> ⚠️ Always include `alt` — it is required for accessibility.

---

## Lists

### Unordered list — bullet points

```html
<ul>
  <li>Apples</li>
  <li>Bananas</li>
  <li>Oranges</li>
</ul>
```

Output:
- Apples
- Bananas
- Oranges

### Ordered list — numbered

```html
<ol>
  <li>First step</li>
  <li>Second step</li>
  <li>Third step</li>
</ol>
```

Output:
1. First step
2. Second step
3. Third step

### Nested list

```html
<ul>
  <li>Fruits
    <ul>
      <li>Apples</li>
      <li>Bananas</li>
    </ul>
  </li>
  <li>Vegetables</li>
</ul>
```

| Tag | What it does |
|-----|-------------|
| `<ul>` | Unordered (bulleted) list |
| `<ol>` | Ordered (numbered) list |
| `<li>` | List item — used inside `<ul>` or `<ol>` |

---

## Tables

Tables display data in rows and columns.

```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>24</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>30</td>
      <td>Melbourne</td>
    </tr>
  </tbody>
</table>
```

| Tag | What it does |
|-----|-------------|
| `<table>` | The table container |
| `<thead>` | Table header section |
| `<tbody>` | Table body section |
| `<tr>` | Table row |
| `<th>` | Table header cell — bold by default |
| `<td>` | Table data cell |

> 💡 **Try it now:** Add a table with 3 columns and 3 rows to your `index.html`.

---

## Full example — all four elements together

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Elements Practice</title>
  </head>
  <body>

    <h1>My Favourite Things</h1>

    <h2>Websites</h2>
    <ul>
      <li><a href="https://github.com" target="_blank">GitHub</a></li>
      <li><a href="https://developer.mozilla.org" target="_blank">MDN Web Docs</a></li>
    </ul>

    <h2>Photo</h2>
    <img src="https://placekitten.com/300/200" alt="A cute kitten">

    <h2>Steps to make tea</h2>
    <ol>
      <li>Boil water</li>
      <li>Put teabag in cup</li>
      <li>Pour water</li>
      <li>Wait 3 minutes</li>
      <li>Enjoy</li>
    </ol>

    <h2>Comparison</h2>
    <table>
      <thead>
        <tr>
          <th>Language</th>
          <th>Used for</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>HTML</td>
          <td>Structure</td>
        </tr>
        <tr>
          <td>CSS</td>
          <td>Appearance</td>
        </tr>
      </tbody>
    </table>

  </body>
</html>
```

---

← [Prev: HTML Structure](./01-html-structure.md) · [Next: CSS Methods →](./03-css-methods.md)
