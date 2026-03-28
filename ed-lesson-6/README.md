# ⚙️ Ed Lesson 6 — Bash Scripting

> **Lab Tutorial** — open your terminal and type along as you read.

← [Back to all lessons](../README.md)

---

## What this lesson covers

A Bash script is a file containing a sequence of Bash commands.  
Instead of typing commands one by one, you write them once, make the file executable, and run it.

This lesson covers everything you need to write real Bash scripts.

---

## 📂 Topics

| # | Topic | What you learn |
|---|-------|----------------|
| 1 | [Your First Script](./01-first-script.md) | `#!/bin/bash`, permissions, running a script, arguments |
| 2 | [Variables](./02-variables.md) | Assigning values, using `$`, rules and common mistakes |
| 3 | [Arithmetic](./03-arithmetic.md) | `$(( ))`, add, subtract, multiply, divide, modulus |
| 4 | [If Statements & Comparisons](./04-if-statements.md) | `if [[ ]]`, string vs numeric comparisons, `elif`, `else`, `fi` |
| 5 | [Script Arguments](./05-arguments.md) | `$1 $2 $3`, `$*`, `$#` |
| 6 | [Redirecting stdout & stderr](./06-redirection.md) | `2>&1`, `1>&2`, sending output between streams |
| 7 | [Summary & Cheat Sheet](./07-summary.md) | All syntax in one place, common mistakes, check your work |

---

## 🚀 How to use this

1. Open your terminal
2. Read each topic file in order
3. Type every script example into a `.sh` file and run it
4. Always make scripts executable before running:

```bash
chmod +x myscript.sh
./myscript.sh
```

---

> 💡 **Bash is very strict about spacing.** No spaces around `=` in assignments.  
> When something does not work — check for extra spaces first.

---

*Ed Lesson 6 · Bash Scripting*
