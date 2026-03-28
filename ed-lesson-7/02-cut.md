# ✂️ Topic 2 — Extracting Columns with `cut`

> **`cut` extracts specific fields from each line of a file — like selecting a column from a table.**

← [Prev: Data Files](./01-data-files.md) · [Next: sort →](./03-sort.md)

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

File `cars.csv`:
```
Honda,18000,35.2,1
Toyota,12000,28.7,2
BMW,22000,18.1,3
```

Get only the brand names (field 1):

```bash
cut -f1 -d, cars.csv
# Honda
# Toyota
# BMW
```

Get only the prices (field 2):

```bash
cut -f2 -d, cars.csv
# 18000
# 12000
# 22000
```

Get field 1 and field 3 together:

```bash
cut -f1,3 -d, cars.csv
# Honda,35.2
# Toyota,28.7
# BMW,18.1
```

---

## Using `cut` with pipe

`cut` works on stdin too — combine it with `cat` or other commands:

```bash
cat cars.csv | cut -f1 -d,
# Honda
# Toyota
# BMW
```

```bash
grep "Honda" cars.csv | cut -f2 -d,
# 18000
```

---

## Why you need the CSV file first

If you try `cut` on a file with irregular whitespace:

```bash
cat cars.txt
# Honda       18000    35.2    1

cut -f2 -d' ' cars.txt
# (empty or wrong — multiple spaces = multiple delimiters)
```

After converting to CSV:

```bash
cut -f2 -d, cars.csv
# 18000    ✅
```

**This is why [Topic 1](./01-data-files.md) — cleaning the data — comes first.**

---

## Extracting a specific value

Combine `grep` to find the right row, then `cut` to get the column:

```bash
# What is Honda's price?
grep "Honda" cars.csv | cut -f2 -d,
# 18000

# What is BMW's rank?
grep "BMW" cars.csv | cut -f4 -d,
# 3
```

---

## Storing `cut` output in a variable

```bash
honda_price=$(grep "Honda" cars.csv | cut -f2 -d,)
echo "Honda costs $honda_price"
# Honda costs 18000
```

You will learn more about this in [Topic 5 — Inline Execution](./05-inline-execution.md).

---

## Common mistakes

**Mistake 1 — wrong delimiter:**
```bash
cut -f2 -d' ' file_with_commas.csv    ❌ wrong delimiter
cut -f2 -d, file.csv                   ✅
```

**Mistake 2 — field numbers start at 1, not 0:**
```bash
cut -f0 -d, cars.csv    ❌ field 0 does not exist
cut -f1 -d, cars.csv    ✅ first field
```

**Mistake 3 — trying to use `cut` on unclean whitespace data:**
```bash
# Always clean whitespace to commas first (Topic 1), then use cut
```

---

> 💡 **Try it now:**
> 1. Create `cars.csv` with the content above
> 2. `cut -f1 -d, cars.csv` — see only names
> 3. `cut -f2 -d, cars.csv` — see only prices
> 4. `grep "Toyota" cars.csv | cut -f2 -d,` — get Toyota's price only

---

← [Prev: Data Files](./01-data-files.md) · [Next: sort →](./03-sort.md)
