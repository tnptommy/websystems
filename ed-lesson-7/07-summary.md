# ✅ Topic 7 — Summary & Cheat Sheet

> **All commands, patterns, and workflows from Lesson 7 in one place.**

← [Prev: Putting It All Together](./06-scripts.md) · [Back to README](./README.md)

---

## The data analysis workflow — always follow this order

```
1. CLEAN    → convert whitespace to commas with Vim  :%s/\s\+/,/g
2. EXTRACT  → get the column you need with cut
3. FILTER   → find the rows you need with grep
4. SORT     → order the result with sort
5. STORE    → save a value in a variable with $()
6. COMBINE  → put it all together in a script
```

---

## Cheat Sheet

```bash
# ── CLEANING DATA (Vim) ───────────────────────────────────────
:%s/^\s\+//g           # remove leading whitespace
:%s/\s\+$//g           # remove trailing whitespace
:%s/\s\+/,/g           # replace all whitespace with commas

# ── cut ───────────────────────────────────────────────────────
cut -f1 -d, file.csv            # get field 1 (delimiter = comma)
cut -f2 -d, file.csv            # get field 2
cut -f1,3 -d, file.csv          # get fields 1 and 3
grep "X" file.csv | cut -f2 -d, # get field 2 from matching lines only

# ── sort ──────────────────────────────────────────────────────
sort file.txt                   # alphabetical A→Z
sort -r file.txt                # reverse Z→A
sort -n numbers.txt             # numeric order
sort -n -r numbers.txt          # numeric, largest first
sort -t, -k2 -n file.csv        # sort CSV by field 2 numerically

# ── grep — basic ──────────────────────────────────────────────
grep "word" file.txt            # lines containing "word"
grep "^word" file.txt           # lines STARTING with "word"
grep "word$" file.txt           # lines ENDING with "word"
grep -i "word" file.txt         # case-insensitive
grep -v "word" file.txt         # lines NOT containing "word"
grep -w "word" file.txt         # whole word match only
grep -q "word" file.txt         # quiet — no output, just sets $?
grep -l "word" *.txt            # list files that contain "word"
grep -r "word" ./folder/        # search recursively in directory

# ── grep — regular expressions ────────────────────────────────
grep '^[A-Z]' file.txt          # starts with uppercase
grep '^[A-Z][a-z]\+' file.txt   # uppercase then one or more lowercase
grep '^ABC\|^DEF' file.txt      # starts with ABC OR DEF
grep '\<word\>' file.txt        # whole word only (with boundaries)
grep '[0-9]' file.txt           # contains any digit
grep '^[^A-Z]' file.txt         # does NOT start with uppercase
# Always use single quotes around patterns with special characters

# ── inline command execution ──────────────────────────────────
var=$(command)                       # run command, store output
var=$(grep "X" file | cut -f2 -d,)  # common pattern: grep + cut

# ── grep return value ─────────────────────────────────────────
grep -q "word" file.txt
echo $?                         # 0 = found, 1 = not found

# ── combined pipelines ────────────────────────────────────────
grep "^X" file.csv | cut -f1 -d, | sort
# find rows starting with X → get column 1 → sort alphabetically

cut -f2 -d, file.csv | sort -n
# get column 2 → sort numerically
```

---

## grep regular expression reference

| Pattern | Matches |
|---------|---------|
| `^abc` | Line starts with abc |
| `abc$` | Line ends with abc |
| `\<abc\>` | Whole word abc only |
| `.` | Any single character |
| `[abc]` | One of: a, b, or c |
| `[^abc]` | Any character except a, b, c |
| `[a-z]` | Any lowercase letter |
| `[A-Z]` | Any uppercase letter |
| `[0-9]` | Any digit |
| `abc*` | ab + zero or more c |
| `abc\+` | ab + one or more c |
| `abc\|def` | abc or def |

---

## Script template for data analysis

```bash
#!/bin/bash

# 1. Check arguments
if [[ $# -ne 1 ]]; then
    echo "Usage: ./script.sh NAME" 1>&2
    exit 1
fi

name=$1
csv_file="data.csv"

# 2. Get a value from the data file
value=$(grep "^$name," $csv_file | cut -f2 -d,)

# 3. Check it was found
if [[ -z $value ]]; then
    echo "Not found: $name" 1>&2
    exit 1
fi

# 4. Use the value to find related data
grep ",$value," $csv_file | cut -f1 -d, | sort
```

---

## Read the question → know what to do

| Question says | Use this |
|---------------|----------|
| *"convert whitespace to commas"* | Vim `:%s/\s\+/,/g` |
| *"extract column N"* | `cut -fN -d, file.csv` |
| *"lines starting with X"* | `grep "^X" file` |
| *"match whole word only"* | `grep -w "word"` or `grep '\<word\>'` |
| *"lines starting with A or B"* | `grep '^A\|^B' file` |
| *"sort alphabetically"* | `sort` |
| *"sort numerically"* | `sort -n` |
| *"sort by field 2"* | `sort -t, -k2 -n` |
| *"files containing a string"* | `grep -l "word" *.txt` |
| *"store command output"* | `var=$(command)` |
| *"check if string is in file"* | `grep -q "word" file; echo $?` |
| *"get value of one row, one column"* | `grep "^NAME," file.csv \| cut -f2 -d,` |
| *"find all rows matching a value"* | `grep ",$value," file.csv` |

---

## Common mistakes in this lesson

**Mistake 1 — using `cut` before cleaning the data:**
```bash
cut -f2 -d' ' messy_file.txt    # ❌ multiple spaces = empty fields
# clean first with Vim, then use cut
```

**Mistake 2 — not anchoring grep with `^`:**
```bash
grep "ANA" names.csv         # ❌ matches SUSANA, JOANA too
grep "^ANA" names.csv        # ✅ only lines starting with ANA
```

**Mistake 3 — forgetting quotes around grep patterns:**
```bash
grep ^[A-Z] file.txt         # ❌ Bash may expand [A-Z]
grep '^[A-Z]' file.txt       # ✅ single quotes protect the pattern
```

**Mistake 4 — `$(())` vs `$()`:**
```bash
result=$((grep "X" file | cut -f2 -d,))    # ❌ arithmetic syntax
result=$(grep "X" file | cut -f2 -d,)      # ✅ command substitution
```

**Mistake 5 — not checking `$?` immediately after grep:**
```bash
grep -q "word" file.txt
echo "something"    # ❌ this resets $? to echo's exit status
echo $?             # shows wrong value

grep -q "word" file.txt
if [[ $? -eq 0 ]]; then    # ✅ check immediately after grep
```

---

## Check your work before submitting

```bash
# File exists and has content
cat ~/output.txt

# No extra blank lines
grep -c "." ~/output.txt          # count non-empty lines

# No leading/trailing spaces in output
cat ~/output.txt | grep "^ "      # should return nothing
cat ~/output.txt | grep " $"      # should return nothing

# Script works with valid input
./myscript.sh validarg

# Script handles wrong number of arguments
./myscript.sh
# should print usage/error, not crash
```

---

← [Prev: Putting It All Together](./06-scripts.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
