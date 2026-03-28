# 👁️ Topic 2 — Reading Permissions

> **Learn to read the permission string from `ls -l` output.**

← [Prev: Users & Groups](./01-users-groups.md) · [Next: Numeric Permissions →](./03-numeric-permissions.md)

---

## Viewing permissions with `ls -l`

To see permissions for files in your current directory:

```bash
ls -l
```

Example output:

```
-rw-r--r-- 1 root root 1234 Jan 10 14:32 file.txt
drwxr-xr-x 2 user group 4096 Jan 10 14:30 myfolder
```

There is a lot of information here. Let's break it down piece by piece.

---

## Reading the full output

```
-rw-r--r--  1  root  root  1234  Jan 10 14:32  file.txt
^          ^   ^     ^     ^     ^              ^
|          |   |     |     |     |              filename
|          |   |     |     |     date modified
|          |   |     |     file size (bytes)
|          |   |     group owner
|          |   user (owner)
|          number of hard links
permission string (10 characters)
```

---

## The permission string — 10 characters

```
- r w - r - - r - -
^ ^^^ ^^^ ^^^
| |   |   |
| |   |   └── Others permissions (everyone else)
| |   └─────── Group permissions
| └─────────── User (owner) permissions
└───────────── File type
```

### Character 1 — File type

| Symbol | Meaning |
|--------|---------|
| `-` | Regular file |
| `d` | Directory (folder) |
| `l` | Symbolic link |

### Characters 2–4 — User (owner) permissions

```
rw-    ← owner can read and write, but NOT execute
```

### Characters 5–7 — Group permissions

```
r--    ← group can read only
```

### Characters 8–10 — Others permissions

```
r--    ← everyone else can read only
```

---

## Permission symbols

| Symbol | Meaning | On a file | On a directory |
|--------|---------|-----------|----------------|
| `r` | Read | Can view file contents | Can list files inside |
| `w` | Write | Can modify file | Can create/delete files inside |
| `x` | Execute | Can run as a program | Can enter (cd into) the directory |
| `-` | No permission | Denied | Denied |

---

## Full examples

**Example 1:**
```
-rw-r--r--   file.txt
```

| Who | Permissions | Can do |
|-----|-------------|--------|
| Owner | `rw-` | Read and write |
| Group | `r--` | Read only |
| Others | `r--` | Read only |

---

**Example 2:**
```
drwxr-xr-x   myfolder
```

| Who | Permissions | Can do |
|-----|-------------|--------|
| Owner | `rwx` | Read, write, and enter folder |
| Group | `r-x` | List files and enter folder |
| Others | `r-x` | List files and enter folder |

---

**Example 3:**
```
-rwxr-xr-x   script.sh
```

| Who | Permissions | Can do |
|-----|-------------|--------|
| Owner | `rwx` | Read, write, and run |
| Group | `r-x` | Read and run |
| Others | `r-x` | Read and run |

---

## Try reading permissions yourself

```bash
ls -l /etc/passwd
# -rw-r--r-- 1 root root 2847 Jan 10 file

ls -l /etc/shadow
# -rw-r----- 1 root shadow 1234 Jan 10 file
# notice: others have NO permissions on shadow
```

> 💡 **Try it now:** Run `ls -l ~` and read the permissions on each file in your home folder

---

← [Prev: Users & Groups](./01-users-groups.md) · [Next: Numeric Permissions →](./03-numeric-permissions.md)
