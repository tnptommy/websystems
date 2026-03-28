# 📄 Topic 4 — Redirection

> **Save output to a file instead of the screen.**

← [Prev: Viewing Files](./03-viewing-files.md) · [Next: Summary →](./05-summary.md)

---

## What is output?

When you run any command, it produces two types of output:

| Name | What it is | Where it goes by default |
|------|-----------|--------------------------|
| **stdout** (standard output) | The normal result | Screen |
| **stderr** (standard error) | Error messages | Screen |

Both look the same on screen — but they are treated separately.  
**Redirection** lets you send either one into a file instead.

---

## `>` — save stdout to a file

The `>` symbol sends the normal output of a command **into a file**.

**Without `>`:**
```bash
echo "Hello World"
# Hello World
# shows on screen, then gone
```

**With `>`:**
```bash
echo "Hello World" > test.txt
# nothing shows on screen
# "Hello World" is now saved inside test.txt
```

**Check it:**
```bash
cat test.txt
# Hello World   ✅
```

**Works with any command:**
```bash
date > now.txt
cat now.txt
# Sat Mar 28 10:22:00 UTC 2026
```

How to read the command:
```
echo "Hello World"   >   test.txt
         ^           ^       ^
     run this      save    into this file
```

> 💡 **Try it now:** `echo "Hello World" > test.txt` then `cat test.txt`

---

## ⚠️ Warning — `>` deletes old content!

Every time you use `>`, the file is **wiped and rewritten from scratch**.

```bash
echo "Hello World" > test.txt
cat test.txt
# Hello World

echo "Goodbye Universe" > test.txt
cat test.txt
# Goodbye Universe
# Hello World is gone! ❌
```

To keep old content and add more → use `>>` (next section).

---

## `>>` — append to a file, keep old content

The `>>` symbol adds to the **end** of a file without deleting what is already there.

```bash
echo "Hello World" > test.txt
echo "Goodbye Universe" >> test.txt

cat test.txt
# Hello World
# Goodbye Universe   ✅ both lines are kept
```

**The difference:**

| Symbol | What it does | Old content |
|--------|-------------|-------------|
| `>` | Overwrite — wipe then write | ❌ Deleted |
| `>>` | Append — add to the end | ✅ Kept |

> 💡 **Try it now:** Run both echo commands above, then `cat test.txt`

---

## `2>` — save stderr to a file

Error messages go to **stderr**, not stdout.  
Using `>` alone will **not** capture error messages.

**Example — a command that causes an error:**
```bash
rm sillyfilename
# rm: cannot remove 'sillyfilename': No such file or directory
# this is an error message — it goes to stderr
```

**Using `>` does NOT capture the error:**
```bash
rm sillyfilename > silly.output
# rm: cannot remove 'sillyfilename': No such file or directory
# error still shows on screen — not saved to file ❌

cat silly.output
# (empty — nothing was saved)
```

**Using `2>` captures the error:**
```bash
rm sillyfilename 2> silly.output
# nothing shows on screen

cat silly.output
# rm: cannot remove 'sillyfilename': No such file or directory   ✅
```

The `2` refers to stderr's channel number. stdout is channel `1`.

> 💡 **Try it now:** `rm fakefile 2> error.txt` then `cat error.txt`

---

## Redirect both stdout and stderr

```bash
command > output.txt 2> errors.txt    # stdout to one file, stderr to another
command > output.txt 2>&1             # both stdout and stderr to same file
```

---

## Practical examples

**Save the current date to a file:**
```bash
date > now.txt
cat now.txt
# Sat Mar 28 10:22:00 UTC 2026
```

**Save a list of files to a text file:**
```bash
ls > filelist.txt
cat filelist.txt
```

**Build a file line by line:**
```bash
echo "Line 1" > myfile.txt
echo "Line 2" >> myfile.txt
echo "Line 3" >> myfile.txt
cat myfile.txt
# Line 1
# Line 2
# Line 3
```

**Capture an error for later inspection:**
```bash
rm nonexistent_file 2> errors.txt
cat errors.txt
# rm: cannot remove 'nonexistent_file': No such file or directory
```

---

## Summary table

| Symbol | What it redirects | Old content |
|--------|------------------|-------------|
| `>` | stdout | ❌ Overwritten |
| `>>` | stdout | ✅ Appended |
| `2>` | stderr | ❌ Overwritten |
| `2>>` | stderr | ✅ Appended |
| `> file 2>&1` | stdout + stderr | ❌ Overwritten |

---

← [Prev: Viewing Files](./03-viewing-files.md) · [Next: Summary →](./05-summary.md)
