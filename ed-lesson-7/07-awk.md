# 📊 Topic 7 — Column Processing with `awk`

> **`awk` reads files column by column — it can filter rows AND extract columns in one command.**

← [Prev: grep](./06-grep.md) · [Next: Checking Output →](./08-check.md)

---

## What is `awk`?

`awk` reads each line and automatically splits it into columns — no delimiter setup needed for space-separated files.

Given this line:
```
SYDNEY         5.3    5.3    1
```

`awk` sees it as:

| Variable | Value |
|----------|-------|
| `$0` | `SYDNEY         5.3    5.3    1` (the whole line) |
| `$1` | `SYDNEY` |
| `$2` | `5.3` |
| `$3` | `5.3` |
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

Assume a file `cities.txt`:
```
SYDNEY     5.3   5.3   1
MELBOURNE  5.0  10.3   2
BRISBANE   2.5  12.8   3
PERTH      2.1  14.9   4
```

```bash
# Print column 1 only (city names)
awk '{print $1}' cities.txt
# SYDNEY
# MELBOURNE
# BRISBANE
# PERTH

# Print columns 1 and 2
awk '{print $1, $2}' cities.txt
# SYDNEY 5.3
# MELBOURNE 5.0

# Print the entire line (same as cat)
awk '{print $0}' cities.txt
```

---

## Filter rows with a condition

```bash
# Print only the line where column 1 equals "SYDNEY"
awk '$1 == "SYDNEY"' cities.txt
# SYDNEY     5.3   5.3   1

# Print column 2 only, where column 1 equals "SYDNEY"
awk '$1 == "SYDNEY" {print $2}' cities.txt
# 5.3

# Print all cities where rank (column 4) is less than 3
awk '$4 < 3 {print $1}' cities.txt
# SYDNEY
# MELBOURNE
```

---

## Passing shell variables into awk — use `-v`

`awk` cannot read shell variables directly. You must pass them in with `-v`:

```bash
CITY="SYDNEY"
awk -v c="$CITY" '$1 == c {print $2}' cities.txt
# 5.3
```

In a script, `$1` is the argument passed in by the user:

```bash
#!/bin/bash
# User runs: ./getpop.sh SYDNEY
awk -v c="$1" '$1 == c {print $2}' cities.txt
```

---

## awk vs grep + cut — same result, one command

Both approaches below produce the same output:

```bash
# grep + cut — two commands joined by a pipe
grep "^SYDNEY " cities.txt | cut -d' ' -f2

# awk — one command does both filter and extract
awk '$1 == "SYDNEY" {print $2}' cities.txt
```

Use whichever makes more sense to you. `awk` is shorter and more reliable because it compares whole column values — it will never accidentally match `SYDNEY-NORTH` when you search for `SYDNEY`.

---

## Two-step lookup — find a value, then use it

This is the most important pattern in data analysis scripts.

**Scenario:** Find all cities that share the same population share as DARWIN.

```bash
# Step 1 — get DARWIN's population, store it
POP=$(awk '$1 == "DARWIN" {print $2}' cities.txt)
echo $POP
# 0.1

# Step 2 — find all cities with that same population
awk -v p="$POP" '$2 == p {print $1}' cities.txt | sort
# ALBANY
# DARWIN
```

This two-step pattern — **find a value, then use it to search again** — is exactly what you need in the skills test scripts.

---

## awk with CSV files (comma delimiter)

By default, `awk` splits by whitespace. For CSV files, set the delimiter with `-F`:

```bash
# Assume cities.csv with comma-separated values
awk -F, '{print $1}' cities.csv          # column 1
awk -F, '$1 == "SYDNEY" {print $2}' cities.csv
```

---

## Quick reference

| Code | Meaning |
|------|---------|
| `$0` | Entire line |
| `$1` | Column 1 |
| `$2` | Column 2 |
| `$NF` | Last column (works for any number of columns) |
| `{print $1}` | Print column 1 — runs on every line |
| `$1 == "X"` | Only run if column 1 exactly equals X |
| `-v n="$1"` | Pass shell variable `$1` into awk as `n` |
| `-F,` | Use comma as field separator (for CSV files) |

---

> 💡 **Try it now:**
> 1. `awk '{print $1}' /course/linuxgym/census/femalenames.txt | head -5`
> 2. `awk '$1 == "MARY" {print $2}' /course/linuxgym/census/femalenames.txt`
> 3. `POP=$(awk '$1 == "MARY" {print $2}' /course/linuxgym/census/femalenames.txt)` then `echo $POP`

---

← [Prev: grep](./06-grep.md) · [Next: Checking Output →](./08-check.md)
