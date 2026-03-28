# 📋 Topic 5 — Copy, Cut & Paste

> **Use marks to bookmark lines, then copy or cut blocks of text.**

← [Prev: Search & Replace](./04-search-replace.md) · [Next: Summary →](./06-summary.md)

---

## What are marks?

Marks let you **bookmark a specific line** in Vim so you can refer back to it.  
This is how you select a block of text to copy or cut — by marking the start, then acting on everything up to where you are.

All mark commands work in **Normal Mode**.

---

## Setting a mark

Move your cursor to the line you want to mark, then type:

```
ma    ← set mark "a" at current line
mb    ← set mark "b" at current line
mz    ← set mark "z" at current line
```

You can use any lowercase letter (`a` to `z`) as the mark name.

---

## Jumping to a mark

To jump back to a marked line:

```
'a    ← jump to the line marked "a"
'b    ← jump to the line marked "b"
```

---

## Copy (yank) a block of text

**Step by step:**

1. Move cursor to the **first line** of the section you want to copy
2. Set a mark: `ma`
3. Move cursor to the **last line** of the section
4. Yank (copy) from there back to the mark: `y'a`
5. Move cursor to **where you want to paste**
6. Paste: `p`

**Example:**

```
File content (with line numbers):
1  Introduction
2  Hello World
3  This is line 3
4  This is line 4
5  Conclusion

Goal: copy lines 2–4 and paste after line 5
```

```
:2          ← go to line 2
ma          ← mark it as "a"
:4          ← go to line 4
y'a         ← yank from line 4 back to mark "a" (copies lines 2, 3, 4)
:5          ← go to line 5
p           ← paste
```

Result:
```
1  Introduction
2  Hello World
3  This is line 3
4  This is line 4
5  Conclusion
6  Hello World       ← pasted
7  This is line 3    ← pasted
8  This is line 4    ← pasted
```

> 💡 `p` pastes **below** the current line. Use `P` (capital P) to paste **above**.

---

## Cut and paste (delete + paste)

Cut works exactly like copy — but you use `d'a` instead of `y'a`.

**Step by step:**

1. Move cursor to the **first line** of the section
2. Set a mark: `ma`
3. Move cursor to the **last line** of the section
4. Delete from there back to mark: `d'a`
5. Move to **where you want to paste**
6. Paste: `p`

**Example:**

```
Goal: move lines 2–4 to after line 5
```

```
:2          ← go to line 2
ma          ← mark it
:4          ← go to line 4
d'a         ← delete lines 2–4 (they are now in the clipboard)
:2          ← go to line 2 (which is now "Conclusion" after deletion)
p           ← paste
```

---

## Quick single-line copy

To copy just one line without marks:

```
yy    ← copy (yank) the current line
3yy   ← copy 3 lines from cursor down
```

Then move to where you want it and press `p`.

---

## Summary

| Command | What it does |
|---------|-------------|
| `ma` | Set mark "a" at current line |
| `'a` | Jump to mark "a" |
| `y'a` | Yank (copy) from current line back to mark "a" |
| `d'a` | Delete (cut) from current line back to mark "a" |
| `p` | Paste below current line |
| `P` | Paste above current line |
| `yy` | Copy current line |
| `3yy` | Copy 3 lines |
| `u` | Undo last action |
| `Ctrl + r` | Redo |

---

← [Prev: Search & Replace](./04-search-replace.md) · [Next: Summary →](./06-summary.md)
