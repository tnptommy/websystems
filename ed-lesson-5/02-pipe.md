# 🔗 Topic 2 — Pipe

> **Send the output of one command straight into another command.**

← [Prev: Redirection](./01-redirection.md) · [Next: Wildcards →](./03-wildcards.md)

---

## What is a pipe?

The `|` symbol sends the output of one command **straight into** another command — without showing it on screen first.

Think of it like a factory line:

```
Factory A makes a product
  → instead of storing it, sends it straight to Factory B
    → Factory B processes it → final result
```

In the terminal:

```
Command A runs → output does NOT go to screen
              → goes straight into Command B
                          → Command B processes it → result
```

The symbol:

```bash
command_A | command_B
```

---

## Understand `grep` first

Before using pipe, you need to understand `grep`.

`grep` reads each line and **keeps only lines that contain the word you search for**.

```bash
cat fruits.txt
# apple
# banana
# apricot
# grape

grep "ap" fruits.txt
# apple    ← has "ap" ✅
# apricot  ← has "ap" ✅
# banana   ← no "ap"  ❌ removed
# grape    ← no "ap"  ❌ removed
```

> 💡 **Try it now:** `grep "root" /etc/passwd`

---

## Pipe `ls` into `grep`

**Without pipe** — you see everything, and have to search by eye:

```bash
ls /etc
# adduser.conf  apt  bash.bashrc  cron.d  hostname ...
# hard to find what you need ❌
```

**With pipe** — filter instantly:

```bash
ls /etc | grep "conf"
# adduser.conf
# bash.bashrc
# host.conf
# only lines with "conf" ✅
```

What happens step by step:

```
ls /etc      → lists all files
     |       → list goes straight into grep
grep "conf"  → keeps only lines with "conf"
             → shows on screen
```

> 💡 **Try it now:** `ls /etc | grep "conf"`

---

## Pipe + save to file

You can use pipe and `>` at the same time:

```bash
ls /etc | grep "conf" > conflist.txt

cat conflist.txt
# adduser.conf
# bash.bashrc
# host.conf
```

Read left to right:

```
ls /etc        → get all files
       |       → send to grep
grep "conf"    → keep lines with "conf"
           >   → instead of screen
conflist.txt   → save into this file
```

> 💡 **Try it now:** Run that command, then `cat conflist.txt`

---

## Why pipe instead of wildcard?

These two commands give a similar result:

```bash
ls *conf*           # wildcard
ls | grep "conf"    # pipe
```

But pipe is more powerful because you can **chain more commands**:

```bash
ls | grep "conf" | wc -l
# counts how many files contain "conf"
# wildcard cannot do this directly
```

---

## `grep -v` — remove lines instead of keeping them

Normal `grep` keeps lines that **match**.  
`grep -v` keeps lines that **do not match** — it removes matching lines.

```bash
ls /etc | grep -v "conf"
# shows everything EXCEPT lines with "conf"
```

You will use this again in [Topic 4 — Commands](./04-commands.md).

---

← [Prev: Redirection](./01-redirection.md) · [Next: Wildcards →](./03-wildcards.md)
