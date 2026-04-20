# ✂️ Topic 4 — Extracting Columns with `cut`

> **`cut` extracts specific fields from each line of a file — like selecting a column from a spreadsheet.**

← [Prev: tr](./03-tr.md) · [Next: sort →](./05-sort.md)

---

## What does `cut` do?

`cut` reads each line and prints only the **field(s) you specify**.

Think of it like highlighting one column in a spreadsheet — you see only that column, for every row.

---

## Basic syntax

```bash
cut -f FIELD_NUMBER -d DELIMITER filename
```

| Option | Meaning |
|--------|---------|
| `-f N` | Print field number N (counting from 1) |
| `-d X` | Use X as the delimiter between fields |

---

## Simple example

File `table.csv`:
```
MARY,2.629,2.629,1
PATRICIA,1.073,3.702,2
LINDA,1.035,4.736,3
```

Get only the names (field 1):

```bash
cut -f1 -d, table.csv
# MARY
# PATRICIA
# LINDA
```

Get only the frequencies (field 2):

```bash
cut -f2 -d, table.csv
# 2.629
# 1.073
# 1.035
```

Get fields 1 and 3 together:

```bash
cut -f1,3 -d, table.csv
# MARY,2.629
# PATRICIA,3.702
# LINDA,4.736
```

---

## Using `cut` with a pipe

`cut` works on stdin too — chain it after `grep` or other commands:

```bash
# Get all names from the CSV
cat table.csv | cut -f1 -d,

# Get the frequency of MARY only
grep "^MARY," table.csv | cut -f2 -d,
# 2.629
```

---

## Why you must clean the file first

If you try `cut` on a file with irregular whitespace:

```bash
cut -f2 -d' ' femalenames.txt
# (empty or wrong — multiple spaces = multiple delimiters)
```

After converting to CSV with `sed`:

```bash
cut -f2 -d, table.csv
# 2.629   ✅
```

**This is why Topics 1–3 come before this one — always clean first.**

---

## Extracting a specific value

Combine `grep` to find the right row, then `cut` to get the column:

```bash
# What is the frequency of ANA?
grep "^ANA," ~/table.csv | cut -f2 -d,
# 0.120

# What is the rank of MARY?
grep "^MARY," ~/table.csv | cut -f4 -d,
# 1
```

---

## Storing `cut` output in a variable

```bash
freq=$(grep "^ANA," ~/table.csv | cut -f2 -d,)
echo "ANA frequency: $freq"
# ANA frequency: 0.120
```

You will learn more about this in [Topic 9 — Inline Execution](./09-inline-execution.md).

---

## Common mistakes

**Mistake 1 — wrong delimiter:**
```bash
cut -f2 -d' ' file.csv    # ❌ wrong delimiter for a CSV
cut -f2 -d, file.csv       # ✅ comma delimiter
```

**Mistake 2 — field numbers start at 1, not 0:**
```bash
cut -f0 -d, table.csv    # ❌ field 0 does not exist
cut -f1 -d, table.csv    # ✅ first field
```

**Mistake 3 — trying to use `cut` on unclean whitespace data:**
```bash
# Always clean whitespace to commas first (Topics 1–3), then use cut
sed 's/\s\+/,/g' femalenames.txt > table.csv
cut -f2 -d, table.csv    # ✅ now it works
```

---

> 💡 **Try it now:**
> 1. `cut -f1 -d, ~/table.csv | head -5` — see only names
> 2. `cut -f2 -d, ~/table.csv | head -5` — see only frequencies
> 3. `grep "^ANA," ~/table.csv | cut -f2 -d,` — get ANA's frequency

---

← [Prev: tr](./03-tr.md) · [Next: sort →](./05-sort.md)
