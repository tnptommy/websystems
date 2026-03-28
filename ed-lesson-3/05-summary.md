# ✅ Topic 5 — Summary & Cheat Sheet

> **All permission concepts and commands in one place.**

← [Prev: chmod](./04-chmod.md) · [Back to README](./README.md)

---

## Key concepts

| Concept | What it means |
|---------|--------------|
| User | The owner of the file |
| Group | Users who share the same group |
| Others | Everyone else on the system |
| `r` | Read — view contents |
| `w` | Write — modify contents |
| `x` | Execute — run (file) or enter (directory) |
| `-` | No permission |

---

## Numeric values — memorise these

```
r = 4
w = 2
x = 1
- = 0

rwx = 7    (4+2+1)
rw- = 6    (4+2+0)
r-x = 5    (4+0+1)
r-- = 4    (4+0+0)
--- = 0    (0+0+0)
```

---

## Cheat Sheet

```bash
# ── VIEWING ───────────────────────────────────────────────────
ls -l                        # view permissions for files in current dir
ls -l filename               # view permissions for a specific file
stat filename                # view numeric permissions

# ── USERS & GROUPS ────────────────────────────────────────────
whoami                       # see your current username
groups                       # see your groups
less /etc/passwd             # list all users on the system
less /etc/group              # list all groups on the system

# ── chmod WITH LETTERS ────────────────────────────────────────
chmod u+x file               # add execute for owner
chmod g+w file               # add write for group
chmod o-r file               # remove read from others
chmod o+rx directory         # add read and enter for others
chmod a+r file               # add read for everyone
chmod o-rwx file             # remove all permissions from others

# ── chmod WITH NUMBERS ────────────────────────────────────────
chmod 755 file               # rwxr-xr-x  (scripts, directories)
chmod 644 file               # rw-r--r--  (regular files)
chmod 700 file               # rwx------  (private scripts)
chmod 600 file               # rw-------  (private files)
chmod 777 file               # rwxrwxrwx  (avoid on servers!)

# ── MAKING A SCRIPT EXECUTABLE ────────────────────────────────
echo "echo Hello!" > hello.sh    # create a simple script
chmod +x hello.sh                # make it executable
./hello.sh                       # run it
```

---

## Common permission numbers

| Number | String | When to use |
|--------|--------|-------------|
| `755` | `rwxr-xr-x` | Scripts, programs, directories |
| `644` | `rw-r--r--` | Regular text files, config files |
| `700` | `rwx------` | Private scripts — only you |
| `600` | `rw-------` | Private files — only you |
| `777` | `rwxrwxrwx` | Everyone full access — avoid this |

---

## Reading `ls -l` output

```
-  rw-  r--  r--   1   root  root  1234  Jan 10  file.txt
^  ^^^  ^^^  ^^^   ^   ^^^^  ^^^^  ^^^^
|   |    |    |    |    |     |     |
|   |    |    |    |    |     |    file size
|   |    |    |    |    |    group owner
|   |    |    |    |   user (owner)
|   |    |    |   number of hard links
|   |    |   others permissions
|   |   group permissions
|  user (owner) permissions
file type (- = file, d = directory)
```

---

## Read the question → know what to do

| Question says | Use this |
|---------------|----------|
| *"view permissions"* | `ls -l` |
| *"who owns the file"* | `ls -l` → 3rd column |
| *"what are the numeric permissions"* | `stat filename` |
| *"add execute for owner"* | `chmod u+x file` or `chmod 755 file` |
| *"remove read from others"* | `chmod o-r file` or `chmod 640 file` |
| *"make a script runnable"* | `chmod +x script.sh` then `./script.sh` |
| *"only owner can access"* | `chmod 700 file` |
| *"everyone can read"* | `chmod a+r file` or `chmod 644 file` |
| *"what does 755 mean"* | `rwxr-xr-x` — owner full, group/others read+execute |
| *"what does 644 mean"* | `rw-r--r--` — owner read+write, group/others read only |

---

## Check your work before submitting

```bash
# Check the current permissions on a file
ls -l filename

# Check numeric permissions
stat filename

# Verify a script is executable
ls -l script.sh
# should show x in the permission string

# Run the script to confirm it works
./script.sh
```

---

← [Prev: chmod](./04-chmod.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
