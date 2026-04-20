# 📁 Topic 1 — Data Files & the Problem with Spaces

> **Real data files are messy. Before you can analyse them, you need to clean them up.**

← [Back to README](./README.md) · [Next: sed →](./02-sed.md)

---

## What does a data file look like?

Many data files are stored as plain text with columns separated by spaces or tabs.

For example, a file of female names might look like this:

```
MARY       2.629   2.629    1
PATRICIA   1.073   3.702    2
LINDA      1.035   4.736    3
```

Columns: NAME, FREQUENCY, CUMULATIVE FREQUENCY, RANK

It is easy to read with your eyes — but very hard to process with `cut`.

---

## Why whitespace breaks `cut`

The `cut` command splits each line by a **delimiter** — a single character that separates fields.

If you tell `cut` the delimiter is a space, it treats **every single space** as a separator.
Multiple spaces between columns = many empty fields between the real data.

```bash
echo "MARY       2.629" | cut -f2 -d' '
# (empty — the second "field" is just another space, not the number)
```

This does not work. You need a **single consistent delimiter** between each field.

---

## The fix — replace whitespace with commas

The goal is to turn this:

```
MARY       2.629   2.629    1
```

into this:

```
MARY,2.629,2.629,1
```

Now `cut -d,` works perfectly.

---

## Method 1 — Fix it in Vim

Open the file in Vim, then use a substitution command:

```
:%s/\s\+/,/g
```

Breaking it down:

| Part | Meaning |
|------|---------|
| `:%s` | Substitute across the whole file |
| `/\s\+/` | Find: one or more whitespace characters |
| `/,/` | Replace with: a comma |
| `g` | Replace all occurrences on each line |

Step by step:

```bash
# Copy the file to your home directory first
cp /course/linuxgym/census/femalenames.txt ~/table.csv

# Open in Vim
vim ~/table.csv

# Run the substitution (in Command Mode — press : first)
:%s/\s\+/,/g

# Save and quit
:wq
```

---

## Method 2 — Fix it with `sed` (no Vim needed)

```bash
sed 's/\s\+/,/g' /course/linuxgym/census/femalenames.txt > ~/table.csv
```

One command — same result. You will learn `sed` in detail in [Topic 2](./02-sed.md).

---

## Watch out for leading and trailing spaces

If the original file has spaces at the **start or end** of lines:

```
  MARY       2.629   2.629    1  
```

A simple replacement gives:

```
,MARY,2.629,2.629,1,
```

Fix — remove leading and trailing whitespace first in Vim:

```
:%s/^\s\+//g       ← remove whitespace at START of each line
:%s/\s\+$//g       ← remove whitespace at END of each line
:%s/\s\+/,/g       ← then replace internal whitespace with commas
```

Then check the result:

```bash
head -3 ~/table.csv
tail -3 ~/table.csv
```

---

## Check the result

```bash
cat ~/table.csv
# MARY,2.629,2.629,1
# PATRICIA,1.073,3.702,2
# LINDA,1.035,4.736,3
```

Now each line has exactly one comma between fields — `cut` can work with this.

---

## Why name it `.csv`?

CSV stands for **comma-separated values** — a standard format for structured data.
Naming your cleaned file `table.csv` makes it clear what format it is in.

---

> 💡 **Try it now:**
> 1. `cp /course/linuxgym/census/femalenames.txt ~/table.csv`
> 2. `vim ~/table.csv` then run `:%s/\s\+/,/g` then `:wq`
> 3. Check: `head -3 ~/table.csv`

---

← [Back to README](./README.md) · [Next: sed →](./02-sed.md)
