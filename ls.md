# `ls` — List Directory Contents

## Overview

The `ls` command is one of the most frequently used commands in Linux/Ubuntu. It **lists the contents of a directory** — files, subdirectories, symbolic links, and more. By default, it lists the contents of the current working directory.

---

## Basic Syntax

```bash
ls [OPTIONS] [FILE/DIRECTORY]
```

- `OPTIONS` — Flags that modify the behavior or output format.
- `FILE/DIRECTORY` — The target path to list. If omitted, the **current directory** is used.

---

## Basic Usage

```bash
ls
```
Lists files and directories in the current directory (non-hidden, unsorted by detail).

```bash
ls /home/user/Documents
```
Lists contents of a specific directory.

```bash
ls file.txt
```
If given a file name, it simply confirms the file exists by printing its name.

---

## Common Options (Flags)

### `-l` — Long Listing Format
```bash
ls -l
```
Displays detailed information in a column format:
```
-rw-r--r-- 1 alice alice 4096 Jun 8 10:00 notes.txt
```
| Column | Meaning |
|---|---|
| `-rw-r--r--` | File permissions |
| `1` | Number of hard links |
| `alice` | Owner (user) |
| `alice` | Owner (group) |
| `4096` | File size in bytes |
| `Jun 8 10:00` | Last modification date/time |
| `notes.txt` | File/directory name |

---

### `-a` — Show All (Including Hidden Files)
```bash
ls -a
```
Hidden files in Linux start with a `.` (dot). This flag reveals them.
- `.` → current directory
- `..` → parent directory
- `.bashrc`, `.ssh/` → hidden config files/folders

---

### `-A` — Show Almost All (Hidden, Except `.` and `..`)
```bash
ls -A
```
Same as `-a` but excludes the `.` and `..` entries.

---

### `-h` — Human-Readable File Sizes
```bash
ls -lh
```
Used **with `-l`**, converts file sizes into readable units:
- `4.0K` instead of `4096`
- `1.5M`, `2.3G`, etc.

---

### `-r` — Reverse Order
```bash
ls -r
```
Lists files in reverse alphabetical order (or reverse of whatever sort is active).

---

### `-t` — Sort by Modification Time
```bash
ls -lt
```
Sorts files by **last modified time**, newest first.  
Combine with `-r` to show oldest first:
```bash
ls -ltr
```

---

### `-S` — Sort by File Size
```bash
ls -lS
```
Sorts files by size, **largest first**.

---

### `-R` — Recursive Listing
```bash
ls -R
```
Lists contents of the directory **and all its subdirectories** recursively.

---

### `-1` — One File Per Line
```bash
ls -1
```
Forces output to show **one entry per line**. Useful for scripting.

---

### `-d` — List Directory Itself (Not Its Contents)
```bash
ls -d /etc/
```
Shows info about the **directory itself**, not what's inside it.  
Useful with `-l`:
```bash
ls -ld /etc/
```

---

### `-i` — Show Inode Numbers
```bash
ls -i
```
Displays the **inode number** of each file — a unique identifier used by the filesystem.

---

### `-F` — Classify Entries with Symbols
```bash
ls -F
```
Appends a symbol to each entry to indicate its type:
| Symbol | Meaning |
|---|---|
| `/` | Directory |
| `*` | Executable file |
| `@` | Symbolic link |
| `\|` | Named pipe (FIFO) |
| `=` | Socket |
| (none) | Regular file |

---

### `--color` — Colorized Output
```bash
ls --color=auto
```
Enables color-coded output (usually enabled by default in Ubuntu via `.bashrc` alias):
- **Blue** → Directories
- **Green** → Executables
- **Cyan** → Symbolic links
- **Red** → Compressed/archive files
- **White/Gray** → Regular files

---

## Combining Options (Flags)

Flags can be combined together:

```bash
ls -lah
```
- `-l` → long format
- `-a` → include hidden files
- `-h` → human-readable sizes

```bash
ls -ltr
```
- `-l` → long format
- `-t` → sort by time
- `-r` → reverse (oldest first)

```bash
ls -lSh
```
- Sort by size, largest first, with human-readable sizes.

---

## Using Wildcards with `ls`

```bash
ls *.txt
```
Lists all `.txt` files in the current directory.

```bash
ls /etc/*.conf
```
Lists all `.conf` files inside `/etc/`.

```bash
ls file?.txt
```
`?` matches any **single character** — e.g., `file1.txt`, `fileA.txt`.

```bash
ls file[123].txt
```
Matches `file1.txt`, `file2.txt`, or `file3.txt`.

---

## Listing Multiple Directories at Once

```bash
ls /home /etc /var
```
Lists the contents of all three directories in sequence.

---

## Output Redirection

Save the output of `ls` to a file:
```bash
ls -lah > directory_listing.txt
```

Append to an existing file:
```bash
ls -lah >> directory_listing.txt
```

---

## `ls` in Scripts

When using `ls` inside shell scripts, prefer `find` or globbing for robustness, but `ls` works for quick listings:

```bash
#!/bin/bash
echo "Files in current directory:"
ls -1
```

> ⚠️ **Note:** Parsing `ls` output in scripts is discouraged for production use. Use `find` or bash globbing (`for f in *`) instead, as filenames with spaces or special characters can break `ls` parsing.

---

## Alias — Why `ls` Shows Colors by Default

In Ubuntu, `ls` is usually **aliased** in `~/.bashrc`:

```bash
alias ls='ls --color=auto'
```

You can check your alias with:
```bash
alias ls
```

To use the raw `ls` without the alias:
```bash
\ls
```

---

## Related Commands

| Command | Description |
|---|---|
| `dir` | Similar to `ls`, less feature-rich |
| `vdir` | Like `ls -l` |
| `find` | Search for files with advanced filters |
| `tree` | Display directory structure as a tree |
| `stat` | Detailed file/filesystem status |
| `file` | Identify file type |
| `du` | Disk usage of files/directories |

---

## Quick Reference Cheat Sheet

| Command | What it does |
|---|---|
| `ls` | List current directory |
| `ls -l` | Long/detailed format |
| `ls -a` | Show hidden files |
| `ls -A` | Hidden files, no `.` or `..` |
| `ls -lh` | Long format, human-readable sizes |
| `ls -lt` | Sort by modification time |
| `ls -lS` | Sort by file size |
| `ls -R` | Recursive listing |
| `ls -F` | Show file type indicators |
| `ls -i` | Show inode numbers |
| `ls -lah` | Long + hidden + human-readable |
| `ls -ltr` | Long + time-sorted + reversed |
| `ls *.txt` | List only `.txt` files |
| `ls -d */` | List only directories |

---

## Tips & Tricks

- **List only directories:**
  ```bash
  ls -d */
  ```

- **Count files in a directory:**
  ```bash
  ls -1 | wc -l
  ```

- **Find the most recently modified file:**
  ```bash
  ls -lt | head -2
  ```

- **List files sorted by extension:**
  ```bash
  ls -lX
  ```

- **Show full timestamps:**
  ```bash
  ls -l --full-time
  ```

---

*Notes compiled for Ubuntu/Linux command reference.*
