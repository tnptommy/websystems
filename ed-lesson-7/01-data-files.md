# 📁 Topic 1 — Data Files & the Problem with Spaces

> **Real data files are messy. Before you can analyse them, you need to clean them up.**

← [Back to README](./README.md) · [Next: cut →](./02-cut.md)

---

## What does a data file look like?

Many data files are stored as plain text with columns separated by spaces or tabs.

For example, a file of car prices might look like this:

```
Honda       18000    35.2    1
Toyota      12000    28.7    2
BMW         22000    18.1    3
```

It is easy to read with your eyes — but very hard to process with `cut`.

---

## Why whitespace breaks `cut`

The `cut` command splits each line by a **delimiter** — a single character that separates fields.

If you tell `cut` the delimiter is a space, it treats **every single space** as a separator.  
Multiple spaces between columns = many empty fields between the real data.

```bash
echo "Honda       18000" | cut -f2 -d' '
# (empty — the second "field" is just another space, not the number)
```

This does not work. You need a **single consistent delimiter** between each field.

---

## The fix — replace whitespace with commas

The goal is to turn this:

```
Honda       18000    35.2    1
```

into this:

```
Honda,18000,35.2,1
```

Now `cut -d,` works perfectly.

---

## How to do it — Vim substitution

Open the file in Vim, then use a substitution command to replace all whitespace with a comma:

```
:%s/\s\+/,/g
```

Breaking it down:

| Part | Meaning |
|------|---------|
| `:%s` | Substitute across the whole file |
| `/\s\+/` | Find: one or more whitespace characters (`\s` = any whitespace, `\+` = one or more) |
| `/,/` | Replace with: a comma |
| `g` | Replace all occurrences on each line |

**Step by step:**

```bash
# Copy the file to your home directory first
cp /path/to/data.txt ~/data.txt

# Open in Vim
vim ~/data.txt

# Run the substitution (in Command Mode)
:%s/\s\+/,/g

# Save and quit
:wq
```

---

## Check the result

```bash
cat ~/data.txt
# Honda,18000,35.2,1
# Toyota,12000,28.7,2
# BMW,22000,18.1,3
```

Now each line has exactly one comma between fields — `cut` can work with this.

---

## ⚠️ Watch out for leading/trailing spaces

If the original file has spaces at the **beginning or end** of lines, the substitution will add a comma there too:

```
  Honda       18000    35.2    1  
```

becomes:

```
,Honda,18000,35.2,1,
```

**Fix — remove leading/trailing whitespace first in Vim:**

```
:%s/^\s\+//g       ← remove whitespace at start of each line
:%s/\s\+$//g       ← remove whitespace at end of each line
:%s/\s\+/,/g       ← then replace internal whitespace with commas
```

Or combine the internal replacement after trimming:

```
:%s/\s\+/,/g
```

Then check the first and last few lines:

```bash
head -3 data.txt
tail -3 data.txt
```

---

## Why save as `.csv`?

CSV stands for **comma-separated values** — a standard format for structured data.  
Naming your cleaned file `data.csv` makes it clear what format it is in.

```bash
cp ~/data.txt ~/data.csv
```

Or clean it directly into a new file.

---

> 💡 **Try it now:**
> 1. Create a test file: `echo -e "Honda       18000\nToyota      12000" > test.txt`
> 2. Open in Vim: `vim test.txt`
> 3. Run `:%s/\s\+/,/g` then `:wq`
> 4. Check: `cat test.txt` — should show `Honda,18000` and `Toyota,12000`

---

← [Back to README](./README.md) · [Next: cut →](./02-cut.md)
