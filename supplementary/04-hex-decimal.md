# 🔢 Topic 4 — Hexadecimal ↔ Decimal

> **Use powers of 16 for hex→decimal, or go via binary for decimal→hex.**

← [Prev: Binary ↔ Hex](./03-binary-hex.md) · [Next: Binary Arithmetic →](./05-binary-arithmetic.md)

---

## Hexadecimal to Decimal

**Method:** Build a table of powers of 16. Multiply each hex digit's decimal value by its position's power of 16. Add them all up.

| Power | Value |
|-------|-------|
| 16⁰ | 1 |
| 16¹ | 16 |
| 16² | 256 |
| 16³ | 4096 |
| 16⁴ | 65536 |

Remember: hex digits A–F have decimal values 10–15.

---

### Example — convert `5C2B` to decimal

Position values (right to left):

```
5    C    2    B
^    ^    ^    ^
16³  16²  16¹  16⁰
4096  256  16    1
```

Calculate:

```
5 × 4096 = 20480
C × 256  = 12 × 256 = 3072
2 × 16   = 32
B × 1    = 11 × 1 = 11
```

Total: 20480 + 3072 + 32 + 11 = **23595**

---

### Example — convert `AAAA` to decimal

```
A × 4096 = 10 × 4096 = 40960
A × 256  = 10 × 256  = 2560
A × 16   = 10 × 16   = 160
A × 1    = 10 × 1    = 10
```

Total: 40960 + 2560 + 160 + 10 = **43690**

---

### Does case matter?

**No.** Hex is case-insensitive.

`9E3B` and `9e3b` are exactly the same number. The answer is always the same regardless of upper or lower case.

---

## Decimal to Hexadecimal

**Best method:** Convert decimal → binary first (Topic 2), then binary → hex (Topic 3).

---

### Example — convert `28439` to hex

**Step 1 — decimal to binary** (repeated division by 2):

| Number | Remainder |
|--------|-----------|
| 28439 | 1 |
| 14219 | 1 |
| 7109 | 1 |
| 3554 | 0 |
| 1777 | 1 |
| 888 | 0 |
| 444 | 0 |
| 222 | 0 |
| 111 | 1 |
| 55 | 1 |
| 27 | 1 |
| 13 | 1 |
| 6 | 0 |
| 3 | 1 |
| 1 | 1 |

Read bottom to top: `110111100010111` (15 digits)

**Step 2 — pad to multiple of 4:**

`0110 1111 0001 0111` (padded to 16 digits)

**Step 3 — binary to hex:**

```
0110 = 6
1111 = F
0001 = 1
0111 = 7
```

**Result: `6F17`**

---

### Verify — convert `6F17` back to decimal

```
6 × 4096 = 24576
F × 256  = 15 × 256 = 3840
1 × 16   = 16
7 × 1    = 7
```

Total: 24576 + 3840 + 16 + 7 = **28439** ✅

---

## Common mistakes

**Mistake 1 — forgetting to convert A–F to their decimal values:**
```
C × 256 = C × 256   ❌  C is not a number
C × 256 = 12 × 256  ✅  C = 12
```

**Mistake 2 — reading the wrong direction in binary division:**

Always read remainders **bottom to top** for decimal → binary.

**Mistake 3 — not padding to a multiple of 4 before binary → hex:**

```
Binary: 110111100010111    (15 digits — not a multiple of 4)
Padded: 0110111100010111   (wrong! that's 16 but grouped wrong)
Right:  0110 1111 0001 0111 ✅
```

---

← [Prev: Binary ↔ Hex](./03-binary-hex.md) · [Next: Binary Arithmetic →](./05-binary-arithmetic.md)
