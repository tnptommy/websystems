# 🔢 Topic 3 — Numeric Permissions

> **A faster way to read and write permissions using numbers.**

← [Prev: Reading Permissions](./02-reading-permissions.md) · [Next: chmod →](./04-chmod.md)

---

## Why numbers?

Instead of writing `rwx` every time, Linux lets you use **numbers** to represent permissions.  
This is faster and is what you will see used in real systems.

---

## The values

Each permission letter has a number value:

| Symbol | Meaning | Value |
|--------|---------|-------|
| `r` | Read | **4** |
| `w` | Write | **2** |
| `x` | Execute | **1** |
| `-` | No permission | **0** |

To get the number for a set of permissions, **add the values together**.

---

## Calculating permissions

| Permission | Calculation | Result |
|------------|-------------|--------|
| `rwx` | 4 + 2 + 1 | **7** |
| `rw-` | 4 + 2 + 0 | **6** |
| `r-x` | 4 + 0 + 1 | **5** |
| `r--` | 4 + 0 + 0 | **4** |
| `-wx` | 0 + 2 + 1 | **3** |
| `-w-` | 0 + 2 + 0 | **2** |
| `--x` | 0 + 0 + 1 | **1** |
| `---` | 0 + 0 + 0 | **0** |

---

## Three digits — one for each group

A full permission number has **3 digits**:

```
7  5  5
^  ^  ^
|  |  └── Others
|  └───── Group
└──────── User (owner)
```

### Reading `755`

```
7 = rwx   → owner can read, write, execute
5 = r-x   → group can read and execute
5 = r-x   → others can read and execute
```

Full string: `-rwxr-xr-x`

### Reading `644`

```
6 = rw-   → owner can read and write
4 = r--   → group can read only
4 = r--   → others can read only
```

Full string: `-rw-r--r--`

---

## Common permission numbers

| Number | String | Typical use |
|--------|--------|-------------|
| `755` | `rwxr-xr-x` | Scripts, programs, directories |
| `644` | `rw-r--r--` | Regular files (text, config) |
| `700` | `rwx------` | Private scripts — only you can use |
| `600` | `rw-------` | Private files — only you can read/write |
| `777` | `rwxrwxrwx` | Everyone full access — avoid this on servers |

---

## Practice — convert these yourself

Try to work out the number before checking the answer:

| Permission string | Answer |
|------------------|--------|
| `-rwxr-xr-x` | `755` |
| `-rw-r--r--` | `644` |
| `-rwx------` | `700` |
| `-rw-rw-r--` | `664` |
| `drwxr-xr-x` | `755` (directory) |

**How to check your answer:**

```bash
ls -l filename       # see the current permission string
stat filename        # shows numeric permissions directly
```

---

## Quick reference

```
r = 4
w = 2
x = 1

rwx = 7
rw- = 6
r-x = 5
r-- = 4
--- = 0

755 = rwxr-xr-x   (common for scripts and folders)
644 = rw-r--r--   (common for regular files)
```

---

← [Prev: Reading Permissions](./02-reading-permissions.md) · [Next: chmod →](./04-chmod.md)
