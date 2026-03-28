# 🔀 Topic 4 — If Statements & Comparisons

> **Make decisions in your script — but string and number comparisons use different operators.**

← [Prev: Arithmetic](./03-arithmetic.md) · [Next: Script Arguments →](./05-arguments.md)

---

## The `if` structure

```bash
if [[ condition ]]; then
    # commands if condition is true
elif [[ other condition ]]; then
    # commands if other condition is true
else
    # commands if nothing matched
fi
```

**Critical spacing rules — every space matters:**

| Part | Required? |
|------|-----------|
| Space after `[[` | ✅ Yes |
| Space before `]]` | ✅ Yes |
| Space around comparison operator | ✅ Yes |
| `;` after `]]` | ✅ Yes |
| `then` after `;` | ✅ Yes |
| `fi` at the end | ✅ Yes |

```bash
if [[ $a == $b ]]; then    ✅ correct
if [[$a==$b]]; then        ❌ missing spaces — will not work
```

---

## Comparing strings

Use these operators for **string** variables:

| Operator | Meaning | Example |
|----------|---------|---------|
| `==` | Equal to | `[[ $a == $b ]]` |
| `!=` | Not equal to | `[[ $a != $b ]]` |
| `<` | Less than (alphabetical) | `[[ $a < $b ]]` |
| `<=` | Less than or equal | `[[ $a <= $b ]]` |
| `>` | Greater than (alphabetical) | `[[ $a > $b ]]` |
| `>=` | Greater than or equal | `[[ $a >= $b ]]` |

**Example — compare two names:**

```bash
#!/bin/bash

P1="Alan Ballard"
P2="Bob Quimby"

echo "P1 = $P1"
echo "P2 = $P2"
echo "================="

if [[ $P1 > $P2 ]]; then
    echo "$P1 is greater than $P2"
elif [[ $P1 < $P2 ]]; then
    echo "$P1 is less than $P2"
else
    echo "$P1 is equal to $P2"
fi
```

Output:
```
P1 = Alan Ballard
P2 = Bob Quimby
=================
Alan Ballard is less than Bob Quimby
```

(A comes before B alphabetically → Alan < Bob)

---

## Comparing numbers

Use these operators for **numeric** variables — different from strings:

| Operator | Meaning | Example |
|----------|---------|---------|
| `-eq` | Equal to | `[[ $a -eq $b ]]` |
| `-ne` | Not equal to | `[[ $a -ne $b ]]` |
| `-lt` | Less than | `[[ $a -lt $b ]]` |
| `-le` | Less than or equal | `[[ $a -le $b ]]` |
| `-gt` | Greater than | `[[ $a -gt $b ]]` |
| `-ge` | Greater than or equal | `[[ $a -ge $b ]]` |

> ⚠️ **Do not mix them up.** Using `>` to compare numbers works in some cases but compares as strings — `9 > 10` would be `true` because `"9" > "10"` alphabetically.

**Example — compare two numbers:**

```bash
#!/bin/bash

N1=43
N2=102

echo "N1 is equal to $N1"
echo "N2 is equal to $N2"
echo "================="

if [[ $N1 -gt $N2 ]]; then
    echo "$N1 is greater than $N2"
elif [[ $N1 -lt $N2 ]]; then
    echo "$N1 is less than $N2"
else
    echo "$N1 is equal to $N2"
fi
```

Output:
```
N1 is equal to 43
N2 is equal to 102
=================
43 is less than 102
```

---

## String vs numeric operators — side by side

| Comparison | String operator | Numeric operator |
|------------|----------------|-----------------|
| Equal | `==` | `-eq` |
| Not equal | `!=` | `-ne` |
| Less than | `<` | `-lt` |
| Less or equal | `<=` | `-le` |
| Greater than | `>` | `-gt` |
| Greater or equal | `>=` | `-ge` |

**Memory trick for numeric operators:**  
`-lt` = **l**ess **t**han | `-gt` = **g**reater **t**han | `-eq` = **eq**ual

---

## Checking the number of arguments

A common use of `if` in scripts — validate that the right number of arguments was passed:

```bash
#!/bin/bash

if [[ $# -ne 2 ]]; then
    echo "Error: exactly 2 arguments required" 1>&2
    exit 1
fi

echo "First argument: $1"
echo "Second argument: $2"
```

- `$#` = number of arguments passed
- `exit 1` = stop the script and signal an error
- `1>&2` = send the error message to stderr (covered in [Topic 6](./06-redirection.md))

---

## Try it now

Create `compare.sh`:

```bash
#!/bin/bash

score=75

if [[ $score -ge 85 ]]; then
    echo "High distinction"
elif [[ $score -ge 75 ]]; then
    echo "Distinction"
elif [[ $score -ge 65 ]]; then
    echo "Credit"
elif [[ $score -ge 50 ]]; then
    echo "Pass"
else
    echo "Fail"
fi
```

```bash
chmod +x compare.sh
./compare.sh
# Distinction
```

Try changing `score` to different values and re-running.

---

← [Prev: Arithmetic](./03-arithmetic.md) · [Next: Script Arguments →](./05-arguments.md)
