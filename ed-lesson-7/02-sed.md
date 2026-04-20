# 🔄 Topic 2 — Cleaning Data with `sed`

> **`sed` edits text without opening a file — perfect for cleaning data directly in the terminal or inside a script.**

← [Prev: Data Files](./01-data-files.md) · [Next: tr →](./03-tr.md)

---

## What is `sed`?

`sed` stands for **stream editor**.

It reads a file line by line, applies a change to each line, and prints the result.
You never need to open the file — everything happens in one command.

---

## Basic syntax

```bash
sed 's/FIND/REPLACE/g' filename
```

| Part | Meaning |
|------|---------|
| `s` | substitute — this means "replace" |
| `FIND` | the text or pattern to look for |
| `REPLACE` | what to put in instead |
| `g` | global — replace ALL matches on each line, not just the first |

---

## The most important use — clean whitespace to commas

This is the command you will use most in this lesson:

```bash
sed 's/\s\+/,/g' femalenames.txt > table.csv
```

- `\s` = any whitespace character (space or tab)
- `\+` = one or more of them
- So `\s\+` = one or more spaces or tabs in a row
- `,` = replace with a single comma
- `> table.csv` = save the result to a new file

Before:
```
MARY       2.629   2.629    1
```

After:
```
MARY,2.629,2.629,1
```

---

## More useful sed patterns

```bash
# Remove leading whitespace (spaces at the start of each line)
sed 's/^\s\+//' file.txt

# Remove trailing whitespace (spaces at the end of each line)
sed 's/\s\+$//' file.txt

# Delete all blank lines
sed '/^$/d' file.txt

# Print only lines that start with ANA (like grep)
sed -n '/^ANA/p' file.txt

# Replace a specific word
sed 's/female/FEMALE/g' file.txt
```

---

## Save to a new file vs edit in place

```bash
# Save result to a NEW file (original stays unchanged)
sed 's/\s\+/,/g' femalenames.txt > table.csv

# Edit the SAME file directly (-i flag)
sed -i 's/\s\+/,/g' femalenames.txt
```

> ⚠️ Be careful with `-i` — it overwrites the original file. Always work on a copy first.

---

## sed vs Vim — when to use which

| Situation | Use |
|-----------|-----|
| You are already inside a file editing it | Vim |
| You want a one-line fix in the terminal | `sed` |
| You are writing a script | `sed` — scripts cannot open Vim |
| You want to save to a new file | `sed 's/.../' file > newfile` |

---

## Full example — clean femalenames.txt

```bash
# Step 1 — check the original file
head -3 /course/linuxgym/census/femalenames.txt
# MARY       2.629   2.629    1

# Step 2 — clean it and save as CSV
sed 's/\s\+/,/g' /course/linuxgym/census/femalenames.txt > ~/table.csv

# Step 3 — check the result
head -3 ~/table.csv
# MARY,2.629,2.629,1
```

---

> 💡 **Try it now:**
> 1. `sed 's/\s\+/,/g' /course/linuxgym/census/femalenames.txt > ~/table.csv`
> 2. `head -5 ~/table.csv` — check it looks right
> 3. `wc -l ~/table.csv` — line count should match the original

---

← [Prev: Data Files](./01-data-files.md) · [Next: tr →](./03-tr.md)
