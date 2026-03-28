# ✅ Topic 5 — Summary & Cheat Sheet

> **All commands from Lesson 1 in one place.**

← [Prev: Redirection](./04-redirection.md) · [Back to README](./README.md)

---

## Key concepts

| Concept | What it means |
|---------|--------------|
| Working directory | The folder you are currently inside in the terminal |
| Absolute path | Starts with `/` — works from anywhere |
| Relative path | Starts from your current location |
| stdout | Normal output from a command |
| stderr | Error output from a command |
| Redirection | Sending output to a file instead of the screen |

---

## Cheat Sheet

```bash
# ── NAVIGATION ────────────────────────────────────────────────
pwd                    # show current folder
cd /path/to/folder     # go to folder (absolute path)
cd foldername          # go into folder (relative path)
cd ..                  # go up one level
cd                     # go to home folder
cd ~                   # same as above

# ── LISTING FILES ─────────────────────────────────────────────
ls                     # list files in current folder
ls /path/to/folder     # list files in another folder
ls -a                  # include hidden files (starting with .)
ls -l                  # long listing with size and permissions
ls -S                  # sort by size (largest first)
ls -t                  # sort by modification time (newest first)
ls -r                  # reverse the order
ls -la                 # long listing including hidden files
ls -lart               # long listing, all files, oldest last

# ── CREATE & DELETE ───────────────────────────────────────────
mkdir foldername       # create a folder
mkdir -p a/b/c         # create nested folders
touch filename         # create an empty file
rm filename            # delete a file
rm -r foldername       # delete a folder and everything inside
rmdir foldername       # delete an empty folder only

# ── COPY ──────────────────────────────────────────────────────
cp source dest         # copy a file
cp -r folder/ dest/    # copy a folder

# ── VIEWING FILES ─────────────────────────────────────────────
cat file               # print entire file
head file              # first 10 lines
head -n N file         # first N lines
tail file              # last 10 lines
tail -n N file         # last N lines
tail -f file           # follow file as it grows (Ctrl+C to stop)
wc file                # count lines, words, characters
wc -l file             # lines only
wc -w file             # words only
wc -m file             # characters only

# ── REDIRECTION ───────────────────────────────────────────────
command > file         # save stdout to file (overwrites)
command >> file        # append stdout to file (keeps old content)
command 2> file        # save stderr to file
command > file 2>&1    # save both stdout and stderr to file

# ── GETTING HELP ──────────────────────────────────────────────
man command            # open the manual page for a command
command --help         # quick help for a command

# ── PATH SHORTCUTS ────────────────────────────────────────────
~                      # your home folder
.                      # current folder
..                     # parent folder (one level up)
/                      # root of the entire file system
```

---

## Read the question → know what to do

| Question says | Use this |
|---------------|----------|
| *"where am I?"* | `pwd` |
| *"go to this folder"* | `cd /path/to/folder` |
| *"go up one level"* | `cd ..` |
| *"go home"* | `cd` or `cd ~` |
| *"list files"* | `ls` |
| *"list hidden files too"* | `ls -a` |
| *"sort by size"* | `ls -S` |
| *"create a folder"* | `mkdir foldername` |
| *"create a file"* | `touch filename` |
| *"copy a file"* | `cp source dest` |
| *"copy a folder"* | `cp -r folder/ dest/` |
| *"delete a file"* | `rm filename` |
| *"delete a folder"* | `rm -r foldername` |
| *"read a file"* | `cat file` |
| *"first N lines"* | `head -n N file` |
| *"last N lines"* | `tail -n N file` |
| *"count lines"* | `wc -l file` |
| *"count characters"* | `wc -m file` |
| *"save output to file"* | `command > file` |
| *"append to file"* | `command >> file` |
| *"save error to file"* | `command 2> file` |

---

## Check your work before submitting

```bash
# Does the file exist?
ls ~/output.txt

# Does the content look right?
cat ~/output.txt

# Correct number of lines?
wc -l ~/output.txt

# Is the folder there?
ls ~/ | grep foldername
```

> 💡 Always `cat` your output file, re-read the question, and compare before submitting.

---

← [Prev: Redirection](./04-redirection.md) · [Back to README](./README.md) · [All Lessons →](../README.md)
