# 🔀 Topic 6 — Redirecting stdout & stderr

> **Send error output where it belongs — and keep your script's output clean.**

← [Prev: Script Arguments](./05-arguments.md) · [Next: Summary →](./07-summary.md)

---

## Recap — two output streams

Every command produces two types of output:

| Stream | Name | Number | Default destination |
|--------|------|--------|-------------------|
| stdout | Standard output | `1` | Screen |
| stderr | Standard error | `2` | Screen |

Both look the same on screen — but they are separate streams.

You already know how to save them to files (`>` for stdout, `2>` for stderr).  
Now you learn how to **redirect one stream into the other**.

---

## Send stderr to stdout — `2>&1`

```bash
command 2>&1
```

This means: *"send stream 2 (stderr) to wherever stream 1 (stdout) is going"*

**Why use it?**  
When you pipe or redirect output, only stdout is captured.  
Error messages (stderr) still appear on screen.

```bash
ls /fakepath > output.txt
# ls: cannot access '/fakepath': No such file or directory
# (error still shows on screen — not saved to file)

cat output.txt
# (empty — only stdout was redirected)
```

With `2>&1` — both streams go to the file:

```bash
ls /fakepath > output.txt 2>&1
# (nothing on screen)

cat output.txt
# ls: cannot access '/fakepath': No such file or directory ✅
```

---

## Send stdout to stderr — `1>&2`

```bash
command 1>&2
```

This means: *"send stream 1 (stdout) to wherever stream 2 (stderr) is going"*

**Why use it?**  
In scripts, error messages should go to stderr — not stdout.  
This way, if someone redirects your script's output, error messages do not end up in the data file.

**Example — argument validation in a script:**

```bash
#!/bin/bash

if [[ $# -ne 2 ]]; then
    echo "Error: exactly 2 arguments required" 1>&2
    exit 1
fi

echo "Processing $1 and $2..."
```

The `echo` inside the `if` sends its message to **stderr** with `1>&2`.

```bash
./myscript.sh only-one
# Error: exactly 2 arguments required    ← appears on screen (stderr)

./myscript.sh only-one > output.txt
# Error: exactly 2 arguments required    ← still appears on screen ✅
# (stdout went to output.txt, stderr was not captured)

cat output.txt
# (empty — the error message was stderr, not stdout)
```

---

## Side by side comparison

| Redirect | Meaning | When to use |
|----------|---------|-------------|
| `2>&1` | stderr → stdout | Capture everything in one place (file or pipe) |
| `1>&2` | stdout → stderr | Send an error message from within a script |

---

## Reading the syntax

```
2  >  &1
^  ^   ^
|  |   └── "to the same destination as stream 1"
|  └─────── redirect
└────────── stream 2 (stderr)
```

The `&` before the number is important — it means "stream number", not a file named `1`.

```bash
command 2>1      ❌ creates a file literally called "1"
command 2>&1     ✅ redirects stderr to stdout
```

---

## Practical example — clean script output

```bash
#!/bin/bash

# Check arguments — send error to stderr
if [[ $# -lt 1 ]]; then
    echo "Usage: ./process.sh filename" 1>&2
    exit 1
fi

# Normal output goes to stdout
echo "Processing file: $1"
echo "Done."
```

Run normally — see both:
```bash
./process.sh
# Usage: ./process.sh filename    ← stderr, shown on screen
```

Run with redirect — error still visible, stdout goes to file:
```bash
./process.sh myfile.txt > results.txt
# (nothing on screen)

cat results.txt
# Processing file: myfile.txt
# Done.
```

---

← [Prev: Script Arguments](./05-arguments.md) · [Next: Summary →](./07-summary.md)
