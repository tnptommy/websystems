# 📊 Topic 7 — Column Processing with `awk`

> **`awk` reads files column by column — it can filter rows AND extract columns in one command.**

← [Prev: grep](./06-grep.md) · [Next: Checking Output →](./08-check.md)

---

## What is `awk`?

`awk` reads each line and automatically splits it into columns — no delimiter setup needed for space-separated files.

Given this line:
```
MARY       2.629   2.629    1
```

`awk` sees it as:

| Variable | Value |
|----------|-------|
| `$0` | `MARY       2.629   2.629    1` (the whole line) |
| `$1` | `MARY` |
| `$2` | `2.629` |
| `$3` | `2.629` |
| `$4` | `1` |
| `$NF` | `1` (last column — works for any number of columns) |

---

## Basic syntax

```bash
awk 'CONDITION { ACTION }' filename
```

- If CONDITION is true → run ACTION on that line
- If there is no CONDITION → run ACTION on every line

---

## Simple examples — print columns

```bash
# Print column 1 (names only)
awk '{print $1}' /course/linuxgym/census/femalenames.txt

# Print columns 1 and 2
awk '{print $1, $2}' /course/linuxgym/census/femalenames.txt

# Print the entire line (same as cat)
awk '{print $0}' /course/linuxgym/census/femalenames.txt
```

---

## Filter rows with a condition

```bash
# Print only the line where column 1 equals "ANA"
awk '$1 == "ANA"' /course/linuxgym/census/femalenames.txt
# ANA            0.120 55.989    181

# Print column 2 only, where column 1 equals "ANA"
awk '$1 == "ANA" {print $2}' /course/linuxgym/census/femalenames.txt
# 0.120
```

---

## Passing shell variables into awk — use `-v`

`awk` cannot read shell variables directly. You must pass them in with `-v`:

```bash
NAME="ANA"
awk -v n="$NAME" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt
# 0.120
```

In a script, `$1` is the argument passed in by the user:

```bash
#!/bin/bash
awk -v n="$1" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt
```

---

## awk vs grep + cut — same result, one command

Both approaches below produce the same output:

```bash
# grep + cut — two commands joined by a pipe
grep "^ANA " /course/linuxgym/census/femalenames.txt | cut -d' ' -f1

# awk — one command does both filter and extract
awk '$1 == "ANA" {print $2}' /course/linuxgym/census/femalenames.txt
```

Use whichever makes more sense to you. `awk` is shorter and more reliable because it compares whole column values — it will never accidentally match `ANASTASIA` when you search for `ANA`.

---

## Real example — Q8 namefreq.sh

**Task:** Print the frequency (column 2) for a given name.

```bash
#!/bin/bash
awk -v n="$1" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt
```

```bash
./namefreq.sh ANA
# 0.120
```

---

## Real example — Q10 samefreq.sh

**Task:** Find all names with the same frequency as the given name, sorted.

```bash
#!/bin/bash
# Step 1 — find the frequency of the given name
FREQ=$(awk -v n="$1" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt)

# Step 2 — find all names that share that frequency
awk -v f="$FREQ" '$2 == f {print $1}' /course/linuxgym/census/femalenames.txt | sort
```

```bash
./samefreq.sh ANA
# ANA
# RENEE
```

---

## awk with CSV files (comma delimiter)

By default, `awk` splits by whitespace. For CSV files, set the delimiter with `-F`:

```bash
awk -F, '{print $1}' ~/table.csv          # field separator = comma
awk -F, '$1 == "ANA" {print $2}' ~/table.csv
```

---

## Quick reference

| Code | Meaning |
|------|---------|
| `$0` | Entire line |
| `$1` | Column 1 |
| `$2` | Column 2 |
| `$NF` | Last column |
| `{print $1}` | Print column 1 — runs on every line |
| `$1 == "X"` | Only run if column 1 exactly equals X |
| `-v n="$1"` | Pass shell variable `$1` into awk as `n` |
| `-F,` | Use comma as field separator |

---

> 💡 **Try it now:**
> 1. `awk '{print $1}' /course/linuxgym/census/femalenames.txt | head -5`
> 2. `awk '$1 == "MARY" {print $2}' /course/linuxgym/census/femalenames.txt`
> 3. `awk -v n="ANA" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt`

---

← [Prev: grep](./06-grep.md) · [Next: Checking Output →](./08-check.md)
