# ⚙️ Topic 4 — New Commands

> **`wc`, `tail`, `cp -r`, `ls -S` — four commands you need for this lab.**

← [Prev: Wildcards](./03-wildcards.md) · [Next: Summary →](./05-summary.md)

---

## `wc` — count lines, words, and characters

`wc` stands for **word count**. It counts things inside a file.

```bash
wc notes.txt
#  47   312   1842   notes.txt
#   ^    ^     ^         ^
# lines words chars   filename
```

Count just one thing at a time:

```bash
wc -l notes.txt    # 47 notes.txt    ← lines only
wc -w notes.txt    # 312 notes.txt   ← words only
wc -m notes.txt    # 1842 notes.txt  ← characters only
```

> 💡 **Try it now:** `wc -l /etc/passwd`

---

## `wc` through a pipe — remove the filename

**Problem:** `wc` always prints the filename next to the number.

```bash
wc -m notes.txt
# 1842 notes.txt   ← only want the number, not the filename
```

**Solution — use `cat` and pipe:**

```bash
cat notes.txt | wc -m
# 1842             ← number only ✅
```

Why does this work?

```
wc notes.txt    → wc sees the filename → prints number AND filename
cat notes.txt
     |          → wc only sees text coming in
wc -m           → does not know the filename → prints number only
```

Save the result:

```bash
cat notes.txt | wc -m > charcount.txt
cat charcount.txt
# 1842   ✅
```

> 💡 **Try it now:** `cat /etc/passwd | wc -l`

---

## `tail` — get the last lines of a file

`cat` reads the **whole file**. `tail` only reads the **end**.

```bash
tail notes.txt           # last 10 lines (default)
tail -n 5 notes.txt      # last 5 lines
tail -n 50 notes.txt     # last 50 lines
```

Save to a file:

```bash
tail -n 50 notes.txt > last50.txt
```

Check the line count:

```bash
wc -l last50.txt
# 50  ✅
```

> ⚠️ `tail` counts **all** lines — empty lines count too. No extra options needed.

`head` does the opposite:

```bash
head -n 5 notes.txt      # first 5 lines
```

> 💡 **Try it now:** `tail -n 5 /etc/passwd`

---

## `cp` — copy files and folders

Copy a file:

```bash
cp notes.txt backup.txt         # copy and rename
cp notes.txt ~/Documents/       # copy into a folder
cp *.txt ~/backup/              # copy many files at once using wildcard
```

**Copying a folder — you must add `-r`:**

```bash
cp myfolder/ ~/backup/
# Error: cp: -r not specified; omitting directory ❌
```

```bash
cp -r myfolder/ ~/backup/       # ✅
```

`-r` means **recursive** — it goes inside the folder and copies everything, including folders inside folders.

```
myfolder/
├── index.html   ← copied
├── style.css    ← copied
└── images/      ← goes inside
    ├── logo.png ← copied
    └── bg.jpg   ← copied
```

> 💡 Simple rule: **file** → `cp` | **folder** → `cp -r`

---

## `ls -S` — sort files by size

`-S` sorts files from **biggest to smallest**:

```bash
ls -S ~/Downloads/
# movie.mp4        ← biggest
# slides.pdf
# notes.txt
# todo.txt         ← smallest
```

**Problem — `ls -S` shows folders too:**

```bash
ls -S
# movie.mp4   images/   notes.txt   src/
#                 ^                   ^
#             folder               folder
```

**Solution — use `-p` and `grep -v` together:**

```bash
ls -Sp | grep -v "/$"
# movie.mp4
# notes.txt   ← files only ✅
```

How it works step by step:

| Step | Command | What it does |
|------|---------|-------------|
| 1 | `ls -S` | list files sorted by size |
| 2 | `-p` | add `/` to the end of every folder name |
| 3 | `grep -v "/$"` | remove any line that ends with `/` |
| Result | — | only files remain |

> 💡 `grep -v` = remove lines that **match** the pattern (opposite of normal grep)

---

## Avoid full path in output

**Problem:** When you run `ls` with a full path, the output includes the full path.

```bash
ls /home/user/documents/*report*
# /home/user/documents/annual_report.txt   ← has path ❌
# /home/user/documents/report_final.pdf    ← has path ❌
```

**Solution — `cd` into the folder first, then run `ls`:**

```bash
cd /home/user/documents/
ls *report*
# annual_report.txt   ← filename only ✅
# report_final.pdf    ← filename only ✅
```

Save to your home folder while inside another folder:

```bash
cd /home/user/documents/
ls *report* > ~/reportlist.txt
#             ^
#             ~ = your home folder — works from anywhere
```

Check there is no path in the result:

```bash
cat ~/reportlist.txt | grep "/"
# no result = no path = ✅
```

> 💡 `~` is always a shortcut for your home folder — use it from anywhere

---

← [Prev: Wildcards](./03-wildcards.md) · [Next: Summary →](./05-summary.md)
