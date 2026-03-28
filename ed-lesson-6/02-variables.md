# 📦 Topic 2 — Variables

> **Store values and reuse them — but Bash has strict rules about spacing.**

← [Prev: First Script](./01-first-script.md) · [Next: Arithmetic →](./03-arithmetic.md)

---

## Assigning a variable

```bash
name="Alice"
number=42
greeting="Hello World"
```

**The most important rule in Bash:**

> ⚠️ **No spaces around the `=` sign.** Ever.

```bash
name="Alice"     ✅ correct
name = "Alice"   ❌ Bash thinks "name" is a command — error
name ="Alice"    ❌ error
name= "Alice"    ❌ error
```

This is different from most other languages like Python or Java where spaces are fine.  
In Bash — no spaces, no exceptions.

---

## Using a variable — the `$` sign

To **read** the value of a variable, put `$` before the name:

```bash
name="Alice"
echo $name         # prints: Alice
echo "Hello $name" # prints: Hello Alice
```

**The rule for `$`:**

| Situation | Use `$`? | Example |
|-----------|----------|---------|
| Left side of `=` (assigning) | ❌ No | `name="Alice"` |
| Right side of `=` (reading) | ✅ Yes | `greeting=$name` |
| Inside `echo` | ✅ Yes | `echo $name` |
| Inside `[[ ]]` comparisons | ✅ Yes | `[[ $a == $b ]]` |

---

## Full example

```bash
#!/bin/bash

a="Hello World"
echo $a

number1=25
echo "number 1 = $number1"

number2=$number1
number1=54

echo "number1 = $number1 number2 = $number2"
```

Run it:

```bash
chmod +x variables.sh
./variables.sh
```

Output:

```
Hello World
number 1 = 25
number1 = 54 number2 = 25
```

Notice: `number2` kept the value `25` — it stored the value at the time of assignment, not a reference to `number1`.

---

## Quotes — single vs double

```bash
name="Alice"

echo "Hello $name"    # Hello Alice     ← $name is expanded
echo 'Hello $name'    # Hello $name     ← single quotes = no expansion
```

Use **double quotes** `"..."` when your value contains spaces or you want variables expanded.  
Use **single quotes** `'...'` when you want the literal text, no substitution.

---

## Variable naming rules

```bash
myvar="ok"        ✅ lowercase
MY_VAR="ok"       ✅ uppercase with underscore
myVar="ok"        ✅ camelCase
2var="bad"        ❌ cannot start with a number
my-var="bad"      ❌ hyphens not allowed
my var="bad"      ❌ spaces not allowed
```

---

## Try it now

Create `variables.sh`:

```bash
#!/bin/bash

first="Web"
second="Systems"
combined="$first $second"

echo "Subject: $combined"
echo "First word: $first"
echo "Second word: $second"
```

```bash
chmod +x variables.sh
./variables.sh
# Subject: Web Systems
# First word: Web
# Second word: Systems
```

---

← [Prev: First Script](./01-first-script.md) · [Next: Arithmetic →](./03-arithmetic.md)
