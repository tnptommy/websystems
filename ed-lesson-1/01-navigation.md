# 📍 Topic 1 — Working Directory & Navigation

> **At any moment in the terminal, you are always inside a folder. This is called your working directory.**

← [Back to README](./README.md) · [Next: Files & Directories →](./02-files-directories.md)

---

## What is a working directory?

The biggest difference between the terminal and a graphical file explorer is this:

In a graphical interface, you can see all your folders at once and click between them.  
In the terminal, you are always **inside one specific folder** at a time — your working directory.

Everything you type affects that folder unless you say otherwise.

---

## `pwd` — where am I right now?

`pwd` stands for **print working directory**. It tells you which folder you are currently in.

```bash
pwd
# /home/username
```

> 💡 **Try it now:** Type `pwd` and press Enter. You will see your current location.

---

## `cd` — move to a different folder

`cd` stands for **change directory**.

```bash
cd /home          # go to the /home folder
cd Documents      # go into the Documents folder (inside current folder)
cd ..             # go up one level — to the parent folder
cd                # go back to your home folder from anywhere
cd ~              # same as above — ~ is a shortcut for home
```

**What is `..`?**

Every folder has a parent — the folder that contains it.  
`..` means "the folder above this one".

```bash
pwd
# /home/username/Documents

cd ..

pwd
# /home/username        ← moved up one level
```

> 💡 **Try it now:** Type `cd ..` then `pwd` to see where you ended up.

---

## Absolute paths vs relative paths

There are two ways to describe where a folder is.

### Absolute path

An absolute path **always starts with `/`** — the root of the entire file system.  
It works from anywhere, no matter where you currently are.

```bash
cd /home/username/Documents     # always goes to this exact location
cd /course/linuxgym             # works from anywhere
```

### Relative path

A relative path **starts from your current location**.  
It only works if that folder actually exists where you currently are.

```bash
cd Documents      # goes into Documents inside your CURRENT folder
cd linuxgym       # only works if linuxgym exists in your current folder
```

**Easy way to remember:**

| Starts with | Type | Works from |
|-------------|------|-----------|
| `/` | Absolute | Anywhere |
| a folder name | Relative | Current location only |

---

## Special path shortcuts

| Shortcut | Meaning |
|----------|---------|
| `~` | Your home directory |
| `.` | The current directory (where you are right now) |
| `..` | The parent directory (one level up) |

**The `.` shortcut** is useful when copying files to your current location:

```bash
cp /course/linuxgym/file.txt .
# copies file.txt into wherever you currently are
```

---

## The file system layout

The file system starts at `/` (called **root**) and branches out into folders:

```
/
├── home/
│   └── username/       ← your home folder (~)
├── course/
│   └── linuxgym/       ← where lab files are stored
├── etc/
└── usr/
```

- `/` = the very top of the file system
- `/home/username` = your home folder
- `/course/linuxgym` = where most lab exercises live

---

## `man` — read the manual for any command

Every command has a manual page. To read it:

```bash
man pwd       # manual for pwd
man cd        # manual for cd
man ls        # manual for ls
```

**How to use `man`:**

| Key | Action |
|-----|--------|
| `Space` | Jump to next page |
| `↑` / `↓` | Move up / down one line |
| `/word` then `Enter` | Search for "word" |
| `q` | Quit and go back to terminal |

> 💡 **Try it now:** `man pwd` — press `q` when done

---

## Common mistakes

**Mistake 1 — using a relative path from the wrong location:**
```bash
pwd
# /home/username

cd linuxgym
# Error: No such file or directory
# because linuxgym is not inside /home/username

cd /course/linuxgym    # ✅ use absolute path instead
```

**Mistake 2 — forgetting `cd` goes to home with no argument:**
```bash
cd            # ✅ goes to home folder — same as cd ~
cd /          # ❌ this goes to root, not home
```

---

← [Back to README](./README.md) · [Next: Files & Directories →](./02-files-directories.md)
