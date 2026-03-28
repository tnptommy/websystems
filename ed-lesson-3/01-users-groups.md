# 👤 Topic 1 — Users & Groups

> **Before permissions can be applied, Linux must know who you are.**

← [Back to README](./README.md) · [Next: Reading Permissions →](./02-reading-permissions.md)

---

## Why users and groups exist

Linux is designed to run with **multiple users at the same time** — on servers, shared machines, and lab environments.

Permissions only make sense once Linux knows:
- **Who** is trying to access a file
- **What group** that person belongs to

---

## Your user

When you open the terminal, you are logged in as a specific user.

To see who you are:

```bash
whoami
# username
```

To see all users on the system:

```bash
less /etc/passwd
```

Each line in `/etc/passwd` represents one user on the system.  
The format is:

```
username:x:UID:GID:description:home_directory:shell
```

Example line:
```
root:x:0:0:root:/root:/bin/bash
```

| Field | Meaning |
|-------|---------|
| `root` | Username |
| `x` | Password placeholder (stored elsewhere) |
| `0` | User ID (UID) — root is always 0 |
| `0` | Group ID (GID) |
| `root` | Description |
| `/root` | Home directory |
| `/bin/bash` | Default shell |

> 💡 **Try it now:** `less /etc/passwd` — press `q` to quit

---

## Your group

Every user also belongs to one or more **groups**.  
Groups let you apply the same permissions to multiple users at once.

To see all groups on the system:

```bash
less /etc/group
```

To see which groups your current user belongs to:

```bash
groups
# username sudo staff
```

---

## Why this matters for permissions

Every file on Linux has **three levels of access** based on identity:

| Level | Who it applies to |
|-------|------------------|
| **User** (owner) | The person who owns the file |
| **Group** | Anyone in the file's assigned group |
| **Others** | Everyone else on the system |

When you access a file, Linux checks:
1. Are you the **owner**? → apply owner permissions
2. Are you in the **group**? → apply group permissions
3. Are you **neither**? → apply others permissions

You will see exactly how this looks in [Topic 2 — Reading Permissions](./02-reading-permissions.md).

---

← [Back to README](./README.md) · [Next: Reading Permissions →](./02-reading-permissions.md)
