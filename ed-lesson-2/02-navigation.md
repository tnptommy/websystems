# 🧭 Topic 2 — Navigation

> **Move around a file quickly — all from Normal Mode, no mouse needed.**

← [Prev: Modes](./01-modes.md) · [Next: Inserting & Deleting →](./03-editing.md)

---

## Before you start

All navigation commands work in **Normal Mode**.  
If you are in Insert Mode, press `Esc` first.

---

## Basic movement

You can always use the arrow keys. But Vim also has letter shortcuts that keep your hands on the home row:

| Key | Direction | Example |
|-----|-----------|---------|
| `h` | Left | Press `h` 5 times → move 5 characters left |
| `l` | Right | Press `l` → move 1 character right |
| `j` | Down | Press `j` → move down 1 line |
| `k` | Up | Press `k` → move up 1 line |

**Memory trick:** `h` is leftmost, `l` is rightmost, `j` looks like a down arrow, `k` is up.

> 💡 **Try it now:** Open a file with `vim /etc/passwd` and practice `h j k l`

---

## Jump to top and bottom

| Key | What it does |
|-----|-------------|
| `gg` | Jump to the **top** of the file (first line) |
| `G` | Jump to the **bottom** of the file (last line) |

```
gg    ← go to line 1
G     ← go to last line
```

> 💡 **Try it now:** Press `G` to jump to the bottom, then `gg` to jump back to the top.

---

## Jump to a specific line

Type `:` then the line number, then press `Enter`:

```
:10     ← jump to line 10
:25     ← jump to line 25
:1      ← jump to line 1 (same as gg)
```

**Show line numbers first** so you know where you are:

```
:set number     ← turn on line numbers
:set nonumber   ← turn off line numbers
:set nu         ← short version of :set number
:set nonu       ← short version of :set nonumber
```

> 💡 **Try it now:**  
> 1. Open `vim /etc/passwd`  
> 2. Type `:set number` → press `Enter`  
> 3. Type `:10` → press `Enter` — you jump to line 10

---

## Page up and down

| Key | What it does |
|-----|-------------|
| `Page Up` | Scroll up one full screen |
| `Page Down` | Scroll down one full screen |
| `Ctrl + u` | Scroll up half a screen |
| `Ctrl + d` | Scroll down half a screen |

---

## Navigation summary

| Key | Goes to |
|-----|---------|
| `h` | Left 1 character |
| `l` | Right 1 character |
| `j` | Down 1 line |
| `k` | Up 1 line |
| `gg` | First line of file |
| `G` | Last line of file |
| `:n` | Line number n |
| `Page Up` | Previous screen |
| `Page Down` | Next screen |

---

← [Prev: Modes](./01-modes.md) · [Next: Inserting & Deleting →](./03-editing.md)
