# 🔄 Topic 2 — Binary ↔ Decimal

> **The two most fundamental conversions — work through every step.**

← [Prev: Overview](./01-number-systems.md) · [Next: Binary ↔ Hex →](./03-binary-hex.md)

---

## Binary to Decimal

Each binary digit (bit) represents a power of 2. The rightmost bit is 2⁰, the next is 2¹, and so on.

**Method:** Write the binary number under a row of powers of 2. Add up the values where the bit is 1.

---

### Example — convert `1011` to decimal

Set up the table (right to left, starting at 2⁰):

| 2³ | 2² | 2¹ | 2⁰ |
|----|----|----|-----|
| 8  | 4  | 2  | 1  |
| 1  | 0  | 1  | 1  |

Add where bits are 1: **8 + 0 + 2 + 1 = 11**

So binary `1011` = decimal **11**

---

### Example — convert `1011011011000101` to decimal

| 2¹⁵ | 2¹⁴ | 2¹³ | 2¹² | 2¹¹ | 2¹⁰ | 2⁹ | 2⁸ | 2⁷ | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
|------|------|------|------|------|------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| 32768 | 16384 | 8192 | 4096 | 2048 | 1024 | 512 | 256 | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 1 | 0 | 1 |

Add the values under each `1`:

32768 + 8192 + 4096 + 1024 + 512 + 128 + 64 + 4 + 1 = **46789**

---

## Decimal to Binary

**Method:** Repeatedly divide by 2. Record the remainder (0 or 1) each time. Read remainders from **bottom to top**.

---

### Example — convert `45921` to binary

| Number (quotient) | Remainder |
|-------------------|-----------|
| 45921 | **1** |
| 22960 | **0** |
| 11480 | **0** |
| 5740 | **0** |
| 2870 | **0** |
| 1435 | **1** |
| 717 | **1** |
| 358 | **0** |
| 179 | **1** |
| 89 | **1** |
| 44 | **0** |
| 22 | **0** |
| 11 | **1** |
| 5 | **1** |
| 2 | **0** |
| 1 | **1** |

Read remainders **bottom to top**: **1011001101100001**

So decimal `45921` = binary **1011001101100001**

---

### Step by step for a smaller example — convert `13` to binary

| Number | ÷ 2 = quotient | Remainder |
|--------|---------------|-----------|
| 13 | 6 | **1** |
| 6 | 3 | **0** |
| 3 | 1 | **1** |
| 1 | 0 | **1** |

Read bottom to top: **1101**

Check: 8 + 4 + 0 + 1 = 13 ✅

---

## Common mistake — reading the remainders the wrong direction

```
13 ÷ 2 = 6 remainder 1   ← this is the LAST bit (rightmost)
 6 ÷ 2 = 3 remainder 0
 3 ÷ 2 = 1 remainder 1
 1 ÷ 2 = 0 remainder 1   ← this is the FIRST bit (leftmost)

Wrong order: 1011   ❌  (= 11, not 13)
Right order: 1101   ✅  (= 13)
```

Always read from **bottom to top**, write from **left to right**.

---

## Quick check — verify your answer

After converting decimal → binary, convert back to decimal to check:

```
1101 = 8 + 4 + 0 + 1 = 13 ✅
```

---

← [Prev: Overview](./01-number-systems.md) · [Next: Binary ↔ Hex →](./03-binary-hex.md)
