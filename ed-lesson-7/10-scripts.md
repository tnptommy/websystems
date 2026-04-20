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

## Script examples — skills test questions

---

### Q4 — searchprefix.sh

**Task:** Print all lines that START with a given string.

```bash
cat > ~/searchprefix.sh << 'EOF'
#!/bin/bash
grep "^$1" "$2"
EOF
chmod +x ~/searchprefix.sh
```

```bash
./searchprefix.sh ANA /course/linuxgym/census/femalenames.txt
# ANA            0.120 55.989    181
# ANASTASIA      0.010 81.026    907
# ANABEL         0.004 85.078   1569
```

What each part does:
- `^$1` → start of line (`^`) + first argument (the prefix)
- `"$2"` → second argument (the file)

---

### Q8 — namefreq.sh

**Task:** Print the frequency (column 2) for a given name.

```bash
cat > ~/namefreq.sh << 'EOF'
#!/bin/bash
awk -v n="$1" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt
EOF
chmod +x ~/namefreq.sh
```

```bash
./namefreq.sh ANA
# 0.120
```

Alternative using grep + cut:

```bash
cat > ~/namefreq.sh << 'EOF'
#!/bin/bash
grep "^$1," ~/table.csv | cut -f2 -d,
EOF
chmod +x ~/namefreq.sh
```

---

### Q9 — gender.sh

**Task:** Print "female" if the name is in femalenames.txt, otherwise "male".

```bash
cat > ~/gender.sh << 'EOF'
#!/bin/bash
if grep -qw "$1" /course/linuxgym/census/femalenames.txt; then
    echo "female"
else
    echo "male"
fi
EOF
chmod +x ~/gender.sh
```

```bash
./gender.sh MARY     # female
./gender.sh JAMES    # male
```

What each part does:
- `grep -q` → quiet mode — no output, just sets exit status
- `grep -w` → whole word — avoids matching ANA inside ANASTASIA
- `if grep ...; then` → if grep found something (exit code 0) → female
- `else` → not found → male

---

### Q10 — samefreq.sh

**Task:** Print all names with the same frequency as the given name, sorted.

```bash
cat > ~/samefreq.sh << 'EOF'
#!/bin/bash
FREQ=$(awk -v n="$1" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt)
awk -v f="$FREQ" '$2 == f {print $1}' /course/linuxgym/census/femalenames.txt | sort
EOF
chmod +x ~/samefreq.sh
```

```bash
./samefreq.sh ANA
# ANA
# RENEE
```

Alternative using table.csv:

```bash
cat > ~/samefreq.sh << 'EOF'
#!/bin/bash
FREQ=$(grep "^$1," ~/table.csv | cut -f2 -d,)
grep ",$FREQ," ~/table.csv | cut -f1 -d, | sort
EOF
chmod +x ~/samefreq.sh
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
