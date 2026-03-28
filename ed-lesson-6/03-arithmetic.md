# 🔢 Topic 3 — Arithmetic

> **Bash supports integer arithmetic using `$(( ))` syntax.**

← [Prev: Variables](./02-variables.md) · [Next: If Statements →](./04-if-statements.md)

---

## Integer arithmetic only

Bash only supports **integer (whole number) arithmetic** — no decimal points.

Division rounds **down** to the nearest integer:

```bash
echo $(( 7 / 2 ))    # 3  (not 3.5)
echo $(( 9 / 4 ))    # 2  (not 2.25)
```

---

## The `$(( ))` syntax

Wrap any arithmetic expression in `$(( ))`:

```bash
result=$(( 10 + 3 ))
echo $result    # 13
```

| Operation | Symbol | Example | Result |
|-----------|--------|---------|--------|
| Addition | `+` | `$(( 25 + 10 ))` | `35` |
| Subtraction | `-` | `$(( 25 - 10 ))` | `15` |
| Multiplication | `*` | `$(( 25 * 10 ))` | `250` |
| Division | `/` | `$(( 25 / 10 ))` | `2` (rounded down) |
| Modulus (remainder) | `%` | `$(( 25 % 10 ))` | `5` |

---

## Full example

Create `arithmetic.sh`:

```bash
#!/bin/bash

a=25
b=10

echo "a is equal to $a"
echo "b is equal to $b"
echo "====================="

add_result=$(($a + $b))
sub_result=$(($a - $b))
div_result=$(($a / $b))
mult_result=$(($a * $b))
mod_result=$(($a % $b))

echo "sum is $add_result"
echo "difference is $sub_result"
echo "division is $div_result"
echo "mult_result is $mult_result"
echo "mod_result is $mod_result"
```

Run it:

```bash
chmod +x arithmetic.sh
./arithmetic.sh
```

Output:

```
a is equal to 25
b is equal to 10
=====================
sum is 35
difference is 15
division is 2
mult_result is 250
mod_result is 5
```

---

## Using variables inside `$(( ))`

```bash
x=8
y=3

# Both of these work:
result=$(( $x + $y ))    # with $
result=$(( x + y ))      # without $ — also valid inside (( ))

echo $result    # 11
```

---

## Modulus — what is it?

Modulus gives you the **remainder** after division.

```bash
echo $(( 10 % 3 ))    # 1   because 10 = 3*3 + 1
echo $(( 20 % 6 ))    # 2   because 20 = 6*3 + 2
echo $(( 15 % 5 ))    # 0   because 15 = 5*3 + 0 (divides evenly)
```

**Common use:** Check if a number is even or odd:

```bash
num=7
remainder=$(( num % 2 ))
echo $remainder    # 1 = odd (0 = even)
```

---

## Common mistakes

**Mistake 1 — spaces around `=` in assignment:**
```bash
result = $(( 5 + 3 ))    ❌ space around = causes error
result=$(( 5 + 3 ))      ✅
```

**Mistake 2 — forgetting `$(( ))`:**
```bash
result=$a + $b     ❌ this is string concatenation, not addition
result=$(($a + $b))  ✅
```

**Mistake 3 — expecting decimal results:**
```bash
echo $(( 7 / 2 ))    # 3  ← not 3.5, Bash truncates
```

---

> 💡 **Try it now:** Create `arithmetic.sh`, run it, then try changing `a` and `b` to different values and see the results change.

---

← [Prev: Variables](./02-variables.md) · [Next: If Statements →](./04-if-statements.md)
