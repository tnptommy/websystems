# ✅ Topic 6 — File Permissions & Summary

> **Why you copy files before editing, plus all Vim commands in one place.**

← [Prev: Copy, Cut & Paste](./05-copy-cut-paste.md) · [Back to README](./README.md)

---

## ⚠️ File Permissions — Very Important for This Lab

In Ed Lesson 2, some files you need to edit are in **protected directories**.  
You do not have permission to save changes directly to those files.

If you try to edit and save in-place, Vim will show:

```
E212: Can't open file for writing
```

### The fix — copy first, then edit

**Step 1 — Copy the file to your home directory:**

```bash
cp /absolute/path/to/file.txt ~/
```

Example:
```bash
cp /etc/hosts ~/
```

**Step 2 — Go to your home directory:**

```bash
cd ~
```

**Step 3 — Edit the copy:**

```bash
vim hosts
```

> 💡 **Rule: Copy → Then Edit. Never edit directly inside protected directories.**

### Why does this work?

Your home directory (`~`) is the one folder you always have full read and write access to.  
Copying the file there gives you an editable version to work on.

---

## Cheat Sheet

```
# ── OPENING & SAVING ──────────────────────────────────────────
vim filename        open or create a file
:w                  save (write)
:q                  quit
:wq                 save and quit
:q!                 quit WITHOUT saving (force quit)

# ── MODES ─────────────────────────────────────────────────────
Esc                 return to Normal Mode (from anywhere)
i                   insert before cursor
a                   append after cursor
I                   insert at beginning of line
A                   append at end of line
o                   open new line below and insert

# ── NAVIGATION ────────────────────────────────────────────────
h  j  k  l         left / down / up / right
gg                  go to first line
G                   go to last line
:n                  go to line n (e.g. :10)
Page Up / Down      scroll by screen

# ── LINE NUMBERS ──────────────────────────────────────────────
:set number         show line numbers
:set nonumber       hide line numbers
:set nu             short for :set number
:set nonu           short for :set nonumber

# ── DELETING ──────────────────────────────────────────────────
x                   delete character under cursor
D                   delete from cursor to end of line
dd                  delete current line
ndd                 delete n lines (e.g. 3dd)
dw                  delete one word
ndw                 delete n words (e.g. 2dw)
dG                  delete from cursor to end of file
dnG                 delete from cursor to line n (e.g. d5G)

# ── JOINING ───────────────────────────────────────────────────
J                   join current line with the line below

# ── UNDO & REDO ───────────────────────────────────────────────
u                   undo last action
Ctrl + r            redo

# ── SEARCHING ─────────────────────────────────────────────────
/word               search for "word"
n                   next match
N                   previous match
/[aB]c              match "ac" or "Bc"
/ab*c               match "ac", "abc", "abbc", etc.
/\<word\>           match whole word only

# ── SEARCH & REPLACE ──────────────────────────────────────────
:%s/old/new/g       replace all in file
:s/old/new/g        replace all on current line only
:%s/old/new/gc      replace all with confirmation

# ── MARKS ─────────────────────────────────────────────────────
ma                  set mark "a" at current line
'a                  jump to mark "a"
y'a                 copy (yank) from here back to mark "a"
d'a                 cut (delete) from here back to mark "a"
p                   paste below current line
P                   paste above current line
yy                  copy current line
3yy                 copy 3 lines

# ── EXTRA PRACTICE ────────────────────────────────────────────
vimtutor            built-in interactive Vim tutorial (run in terminal)
```

---

## Read the question → know what to do

| Question says | Use this |
|---------------|----------|
| *"open a file"* | `vim filename` |
| *"save the file"* | `:w` |
| *"save and quit"* | `:wq` |
| *"quit without saving"* | `:q!` |
| *"go to line N"* | `:N` |
| *"show line numbers"* | `:set number` |
| *"insert text"* | Press `i` or `a`, type, then `Esc` |
| *"delete a line"* | `dd` |
| *"delete N lines"* | `Ndd` (e.g. `3dd`) |
| *"delete a word"* | `dw` |
| *"delete to end of line"* | `D` |
| *"join two lines"* | `J` |
| *"search for word"* | `/word` then `n` / `N` |
| *"replace all X with Y"* | `:%s/X/Y/g` |
| *"copy a block of lines"* | Mark start with `ma`, go to end, `y'a`, go to dest, `p` |
| *"move a block of lines"* | Mark start with `ma`, go to end, `d'a`, go to dest, `p` |
| *"cannot save — permission error"* | `cp /path/to/file ~/` then edit the copy |

---

## Check your work before submitting

```bash
# Did you save? Check the file exists and has content
cat ~/filename

# Did the replacement work?
grep "newword" ~/filename

# Correct number of lines after deletion?
wc -l ~/filename
```

> 💡 Always `:wq` to save before checking. If you only `:q!`, your changes are lost.

---

← [Prev: Copy, Cut & Paste](./05-copy-cut-paste.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
