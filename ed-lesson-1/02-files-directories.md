# 📁 Topic 2 — Files & Directories

> **Create, copy, move, and delete files and folders.**

← [Prev: Navigation](./01-navigation.md) · [Next: Viewing Files →](./03-viewing-files.md)

---

## `ls` — list files in a folder

You already saw `ls` in [Topic 1](./01-navigation.md). Here are the options you will use most.

### List files in your current folder

```bash
ls
# notes.txt   photo.jpg   Documents   Downloads
```

### List files in a different folder (without `cd` first)

```bash
ls /course/linuxgym
# emptystuff   gutenberg   census
```

### List hidden files too

Files that start with `.` are hidden — `ls` does not show them by default.

```bash
ls -a
# .bashrc   .profile   notes.txt   photo.jpg
# ^         ^
# hidden    hidden
```

### Long listing — show size, owner, permissions

```bash
ls -l
# -rw-r--r-- 1 user group 1842 Jan 10 notes.txt
```

### Sort by modification time (newest first)

```bash
ls -t
```

### Sort by size (largest first)

```bash
ls -S       # capital S
```

### Combine options

```bash
ls -la      # long listing including hidden files
ls -lS      # long listing sorted by size
ls -lart    # long listing, all files, reverse time order (oldest first)
```

> 💡 **Try it now:** `ls -la` in your home folder

---

## `mkdir` — create a new folder

```bash
mkdir myfolder                    # create folder in current location
mkdir ~/projects                  # create folder in home directory
mkdir -p ~/projects/week1/notes   # create nested folders all at once
```

`-p` means "create parent folders too if they do not exist yet"

> 💡 **Try it now:** `mkdir testfolder` then `ls` to see it appear

---

## `touch` — create an empty file

```bash
touch notes.txt         # creates an empty file called notes.txt
touch ~/report.txt      # creates an empty file in home folder
```

If the file already exists, `touch` just updates the last-modified time — it does not delete the contents.

> 💡 **Try it now:** `touch myfile.txt` then `ls` to see it

---

## `cp` — copy a file

```bash
cp source.txt destination.txt       # copy and rename in same folder
cp notes.txt ~/backup/              # copy into a different folder
cp *.txt ~/backup/                  # copy all .txt files at once
```

**Copy a folder — must add `-r`:**

```bash
cp myfolder/ ~/backup/
# Error: cp: -r not specified; omitting directory ❌

cp -r myfolder/ ~/backup/           # ✅ copies folder and everything inside
```

> 💡 Simple rule: **file** → `cp` | **folder** → `cp -r`

---

## `rm` — delete a file

```bash
rm notes.txt            # delete a file
rm file1.txt file2.txt  # delete multiple files
rm *.txt                # delete all .txt files
```

> ⚠️ **Warning:** `rm` is permanent. There is no recycle bin in the terminal.

**Delete a folder and everything inside:**

```bash
rmdir myfolder          # only works if the folder is EMPTY
rm -r myfolder          # deletes folder and all contents — be careful!
```

---

## `rmdir` — delete an empty folder

```bash
rmdir emptyfolder       # only works if folder has nothing inside
```

If the folder is not empty, you will get an error:

```bash
rmdir Documents
# rmdir: failed to remove 'Documents': Directory not empty ❌

rm -r Documents         # use this instead — but double-check first!
```

---

## Summary table

| Command | What it does | Example |
|---------|-------------|---------|
| `ls` | List files | `ls -la` |
| `ls -a` | List including hidden | `ls -a ~/` |
| `ls -S` | List sorted by size | `ls -S /etc` |
| `mkdir` | Create a folder | `mkdir myfolder` |
| `mkdir -p` | Create nested folders | `mkdir -p a/b/c` |
| `touch` | Create an empty file | `touch notes.txt` |
| `cp` | Copy a file | `cp a.txt b.txt` |
| `cp -r` | Copy a folder | `cp -r dir/ backup/` |
| `rm` | Delete a file | `rm notes.txt` |
| `rm -r` | Delete a folder | `rm -r myfolder` |
| `rmdir` | Delete an empty folder | `rmdir emptyfolder` |

---

## Common mistakes

**Mistake 1 — `rm` a folder without `-r`:**
```bash
rm myfolder
# rm: cannot remove 'myfolder': Is a directory ❌

rm -r myfolder    # ✅
```

**Mistake 2 — `rmdir` a folder that is not empty:**
```bash
rmdir Documents
# rmdir: failed to remove 'Documents': Directory not empty ❌

rm -r Documents   # ✅ but make sure you want to delete everything inside!
```

**Mistake 3 — `cp` a folder without `-r`:**
```bash
cp myfolder/ backup/
# cp: -r not specified; omitting directory 'myfolder' ❌

cp -r myfolder/ backup/   # ✅
```

---

← [Prev: Navigation](./01-navigation.md) · [Next: Viewing Files →](./03-viewing-files.md)
