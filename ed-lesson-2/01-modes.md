# 🟢 Topic 1 — Vim Modes & Opening Files

> **Vim has modes. Understanding modes is the most important thing in this lesson.**

← [Back to README](./README.md) · [Next: Navigation →](./02-navigation.md)

---

## Opening a file in Vim

To open an existing file, or create a new one:

```bash
vim filename.txt
```

Example:
```bash
vim notes.txt       # opens notes.txt (creates it if it does not exist)
vim ~/report.txt    # opens report.txt in your home folder
```

---

## The three modes

This is what makes Vim confusing at first — **you cannot just type straight away**.  
Vim has three modes, and each one does something different.

| Mode | What you can do | How to get there |
|------|----------------|-----------------|
| **Normal Mode** | Navigate, delete, copy, search | Press `Esc` from anywhere |
| **Insert Mode** | Type and edit text | Press `i`, `a`, `o`, etc. from Normal Mode |
| **Command Mode** | Save, quit, search & replace | Press `:` from Normal Mode |

---

## Normal Mode

This is where Vim **starts** every time you open a file.

In Normal Mode, every key on your keyboard is a **command** — not a letter.  
Pressing `d` does not type the letter d — it starts a delete command.

**How to get back to Normal Mode from anywhere:**
```
Esc
```

> 💡 **Rule 1:** If something is not working — press `Esc` first.

---

## Insert Mode

Insert Mode is where you actually **type text**.

To enter Insert Mode from Normal Mode:

```
i    ← insert before cursor
a    ← append after cursor
o    ← open a new line below and start typing
```

You will see `-- INSERT --` at the bottom of the screen when you are in Insert Mode.

To go back to Normal Mode:
```
Esc
```

---

## Command Mode

Command Mode lets you **save, quit, and run commands** on the file.

To enter Command Mode from Normal Mode, press `:` — you will see it appear at the bottom of the screen.

**The most important commands:**

| Command | What it does |
|---------|-------------|
| `:w` | Save the file (write) |
| `:q` | Quit Vim |
| `:wq` | Save and quit |
| `:q!` | Quit WITHOUT saving — force quit |

> ⚠️ **`:q!` discards all your changes** — use it when you made a mistake and want to start over.

---

## The mode flow

```
Open Vim
    ↓
Normal Mode  ←──── Esc ────┐
    ↓                       │
  i / a / o                 │
    ↓                       │
Insert Mode ────────────────┘
    
Normal Mode
    ↓
  : (colon)
    ↓
Command Mode  (:w  :q  :wq  :q!)
```

---

## Try it now

```bash
vim practice.txt
```

1. Vim opens in **Normal Mode**
2. Press `i` → enter **Insert Mode** → type `Hello World`
3. Press `Esc` → back to **Normal Mode**
4. Press `:` → enter **Command Mode** → type `wq` → press `Enter`
5. File is saved and you are back in the terminal

Verify:
```bash
cat practice.txt
# Hello World
```

---

← [Back to README](./README.md) · [Next: Navigation →](./02-navigation.md)
