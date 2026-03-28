# 🔀 Topic 7 — Boolean Logic

> **The foundation of how computers make decisions — gates, symbols, theorems, and proofs.**

← [Prev: Octal](./06-octal.md) · [Next: Practice Problems →](./08-practice.md)

---

## What is Boolean logic?

Boolean logic deals with values that are either **true** or **false** — represented as **1** or **0**.  
Every decision a computer makes comes down to these operations.

Each operation is called a **gate**. Gates can be combined to build any logic circuit.

---

## Notation used in this page

Different textbooks use different symbols. This page uses **word notation** for readability, with the standard symbol notation shown alongside.

| Meaning | Word notation | Symbol notation | Read as |
|---------|--------------|----------------|---------|
| NOT A | `NOT A` | `Ā` | "A bar" |
| A AND B | `A AND B` | `A · B` | "A dot B" |
| A OR B | `A OR B` | `A + B` | "A plus B" |
| A NAND B | `A NAND B` | `A · B` with bar over whole thing | "A dot B bar" |
| A NOR B | `A NOR B` | `A + B` with bar over whole thing | "A plus B bar" |
| A XOR B | `A XOR B` | `A ⊕ B` | "A xor B" |
| A XNOR B | `A XNOR B` | `A ⊕ B` with bar over whole thing | "A xor B bar" |

> 💡 The **bar** over a variable or expression means NOT. `Ā` = NOT A. `A̅B̅` = NOT(A AND B).

---

## The six gates

---

### NOT — invert the input

**Plain English:** Flip the value. 0 becomes 1, 1 becomes 0.

**Notation:**

```
Word:    NOT A
Symbol:  Ā
```

| A | Ā |
|---|---|
| 0 | **1** |
| 1 | **0** |

---

### AND — both must be true

**Plain English:** Output is 1 **only when every input is 1**.

**Notation:**

```
Word:    A AND B
Symbol:  A · B
```

| A | B | A · B |
|---|---|-------|
| 0 | 0 | **0** |
| 0 | 1 | **0** |
| 1 | 0 | **0** |
| 1 | 1 | **1** |

---

### OR — at least one must be true

**Plain English:** Output is 1 **when at least one input is 1**.

**Notation:**

```
Word:    A OR B
Symbol:  A + B
```

| A | B | A + B |
|---|---|-------|
| 0 | 0 | **0** |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | **1** |

---

### NAND — NOT AND

**Plain English:** Output is 0 **only when both inputs are 1** — everything else is 1.  
It is AND followed by NOT.

**Notation:**

```
Word:    A NAND B
Symbol:  A·B with bar  (NOT of A AND B)
```

| A | B | A · B | NAND |
|---|---|-------|------|
| 0 | 0 | 0 | **1** |
| 0 | 1 | 0 | **1** |
| 1 | 0 | 0 | **1** |
| 1 | 1 | 1 | **0** |

> 💡 **NAND is a universal gate** — you can build any other gate using only NAND.

---

### NOR — NOT OR

**Plain English:** Output is 1 **only when both inputs are 0** — everything else is 0.  
It is OR followed by NOT.

**Notation:**

```
Word:    A NOR B
Symbol:  A+B with bar  (NOT of A OR B)
```

| A | B | A + B | NOR |
|---|---|-------|-----|
| 0 | 0 | 0 | **1** |
| 0 | 1 | 1 | **0** |
| 1 | 0 | 1 | **0** |
| 1 | 1 | 1 | **0** |

> 💡 **NOR is also a universal gate** — you can build any other gate using only NOR.

---

### XOR — exclusive OR

**Plain English:** Output is 1 **when the inputs are different**. Same inputs → output 0.

**Notation:**

```
Word:    A XOR B
Symbol:  A ⊕ B
```

| A | B | A ⊕ B |
|---|---|-------|
| 0 | 0 | **0** |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | **0** |

**Alternative definition:**

```
A ⊕ B  =  (A + B) · A·B with bar
         = OR, but with "both true" excluded
```

---

### XNOR — exclusive NOR (also called XAND)

**Plain English:** Output is 1 **when the inputs are the same**. Different inputs → output 0.  
It is XOR followed by NOT.

**Notation:**

```
Word:    A XNOR B
Symbol:  A ⊕ B with bar  (NOT of XOR)
```

| A | B | A ⊕ B | XNOR |
|---|---|-------|------|
| 0 | 0 | 0 | **1** |
| 0 | 1 | 1 | **0** |
| 1 | 0 | 1 | **0** |
| 1 | 1 | 0 | **1** |

> 💡 XNOR is also called **equivalence** — output is 1 when A and B are equal.

---

## All six gates — comparison table

| A | B | Ā | A · B | A + B | NAND | NOR | A ⊕ B | XNOR |
|---|---|---|-------|-------|------|-----|-------|------|
| 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 | 1 | 0 | 1 | 0 |
| 1 | 0 | 0 | 0 | 1 | 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 | 1 |

---

## Boolean Theorems

These laws let you simplify and transform boolean expressions.

In the theorems below:
- `Ā` means NOT A
- `·` means AND
- `+` means OR

---

### Identity laws

```
A · 1 = A
A + 0 = A
```

AND with 1 changes nothing. OR with 0 changes nothing.

---

### Null (domination) laws

```
A · 0 = 0
A + 1 = 1
```

AND with 0 is always 0 — A does not matter.  
OR with 1 is always 1 — A does not matter.

---

### Idempotent laws

```
A · A = A
A + A = A
```

Using the same input twice has no effect.

---

### Complement laws

