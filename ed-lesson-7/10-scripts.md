# 🔧 Topic 10 — Putting It All Together

> **Real examples combining everything — clean data, cut, grep, sort, awk, inline execution, and scripts.**

← [Prev: Inline Execution](./09-inline-execution.md) · [Next: Summary →](./11-summary.md)

---

## The data analysis workflow

Every data analysis task in this lesson follows the same pattern:

```
1. Clean the data         → sed or Vim (whitespace → commas)
2. Extract the column     → cut or awk
3. Filter rows            → grep or awk
4. Sort the result        → sort
5. Store values           → $()
6. Combine into a script  → bash script
```

---

## Before writing a script — understand these basics

### What is a bash script?

A bash script is a text file containing commands — the same commands you type in the terminal, saved to a file so you can run them again.

```bash
#!/bin/bash
echo "Hello"
```

The first line `#!/bin/bash` tells the system this file uses bash.

### How to create and run a script

```bash
# Step 1 — create the file
cat > ~/myscript.sh << 'EOF'
#!/bin/bash
echo "Hello from my script"
EOF

# Step 2 — make it executable (only need to do this once)
chmod +x ~/myscript.sh

# Step 3 — run it
./myscript.sh
# Hello from my script
```

### What is `chmod +x`?

`chmod` = **ch**ange **mod**e (file permissions)
`+x` = add e**x**ecute permission

Without this step, you get `Permission denied` when you try to run the script.

---

## Arguments — passing values into a script

When you run a script, you can pass values (called **arguments**) after the script name:

```bash
./myscript.sh ANA
```

Inside the script, you access them with:

| Variable | Value |
|----------|-------|
| `$1` | First argument (ANA) |
| `$2` | Second argument |
| `$#` | Total number of arguments passed |

---

## Checking the number of arguments — `$#`

Always check that the correct number of arguments was passed:

```bash
#!/bin/bash
if [[ $# -ne 1 ]]; then
    echo "Usage: ./myscript.sh NAME" 1>&2
    exit 1
fi

echo "You passed: $1"
```

```bash
./myscript.sh            # Usage: ./myscript.sh NAME
./myscript.sh ANA        # You passed: ANA
./myscript.sh ANA MARY   # Usage: ./myscript.sh NAME
```

| Code | Meaning |
|------|---------|
| `$#` | Number of arguments |
| `-ne 1` | Not equal to 1 |
| `1>&2` | Send error message to stderr (not stdout) |
| `exit 1` | Stop the script with an error |

---

## Checking if a variable is empty — `-z`

After storing a value with `$()`, check it was actually found:

```bash
value=$(grep "^$1," ~/table.csv | cut -f2 -d,)

if [[ -z $value ]]; then
    echo "Not found: $1" 1>&2
    exit 1
fi
```

| Check | Meaning |
|-------|---------|
| `[[ -z $var ]]` | True if variable IS empty |
| `[[ -n $var ]]` | True if variable is NOT empty |

---

## Script examples — practice with a fictional dataset

The following examples use a made-up `cities.csv` file:

```
SYDNEY,5.3,5.3,1
MELBOURNE,5.0,10.3,2
BRISBANE,2.5,12.8,3
PERTH,2.1,14.9,4
DARWIN,0.1,15.0,50
ALBANY,0.1,15.1,51
```

Columns: CITY, POPULATION%, CUMULATIVE, RANK

Study these examples carefully — they follow the same patterns you will need in the skills test.

---

### Example A — script that searches from start of line

**Task:** Print all lines that start with a given prefix string.

```bash
cat > ~/searchcity.sh << 'EOF'
#!/bin/bash
grep "^$1" "$2"
EOF
chmod +x ~/searchcity.sh
```

```bash
./searchcity.sh SYD cities.csv
# SYDNEY,5.3,5.3,1

./searchcity.sh BRI cities.csv
# BRISBANE,2.5,12.8,3
```

What each part does:
- `^` → anchor to start of line — only matches if the string is at the beginning
- `$1` → the prefix argument the user types in
- `"$2"` → the file argument

---

### Example B — script that looks up one column value

**Task:** Print the population (column 2) for a given city name.

```bash
cat > ~/getpop.sh << 'EOF'
#!/bin/bash
awk -v c="$1" '$1 == c {print $2}' cities.txt
EOF
chmod +x ~/getpop.sh
```

```bash
./getpop.sh SYDNEY
# 5.3
```

Alternative using grep + cut on the CSV:

```bash
cat > ~/getpop.sh << 'EOF'
#!/bin/bash
grep "^$1," cities.csv | cut -f2 -d,
EOF
chmod +x ~/getpop.sh
```

Both produce the same result. The key difference:
- `awk` compares column 1 exactly — safe with space-separated files
- `grep "^$1,"` anchors to start of line and uses the comma as a boundary — safe with CSV

---

### Example C — script that checks if a value exists in a file

**Task:** Print "found" if the city exists in the file, otherwise "not found".

```bash
cat > ~/checkcity.sh << 'EOF'
#!/bin/bash
if grep -qw "$1" cities.txt; then
    echo "found"
else
    echo "not found"
fi
EOF
chmod +x ~/checkcity.sh
```

```bash
./checkcity.sh SYDNEY      # found
./checkcity.sh LONDON      # not found
```

What each part does:
- `grep -q` → quiet — runs silently, sets exit code only
- `grep -w` → whole word — avoids matching SYDNEY inside SYDNEY-NORTH
- `if grep ...; then` → exit code 0 means found → print "found"
- `else` → exit code 1 means not found → print "not found"

---

### Example D — two-step script: find a value, then use it

**Task:** Find all cities that share the same population as a given city, sorted.

```bash
cat > ~/samepop.sh << 'EOF'
#!/bin/bash
# Step 1 — find the population of the given city
POP=$(grep "^$1," cities.csv | cut -f2 -d,)

# Step 2 — find all cities with that same population
grep ",$POP," cities.csv | cut -f1 -d, | sort
EOF
chmod +x ~/samepop.sh
```

```bash
./samepop.sh DARWIN
# ALBANY
# DARWIN
```

The same logic using awk:

```bash
cat > ~/samepop.sh << 'EOF'
#!/bin/bash
POP=$(awk -F, -v c="$1" '$1 == c {print $2}' cities.csv)
awk -F, -v p="$POP" '$2 == p {print $1}' cities.csv | sort
EOF
chmod +x ~/samepop.sh
```

---

## The complete pipeline — reading it left to right

When you see a long command, read each `|` as "then":

```bash
grep "^ANA" /course/linuxgym/census/femalenames.txt | awk '{print $1}' | sort
```

Read as:
```
Find lines starting with ANA   →   get only the name column   →   sort alphabetically
```

---

## Standard script template

Use this template for any data analysis script:

```bash
#!/bin/bash

# 1. Check the right number of arguments was passed
if [[ $# -ne 1 ]]; then
    echo "Usage: ./script.sh NAME" 1>&2
    exit 1
fi

name=$1
file="/course/linuxgym/census/femalenames.txt"
csv=~/table.csv

# 2. Get a value from the data file
value=$(awk -v n="$name" '$1 == n {print $2}' $file)

# 3. Check the value was actually found
if [[ -z $value ]]; then
    echo "Not found: $name" 1>&2
    exit 1
fi

# 4. Use the value to find related data
awk -v v="$value" '$2 == v {print $1}' $file | sort
```

---

> 💡 **Build commands step by step — never write the whole pipeline at once.**
> Test each piece first, then connect them with pipes.

---

← [Prev: Inline Execution](./09-inline-execution.md) · [Next: Summary →](./11-summary.md)
