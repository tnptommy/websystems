# 🔀 Topic 3 — Binary ↔ Hexadecimal

> **The easiest conversion — group binary digits into sets of 4.**

← [Prev: Binary ↔ Decimal](./02-binary-decimal.md) · [Next: Hex ↔ Decimal →](./04-hex-decimal.md)

---

## Why this is easy

Each hex digit maps **exactly** to 4 binary digits (bits). There is no arithmetic involved — just substitution using the table.

| Hex | Binary | | Hex | Binary |
|-----|--------|-|-----|--------|
| 0 | 0000 | | 8 | 1000 |
| 1 | 0001 | | 9 | 1001 |
| 2 | 0010 | | A | 1010 |
| 3 | 0011 | | B | 1011 |
| 4 | 0100 | | C | 1100 |
| 5 | 0101 | | D | 1101 |
| 6 | 0110 | | E | 1110 |
| 7 | 0111 | | F | 1111 |

---

## Binary to Hexadecimal

**Method:**
1. Split the binary number into groups of 4 digits, starting from the **right**
2. If the leftmost group has fewer than 4 digits, pad with leading zeros
3. Replace each group with the matching hex digit from the table

---

### Example — convert `1001111000111010` to hex

**Step 1 — split into groups of 4 from the right:**

```
1001  1110  0011  1010
```

**Step 2 — replace each group:**

```
1001 = 9
1110 = E
0011 = 3
1010 = A
```

**Result: `9E3A`**

---

### Example — padding when groups are uneven

Binary number `11001101001010` — only 14 digits, not a multiple of 4.

Pad with **leading zeros** to make 16 digits:

```
0011 0011 0100 1010
```

Replace:
```
0011 = 3
0011 = 3
0100 = 4
1010 = A
```

**Result: `334A`**

---

## Hexadecimal to Binary

**Method:** Replace each hex digit with its 4-bit binary equivalent. Always use exactly 4 bits — pad with leading zeros if needed.

---

### Example — convert `F04C` to binary

```
F = 1111
0 = 0000
4 = 0100
C = 1100
```

**Result: `1111000001001100`**

---

### Example — convert `83` to binary

```
8 = 1000
3 = 0011
```

**Result: `10000011`**

---

### Example — why you must always use 4 bits per digit

```
Hex digit 3 = binary 11   ❌ — missing leading zeros
Hex digit 3 = binary 0011 ✅ — always 4 bits
```

If you skip leading zeros, your groups blur together and the number is wrong:

```
Hex A3:
A = 1010  →  1010
3 = 11    →  11       ← only 2 bits — WRONG
Combined: 101011  (6 bits, wrong value)

A = 1010  →  1010
3 = 0011  →  0011     ← 4 bits — CORRECT
Combined: 10100011  (8 bits, correct)
```

---

## Verify your answer

To check binary → hex: convert your hex answer back to binary and compare.

```
Binary input:   1001 1110 0011 1010
Hex answer:     9    E    3    A
Check (hex→bin): 1001 1110 0011 1010  ✅ matches
```

---

← [Prev: Binary ↔ Decimal](./02-binary-decimal.md) · [Next: Hex ↔ Decimal →](./04-hex-decimal.md)
