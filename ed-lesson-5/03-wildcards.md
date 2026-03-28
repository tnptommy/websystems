# 🔍 Topic 3 — Wildcards

> **Match multiple files by pattern — without typing each name.**

← [Prev: Pipe](./02-pipe.md) · [Next: New Commands →](./04-commands.md)

---

## What is a wildcard?

**Problem:** You have 100 `.txt` files and want to list them all. Do you type each name?

**Solution:**

```bash
ls *.txt
```

The `*` means: *"anything can go here"*

```bash
ls *.txt
# notes.txt   report.txt   readme.txt   diary.txt
# all match because they all end with .txt
```

Wildcards also work with `cp`, `rm`, and other commands — not just `ls`.

---

## The `*` symbol — anything

| Pattern | Matches |
|---------|---------|
| `*.txt` | any file ending with `.txt` |
| `report*` | any file starting with `report` |
| `*2024*` | any file containing `2024` anywhere |
| `*` | every file |

```bash
ls *.txt          # ends with .txt
ls report*        # starts with "report", anything after
ls *2024*         # contains "2024" anywhere in name
```

> 💡 **Try it now:** `ls /etc/*.conf`

---

## The `?` symbol — exactly one character

`?` matches **exactly 1 character** — any character.

```bash
ls file?.txt
# file1.txt   ✅  (? matched "1")
# fileA.txt   ✅  (? matched "A")
# file10.txt  ❌  (two characters, not one)
```

---

## `[abc]` — match one character from a list

`[abc]` matches **exactly 1 character** from the characters inside the brackets.

```bash
ls [abc]*.txt
# apple.txt    ✅  (starts with a)
# banana.txt   ✅  (starts with b)
# cat.txt      ✅  (starts with c)
# dog.txt      ❌  (starts with d — not in [abc])
```

Use a range instead of listing every character:

```bash
ls [a-z]*.txt   # starts with any lowercase letter
ls [A-Z]*       # starts with any uppercase letter
ls [0-9]*       # starts with any number
```

> 💡 **Try it now:** `ls /etc/[abc]*`

---

## `[[:digit:]]` — match any number character

`[[:digit:]]` matches **any single number** (0 to 9).

```bash
ls *[[:digit:]]*
# chapter1.txt    ✅  (has number 1)
# report2024.pdf  ✅  (has numbers 2024)
# notes.txt       ❌  (no numbers in name)
```

Other useful character classes:

| Class | Matches |
|-------|---------|
| `[[:digit:]]` | any number: 0–9 |
| `[[:alpha:]]` | any letter: a–z or A–Z |
| `[[:upper:]]` | any uppercase letter: A–Z |
| `[[:lower:]]` | any lowercase letter: a–z |

> 💡 **Try it now:** `ls /etc/*[[:digit:]]*`

---

## `{a,b}` — this pattern or that pattern

`{a,b}` matches **this pattern OR that pattern**.

```bash
ls {*.txt,*.pdf}
# notes.txt      ✅
# report.pdf     ✅
# photo.jpg      ❌
# diary.txt      ✅
```

Read it as: *"files ending in `.txt` OR ending in `.pdf`"*

Another example:

```bash
ls {report*,notes*}
# report_2024.txt   ✅
# report_final.pdf  ✅
# notes.txt         ✅
# photo.jpg         ❌
```

---

## `[!x]` — everything except this character

`[!x]` matches any character that is **not** `x`.

```bash
ls [!a]*.txt
# banana.txt   ✅  (starts with b, not a)
# cat.txt      ✅  (starts with c, not a)
# apple.txt    ❌  (starts with a)
```

---

## Quick reference

| Symbol | Meaning | Example |
|--------|---------|---------|
| `*` | any string (including empty) | `*.txt` |
| `?` | exactly one character | `file?.txt` |
| `[abc]` | one of these characters | `[123]*` |
| `[a-z]` | one character in this range | `[a-z]*` |
| `[[:digit:]]` | one number character | `*[[:digit:]]*` |
| `{a,b}` | this pattern or that pattern | `{*.txt,*.pdf}` |
| `[!x]` | anything except x | `[!a]*.txt` |

---

← [Prev: Pipe](./02-pipe.md) · [Next: New Commands →](./04-commands.md)
