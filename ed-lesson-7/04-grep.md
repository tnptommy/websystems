# 🔍 Topic 4 — Pattern Matching with `grep`

> **`grep` finds lines that match a pattern — and with regular expressions, the patterns are very powerful.**

← [Prev: sort](./03-sort.md) · [Next: Inline Execution →](./05-inline-execution.md)

---

## What is `grep`?

`grep` reads a file line by line and **prints every line that matches your pattern**.

```bash
grep "Honda" cars.txt
# Honda,18000,35.2,1    ← this line contains "Honda" — printed
# Toyota,12000...       ← no "Honda" — skipped
# BMW,22000...          ← no "Honda" — skipped
```

---

## Basic usage

```bash
grep "pattern" filename          # search in a file
cat filename | grep "pattern"    # search from stdin (pipe)
```

---

## Regular expressions — matching more than just exact words

Regular expressions (regex) let you match **patterns** instead of just fixed text.

### `^` — match start of line

```bash
grep "^Honda" cars.csv      # lines that START with Honda
grep "^[A-Z]" names.txt     # lines that start with an uppercase letter
```

Without `^`:
```bash
grep "Honda" cars.csv
# Honda,18000,35.2,1    ← matches (Honda at start)
# OldHonda,9000,5.1,9  ← also matches! (Honda anywhere in line)
```

With `^`:
```bash
grep "^Honda" cars.csv
# Honda,18000,35.2,1    ← only this (Honda at START of line) ✅
```

---

### `$` — match end of line

```bash
grep "txt$" filelist.txt    # lines ending with "txt"
grep ",$" data.csv          # lines ending with a comma
```

---

### `\<` and `\>` — match whole words only

```bash
grep "Ann" names.txt
# Ann         ← matches
# Annette     ← also matches (Ann is inside Annette) — may not want this

grep "\<Ann\>" names.txt
# Ann         ← matches whole word only ✅
# Annette     ← NOT matched
```

---

### `.` — match any single character

```bash
grep "B.W" cars.txt
# BMW    ← B + any character + W ✅
# BXW    ← also matches
```

---

### `[abc]` — match one character from a set

```bash
grep "^[HT]" cars.csv      # lines starting with H or T
# Honda,18000,35.2,1
# Toyota,12000,28.7,2

grep "[aeiou]" names.txt    # lines containing a vowel
```

### `[^abc]` — match any character NOT in the set

```bash
grep "^[^A-Z]" file.txt    # lines that do NOT start with uppercase
```

### `[a-z]` `[A-Z]` `[0-9]` — ranges

```bash
grep "^[A-Z]" names.txt        # starts with any uppercase letter
grep "[0-9]" data.txt          # contains any digit
grep "^[A-Z][a-z]" names.txt   # starts with uppercase then lowercase
```

---

### `*` and `\+` — repetition

| Pattern | Matches |
|---------|---------|
| `a*` | Zero or more `a` characters: `""`, `"a"`, `"aa"`, `"aaa"` |
| `a\+` | One or more `a` characters: `"a"`, `"aa"`, `"aaa"` |
| `ab*c` | `ac`, `abc`, `abbc`, `abbbc` |
| `ab\+c` | `abc`, `abbc`, `abbbc` (NOT `ac` — needs at least one b) |

```bash
grep "^[A-Z]\+" names.txt    # lines starting with one or more uppercase letters
```

---

### `string1\|string2` — match either pattern

```bash
grep "Honda\|Toyota" cars.csv
# Honda,18000,35.2,1
# Toyota,12000,28.7,2

grep "^NAT\|^MAT" names.txt    # lines starting with NAT or MAT
```

---

## Always quote your pattern

When using special characters in grep, **wrap the pattern in single quotes** to stop Bash from interpreting them:

```bash
grep '^[A-Z]' names.txt       ✅ single quotes — Bash leaves it alone
grep ^[A-Z] names.txt         ❌ Bash may try to expand [A-Z] itself
```

---

## Useful grep options

| Option | What it does | Example |
|--------|-------------|---------|
| `-i` | Case-insensitive match | `grep -i "honda" cars.csv` |
| `-w` | Match whole word only | `grep -w "Ann" names.txt` |
| `-l` | List only filenames (not matching lines) | `grep -l "Honda" *.txt` |
| `-r` | Search recursively in all subdirectories | `grep -r "Honda" .` |
| `-v` | Invert — show lines that do NOT match | `grep -v "Honda" cars.csv` |
| `-q` | Quiet — no output, just return value | `grep -q "Honda" cars.csv` |
| `--color` | Highlight the matched part in colour | `grep --color "Honda" cars.csv` |

---

## The return value of `grep`

`grep` sets a **return value** after running:

| Return value | Meaning |
|-------------|---------|
| `0` | Match found |
| `1` | No match found |

Check it with `$?` immediately after running grep:

```bash
grep "Honda" cars.csv
echo $?
# 0    ← found

grep "Ferrari" cars.csv
echo $?
# 1    ← not found
```

**This is very useful in scripts:**

```bash
grep -q "Honda" cars.csv    # -q = quiet, no output
if [[ $? -eq 0 ]]; then
    echo "Honda found"
else
    echo "Honda not found"
fi
```

---

## Searching multiple files

```bash
grep "Honda" *.csv           # search all .csv files
grep -l "Honda" *.csv        # list which files contain Honda
grep -r "Honda" ./data/      # search all files inside ./data/ recursively
```

---

> 💡 **Try it now:**
> 1. `grep "^H" cars.csv` — lines starting with H
> 2. `grep "\<Honda\>" cars.csv` — only the whole word Honda
> 3. `grep "Honda\|BMW" cars.csv` — lines with Honda OR BMW
> 4. `grep -q "Ferrari" cars.csv; echo $?` — check return value

---

← [Prev: sort](./03-sort.md) · [Next: Inline Execution →](./05-inline-execution.md)
