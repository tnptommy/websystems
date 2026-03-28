# 🔢 Topic 6 — Octal (Base 8)

> **Octal uses 3 bits per digit — you already know it from Unix file permissions.**

← [Prev: Binary Arithmetic](./05-binary-arithmetic.md) · [Next: Boolean Logic →](./07-boolean-logic.md)

---

## What is octal?

Octal is base 8 — it uses the digits `0` through `7`.

Each octal digit maps exactly to **3 binary digits**, just like hexadecimal maps to 4.

| Octal | Binary |
|-------|--------|
| 0 | 000 |
| 1 | 001 |
| 2 | 010 |
| 3 | 011 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |

---

## Where you have already seen octal

Unix file permissions use octal:

```bash
chmod 755 script.sh
```

Here `755` is an octal number:
- `7` = `111` = rwx (read, write, execute)
- `5` = `101` = r-x (read, execute)
- `5` = `101` = r-x (read, execute)

---

## Octal to Binary

**Method:** Replace each octal digit with its 3-bit binary equivalent.

### Example — convert `127` to binary

```
1 = 001
2 = 010
7 = 111
```

Result: `001010111`

You can drop the leading zeros if they are at the very start: **`1010111`**

---

### Example — convert `321` to binary

```
3 = 011
2 = 010
1 = 001
```

Result: `011010001`

Drop leading zero: **`11010001`**

---

## Binary to Octal

**Method:** Split binary into groups of **3** from the right. Pad with leading zeros if needed. Replace each group.

### Example — convert `001010111` to octal

Already in groups of 3:

```
001  010  111
 1    2    7
```

Result: **`127`**

---

### Example — convert `11010001` to octal

Pad to multiple of 3 from the left:

```
011  010  001
 3    2    1
```

Result: **`321`**

---

## Octal ↔ Decimal

You can convert via binary, or use powers of 8:

| Power | Value |
|-------|-------|
| 8⁰ | 1 |
| 8¹ | 8 |
| 8² | 64 |
| 8³ | 512 |

### Example — octal `127` to decimal

```
1 × 64 = 64
2 × 8  = 16
7 × 1  = 7
Total  = 87
```

**Check:** Binary `1010111` = 64 + 16 + 4 + 2 + 1 = 87 ✅

---

## Octal vs Hexadecimal — comparison

| | Octal | Hexadecimal |
|-|-------|-------------|
| Base | 8 | 16 |
| Digits | 0–7 | 0–9, A–F |
| Bits per digit | 3 | 4 |
| Common use | Unix permissions | Networking, memory, colours |

---

← [Prev: Binary Arithmetic](./05-binary-arithmetic.md) · [Next: Boolean Logic →](./07-boolean-logic.md)
