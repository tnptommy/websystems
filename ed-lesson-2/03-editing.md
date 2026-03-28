# ✏️ Topic 3 — Inserting & Deleting Text

> **Add text and remove text — all from Normal Mode commands.**

← [Prev: Navigation](./02-navigation.md) · [Next: Search & Replace →](./04-search-replace.md)

---

## Inserting text

All insert commands start from **Normal Mode** and switch you into **Insert Mode**.  
Press `Esc` when you are done typing to return to Normal Mode.

| Command | Where it inserts | Example |
|---------|-----------------|---------|
| `i` | Before the cursor | Cursor on `b` in `abc` → press `i` → type `X` → `aXbc` |
| `a` | After the cursor | Cursor on `a` in `abc` → press `a` → type `X` → `aXbc` |
| `I` | At the beginning of the line | Press `I` → cursor jumps to start of line → type |
| `A` | At the end of the line | Press `A` → cursor jumps to end of line → type |
| `o` | New line below, then insert | Press `o` → new empty line appears below → type |

**The most common ones you will use:**

```
i    ← insert where cursor is
A    ← jump to end of line and insert
o    ← add a new line below and start typing
```

**After typing — always press `Esc` to go back to Normal Mode.**

> 💡 **Try it now:**
> 1. `vim practice.txt`
> 2. Press `i` → type `Hello`
> 3. Press `Esc`
> 4. Press `A` → type ` World`
> 5. Press `Esc`
> 6. Press `o` → type `New line here`
> 7. Press `Esc` → `:wq`

---

## Joining lines

In Normal Mode, press `J` (capital J) to **join the current line with the line below it**.

```
Before:
Line 1: Hello
Line 2: World

Put cursor on Line 1 → press J

After:
Hello World
```

The line break is replaced with a single space.

---

## Deleting text

All delete commands work in **Normal Mode** — you do not need to be in Insert Mode.

### Delete a single character

```
x    ← delete the character under the cursor
```

Example:
```
cursor on c in abc → press x → ab
```

### Delete to end of line

```
D    ← delete from cursor position to end of line
```

Example:
```
cursor is mid-line at "W" in "Hello World"
press D → leaves only "Hello "
```

### Delete a whole line

```
dd    ← delete the entire current line
```

Delete multiple lines at once:
```
3dd   ← delete 3 lines starting from cursor
5dd   ← delete 5 lines starting from cursor
ndd   ← delete n lines
```

### Delete a word

```
dw    ← delete from cursor to end of the word
```

Delete multiple words:
```
2dw   ← delete 2 words
3dw   ← delete 3 words
ndw   ← delete n words
```

### Delete to end of file

```
dG    ← delete from cursor all the way to the last line
```

### Delete to a specific line

```
d5G    ← delete from cursor down to line 5
d20G   ← delete from cursor down to line 20
dnG    ← delete from cursor to line n
```

---

## Delete commands summary

| Command | What it deletes |
|---------|----------------|
| `x` | Character under cursor |
| `D` | From cursor to end of line |
| `dd` | Entire current line |
| `ndd` | n lines from cursor down |
| `dw` | One word from cursor |
| `ndw` | n words from cursor |
| `dG` | From cursor to end of file |
| `dnG` | From cursor to line n |

---

## Common mistake — deleting too much

If you delete more than you intended:

```
u    ← undo the last action
```

Press `u` multiple times to undo multiple steps.

```
Ctrl + r    ← redo (undo the undo)
```

> 💡 **Try it now:**
> 1. Open a file in Vim
> 2. Use `:set number` to see line numbers
> 3. Try `dd` to delete a line
> 4. Press `u` to undo it — the line comes back

---

← [Prev: Navigation](./02-navigation.md) · [Next: Search & Replace →](./04-search-replace.md)
