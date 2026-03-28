# 📄 Topic 1 — Redirection

> **Save output to a file instead of the screen.**

← [Back to README](./README.md) · [Next: Pipe →](./02-pipe.md)

---

## What is output?

When you run `ls`, the result shows on screen and then disappears. You cannot save it.

```bash
ls
# notes.txt   photo.jpg   Downloads
# shows on screen, then gone
```

That result is called **output**.

Normally, output always goes to the **screen**.

Redirection lets you **send output somewhere else** — into a file.

---

## The `>` symbol — save output to a file

```bash
ls > mylist.txt
# nothing shows on screen
# the result is now saved inside mylist.txt
```

Check it:

```bash
cat mylist.txt
# notes.txt   photo.jpg   Downloads
```

How to read the command:

```
ls   >   mylist.txt
^    ^        ^
run  save     save into this file
```

> 💡 **Try it now:** `ls > mylist.txt` then `cat mylist.txt`

---

## ⚠️ Warning — `>` deletes old content!

Every time you use `>`, the file is **wiped and rewritten from scratch**.

```bash
echo "Line 1" > test.txt
cat test.txt
# Line 1
```

> `echo` = a command that prints text to the screen

```bash
echo "Line 2" > test.txt
cat test.txt
# Line 2
# Line 1 is gone! ❌
```

If you want to keep old content and add more → use `>>` below.

---

## The `>>` symbol — add to the end, keep old content

```bash
echo "Line 1" > test.txt
echo "Line 2" >> test.txt
echo "Line 3" >> test.txt

cat test.txt
# Line 1
# Line 2
# Line 3   ✅ all three lines are still here
```

The difference:

| Symbol | What it does | Old content |
|--------|-------------|-------------|
| `>` | Overwrite — wipe then write | ❌ Deleted |
| `>>` | Append — add to the end | ✅ Kept |

> 💡 **Try it now:** Run those 3 echo commands, then `cat test.txt`

---

## Common mistake

```bash
# You want to ADD a new result to a file
# but you accidentally use > instead of >>

echo "Result 1" > results.txt
echo "Result 2" > results.txt   # ❌ Result 1 is now gone!

# Fix: use >> for the second line
echo "Result 1" > results.txt
echo "Result 2" >> results.txt  # ✅ both lines kept
```

---

← [Back to README](./README.md) · [Next: Pipe →](./02-pipe.md)
