# 🔍 Topic 6 — Pattern Matching with `grep`

> **`grep` finds lines that match a pattern — and with regular expressions, the patterns are very powerful.**

← [Prev: sort](./05-sort.md) · [Next: awk →](./07-awk.md)

---

## What is `grep`?

`grep` reads a file line by line and **prints every line that matches your pattern**.

```bash
grep "MARY" table.csv
# MARY,2.629,2.629,1    ← this line contains "MARY" — printed
# PATRICIA,1.073...     ← no "MARY" — skipped
```

---

## Basic usage

```bash
grep "pattern" filename          # search in a file
cat filename | grep "pattern"    # search from a pipe
```

---

## Regular expressions — matching patterns, not just exact words

### `^` — match start of line

```bash
grep "^MARY" table.csv      # lines that START with MARY
```

Without `^`:
```bash
grep "ANA" table.csv
# ANA,0.120,...         ← matches
# ANASTASIA,0.010,...   ← also matches (ANA is inside ANASTASIA)
# JOANA,...             ← also matches (ANA is at the end)
```

With `^`:
```bash
grep "^ANA" table.csv
# ANA,0.120,...         ← only lines starting with ANA ✅
# ANASTASIA,...         ← also matches (starts with ANA) ✅
# JOANA,...             ← NOT matched ✅
```

---

### `$` — match end of line

```bash
grep "1$" table.csv         # lines ending with the number 1
grep ",$" table.csv         # lines ending with a comma
```

---

### `-w` and `\< \>` — match whole words only

```bash
grep "Ann" names.txt
# Ann        ← matches
# Annette    ← also matches (Ann is inside Annette)

grep -w "Ann" names.txt
# Ann        ← whole word only ✅
# Annette    ← NOT matched ✅

# Same result using word boundaries:
grep '\<Ann\>' names.txt
```

---

### `\|` — match either pattern (OR)

```bash
grep "^NAT\|^MAT" femalenames.txt
# lines starting with NAT OR MAT

grep "Honda\|Toyota" cars.csv
# lines containing Honda OR Toyota
```

With `-E` (Extended regex) — cleaner syntax:
```bash
grep -E "^(NAT|MAT)" femalenames.txt
```

---

### `[abc]` — match one character from a set

```bash
grep "^[HT]" table.csv     # lines starting with H or T
grep "[0-9]" file.txt      # lines containing any digit
grep "^[A-Z]" file.txt     # lines starting with any uppercase letter
```

### `[^abc]` — match any character NOT in the set

```bash
grep "^[^A-Z]" file.txt    # lines that do NOT start with uppercase
```

---

### `.` `*` `\+` — repetition

| Pattern | Matches |
|---------|---------|
| `.` | Any single character |
| `a*` | Zero or more `a` |
| `a\+` | One or more `a` |

```bash
grep "^[A-Z]\+" names.txt    # one or more uppercase letters at start
```

---

## Useful grep options

| Option | What it does | Example |
|--------|-------------|---------|
| `-i` | Case-insensitive match | `grep -i "mary" file.csv` |
| `-w` | Whole word match only | `grep -w "Ann" names.txt` |
| `-v` | Invert — lines that do NOT match | `grep -v "MARY" file.csv` |
| `-l` | List filenames only (not matching lines) | `grep -l "Anne" *.txt` |
| `-r` | Search recursively in all subdirectories | `grep -r "Anne" ./gutenberg/` |
| `-q` | Quiet — no output, just sets exit status | `grep -q "MARY" file.csv` |
| `-E` | Extended regex — cleaner OR syntax | `grep -E "^(NAT|MAT)" file` |
| `--color` | Highlight the matched part | `grep --color "MARY" file.csv` |

---

## The return value of `grep`

`grep` sets a **return value** after running:

| Return value | Meaning |
|-------------|---------|
| `0` | Match found |
| `1` | No match found |

Check it with `$?` immediately after running grep:

```bash
grep "MARY" table.csv
echo $?
# 0    ← found

grep "FAKENAME" table.csv
echo $?
# 1    ← not found
```

This is very useful in scripts:

```bash
grep -q "MARY" table.csv    # -q = quiet, no output
if [[ $? -eq 0 ]]; then
    echo "found"
else
    echo "not found"
fi
```

---

## Searching multiple files

```bash
grep "Anne" *.txt            # search all .txt files in current directory
grep -l "Anne" *.txt         # list which files contain Anne
grep -r "Anne" ./gutenberg/  # search all files in gutenberg folder
```

---

## Always quote your pattern

When using special characters in grep, wrap the pattern in **single quotes**:

```bash
grep '^[A-Z]' names.txt       # ✅ single quotes — Bash leaves it alone
grep ^[A-Z] names.txt         # ❌ Bash may try to expand [A-Z] itself
```

---

> 💡 **Try it now:**
> 1. `grep "^ANA" /course/linuxgym/census/femalenames.txt` — names starting with ANA
> 2. `grep -w "ANA" /course/linuxgym/census/femalenames.txt` — only the exact word ANA
> 3. `grep -E "^(NAT|MAT)" /course/linuxgym/census/femalenames.txt` — NAT or MAT
> 4. `grep -rl "Anne" /course/linuxgym/gutenberg/` — files containing Anne

---

← [Prev: sort](./05-sort.md) · [Next: awk →](./07-awk.md)
