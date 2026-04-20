# ✅ Topic 11 — Summary & Cheat Sheet

> **All commands, patterns, and workflows from Lesson 7 in one place.**

← [Prev: Putting It All Together](./10-scripts.md) · [Back to README](./README.md)

---

## Topic order — read in this sequence

| # | Topic | What you learn |
|---|-------|----------------|
| 1 | [Data Files & the Problem with Spaces](./01-data-files.md) | Why whitespace breaks `cut`, how to fix with Vim |
| 2 | [Cleaning Data with `sed`](./02-sed.md) | Replace whitespace with commas — no Vim needed |
| 3 | [Character Replacement with `tr`](./03-tr.md) | Simple character swapping and deletion |
| 4 | [Extracting Columns with `cut`](./04-cut.md) | Get specific fields from structured data |
| 5 | [Sorting with `sort`](./05-sort.md) | Alphabetical, numeric, reverse, by field |
| 6 | [Pattern Matching with `grep`](./06-grep.md) | Search rows, regex, anchors, options |
| 7 | [Column Processing with `awk`](./07-awk.md) | Filter AND extract in one command |
| 8 | [Checking Output with `wc`, `head`, `tail`](./08-check.md) | Verify your results before submitting |
| 9 | [Inline Command Execution](./09-inline-execution.md) | Store command output in variables with `$()` |
| 10 | [Putting It All Together — Scripts](./10-scripts.md) | Combine everything into working scripts |
| 11 | [Summary & Cheat Sheet](./11-summary.md) | This file — all commands in one place |

---

## The data analysis workflow — always follow this order

```
1. CLEAN    → remove whitespace with Vim, sed, or tr
2. EXTRACT  → get the column you need with cut or awk
3. FILTER   → find the rows you need with grep or awk
4. SORT     → order the result with sort
5. STORE    → save a value in a variable with $()
6. COMBINE  → put it all together in a script
```

---

## Cheat Sheet

```bash
# ── CLEANING DATA — Vim ───────────────────────────────────────
:%s/^\s\+//g           # remove leading whitespace
:%s/\s\+$//g           # remove trailing whitespace
:%s/\s\+/,/g           # replace all whitespace with commas

# ── CLEANING DATA — sed (use this in scripts) ─────────────────
sed 's/\s\+/,/g' file.txt > file.csv     # whitespace → comma, save to new file
sed 's/^\s\+//' file.txt                 # remove leading whitespace
sed 's/\s\+$//' file.txt                 # remove trailing whitespace
sed '/^$/d' file.txt                     # delete blank lines
sed -n '/^ANA/p' file.txt               # print only matching lines

# ── CLEANING DATA — tr ────────────────────────────────────────
tr -s ' ' ',' < file.txt                 # squeeze spaces → replace with comma
tr -d '\n' < file.txt                    # delete all newlines
cat file.txt | tr -s ' ' ',' > file.csv  # pipe version

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
grep -E '^(ABC|DEF)' file.txt   # same thing using Extended regex
grep '\<word\>' file.txt        # whole word only (with boundaries)
grep '[0-9]' file.txt           # contains any digit
grep '^[^A-Z]' file.txt         # does NOT start with uppercase
# Always use single quotes around patterns with special characters

# ── awk ───────────────────────────────────────────────────────
awk '{print $1}' file.txt                    # print column 1 of every line
awk '{print $1, $2}' file.txt               # print columns 1 and 2
awk '$1 == "ANA" {print $2}' file.txt       # find row, print column 2
awk -v n="$1" '$1 == n {print $2}' file     # pass shell variable into awk
awk -v f="$FREQ" '$2 == f {print $1}' file  # filter by column 2 value

# ── wc / head / tail ─────────────────────────────────────────
wc -l file.txt                  # count number of lines
head file.txt                   # first 10 lines
head -5 file.txt                # first 5 lines
tail file.txt                   # last 10 lines
tail -5 file.txt                # last 5 lines
tail -n +2 file.txt             # everything except the first line (skip header)

# ── inline command execution ──────────────────────────────────
var=$(command)                       # run command, store output
var=$(grep "X" file | cut -f2 -d,)  # common pattern: grep + cut
var=$(awk -v n="$1" '$1==n{print $2}' file)  # common pattern: awk

# ── grep return value ─────────────────────────────────────────
grep -q "word" file.txt
echo $?                         # 0 = found, 1 = not found

# ── argument checking in scripts ─────────────────────────────
$#                              # number of arguments passed to script
$1, $2, $3                      # argument 1, 2, 3 ...
[[ $# -ne 1 ]]                  # true if NOT exactly 1 argument
[[ -z $var ]]                   # true if variable IS empty
[[ -n $var ]]                   # true if variable is NOT empty
chmod +x script.sh              # make script executable (required once)

# ── combined pipelines ────────────────────────────────────────
grep "^X" file.csv | cut -f1 -d, | sort
# find rows starting with X → get column 1 → sort alphabetically

cut -f2 -d, file.csv | sort -n
# get column 2 → sort numerically

grep -rl "word" ./folder/ | sort
# find all files containing "word" → sort by filename
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

## awk quick reference

| Code | Meaning |
|------|---------|
| `$0` | The entire line |
| `$1` | Column 1 |
| `$2` | Column 2 |
| `$NF` | Last column (works for any number of columns) |
| `{print $1}` | Print column 1 — runs on every line |
| `$1 == "X"` | Only run if column 1 equals X |
| `-v n="$1"` | Pass a shell variable into awk |

---

## sed vs Vim vs tr — which to use?

| Situation | Use |
|-----------|-----|
| One-off fix while working in a file | Vim |
| Inside a script or one-liner in terminal | `sed` |
| Simple single-character replacement | `tr` |
| Need to save to a new file | `sed 's/.../.../' file > newfile` |
| Need to edit the same file directly | `sed -i 's/.../.../' file` |

---

## grep vs awk vs cut — which to use?

| Situation | Use |
|-----------|-----|
| Find rows matching a pattern | `grep` |
| Extract a column from a CSV | `cut` |
| Find a row AND extract a column | `awk` (does both in one step) |
| Match whole word only | `grep -w` |
| Pass a variable into a search | `awk -v n="$var"` |

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
| *"convert whitespace to commas"* | `sed 's/\s\+/,/g' file > file.csv` or Vim `:%s/\s\+/,/g` |
| *"extract column N"* | `cut -fN -d, file.csv` or `awk '{print $N}' file` |
| *"lines starting with X"* | `grep "^X" file` |
| *"match whole word only"* | `grep -w "word"` or `grep '\<word\>'` |
| *"lines starting with A or B"* | `grep '^A\|^B' file` or `grep -E '^(A\|B)' file` |
| *"sort alphabetically"* | `sort` |
| *"sort numerically"* | `sort -n` |
| *"sort by field 2"* | `sort -t, -k2 -n` |
| *"files containing a string"* | `grep -rl "word" ./folder/` |
| *"store command output"* | `var=$(command)` |
| *"check if string is in file"* | `grep -q "word" file` then check `$?` |
| *"get value of one row, one column"* | `grep "^NAME," file.csv \| cut -f2 -d,` or `awk '$1=="NAME"{print $2}' file` |
| *"find all rows matching a value"* | `grep ",$value," file.csv` or `awk -v f="$value" '$2==f' file` |
| *"print female or male"* | `grep -qw "$1" file && echo "female" \|\| echo "male"` |
| *"count lines in file"* | `wc -l file` |
| *"check variable is not empty"* | `[[ -n $var ]]` |
| *"check variable is empty"* | `[[ -z $var ]]` |
| *"how many arguments passed?"* | `$#` |

