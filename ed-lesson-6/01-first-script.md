# 🚀 Topic 1 — Your First Script

> **A Bash script is just a text file with commands in it — made executable.**

← [Back to README](./README.md) · [Next: Variables →](./02-variables.md)

---

## What is a Bash script?

Instead of typing commands one by one in the terminal, you can:

1. Write all the commands into a `.sh` file
2. Make the file executable
3. Run the file as a program

The terminal runs every command in the file, top to bottom.

---

## The shebang line — `#!/bin/bash`

The very first line of every Bash script must be:

```bash
#!/bin/bash
```

This is called the **shebang** (or sha-bang).  
It tells the operating system which program to use to run the file.

Without it, the system does not know what language the file is written in.

| Part | Meaning |
|------|---------|
| `#!` | Tells the OS: "use this interpreter" |
| `/bin/bash` | Path to the Bash program |

---

## Comments

Any line starting with `#` (except the shebang) is a **comment** — ignored by Bash.

```bash
#!/bin/bash

# This is a comment — Bash ignores this line
echo "This runs"    # This comment is after a command — also ignored
```

Use comments to explain what your script does.

---

## Your first script

Create a file called `hello.sh`:

```bash
vim hello.sh
```

Type this:

```bash
#!/bin/bash

# Say hello to the first argument

echo Hello $1!!
```

Save and quit: `:wq`

---

## Making it executable

Before you can run a script, you must give it execute permission:

```bash
chmod +x hello.sh
```

Or set specific permissions (owner: rwx, group: r, others: r):

```bash
chmod 744 hello.sh
```

Check it:

```bash
ls -l hello.sh
# -rwxr--r-- hello.sh    ← x is now set ✅
```

---

## Running the script

```bash
./hello.sh Bill
```

Output:

```
Hello Bill!!
```

The `./` means "run this file from the current directory".

**What `$1` means:**  
`$1` is the first argument you pass after the script name.  
`Bill` → `$1` → inserted into the echo output.

---

## Why `./` before the script name?

When you type a command like `ls`, Bash searches for it in system folders (`/bin`, `/usr/bin`, etc.).  
Your script is not in any of those folders — it is in your current directory.

`./` tells Bash: *"look right here, in the current directory"*.

```bash
./hello.sh       ✅ runs hello.sh from current folder
hello.sh         ❌ Bash looks in system folders, cannot find it
```

---

## Full workflow — every time

```bash
# 1. Create the script
vim myscript.sh

# 2. Make it executable (only need to do this once)
chmod +x myscript.sh

# 3. Run it
./myscript.sh
```

> 💡 **Try it now:** Create `hello.sh`, make it executable, and run `./hello.sh YourName`

---

## Common mistakes

**Mistake 1 — forgetting the shebang:**
```bash
# Missing #!/bin/bash at the top
echo "hello"    # may run but behaves unpredictably ❌
```

**Mistake 2 — forgetting `chmod +x`:**
```bash
./hello.sh
# bash: ./hello.sh: Permission denied ❌

chmod +x hello.sh    # fix it
./hello.sh           # ✅
```

**Mistake 3 — forgetting `./`:**
```bash
hello.sh
# bash: hello.sh: command not found ❌

./hello.sh    # ✅
```

---

← [Back to README](./README.md) · [Next: Variables →](./02-variables.md)
