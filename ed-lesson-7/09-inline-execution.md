# ⚡ Topic 9 — Inline Command Execution

> **Store the output of a command in a variable — so you can use it later in the same script.**

← [Prev: Checking Output](./08-check.md) · [Next: Putting It All Together →](./10-scripts.md)

---

## The problem this solves

Imagine you want to:
1. Find a value from a data file (e.g. the frequency of a name)
2. Use that value in the next command

Without inline execution, you would have to:
- Run the command
- Read the output with your eyes
- Type it manually into the next command

Inline execution lets you **capture command output directly into a variable** and use it automatically.

---

## The syntax — `$()`

```bash
variable=$(command)
```

Example:

```bash
freq=$(grep "^ANA," ~/table.csv | cut -f2 -d,)
echo "ANA frequency: $freq"
# ANA frequency: 0.120
```

---

## You may also see backticks — `` ` ` ``

Old scripts sometimes use backticks instead:

```bash
freq=`grep "^ANA," ~/table.csv | cut -f2 -d,`
```

Both produce the same result. Use `$()` for new scripts — it is easier to read and does not get confused with single quotes.

---

## Do not confuse `$()` with `$(( ))`

They look similar but do very different things:

| Syntax | What it does | Example |
|--------|-------------|---------|
| `$(command)` | Run a command, capture its output | `$(wc -l file.txt)` |
| `$(( expression ))` | Arithmetic — calculate a number | `$(( 5 + 3 ))` |

```bash
lines=$(wc -l ~/table.csv)      # runs wc, stores the line count
total=$(( 10 + 5 ))             # calculates 15, stores 15
```

---

## Step-by-step example

**Task:** Find the frequency of ANA, then find all names with that same frequency.

```bash
# Step 1 — find ANA's frequency and store it
FREQ=$(grep "^ANA," ~/table.csv | cut -f2 -d,)

echo "ANA frequency is: $FREQ"
# ANA frequency is: 0.120

# Step 2 — use that frequency to find all matching names
grep ",$FREQ," ~/table.csv | cut -f1 -d, | sort
# ANA
# RENEE
```

This is the **core pattern** for data analysis scripts in this lesson.

---

## Using awk inside `$()`

```bash
# Same result — using awk instead of grep + cut
FREQ=$(awk -v n="ANA" '$1 == n {print $2}' /course/linuxgym/census/femalenames.txt)
echo $FREQ
# 0.120
```

---

## Inline execution inside a string

You can use `$()` directly inside an `echo`:

```bash
echo "There are $(wc -l < ~/table.csv) lines in the file"
echo "Today is $(date)"
echo "You are logged in as: $(whoami)"
```

---

## Checking if the variable is empty

After storing a value, always check it was actually found:

```bash
FREQ=$(grep "^TYPO," ~/table.csv | cut -f2 -d,)

if [[ -z $FREQ ]]; then
    echo "Name not found"
    exit 1
fi
```

| Check | Meaning |
|-------|---------|
| `[[ -z $var ]]` | True if variable IS empty (zero length) |
| `[[ -n $var ]]` | True if variable is NOT empty |

You will use this in scripts — see [Topic 10](./10-scripts.md).

---

> 💡 **Try it now:**
> 1. `count=$(wc -l ~/table.csv)` then `echo "Lines: $count"`
> 2. `FREQ=$(awk '$1=="MARY"{print $2}' /course/linuxgym/census/femalenames.txt)` then `echo $FREQ`
> 3. `echo "Today: $(date)"`

---

← [Prev: Checking Output](./08-check.md) · [Next: Putting It All Together →](./10-scripts.md)
