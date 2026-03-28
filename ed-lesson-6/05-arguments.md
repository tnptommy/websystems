# 📥 Topic 5 — Script Arguments

> **Pass information into your script when you run it — without hardcoding values.**

← [Prev: If Statements](./04-if-statements.md) · [Next: Redirecting stdout & stderr →](./06-redirection.md)

---

## What are arguments?

When you run a script, you can pass extra values after the script name:

```bash
./hello.sh Bill
#           ^^^^
#           This is the first argument
```

Inside the script, you access them using special variables.

---

## Argument variables

| Variable | What it contains |
|----------|-----------------|
| `$1` | First argument |
| `$2` | Second argument |
| `$3` | Third argument |
| `$n` | nth argument |
| `$*` | All arguments as a single string |
| `$#` | The number of arguments passed |

---

## Full example

Create `args.sh`:

```bash
#!/bin/bash

echo "Number of arguments is $#"
echo "The arguments are $*"
echo "The first argument is $1"
echo "The second argument is $2"
echo "The third argument is $3"
```

Make it executable:

```bash
chmod 744 args.sh
```

Run it:

```bash
./args.sh amazon google apple
```

Output:

```
Number of arguments is 3
The arguments are amazon google apple
The first argument is amazon
The second argument is google
The third argument is apple
```

---

## Using arguments in real scripts

**Example — a script that greets a user by name:**

```bash
#!/bin/bash

echo "Hello $1! Welcome to $2."
```

```bash
./greet.sh Alice "Web Systems"
# Hello Alice! Welcome to Web Systems.
```

**Example — a script that adds two numbers from arguments:**

```bash
#!/bin/bash

result=$(( $1 + $2 ))
echo "$1 + $2 = $result"
```

```bash
./add.sh 15 27
# 15 + 27 = 42
```

---

## Validating arguments with `$#`

It is good practice to check that the correct number of arguments was passed:

```bash
#!/bin/bash

if [[ $# -ne 2 ]]; then
    echo "Usage: ./myscript.sh arg1 arg2" 1>&2
    exit 1
fi

echo "First: $1"
echo "Second: $2"
```

```bash
./myscript.sh only-one-arg
# Usage: ./myscript.sh arg1 arg2
# (script stops here — exit 1)

./myscript.sh hello world
# First: hello
# Second: world
```

- `exit 1` — stops the script. `1` signals an error. `exit 0` means success.
- `1>&2` — sends the usage message to stderr so it does not pollute stdout (see [Topic 6](./06-redirection.md))

---

## Arguments with spaces

If an argument contains spaces, wrap it in quotes:

```bash
./hello.sh "John Smith"
# $1 = "John Smith"   ← treated as one argument ✅

./hello.sh John Smith
# $1 = "John"         ← only first word ❌
# $2 = "Smith"
```

---

## Try it now

Create `calculator.sh`:

```bash
#!/bin/bash

if [[ $# -ne 3 ]]; then
    echo "Usage: ./calculator.sh number1 operator number2"
    echo "Operators: + - * /"
    exit 1
fi

result=$(( $1 $2 $3 ))
echo "$1 $2 $3 = $result"
```

```bash
chmod +x calculator.sh
./calculator.sh 10 + 5    # 10 + 5 = 15
./calculator.sh 20 - 8    # 20 - 8 = 12
./calculator.sh 6 \* 7    # 6 * 7 = 42  (\ escapes * in terminal)
```

---

← [Prev: If Statements](./04-if-statements.md) · [Next: Redirecting stdout & stderr →](./06-redirection.md)
