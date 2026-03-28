# ✅ Topic 7 — Summary & Cheat Sheet

> **All Bash scripting syntax from Lesson 6 in one place.**

← [Prev: Redirecting stdout & stderr](./06-redirection.md) · [Back to README](./README.md)

---

## Key concepts

| Concept | What it means |
|---------|--------------|
| Script | A text file containing Bash commands, made executable |
| Shebang | `#!/bin/bash` — first line, tells OS which interpreter to use |
| Variable | A named container for a value |
| `$varname` | Read the value of a variable |
| `$(( ))` | Integer arithmetic |
| `$1 $2 $3` | Arguments passed to the script |
| `$#` | Number of arguments |
| `$*` | All arguments as one string |
| stdout | Normal output — stream 1 |
| stderr | Error output — stream 2 |
| `2>&1` | Redirect stderr into stdout |
| `1>&2` | Redirect stdout into stderr |

---

## Cheat Sheet

```bash
# ── SCRIPT SETUP ──────────────────────────────────────────────
#!/bin/bash                  # first line of every script
# this is a comment          # ignored by Bash
chmod +x script.sh           # make executable (do once)
chmod 744 script.sh          # rwxr--r-- (owner execute, others read)
./script.sh                  # run the script

# ── VARIABLES ─────────────────────────────────────────────────
name="Alice"                 # assign — NO spaces around =
number=42
echo $name                   # read — always use $
echo "Hello $name"           # $ works inside double quotes
greeting=$name               # copy variable value

# ── ARITHMETIC ────────────────────────────────────────────────
result=$(( $a + $b ))        # addition
result=$(( $a - $b ))        # subtraction
result=$(( $a * $b ))        # multiplication
result=$(( $a / $b ))        # division (rounds down)
result=$(( $a % $b ))        # modulus (remainder)

# ── ARGUMENTS ─────────────────────────────────────────────────
$1 $2 $3                     # first, second, third argument
$*                           # all arguments as one string
$#                           # number of arguments

# ── IF STATEMENTS ─────────────────────────────────────────────
if [[ condition ]]; then
    # commands
elif [[ condition ]]; then
    # commands
else
    # commands
fi

# ── STRING COMPARISONS ────────────────────────────────────────
[[ $a == $b ]]               # equal
[[ $a != $b ]]               # not equal
[[ $a < $b ]]                # less than (alphabetical)
[[ $a > $b ]]                # greater than (alphabetical)

# ── NUMERIC COMPARISONS ───────────────────────────────────────
[[ $a -eq $b ]]              # equal
[[ $a -ne $b ]]              # not equal
[[ $a -lt $b ]]              # less than
[[ $a -le $b ]]              # less than or equal
[[ $a -gt $b ]]              # greater than
[[ $a -ge $b ]]              # greater than or equal

# ── REDIRECTION ───────────────────────────────────────────────
command 2>&1                 # send stderr to stdout
command 1>&2                 # send stdout to stderr
echo "Error" 1>&2            # send error message to stderr (in scripts)
exit 0                       # exit script — success
exit 1                       # exit script — error
```

---

## String vs numeric comparison — quick reference

| Comparison | Strings | Numbers |
|------------|---------|---------|
| Equal | `==` | `-eq` |
| Not equal | `!=` | `-ne` |
| Less than | `<` | `-lt` |
| Less or equal | `<=` | `-le` |
| Greater than | `>` | `-gt` |
| Greater or equal | `>=` | `-ge` |

---

## Template — a well-structured script

```bash
#!/bin/bash

# Check correct number of arguments
if [[ $# -ne 2 ]]; then
    echo "Usage: ./myscript.sh arg1 arg2" 1>&2
    exit 1
fi

# Assign arguments to named variables
first=$1
second=$2

# Do the work
result=$(( $first + $second ))

# Output
echo "$first + $second = $result"
```

---

## Read the question → know what to do

| Question says | Use this |
|---------------|----------|
| *"first line of a script"* | `#!/bin/bash` |
| *"make it executable"* | `chmod +x script.sh` |
| *"run the script"* | `./script.sh` |
| *"assign a variable"* | `name="value"` — no spaces around `=` |
| *"read a variable"* | `$name` |
| *"add two numbers"* | `$(( $a + $b ))` |
| *"remainder / modulus"* | `$(( $a % $b ))` |
| *"compare strings"* | `[[ $a == $b ]]` |
| *"compare numbers"* | `[[ $a -eq $b ]]` |
| *"first argument"* | `$1` |
| *"number of arguments"* | `$#` |
| *"all arguments"* | `$*` |
| *"send error to stderr"* | `echo "msg" 1>&2` |
| *"capture both stdout and stderr"* | `command > file 2>&1` |
| *"stop script on error"* | `exit 1` |

---

## Check your work before submitting

```bash
# Does the script exist and is it executable?
ls -l myscript.sh
# should show x in permissions: -rwxr--r--

# Run with expected arguments
./myscript.sh arg1 arg2

# Run with wrong number of arguments — check error handling
./myscript.sh
# should show usage/error message

# Check output is correct
./myscript.sh 10 20

# If redirecting, check the output file
./myscript.sh > output.txt
cat output.txt
```

> 💡 Test your script with different inputs — including wrong inputs — before submitting.

---

← [Prev: Redirecting stdout & stderr](./06-redirection.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
