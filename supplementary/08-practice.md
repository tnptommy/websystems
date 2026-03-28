# 📝 Topic 8 — Practice Problems

> **Work through these without looking at the answers first. Check your work at the end.**

← [Prev: Boolean Logic](./07-boolean-logic.md) · [Back to README](./README.md)

---

## Part A — Binary Addition

Compute the sum of the following binary numbers.  
Verify by converting to decimal and checking the sum.

**1.** `10101 + 11010`

**2.** `11101 + 11011`

**3.** `10001 + 111`

---

## Part B — Binary to Decimal

Convert the following binary numbers to decimal:

**1.** `1010101011110101`

**2.** `1110101111100111`

**3.** `1010111110011100`

**4.** `1100010001100110`

**5.** `1010101110111010`

**6.** `1100011010011101`

**7.** `1010001100111011`

**8.** `1100111010000111`

---

## Part C — Decimal to Binary

Convert the following decimal numbers to binary:

**1.** 12401

**2.** 83893

**3.** 86522

**4.** 56782

**5.** 28221

**6.** 19567

**7.** 23148

**8.** 42454

**9.** 15636

---

## Part D — Binary to Hexadecimal

Convert the following binary numbers to hexadecimal:

**1.** `1010111110011111`

**2.** `0101001110101011`

**3.** `1100110001100110`

**4.** `1011111010100011`

**5.** `0011011001101100`

**6.** `1000001111010101`

**7.** `1010101010101010`

**8.** `0110111101101101`

**9.** `0010011101010111`

**10.** `1111100010101011`

---

## Part E — Hexadecimal to Binary

Convert the following hex numbers to binary:

**1.** `78A7`

**2.** `B190`

**3.** `FEE0`

**4.** `1775`

**5.** `1E0D`

**6.** `9216`

**7.** `7812`

**8.** `9067`

**9.** `62E7`

**10.** `01AB`

---

## Part F — Hexadecimal to Decimal

Convert the following hex numbers to decimal:

**1.** `AAAA`

**2.** `9E3B`

**3.** `D00D`

**4.** `3D81`

**5.** `18BE`

**6.** `F990`

**7.** `5467`

**8.** `AB83`

**9.** `2557`

---

## Part G — Decimal to Hexadecimal

Convert the following decimal numbers to hexadecimal:

**1.** 42897

**2.** 62388

**3.** 56019

**4.** 97814

**5.** 55632

**6.** 12593

**7.** 78648

**8.** 32077

---

## Part H — Mixed Conversions (Decimal → Binary → Hex → Decimal)

Convert each decimal to binary, then to hex, then back to decimal.  
You should end up where you started.

**1.** 10

**2.** 123

**3.** 456

---

## Part I — Boolean Logic Proofs

Use De Morgan's laws and distributivity to prove each equality.

**1.** `not((x OR y) AND z) = (not(x) AND not(y)) OR not(z)`

**2.** `(not(x) OR y) AND not(z) = not(x OR z) OR (y AND not(z))`

**3.** `not(not(x) AND not(y)) = x OR y`

**4.** Express AND, OR, and NOT using **only NAND**.

---

---

# ✅ Answers

---

## Part A — Binary Addition

**1.** `10101 + 11010`
```
  10101  (= 21)
+ 11010  (= 26)
-------
 101111  (= 47)
```
Check: 21 + 26 = 47 ✅

**2.** `11101 + 11011`
```
  11101  (= 29)
+ 11011  (= 27)
-------
 111000  (= 56)
```
Check: 29 + 27 = 56 ✅

**3.** `10001 + 111`
```
  10001  (= 17)
+ 00111  (= 7)
-------
  11000  (= 24)
```
Check: 17 + 7 = 24 ✅

---

## Part B — Binary to Decimal

| Binary | Decimal |
|--------|---------|
| `1010101011110101` | **43765** |
| `1110101111100111` | **60391** |
| `1010111110011100` | **44956** |
| `1100010001100110` | **50278** |
| `1010101110111010` | **43962** |
| `1100011010011101` | **50845** |
| `1010001100111011` | **41787** |
| `1100111010000111` | **52871** |

---

## Part C — Decimal to Binary

