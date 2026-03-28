# 🔧 Topic 4 — Changing Permissions with `chmod`

> **`chmod` lets you change who can read, write, or execute a file.**

← [Prev: Numeric Permissions](./03-numeric-permissions.md) · [Next: Summary →](./05-summary.md)

---

## The `chmod` command

`chmod` stands for **change mode** — it changes the permissions on a file or directory.

There are two ways to use it:
- **Method A** — using letters (easier to read)
- **Method B** — using numbers (faster, used in real systems)

---

## Method A — Using letters

### The syntax

```bash
chmod who+permission filename    # add a permission
chmod who-permission filename    # remove a permission
```

### Who

| Letter | Who it applies to |
|--------|------------------|
| `u` | User (owner) |
| `g` | Group |
| `o` | Others |
| `a` | All (user + group + others) |

### Permission letters

| Letter | Permission |
|--------|-----------|
| `r` | Read |
| `w` | Write |
| `x` | Execute |

### Examples

```bash
chmod o+rx myfolder       # add read and execute for others
chmod o-r file.txt        # remove read from others
chmod g+w file.txt        # add write for group
chmod u+x script.sh       # add execute for owner
chmod a+r file.txt        # add read for everyone
chmod o-rwx secret.txt    # remove all permissions from others
```

**Before and after:**

```bash
ls -l file.txt
# -rw-r--r-- file.txt    ← others can only read

chmod o-r file.txt

ls -l file.txt
# -rw-r----- file.txt    ← others now have no permissions
```

> 💡 **Try it now:**
> 1. `touch testfile.txt`
> 2. `ls -l testfile.txt` — see default permissions
> 3. `chmod o-r testfile.txt`
> 4. `ls -l testfile.txt` — compare

---

## Method B — Using numbers

You learned numeric permissions in [Topic 3](./03-numeric-permissions.md).  
Apply them directly with `chmod`:

```bash
chmod 755 script.sh      # rwxr-xr-x
chmod 644 file.txt       # rw-r--r--
chmod 700 private.sh     # rwx------
chmod 600 secret.txt     # rw-------
```

**Before and after:**

```bash
ls -l script.sh
# -rw-r--r-- script.sh    ← not executable

chmod 755 script.sh

ls -l script.sh
# -rwxr-xr-x script.sh    ← now executable by everyone
```

---

## Making a file executable

A script is just a file — it only becomes runnable when you add execute permission.

**Step by step:**

```bash
# Step 1 — create a simple script
echo "echo Hello World!" > hello.sh

# Step 2 — try to run it (will fail)
./hello.sh
# bash: ./hello.sh: Permission denied ❌

# Step 3 — check current permissions
ls -l hello.sh
# -rw-r--r-- hello.sh    ← no x anywhere

# Step 4 — add execute permission
chmod +x hello.sh
# (same as chmod a+x, or chmod 755)

# Step 5 — check again
ls -l hello.sh
# -rwxr-xr-x hello.sh    ← x added ✅

# Step 6 — run it
./hello.sh
# Hello World!
```

> 💡 **Try it now:** Follow the 6 steps above

---

## Changing permissions on a directory

Directories also have permissions. The `x` bit on a directory means **"can enter it"** with `cd`.

```bash
chmod 755 myfolder      # others can list and enter
chmod 700 privatefolder # only owner can access
chmod o+rx myfolder     # add read + enter for others
```

> ⚠️ If a directory does not have `x` for a user, they cannot `cd` into it — even if they have `r`.

---

## Summary table

| Command | Result |
|---------|--------|
| `chmod o+rx dir` | Others can read and enter directory |
| `chmod o-r file` | Others cannot read file |
| `chmod g+w file` | Group can now write |
| `chmod +x file` | Everyone can execute |
| `chmod 755 file` | `rwxr-xr-x` |
| `chmod 644 file` | `rw-r--r--` |
| `chmod 700 file` | `rwx------` |
| `chmod 600 file` | `rw-------` |

---

← [Prev: Numeric Permissions](./03-numeric-permissions.md) · [Next: Summary →](./05-summary.md)
