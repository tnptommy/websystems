# 🔤 Topic 5 — Sorting with `sort`

> **`sort` puts lines in order — alphabetically, numerically, or by a specific field.**

← [Prev: cut](./04-cut.md) · [Next: grep →](./06-grep.md)

---

## Basic sort — alphabetical order

By default, `sort` arranges lines in **alphabetical order** (A to Z):

```bash
sort names.txt
```

Or combined with a pipe:

```bash
cut -f1 -d, table.csv | sort
# BARBARA
# DOROTHY
# LINDA
# MARY
# PATRICIA
```

---

## Useful `sort` options

| Option | What it does | Example |
|--------|-------------|---------|
| (none) | Alphabetical A→Z | `sort file.txt` |
| `-r` | Reverse order (Z→A or largest→smallest) | `sort -r file.txt` |
| `-n` | Numeric order (treat values as numbers) | `sort -n numbers.txt` |
| `-n -r` | Numeric, largest first | `sort -n -r file.txt` |
| `-k N` | Sort by field number N | `sort -k2 file.txt` |
| `-t X` | Use X as field delimiter (used with `-k`) | `sort -t, -k2 file.csv` |

---

## Why `-n` matters for numbers

Without `-n`, sort compares numbers as **text**, which gives wrong results:

```bash
cat numbers.txt
# 100
# 20
# 9
# 3

sort numbers.txt
# 100    ← "1" comes before "2" and "9" in text order — WRONG
# 20
# 3
# 9

sort -n numbers.txt
# 3      ← correct numeric order ✅
# 9
# 20
# 100
```

---

## Sort by a specific field (column)

Use `-k` to choose the column and `-t` to set the delimiter:

```bash
# Sort by frequency (field 2), numerically
sort -t, -k2 -n ~/table.csv | head -5
# (names with lowest frequency first)

# Sort by frequency, largest first
sort -t, -k2 -n -r ~/table.csv | head -5
# (names with highest frequency first)
```

---

## Combine with pipe

`sort` works on stdin — chain it after other commands:

```bash
# Get all names, sorted alphabetically
cut -f1 -d, ~/table.csv | sort

# Get all frequencies, sorted from largest to smallest
cut -f2 -d, ~/table.csv | sort -n -r | head -5
```

---

## Save sorted output to a file

```bash
sort /course/linuxgym/census/femalenames.txt > ~/alphabetical.txt
cut -f1 -d, ~/table.csv | sort > ~/sorted_names.txt
```

---

## Common pipeline — filter, extract, sort

```bash
# Find all names starting with ANA, get just the names, sort them
grep "^ANA" /course/linuxgym/census/femalenames.txt | awk '{print $1}' | sort
# ANA
# ANABEL
# ANASTACIA
# ANASTASIA
# ANAMARIA
# ANALISA
```

---

> 💡 **Try it now:**
> 1. `sort /course/linuxgym/census/femalenames.txt | head -5` — first 5 names alphabetically
> 2. `sort -r /course/linuxgym/census/femalenames.txt | head -5` — last 5 names alphabetically
> 3. `cut -f2 -d, ~/table.csv | sort -n | head -5` — 5 lowest frequencies

---

← [Prev: cut](./04-cut.md) · [Next: grep →](./06-grep.md)
