# 🔤 Topic 3 — Sorting with `sort`

> **`sort` puts lines in order — alphabetically, numerically, or by a specific field.**

← [Prev: cut](./02-cut.md) · [Next: grep →](./04-grep.md)

---

## Basic sort — alphabetical order

By default, `sort` arranges lines in **alphabetical order**:

```bash
cat cars.txt
# Honda
# Toyota
# BMW

cat cars.txt | sort
# BMW
# Honda
# Toyota
```

Or directly on a file:

```bash
sort cars.txt
# BMW
# Honda
# Toyota
```

---

## Useful `sort` options

| Option | What it does | Example |
|--------|-------------|---------|
| (none) | Alphabetical A→Z | `sort file.txt` |
| `-r` | Reverse order (Z→A or largest→smallest) | `sort -r file.txt` |
| `-n` | Numeric order (treat values as numbers) | `sort -n numbers.txt` |
| `-k N` | Sort by field number N | `sort -k2 file.txt` |
| `-t X` | Use X as field delimiter with `-k` | `sort -t, -k2 file.csv` |

---

## Why `-n` matters for numbers

Without `-n`, sort compares numbers as **text**, which gives wrong results:

```bash
cat numbers.txt
# 100
# 20
# 9
# 3

sort numbers.txt
# 100    ← "1" comes before "2" and "9" alphabetically — wrong!
# 20
# 3
# 9

sort -n numbers.txt
# 3     ✅ correct numeric order
# 9
# 20
# 100
```

---

## Sort by a specific field

Use `-k` to sort by a column, and `-t` to set the delimiter:

```bash
cat cars.csv
# Honda,18000,35.2,1
# Toyota,12000,28.7,2
# BMW,22000,18.1,3

# Sort by price (field 2), numerically
sort -t, -k2 -n cars.csv
# Toyota,12000,28.7,2
# Honda,18000,35.2,1
# BMW,22000,18.1,3
```

---

## Combine with pipe

`sort` works on stdin — chain it after other commands:

```bash
# Get all brand names, sorted alphabetically
cut -f1 -d, cars.csv | sort
# BMW
# Honda
# Toyota

# Get prices sorted from highest to lowest
cut -f2 -d, cars.csv | sort -n -r
# 22000
# 18000
# 12000
```

---

## Full pipeline example

**Task:** Get all car brands that have a price under 20000, sorted alphabetically.

```bash
# Step 1 — see what we have
cat cars.csv

# Step 2 — filter by price (using awk, or grep for a pattern)
grep ",1[0-9][0-9][0-9][0-9]," cars.csv

# Step 3 — get only the brand name
grep ",1[0-9][0-9][0-9][0-9]," cars.csv | cut -f1 -d,

# Step 4 — sort
grep ",1[0-9][0-9][0-9][0-9]," cars.csv | cut -f1 -d, | sort
# Honda
# Toyota
```

---

## Save sorted output to a file

```bash
sort cars.txt > sorted_cars.txt
cut -f1 -d, cars.csv | sort > sorted_names.txt
```

---

> 💡 **Try it now:**
> 1. Create a file with 5 names in random order
> 2. `sort names.txt` — see them alphabetically
> 3. `sort -r names.txt` — see them reversed
> 4. Create a file with numbers and try `sort` vs `sort -n`

---

← [Prev: cut](./02-cut.md) · [Next: grep →](./04-grep.md)
