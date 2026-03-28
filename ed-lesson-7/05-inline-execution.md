# ⚡ Topic 5 — Inline Command Execution

> **Store the output of a command in a variable — so you can use it later in the same script.**

← [Prev: grep](./04-grep.md) · [Next: Putting It All Together →](./06-scripts.md)

---

## The problem this solves

Imagine you want to:
1. Find what a value is (e.g. a price from a data file)
2. Use that value later in the same script

Without inline execution, you would have to:
- Run the command
- Read the output by eye
- Type it manually into the next command

Inline execution lets you **capture command output directly into a variable**.

---

## Two syntaxes — both do the same thing

### Syntax 1 — backticks `` ` ` ``

```bash
variable=`command`
```

Example:

```bash
line_count=`wc -l cars.csv`
echo "The file has $line_count lines"
```

### Syntax 2 — `$()` (recommended)

```bash
variable=$(command)
```

Example:

```bash
line_count=$(wc -l cars.csv)
echo "The file has $line_count lines"
```

**Both produce the same result.** Use `$()` — it is easier to read and does not get confused with single quotes `'`.

---

## Why backticks can cause confusion

```bash
count=`wc -l file.txt`    # backtick — easy to mistake for ' single quote
count=$(wc -l file.txt)   # $() — clearly a command substitution ✅
```

You will see backticks in old scripts — you need to recognise them.  
For any new script you write, use `$()`.

---

## Do not confuse `$()` with `$(( ))`

They look similar but do very different things:

| Syntax | What it does | Example |
|--------|-------------|---------|
| `$(command)` | **Run a command**, capture its output | `$(wc -l file.txt)` |
| `$(( expression ))` | **Arithmetic** — calculate a number | `$(( 5 + 3 ))` |

```bash
lines=$(wc -l cars.csv)     # runs wc, stores the output
total=$(( 5 + 3 ))          # calculates 8, stores 8
```

---

## Simple example — count lines

```bash
#!/bin/bash

count=$(wc -l cars.csv)
echo "There are $count lines in the file"
```

---

## Practical example — get a value from a data file

```bash
#!/bin/bash

# Get Honda's price from the CSV file
honda_price=$(grep "Honda" cars.csv | cut -f2 -d,)

echo "Honda costs $honda_price dollars"
# Honda costs 18000 dollars
```

**What happens step by step:**

```
grep "Honda" cars.csv     → Honda,18000,35.2,1
             |
cut -f2 -d,               → 18000
             |
$(...)                    → stored in honda_price
             |
echo                      → Honda costs 18000 dollars
```

---

## Using the stored value in the next command

Once you have a value in a variable, use it in another command:

```bash
#!/bin/bash

# Find Honda's price
target_price=$(grep "Honda" cars.csv | cut -f2 -d,)

echo "Looking for other cars at the same price: $target_price"

# Now find all cars with that same price
grep ",$target_price," cars.csv | cut -f1 -d,
```

This is the core pattern for data analysis tasks — **find a value, then use it to search further**.

---

## Nested inline execution

You can put inline execution inside strings:

```bash
echo "File has $(wc -l cars.csv) lines"
echo "Today is $(date)"
echo "You are: $(whoami)"
```

---

## Full script example

```bash
#!/bin/bash

# Script: find cars with the same rank category

car=$1
csv_file="cars.csv"

# Get the rank of the specified car
rank=$(grep "$car" $csv_file | cut -f4 -d,)

echo "$car has rank: $rank"
echo "Other cars in the same rank range:"

# Find all cars near the same rank
grep ",$rank$" $csv_file | cut -f1 -d,
```

Run it:

```bash
./find_rank.sh Honda
# Honda has rank: 1
# Other cars in the same rank range:
# Honda
```

---

> 💡 **Try it now:**
> 1. `today=$(date)` then `echo "Today: $today"`
> 2. `count=$(ls | wc -l)` then `echo "Files in current dir: $count"`
> 3. Write a script that stores the output of any command in a variable and prints it

---

← [Prev: grep](./04-grep.md) · [Next: Putting It All Together →](./06-scripts.md)
