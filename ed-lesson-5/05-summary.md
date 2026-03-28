# ✅ Topic 5 — Summary & Cheat Sheet

> **Patterns, cheat sheet, and how to check your work before submitting.**

← [Prev: New Commands](./04-commands.md) · [Back to README](./README.md)

---

## 5 Common Patterns

These patterns cover most lab questions. Learn to recognise the shape of the problem.

---

### Pattern 1 — Number only, no filename

When the question asks for a count but says the result must not include the filename:

```bash
cat file.txt | wc -m > result.txt
cat file.txt | wc -l > result.txt
```

---

### Pattern 2 — List files, no path

When the question says "do not include the full path" or "filenames only":

```bash
cd /path/to/folder/
ls *keyword* > ~/output.txt
```

---

### Pattern 3 — Get last N lines

When the question asks for the last N lines of a file:

```bash
tail -n 50 file.txt > output.txt
wc -l output.txt    # check: should be 50
```

---

### Pattern 4 — Join two files

When the question asks you to copy one file then add the contents of another:

```bash
cp fileA.txt result.txt       # step 1: copy first file
cat fileB.txt >> result.txt   # step 2: append second file
```

> ⚠️ Use `>>` not `>` in step 2 — otherwise you delete the first file's content

---

### Pattern 5 — List files by size, files only

When the question asks for a size-sorted list with no folder names:

```bash
cd /path/to/folder/
ls -Sp | grep -v "/$" > ~/output.txt
```

---

## Cheat Sheet

```bash
# ── REDIRECTION ───────────────────────────────────────────────
command > file.txt       # overwrite (deletes old content)
command >> file.txt      # append (keeps old content)

# ── PIPE ──────────────────────────────────────────────────────
command_A | command_B    # output A → input B
cat file | wc -m         # count chars, no filename printed
ls | grep "abc"          # filter files containing "abc"
ls -Sp | grep -v "/$"    # files only, no folders

# ── WILDCARDS ─────────────────────────────────────────────────
*abc*                    contains "abc"
*.txt                    ends with .txt
[123]*                   starts with 1, 2, or 3
*[[:digit:]]*            contains a number anywhere
{*.txt,*.pdf}            .txt or .pdf

# ── COMMANDS ──────────────────────────────────────────────────
wc -m / -l / -w          characters / lines / words
tail -n N file           last N lines
head -n N file           first N lines
cp file dest/            copy a file
cp -r folder/ dest/      copy a folder
ls -S                    sort by size (largest first)
grep -v "pattern"        remove lines that match pattern

# ── TIPS ──────────────────────────────────────────────────────
~                        shortcut for your home folder
cd /path/                go into folder to avoid full path in output
```

---

## Read the question → know what to do

| Question says | It means | Use this |
|---------------|----------|----------|
| *"number only, no filename"* | remove filename from wc output | `cat file \| wc -m` |
| *"no path / no pathname"* | output must not include folder path | `cd` into the folder first |
| *"save to a file"* | redirect output | `> ~/output.txt` |
| *"append / add to"* | do not overwrite the file | `>>` not `>` |
| *"last N lines"* | read from end of file | `tail -n N` |
| *"copy a folder"* | folders need recursive copy | `cp -r` |
| *"sorted by size"* | sort from largest to smallest | `ls -S` |
| *"files only, no folders"* | filter out folder names | `ls -Sp \| grep -v "/$"` |
| *"filename contains abc"* | match by pattern | `ls *abc*` |

---

## Check your work before submitting

Run these checks before submitting any lab question:

```bash
# Does the output file exist?
ls ~/output.txt

# Does the content look right?
cat ~/output.txt

# Correct number of lines? (for tail / wc -l questions)
wc -l ~/output.txt

# No path in the result? (for filename-only questions)
cat ~/output.txt | grep "/"
# no result = no path ✅

# Number only, no filename? (for wc -m questions)
cat ~/result.txt
# should show only a number ✅
```

> 💡 Always `cat` your output file, re-read the question, and compare before submitting.

---

← [Prev: New Commands](./04-commands.md) · [Back to README](./README.md)
