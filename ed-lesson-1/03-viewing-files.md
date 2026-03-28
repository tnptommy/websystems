# 👁️ Topic 3 — Viewing Files

> **Read what is inside a file — without opening a text editor.**

← [Prev: Files & Directories](./02-files-directories.md) · [Next: Redirection →](./04-redirection.md)

---

## Four commands for reading files

| Command | What it does |
|---------|-------------|
| `cat` | Print the entire file |
| `head` | Print the first N lines |
| `tail` | Print the last N lines |
| `wc` | Count lines, words, or characters |

---

## `cat` — print the entire file

`cat` prints every line of a file to the screen.

```bash
cat notes.txt
# Hello World
# This is my notes file.
# Goodbye.
```

**Problem with `cat` on long files:**  
If the file has thousands of lines, it scrolls past too fast to read.  
Use `head` or `tail` instead for large files.

> 💡 **Try it now:** `cat /etc/passwd`

---

## `head` — print the first lines

`head` prints only the **top** of a file. Default is 10 lines.

```bash
head notes.txt            # first 10 lines (default)
head -n 5 notes.txt       # first 5 lines
head -n 20 notes.txt      # first 20 lines
```

**When to use `head`:**  
When you want a quick look at what a file contains without printing all of it.

```bash
head /etc/passwd
# root:x:0:0:root:/root:/bin/bash
# daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
# ...first 10 lines only
```

> 💡 **Try it now:** `head -n 5 /etc/passwd`

---

## `tail` — print the last lines

`tail` prints only the **bottom** of a file. Default is 10 lines.

```bash
tail notes.txt            # last 10 lines (default)
tail -n 5 notes.txt       # last 5 lines
tail -n 50 notes.txt      # last 50 lines
```

**When to use `tail`:**  
When you want to see the most recent entries — for example, the end of a log file.

```bash
tail -n 3 /etc/passwd
# ...last 3 lines of the file
```

**`tail -f` — follow a file as it grows:**

```bash
tail -f /var/log/syslog
# keeps watching the file and prints new lines as they are added
# press Ctrl+C to stop
```

> 💡 **Try it now:** `tail -n 5 /etc/passwd`

---

## `wc` — count things inside a file

`wc` stands for **word count**. It counts lines, words, and characters.

```bash
wc notes.txt
#  3   8   44   notes.txt
#  ^   ^    ^       ^
# lines words chars  filename
```

**Count just one thing:**

```bash
wc -l notes.txt    # lines only:      3 notes.txt
wc -w notes.txt    # words only:      8 notes.txt
wc -m notes.txt    # characters only: 44 notes.txt
```

**Practical example:**

```bash
wc -l /etc/passwd
# 35 /etc/passwd
# → there are 35 user accounts on this system
```

> ⚠️ Notice that `wc` always prints the **filename** next to the number.  
> If you need the number only, see [Ed Lesson 5 — Pipe](../ed-lesson-5/02-pipe.md).

> 💡 **Try it now:** `wc -l /etc/passwd`

---

## Combine commands — a preview

These commands become more powerful when combined with each other.

**Count how many lines `head` returns:**
```bash
head -n 20 /etc/passwd | wc -l
# 20
```

**Read the last 5 lines and count their characters:**
```bash
tail -n 5 /etc/passwd | wc -m
# 312
```

You will learn exactly how `|` (pipe) works in [Ed Lesson 5](../ed-lesson-5/README.md).

---

## Summary table

| Command | Flag | What it does |
|---------|------|-------------|
| `cat file` | — | Print entire file |
| `head file` | — | First 10 lines |
| `head -n N file` | `-n` | First N lines |
| `tail file` | — | Last 10 lines |
| `tail -n N file` | `-n` | Last N lines |
| `tail -f file` | `-f` | Follow file as it grows |
| `wc file` | — | Lines, words, characters |
| `wc -l file` | `-l` | Lines only |
| `wc -w file` | `-w` | Words only |
| `wc -m file` | `-m` | Characters only |

---

← [Prev: Files & Directories](./02-files-directories.md) · [Next: Redirection →](./04-redirection.md)
