# 🔀 Topic 7 — Boolean Logic

> **The foundation of how computers make decisions — AND, OR, NOT, and NAND.**

← [Prev: Octal](./06-octal.md) · [Next: Practice Problems →](./08-practice.md)

---

## What is Boolean logic?

Boolean logic deals with values that are either **true** or **false** (1 or 0).  
Every decision a computer makes comes down to these operations.

---

## The three basic operations

### NOT — flip the value

```
NOT 0 = 1
NOT 1 = 0
```

In notation: `not(A)` or `¬A` or `!A`

---

### AND — both must be true

| A | B | A AND B |
|---|---|---------|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Result is 1 **only when both inputs are 1**.

---

### OR — at least one must be true

| A | B | A OR B |
|---|---|--------|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Result is 1 **when at least one input is 1**.

---

## NAND — NOT AND

NAND is AND followed by NOT. It is the opposite of AND.

| A | B | A NAND B |
|---|---|----------|
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Result is 0 **only when both inputs are 1** — everything else is 1.

**NAND is important** because you can build AND, OR, and NOT using only NAND gates. It is called a **universal gate**.

---

## Expressing AND, OR, NOT using only NAND

**NOT using NAND:**

```
not(A) = A NAND A
```

Because: A NAND A = not(A AND A) = not(A)

**AND using NAND:**

```
A AND B = not(A NAND B)
        = (A NAND B) NAND (A NAND B)
```

**OR using NAND:**

```
A OR B = (A NAND A) NAND (B NAND B)
       = not(A) NAND not(B)
       = not(not(A) AND not(B))    ← De Morgan's law
       = A OR B ✅
```

---

## De Morgan's Laws

De Morgan's laws let you convert between AND and OR when negating:

```
not(A AND B) = not(A) OR not(B)
not(A OR B)  = not(A) AND not(B)
```

**In plain English:**
- NOT (A and B) = NOT A, or NOT B (either one failing breaks the AND)
- NOT (A or B) = NOT A, and NOT B (both must fail to break the OR)

---

## Distributivity

Just like in algebra, boolean operations distribute:

```
(x OR y) AND z  =  (x AND z) OR (y AND z)
(x AND y) OR z  =  (x OR z) AND (y OR z)
```

---

## Worked proofs — using De Morgan and distributivity

### Prove: `not((x OR y) AND z) = (not(x) AND not(y)) OR not(z)`

```
Start:    not((x OR y) AND z)

Step 1 — apply De Morgan's law to the outer NOT:
= not(x OR y) OR not(z)

Step 2 — apply De Morgan's law to not(x OR y):
= (not(x) AND not(y)) OR not(z)

Done ✅
```

---

### Prove: `not(not(x) AND not(y)) = x OR y`

```
Start:    not(not(x) AND not(y))

Step 1 — apply De Morgan's law:
= not(not(x)) OR not(not(y))

Step 2 — double negation cancels:
= x OR y

Done ✅
```

---

### Prove: `(not(x) OR y) AND not(z) = not(x OR z) OR (y AND not(z))`

```
Start:    (not(x) OR y) AND not(z)

Step 1 — distribute AND over OR:
= (not(x) AND not(z)) OR (y AND not(z))

Step 2 — apply De Morgan's law to (not(x) AND not(z)):
= not(x OR z) OR (y AND not(z))

Done ✅
```

---

## Key rules summary

| Rule | Formula |
|------|---------|
| Double negation | `not(not(A)) = A` |
| De Morgan 1 | `not(A AND B) = not(A) OR not(B)` |
| De Morgan 2 | `not(A OR B) = not(A) AND not(B)` |
| Distributivity 1 | `(x OR y) AND z = (x AND z) OR (y AND z)` |
| Distributivity 2 | `(x AND y) OR z = (x OR z) AND (y OR z)` |

---

## Tips for proofs

1. Work on one side only — transform it step by step until it matches the other side
2. Look for De Morgan opportunities: any `not(... AND ...)` or `not(... OR ...)`
3. Look for distributivity: any `(... OR ...) AND ...` or `(... AND ...) OR ...`
4. Double negation cancels: `not(not(X)) = X`

---

← [Prev: Octal](./06-octal.md) · [Next: Practice Problems →](./08-practice.md)