| Decimal | Binary |
|---------|--------|
| 12401 | `11000001110001` |
| 83893 | `10100011110110101` |
| 86522 | `10101000111111010` |
| 56782 | `1101110111001110` |
| 28221 | `110111000111101` |
| 19567 | `100110001101111` |
| 23148 | `101101001101100` |
| 42454 | `1010010111010110` |
| 15636 | `11110100010100` |

---

## Part D — Binary to Hexadecimal

| Binary | Hex |
|--------|-----|
| `1010111110011111` | **AF9F** |
| `0101001110101011` | **53AB** |
| `1100110001100110` | **CC66** |
| `1011111010100011` | **BEA3** |
| `0011011001101100` | **366C** |
| `1000001111010101` | **83D5** |
| `1010101010101010` | **AAAA** |
| `0110111101101101` | **6F6D** |
| `0010011101010111` | **2757** |
| `1111100010101011` | **F8AB** |

---

## Part E — Hexadecimal to Binary

| Hex | Binary |
|-----|--------|
| `78A7` | `111100010100111` |
| `B190` | `1011000110010000` |
| `FEE0` | `1111111011100000` |
| `1775` | `1011101110101` |
| `1E0D` | `1111000001101` |
| `9216` | `1001001000010110` |
| `7812` | `111100000010010` |
| `9067` | `1001000001100111` |
| `62E7` | `110001011100111` |
| `01AB` | `110101011` |

---

## Part F — Hexadecimal to Decimal

| Hex | Decimal |
|-----|---------|
| `AAAA` | **43690** |
| `9E3B` | **40507** |
| `D00D` | **53261** |
| `3D81` | **15745** |
| `18BE` | **6334** |
| `F990` | **63888** |
| `5467` | **21607** |
| `AB83` | **43907** |
| `2557` | **9559** |

> 💡 `9E3B` and `9e3b` give the same answer — hex is case-insensitive.

---

## Part G — Decimal to Hexadecimal

| Decimal | Hex |
|---------|-----|
| 42897 | **A791** |
| 62388 | **F3B4** |
| 56019 | **DAD3** |
| 97814 | **17E16** |
| 55632 | **D950** |
| 12593 | **3131** |
| 78648 | **13338** |
| 32077 | **7D4D** |

---

## Part H — Mixed Conversions

**1.** Decimal 10

```
Decimal:  10
Binary:   1010
Hex:      A
Back:     A = 10 ✅
```

**2.** Decimal 123

```
Decimal:  123
Binary:   1111011
Hex:      7B
Back:     7×16 + 11 = 112 + 11 = 123 ✅
```

**3.** Decimal 456

```
Decimal:  456
Binary:   111001000
Hex:      1C8
Back:     1×256 + 12×16 + 8 = 256 + 192 + 8 = 456 ✅
```

---

## Part I — Boolean Logic Proofs

**1.** `not((x OR y) AND z) = (not(x) AND not(y)) OR not(z)`

```
not((x OR y) AND z)
= not(x OR y) OR not(z)         [De Morgan: not(A AND B) = not(A) OR not(B)]
= (not(x) AND not(y)) OR not(z) [De Morgan: not(A OR B) = not(A) AND not(B)]
✅
```

**2.** `(not(x) OR y) AND not(z) = not(x OR z) OR (y AND not(z))`

```
(not(x) OR y) AND not(z)
= (not(x) AND not(z)) OR (y AND not(z))  [distributivity: (A OR B) AND C = (A AND C) OR (B AND C)]
= not(x OR z) OR (y AND not(z))          [De Morgan: not(A) AND not(B) = not(A OR B)]
✅
```

**3.** `not(not(x) AND not(y)) = x OR y`

```
not(not(x) AND not(y))
= not(not(x)) OR not(not(y))  [De Morgan: not(A AND B) = not(A) OR not(B)]
= x OR y                       [double negation: not(not(A)) = A]
✅
```

**4.** AND, OR, NOT using only NAND

```
NOT A     = A NAND A
A AND B   = (A NAND B) NAND (A NAND B)
A OR B    = (A NAND A) NAND (B NAND B)
```

---

← [Prev: Boolean Logic](./07-boolean-logic.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
