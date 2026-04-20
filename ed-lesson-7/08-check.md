# 🔢 Topic 8 — Checking Your Output with `wc`, `head`, `tail`

> **Always verify your output before submitting — these three commands help you catch mistakes fast.**

← [Prev: awk](./07-awk.md) · [Next: Inline Execution →](./09-inline-execution.md)

---

## Why checking output matters

After running a command, you need to confirm:
- The file was created
- The number of lines is correct
- The content looks right
- There are no extra blank lines or spaces

These three commands make that easy.

---

## `wc` — count lines, words, or characters

`wc` stands for **word count**.

```bash
wc -l file.txt      # count lines only        ← most useful
wc -w file.txt      # count words only
wc -c file.txt      # count characters (bytes)
```

### Most common use — verify line count

```bash
# After creating names.txt, check it has the right number of lines
wc -l ~/names.txt
# 4275 /home/user/names.txt

# Compare with the original file
wc -l /course/linuxgym/census/femalenames.txt
# 4275   ← must match ✅
```

### Use in a pipe

```bash
# Count how many lines start with ANA
grep "^ANA" /course/linuxgym/census/femalenames.txt | wc -l
# 6
```

---

## `head` — see the first lines

```bash
head file.txt           # first 10 lines (default)
head -5 file.txt        # first 5 lines
head -1 file.txt        # first line only
head -3 ~/table.csv     # check top of your CSV
```

### Use after any command to preview output

```bash
sort /course/linuxgym/census/femalenames.txt | head -5
# Check: does the sorted output start with names beginning with A?
```

---

## `tail` — see the last lines

```bash
tail file.txt           # last 10 lines (default)
tail -5 file.txt        # last 5 lines
tail -1 file.txt        # last line only
```

### Special use — skip the first line (skip header)

```bash
tail -n +2 file.txt     # print everything EXCEPT the first line
```

This is useful when a file has a header row that you do not want to include in your output.

---

## Use `head` and `tail` together to verify

```bash
# After creating a file, always check both ends
head -3 ~/alphabetical.txt      # does it start with early letters?
tail -3 ~/alphabetical.txt      # does it end with late letters?
```

---

## Full verification checklist — use this before submitting

```bash
# 1. Does the file exist and have content?
cat ~/output.txt

# 2. Does it have the right number of lines?
wc -l ~/output.txt
wc -l /course/linuxgym/census/femalenames.txt   # compare with original

# 3. Are there no extra blank lines?
grep -c "." ~/output.txt        # counts only non-empty lines

# 4. Does the content look right?
head -3 ~/output.txt
tail -3 ~/output.txt

# 5. Are there no leading or trailing spaces?
grep '^ ' ~/output.txt          # should return nothing
grep ' $' ~/output.txt          # should return nothing
```

---

## Examples from the skills test

```bash
# After Q2 — alphabetical.txt
wc -l ~/alphabetical.txt        # must match original
head -3 ~/alphabetical.txt      # should start with names near A

# After Q3 — names.txt
wc -l ~/names.txt               # must match original
head -3 ~/names.txt             # should show only names, no numbers

# After Q5 — anne-files.txt
cat ~/anne-files.txt            # check full paths, one per line
wc -l ~/anne-files.txt          # count how many files found
```

---

> 💡 **Try it now:**
> 1. `wc -l /course/linuxgym/census/femalenames.txt` — how many names?
> 2. `head -5 /course/linuxgym/census/femalenames.txt` — see first 5 lines
> 3. `tail -5 /course/linuxgym/census/femalenames.txt` — see last 5 lines
> 4. `grep "^ANA" /course/linuxgym/census/femalenames.txt | wc -l` — how many ANA names?

---

← [Prev: awk](./07-awk.md) · [Next: Inline Execution →](./09-inline-execution.md)