```
A · Ā = 0
A + Ā = 1
```

A AND its own opposite is always 0.  
A OR its own opposite is always 1.

---

### Double negation law

```
Ā̄ = A
```

Two NOTs cancel. The bar over a bar cancels out.

---

### Commutative laws

```
A · B = B · A
A + B = B + A
```

Order of inputs does not matter for AND or OR.

---

### Associative laws

```
(A · B) · C = A · (B · C)
(A + B) + C = A + (B + C)
```

Grouping (parentheses) does not matter — you can regroup freely.

---

### Distributive laws

```
A · (B + C) = (A · B) + (A · C)
A + (B · C) = (A + B) · (A + C)
```

AND distributes over OR, and OR distributes over AND.  
Both directions work — unlike normal algebra where only one does.

---

### Absorption laws

```
A · (A + B) = A
A + (A · B) = A
```

The larger expression collapses back to A.

**Proof of** `A + (A · B) = A`:
```
  A + (A · B)
= (A · 1) + (A · B)     ← identity: A = A · 1
= A · (1 + B)            ← distributivity
= A · 1                  ← null: 1 + B = 1
= A                      ← identity
✅
```

---

### De Morgan's laws

```
A · B with bar  =  Ā + B̄
A + B with bar  =  Ā · B̄
```

**In plain English:**
- NOT(A AND B) → NOT A OR NOT B — if the AND fails, at least one must be 0
- NOT(A OR B) → NOT A AND NOT B — if the OR fails, both must be 0

**Memory trick — push the bar inside, flip the operator:**

```
Bar over (A · B)  →  Ā + B̄   (AND flips to OR)
Bar over (A + B)  →  Ā · B̄   (OR flips to AND)
```

---

### XOR identities

```
A ⊕ 0 = A
A ⊕ 1 = Ā
A ⊕ A = 0
A ⊕ Ā = 1
```

XOR with 0 → unchanged.  
XOR with 1 → flipped (same as NOT).  
XOR with itself → always 0.  
XOR with its complement → always 1.

---

## Summary table — all theorems

| Law | AND / · form | OR / + form |
|-----|-------------|------------|
| Identity | `A · 1 = A` | `A + 0 = A` |
| Null | `A · 0 = 0` | `A + 1 = 1` |
| Idempotent | `A · A = A` | `A + A = A` |
| Complement | `A · Ā = 0` | `A + Ā = 1` |
| Double negation | `Ā̄ = A` | — |
| Commutative | `A · B = B · A` | `A + B = B + A` |
| Associative | `(A · B) · C = A · (B · C)` | `(A + B) + C = A + (B + C)` |
| Distributive | `A · (B + C) = (A · B) + (A · C)` | `A + (B · C) = (A + B) · (A + C)` |
| Absorption | `A · (A + B) = A` | `A + (A · B) = A` |
| De Morgan | `A·B bar = Ā + B̄` | `A+B bar = Ā · B̄` |

---

## Universal gates — build everything from one gate

### Build everything from NAND

Let `NAND(A,B)` = A·B with bar

```
NOT A       =  NAND(A, A)
A · B       =  NAND( NAND(A,B), NAND(A,B) )
A + B       =  NAND( NAND(A,A), NAND(B,B) )
A ⊕ B      =  NAND( NAND(A, NAND(A,B)), NAND(B, NAND(A,B)) )
```

### Build everything from NOR

Let `NOR(A,B)` = A+B with bar

```
NOT A       =  NOR(A, A)
A + B       =  NOR( NOR(A,B), NOR(A,B) )
A · B       =  NOR( NOR(A,A), NOR(B,B) )
```

---

## Worked proofs

In each proof, the notation is:
- `Ā` = NOT A, `B̄` = NOT B, `C̄` = NOT C
- `·` = AND, `+` = OR

---

### Proof 1 — `(x + y) · z bar = (x̄ · ȳ) + z̄`

Using word notation: `NOT((x OR y) AND z) = (NOT x AND NOT y) OR NOT z`

```
  (x + y) · z  with bar
= (x + y) bar + z̄          ← De Morgan: P·Q bar = P bar + Q bar
= (x̄ · ȳ) + z̄              ← De Morgan: (x+y) bar = x̄ · ȳ
✅
```

---

### Proof 2 — `x̄ · ȳ bar = x + y`

Using word notation: `NOT(NOT x AND NOT y) = x OR y`

```
  x̄ · ȳ  with bar
= x̄ bar + ȳ bar            ← De Morgan: P·Q bar = P bar + Q bar
= x + y                    ← double negation: x̄ bar = x
✅
```

---

### Proof 3 — `(x̄ + y) · z̄ = (x + z) bar + (y · z̄)`

Using word notation: `(NOT x OR y) AND NOT z = NOT(x OR z) OR (y AND NOT z)`

```
  (x̄ + y) · z̄
= (x̄ · z̄) + (y · z̄)       ← distributivity: (P + Q) · R = (P · R) + (Q · R)
= (x + z) bar + (y · z̄)    ← De Morgan: x̄ · z̄ = (x + z) bar
✅
```

---

## Tips for proofs

1. **Work on one side only** — transform it step by step until it matches the other side
2. **Spot De Morgan:** any bar over `P · Q` or `P + Q` — push the bar inside and flip the operator
3. **Spot distributivity:** any `(P + Q) · R` or `(P · Q) + R` — expand it
4. **Double negation cancels:** bar over bar = gone
5. **Write every step** with the rule used — never skip steps

---

← [Prev: Octal](./06-octal.md) · [Next: Practice Problems →](./08-practice.md)
