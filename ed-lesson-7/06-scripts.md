# 🔧 Topic 6 — Putting It All Together

> **Real examples combining everything — clean data, cut, grep, sort, inline execution, and scripts.**

← [Prev: Inline Execution](./05-inline-execution.md) · [Next: Summary →](./07-summary.md)

---

## The data analysis workflow

Every data analysis task in this lesson follows the same pattern:

```
1. Clean the data (whitespace → commas)
2. Extract the column you need (cut)
3. Filter rows (grep)
4. Sort the result (sort)
5. Store values in variables ($())
6. Combine it all into a script
```

Work through each example slowly. Each one builds on the last.

---

## Example setup — a city population file

For all examples below, assume a file `cities.txt` with this content:

```
SYDNEY          5.3    5.3    1
MELBOURNE       5.0   10.3    2
BRISBANE        2.5   12.8    3
PERTH           2.1   14.9    4
ADELAIDE        1.4   16.3    5
DARWIN          0.1   16.4   50
ALBANY          0.1   16.5   51
```

Columns: NAME, POPULATION(%), CUMULATIVE, RANK

---

## Step 1 — Clean the data

**Goal:** Convert `cities.txt` to `cities.csv` with commas instead of whitespace.

```bash
cp cities.txt cities.csv
vim cities.csv
```

In Vim:
```
:%s/^\s\+//g        ← remove leading spaces
:%s/\s\+$//g        ← remove trailing spaces
:%s/\s\+/,/g        ← replace internal whitespace with commas
:wq
```

Check:
```bash
cat cities.csv
# SYDNEY,5.3,5.3,1
# MELBOURNE,5.0,10.3,2
# BRISBANE,2.5,12.8,3
# ...
```

---

## Example A — Extract only city names

**Goal:** Create a file `names.txt` with only column 1 from `cities.csv`, in original order.

```bash
cut -f1 -d, cities.csv > names.txt
cat names.txt
# SYDNEY
# MELBOURNE
# BRISBANE
# PERTH
# ADELAIDE
# DARWIN
# ALBANY
```

---

## Example B — Search from start of line only

**Goal:** Find all cities that START with the letters "AD".

```bash
grep "^AD" cities.csv
# ADELAIDE,1.4,16.3,5
# DARWIN,0.1,16.4,50    ← wait — DARWIN does not start with AD
```

Hmm — DARWIN was not supposed to match. Check the regex:

```bash
grep "^AD" cities.csv
# ADELAIDE,1.4,16.3,5   ← only ADELAIDE starts with AD ✅
```

DARWIN does not match — that was correct. Good.

**Now try cities starting with "D" OR "P":**

```bash
grep "^D\|^P" cities.csv
# PERTH,2.1,14.9,4
# DARWIN,0.1,16.4,50
```

---

## Example C — Find files containing a string

**Goal:** Find all `.txt` files in the current directory that contain the word "SYDNEY".

```bash
grep -l "SYDNEY" *.txt
# cities.txt
```

With full path:

```bash
grep -l "SYDNEY" /home/user/*.txt
# /home/user/cities.txt
```

---

## Example D — Match whole words only

**Goal:** Find lines containing the word "ADE" — but NOT "ADELAIDE".

```bash
grep "ADE" cities.csv
# ADELAIDE,1.4,16.3,5    ← matches because "ADE" is inside ADELAIDE

grep -w "ADE" cities.csv
# (no results)            ← -w requires "ADE" to be a whole word
```

---

## Example E — Get the population of one city (inline execution)

**Goal:** Find Sydney's population percentage and store it in a variable.

```bash
sydney_pop=$(grep "^SYDNEY," cities.csv | cut -f2 -d,)
echo "Sydney population share: $sydney_pop%"
# Sydney population share: 5.3%
```

**Why `^SYDNEY,` instead of just `SYDNEY`?**

```bash
grep "SYDNEY" cities.csv      # matches any line containing SYDNEY anywhere
grep "^SYDNEY," cities.csv    # only lines where SYDNEY is the first field ✅
```

The `,` after SYDNEY ensures we match the full field, not a city called "SYDNEY-NORTH" etc.

---

## Example F — Find all cities with the same population

**Goal:** Script that takes a city name and returns all cities with the same population, sorted.

```bash
#!/bin/bash

# Check arguments
if [[ $# -ne 1 ]]; then
    echo "Usage: ./samepop.sh CITYNAME" 1>&2
    exit 1
fi

city=$1
csv_file="cities.csv"

# Step 1 — get the population of the given city
pop=$(grep "^$city," $csv_file | cut -f2 -d,)

if [[ -z $pop ]]; then
    echo "City not found: $city" 1>&2
    exit 1
fi

echo "Population share for $city: $pop"
echo "Cities with the same population:"

# Step 2 — find all cities with that population, get names, sort
grep ",$pop," $csv_file | cut -f1 -d, | sort
```

Run:
```bash
chmod +x samepop.sh
./samepop.sh DARWIN
# Population share for DARWIN: 0.1
# Cities with the same population:
# ALBANY
# DARWIN
```

---

## Example G — Detect if a city is in the file

**Goal:** Script that prints "found" or "not found" for a given city name.

```bash
#!/bin/bash

city=$1

grep -q "^$city," cities.csv    # -q = quiet, no output

if [[ $? -eq 0 ]]; then
    echo "$city: found"
else
    echo "$city: not found"
fi
```

```bash
./detect.sh SYDNEY
# SYDNEY: found

./detect.sh LONDON
# LONDON: not found
```

**Key point:** `grep -q` produces no output — it just sets `$?` to 0 (found) or 1 (not found).  
We check that value with `$?` immediately after.

---

## The complete pipeline — reading it left to right

When you see a long command, read each `|` as "then":

```bash
grep "^D\|^P" cities.csv | cut -f1 -d, | sort
```

Read as:
```
Find lines starting with D or P    →    get only the name column    →    sort alphabetically
```

Result:
```
DARWIN
PERTH
```

---

> 💡 **Build up commands step by step** — never write the whole pipeline at once.
> Test each piece first, then connect them.

---

← [Prev: Inline Execution](./05-inline-execution.md) · [Next: Summary →](./07-summary.md)
