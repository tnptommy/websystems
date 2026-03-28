# 🔍 Topic 4 — Search & Replace

> **Find text anywhere in a file, and replace it in one command.**

← [Prev: Inserting & Deleting](./03-editing.md) · [Next: Copy, Cut & Paste →](./05-copy-cut-paste.md)

---

## Searching for text

All search commands work in **Normal Mode**.

### Basic search

Type `/` followed by the word you want to find, then press `Enter`:

```
/hello
```

Vim jumps to the first match and highlights it.

**Move between matches:**

| Key | Action |
|-----|--------|
| `n` | Jump to the **next** match |
| `N` | Jump to the **previous** match |

**Example workflow:**
```
/error    ← search for "error"
          ← Vim jumps to first match
n         ← jump to next match
n         ← jump to next match again
N         ← jump back to previous match
```

> 💡 **Try it now:**
> 1. `vim /etc/passwd`
> 2. Type `/root` then press `Enter`
> 3. Press `n` to find the next match

---

## Pattern searching (regular expressions)

Vim search supports patterns, not just exact words.

### Match one character from a set

```
/a[bB]c
```

This matches `abc` or `aBc` — the character inside `[]` can be either `b` or `B`.

### Match zero or more of a character

```
/ab*c
```

This matches: `ac`, `abc`, `abbc`, `abbbc`, ...  
The `*` means "zero or more of the character before it".

### Match whole word only

```
/\<and\>
```

Without word boundaries:
```
/and    ← matches "and" inside "sandy", "standard", "band" too
```

With word boundaries:
```
/\<and\>    ← matches only the standalone word "and"
```

**Example:**
```
Text: "and sandy standard"

/and        → matches: "and", "sandy" (the "and" inside), "standard" (the "and" inside)
/\<and\>    → matches: "and" only
```

---

## Search and Replace

To replace text across the whole file, use the substitute command in **Command Mode**:

```
:%s/old/new/g
```

Breaking it down:

| Part | Meaning |
|------|---------|
| `:` | Enter Command Mode |
| `%` | Apply to the whole file |
| `s` | Substitute (replace) |
| `/old` | The text to find |
| `/new` | The text to replace it with |
| `/g` | Replace **all** occurrences on each line (not just the first) |

**Example:**

```
Before file content:
abc abc abc
abc test abc

:%s/abc/ABC/g

After:
ABC ABC ABC
ABC test ABC
```

### Replace on current line only

```
:s/old/new/g    ← replaces on current line only (no % prefix)
```

### Replace with confirmation

```
:%s/old/new/gc    ← asks you to confirm each replacement
```

For each match, Vim shows:
```
replace with ABC (y/n/a/q)?
y    ← yes, replace this one
n    ← no, skip this one
a    ← replace all remaining
q    ← quit, stop replacing
```

---

## Search summary

| Command | What it does |
|---------|-------------|
| `/word` | Search forward for "word" |
| `n` | Next match |
| `N` | Previous match |
| `/[aB]` | Match either `a` or `B` |
| `/ab*c` | Match `ac`, `abc`, `abbc`, etc. |
| `/\<word\>` | Match whole word only |
| `:%s/old/new/g` | Replace all in file |
| `:s/old/new/g` | Replace all on current line |
| `:%s/old/new/gc` | Replace all with confirmation |

---

← [Prev: Inserting & Deleting](./03-editing.md) · [Next: Copy, Cut & Paste →](./05-copy-cut-paste.md)