---

## Common mistakes in this lesson

**Mistake 1 — using `cut` before cleaning the data:**
```bash
cut -f2 -d' ' messy_file.txt    # ❌ multiple spaces = empty fields
sed 's/\s\+/,/g' messy_file.txt > file.csv
cut -f2 -d, file.csv            # ✅ clean first, then cut
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
result=$((grep "X" file | cut -f2 -d,))    # ❌ arithmetic syntax — wrong
result=$(grep "X" file | cut -f2 -d,)      # ✅ command substitution — correct
```

**Mistake 5 — not checking `$?` immediately after grep:**
```bash
grep -q "word" file.txt
echo "something"             # ❌ echo resets $? — you lose the grep result
echo $?                      # shows echo's exit status, not grep's

grep -q "word" file.txt
if [[ $? -eq 0 ]]; then      # ✅ check $? immediately after grep
```

**Mistake 6 — forgetting `chmod +x` on scripts:**
```bash
./myscript.sh                # ❌ Permission denied
chmod +x myscript.sh
./myscript.sh                # ✅ now it runs
```

**Mistake 7 — using awk variable without `-v`:**
```bash
name="ANA"
awk '$1 == name {print $2}' file     # ❌ awk does not see shell variable "name"
awk -v n="$name" '$1 == n {print $2}' file  # ✅ use -v to pass it in
```

**Mistake 8 — not checking if variable is empty after grep/cut:**
```bash
value=$(grep "^TYPO," file.csv | cut -f2 -d,)
grep ",$value," file.csv    # ❌ value is empty — grep matches everything

if [[ -z $value ]]; then    # ✅ check first
    echo "Not found"
    exit 1
fi
```

---

## Check your work before submitting

```bash
# 1. File exists and has content
cat ~/output.txt

# 2. Correct number of lines — compare with original
wc -l ~/output.txt
wc -l /course/linuxgym/census/femalenames.txt

# 3. No extra blank lines
grep -c "." ~/output.txt

# 4. Preview top and bottom
head -3 ~/output.txt
tail -3 ~/output.txt

# 5. No leading/trailing spaces
grep '^ ' ~/output.txt     # should return nothing
grep ' $' ~/output.txt     # should return nothing

# 6. Script works with valid input
./myscript.sh validarg

# 7. Script handles wrong number of arguments
./myscript.sh              # should print usage/error, not crash
```

---

← [Prev: Putting It All Together](./10-scripts.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
