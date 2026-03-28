# 🔢 Topic 1 — Number Systems Overview

> **Computers use different number systems. Understanding why makes everything else click.**

← [Back to README](./README.md) · [Next: Binary ↔ Decimal →](./02-binary-decimal.md)

---

## What is a number system?

A number system is a way of representing quantities using a set of symbols.

The number system you use every day — decimal — uses 10 symbols: `0 1 2 3 4 5 6 7 8 9`.

Computers use other systems because they are built from switches that are either **on** or **off** — that is, 1 or 0. Everything else is built on top of that.

---

## The four number systems you need to know

| System | Base | Symbols used | Example |
|--------|------|-------------|---------|
| **Binary** | 2 | 0, 1 | `1011` |
| **Octal** | 8 | 0–7 | `127` |
| **Decimal** | 10 | 0–9 | `45921` |
| **Hexadecimal** | 16 | 0–9, A–F | `9E3A` |

---

## What does "base" mean?

The **base** (also called radix) tells you how many different symbols the system uses, and what each position is worth.

In **decimal (base 10)**:

```
  4    5    9    2    1
  ^    ^    ^    ^    ^
 10⁴  10³  10²  10¹  10⁰
10000 1000  100   10    1
```

So 45921 = 4×10000 + 5×1000 + 9×100 + 2×10 + 1×1

In **binary (base 2)**, each position is a power of 2:

```
  1    0    1    1
  ^    ^    ^    ^
  2³   2²   2¹   2⁰
  8    4    2    1
```

So binary `1011` = 8 + 0 + 2 + 1 = **11** in decimal.

---

## Where each system is used

| System | Where you see it |
|--------|-----------------|
| Binary | Inside computers — how data is actually stored |
| Octal | Unix file permissions (`chmod 755`) |
| Decimal | Everyday numbers, IPv4 addresses (`192.168.1.1`) |
| Hexadecimal | MAC addresses, colour codes (`#FF5733`), memory addresses |

---

## Hexadecimal symbols

Hexadecimal needs 16 symbols but we only have 10 digits. Letters fill the gap:

| Decimal | Hex | Binary |
|---------|-----|--------|
| 0 | 0 | 0000 |
| 1 | 1 | 0001 |
| 2 | 2 | 0010 |
| 3 | 3 | 0011 |
| 4 | 4 | 0100 |
| 5 | 5 | 0101 |
| 6 | 6 | 0110 |
| 7 | 7 | 0111 |
| 8 | 8 | 1000 |
| 9 | 9 | 1001 |
| 10 | A | 1010 |
| 11 | B | 1011 |
| 12 | C | 1100 |
| 13 | D | 1101 |
| 14 | E | 1110 |
| 15 | F | 1111 |

> 💡 **Memorise this table.** It is the key to converting between binary and hexadecimal.  
> Note: hex is case-insensitive — `9E3A` and `9e3a` are the same number.

---

## Powers of 2 — essential reference

| Power | Value |
|-------|-------|
| 2⁰ | 1 |
| 2¹ | 2 |
| 2² | 4 |
| 2³ | 8 |
| 2⁴ | 16 |
| 2⁵ | 32 |
| 2⁶ | 64 |
| 2⁷ | 128 |
| 2⁸ | 256 |
| 2⁹ | 512 |
| 2¹⁰ | 1024 |
| 2¹¹ | 2048 |
| 2¹² | 4096 |
| 2¹³ | 8192 |
| 2¹⁴ | 16384 |
| 2¹⁵ | 32768 |

> 💡 You do not need to memorise all of these — just know how to build the table from 2⁰ upward by doubling each time.

---

← [Back to README](./README.md) · [Next: Binary ↔ Decimal →](./02-binary-decimal.md)
