# ➕ Topic 5 — Binary Arithmetic

> **Adding binary numbers follows the same rules as decimal — just with carries happening sooner.**

← [Prev: Hex ↔ Decimal](./04-hex-decimal.md) · [Next: Octal →](./06-octal.md)

---

## The basic rules

In decimal, you carry when a column exceeds 9. In binary, you carry when a column exceeds 1.

There are only four cases to remember:

| A | B | Sum | Carry |
|---|---|-----|-------|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

And when a carry comes in:

| A | B | Carry in | Sum | Carry out |
|---|---|----------|-----|-----------|
| 1 | 1 | 1 | 1 | 1 |

**Key facts to memorise:**

```
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 10   ← "zero carry one"
1 + 1 + 1 = 11  ← "one carry one"
1 + 1 + 1 + 1 = 100  ← "zero carry one" (then zero carry one again)
```

---

## Example — add `10101` + `11010`

Align the numbers on the right:

```
    1 0 1 0 1
  + 1 1 0 1 0
  -----------
```

Work right to left, column by column:

```
Column 1 (rightmost):  1 + 0 = 1          write 1, carry 0
Column 2:              0 + 1 = 1          write 1, carry 0
Column 3:              1 + 0 = 1          write 1, carry 0
Column 4:              0 + 1 = 1          write 1, carry 0
Column 5:              1 + 1 = 10         write 0, carry 1
Column 6 (new):            carry 1        write 1
```

```
  c 1 0 1 0 1
+   1 1 0 1 0
-----------
1 0 1 1 1 1
```

Result: **101111**

**Check:** 10101 = 21, 11010 = 26. 21 + 26 = 47. Binary 101111 = 32 + 8 + 4 + 2 + 1 = 47 ✅

---

## Example — add `11101` + `11011`

```
  1 1 1 0 1
+ 1 1 0 1 1
-----------
```

```
Column 1:  1 + 1 = 10       write 0, carry 1
Column 2:  0 + 1 + carry 1 = 10  write 0, carry 1
Column 3:  1 + 0 + carry 1 = 10  write 0, carry 1
Column 4:  1 + 1 + carry 1 = 11  write 1, carry 1
Column 5:  1 + 1 + carry 1 = 11  write 1, carry 1
Column 6:  carry 1          write 1
```

```
  c c c c
  1 1 1 0 1
+ 1 1 0 1 1
-----------
1 1 1 0 0 0
```

Result: **111000**

**Check:** 11101 = 29, 11011 = 27. 29 + 27 = 56. Binary 111000 = 32 + 16 + 8 = 56 ✅

---

## Example — add `10001` + `111`

```
  1 0 0 0 1
+     1 1 1
-----------
```

Pad the shorter number with leading zeros:

```
  1 0 0 0 1
+ 0 0 1 1 1
-----------
```

```
Column 1:  1 + 1 = 10       write 0, carry 1
Column 2:  0 + 1 + carry 1 = 10  write 0, carry 1
Column 3:  0 + 1 + carry 1 = 10  write 0, carry 1
Column 4:  0 + 0 + carry 1 = 1   write 1, carry 0
Column 5:  1 + 0 = 1        write 1
```

```
  1 0 0 0 1
+ 0 0 1 1 1
-----------
  1 1 0 0 0
```

Result: **11000**

**Check:** 10001 = 17, 111 = 7. 17 + 7 = 24. Binary 11000 = 16 + 8 = 24 ✅

---

## Tips

- Always align numbers on the **right** before adding
- Pad shorter numbers with **leading zeros**
- **Always verify** by converting both numbers and the result to decimal

---

← [Prev: Hex ↔ Decimal](./04-hex-decimal.md) · [Next: Octal →](./06-octal.md)
