# `rmdir` — Remove Empty Directory

## Overview

The `rmdir` command stands for **Remove Directory**. It is used to **delete empty directories** from the Linux/Ubuntu filesystem. Unlike `rm -r`, `rmdir` is a **safe command** — it will **refuse to delete a directory that contains any files or subdirectories**, making it impossible to accidentally wipe out important data.

> `rmdir` is ideal when you want to clean up only empty directories with zero risk of data loss.

---

## Basic Syntax

```bash
rmdir [OPTIONS] DIRECTORY_NAME...
```

- `OPTIONS` — Flags that modify behavior.
- `DIRECTORY_NAME` — Name(s) of the directory/directories to remove. Must be **empty**.

---

## Basic Usage

### Remove a Single Empty Directory
```bash
rmdir myfolder
```
Deletes `myfolder` only if it is **completely empty**.

---

### Remove Multiple Empty Directories at Once
```bash
rmdir folder1 folder2 folder3
```
Removes all three directories in one command — each must be empty.

---

### Remove a Directory at a Specific Path
```bash
rmdir /home/alice/Documents/oldfolder
```
Removes `oldfolder` at the specified absolute path (must be empty).

---

## Options (Flags)

### `-p` — Remove Directory and Its Empty Parents
```bash
rmdir -p a/b/c
```
Removes `c`, then `b` (if now empty), then `a` (if now empty) — working **upward** through the path.

This is the **reverse** of `mkdir -p`.

Example:
```bash
mkdir -p one/two/three   # Creates the full path
rmdir -p one/two/three   # Removes three, then two, then one
```

If any parent still has other contents, removal stops there without error (depending on version):
```bash
rmdir -p projects/2024/june
# Removes june → then 2024 (if empty) → then projects (if empty)
```

---

### `-v` — Verbose Output
```bash
rmdir -v folder1 folder2
```
Prints a confirmation message for each directory removed:
```
rmdir: removing directory, 'folder1'
rmdir: removing directory, 'folder2'
```

---

### Combining Options
```bash
rmdir -pv a/b/c
```
Removes the full empty path and prints each step:
```
rmdir: removing directory, 'a/b/c'
rmdir: removing directory, 'a/b'
rmdir: removing directory, 'a'
```

---

## `rmdir` vs `rm -r`

This is one of the most important distinctions to understand:

| Feature | `rmdir` | `rm -r` |
|---|---|---|
| Removes empty directories | ✅ | ✅ |
| Removes non-empty directories | ❌ (refuses) | ✅ |
| Removes files | ❌ | ✅ |
| Risk of data loss | ❌ Very safe | ⚠️ High if misused |
| Recursively deletes contents | ❌ | ✅ |
| Best use case | Safe cleanup of empty dirs | Full directory tree removal |

> ✅ Use `rmdir` when you want **safety**.
> ⚠️ Use `rm -r` only when you **intentionally** want to delete everything inside.

---

## Common Errors

### `Directory Not Empty`
```bash
rmdir myfolder
# rmdir: failed to remove 'myfolder': Directory not empty
```
**Cause:** The directory contains files or subdirectories.

**Fix options:**
1. Manually empty the directory first, then `rmdir`.
2. Use `rm -r myfolder` to force-delete everything (use with caution).
3. Check what's inside first: `ls -la myfolder`

---

### `No Such File or Directory`
```bash
rmdir ghostfolder
# rmdir: failed to remove 'ghostfolder': No such file or directory
```
**Cause:** The directory doesn't exist.

**Fix:** Verify with `ls` or `[ -d dirname ]`.

---

### `Permission Denied`
```bash
rmdir /etc/somedir
# rmdir: failed to remove '/etc/somedir': Permission denied
```
**Cause:** You don't have write permission on the parent directory.

**Fix:** Use `sudo`:
```bash
sudo rmdir /etc/somedir
```

---

### `Not a Directory`
```bash
rmdir notes.txt
# rmdir: failed to remove 'notes.txt': Not a directory
```
**Cause:** The target is a file, not a directory.

**Fix:** Use `rm notes.txt` to remove files.

---

## Checking Before Removing

Always verify a directory is empty before attempting `rmdir`:

```bash
ls -la myfolder
```

Check if directory is empty in a script:
```bash
if [ -z "$(ls -A myfolder)" ]; then
    echo "Directory is empty"
else
    echo "Directory is NOT empty"
fi
```

---

## `rmdir` in Shell Scripts

### Remove Directory Only If It Exists and Is Empty
```bash
#!/bin/bash
DIR="myfolder"

if [ -d "$DIR" ] && [ -z "$(ls -A "$DIR")" ]; then
    rmdir "$DIR"
    echo "Removed: $DIR"
else
    echo "Skipped: $DIR (does not exist or is not empty)"
fi
```

---

### Safely Remove Multiple Empty Dirs
```bash
for dir in folder1 folder2 folder3; do
    rmdir "$dir" 2>/dev/null && echo "Removed $dir" || echo "Skipped $dir"
done
```
`2>/dev/null` suppresses error messages for non-empty or missing directories.

---

### Remove a Full Chain of Empty Directories
```bash
rmdir -p projects/2024/archive
```
Cleans up the entire empty chain in one command.

---

## Finding and Removing All Empty Directories

`rmdir` alone can't search — combine it with `find` for bulk cleanup:

### Find All Empty Directories
```bash
find . -type d -empty
```

### Remove All Empty Directories Under Current Path
```bash
find . -type d -empty -delete
```
> ⚠️ Double-check with `find . -type d -empty` before adding `-delete`.

### Remove Empty Dirs but Exclude Current Directory
```bash
find . -mindepth 1 -type d -empty -delete
```

---

## Handling Directories with Spaces in Names

### Using Quotes
```bash
rmdir "My Old Folder"
rmdir 'Backup Files'
```

### Using Backslash Escape
```bash
rmdir My\ Old\ Folder
```

---

## Practical Examples

### Clean Up an Empty Project Scaffold
```bash
mkdir -p project/{src,bin,docs}
rmdir project/bin           # Remove unused bin dir
```

### Remove an Entire Empty Directory Tree
```bash
mkdir -p temp/a/b/c
rmdir -p temp/a/b/c         # Removes c → b → a → temp
```

### Remove Multiple Dated Empty Folders
```bash
rmdir backup/2023/{jan,feb,mar}
```

### Safely Remove in a Script with Error Capture
```bash
rmdir olddir && echo "Done" || echo "Could not remove — check if empty"
```

---

## Quick Reference Cheat Sheet

| Command | Action |
|---|---|
| `rmdir dirname` | Remove a single empty directory |
| `rmdir dir1 dir2` | Remove multiple empty directories |
| `rmdir -p a/b/c` | Remove empty dir chain upward |
| `rmdir -v dirname` | Verbose — print confirmation |
| `rmdir -pv a/b/c` | Remove chain with verbose output |
| `sudo rmdir dirname` | Remove with elevated permissions |
| `rmdir "dir name"` | Remove directory with spaces |
| `find . -type d -empty -delete` | Remove all empty dirs recursively |

---

## Related Commands

| Command | Description |
|---|---|
| `rm -r` | Remove directory and **all its contents** |
| `rm -rf` | Force remove directory and contents (no prompts) |
| `mkdir` | Create a new directory |
| `ls -la` | List contents including hidden files |
| `find` | Search for files/directories |
| `tree` | Display directory tree visually |
| `chmod` | Change directory permissions |
| `pwd` | Print current working directory |

---

## Key Takeaway

> `rmdir` = **safe removal** — it will never delete data.
> If a directory has anything inside it, `rmdir` will stop and warn you.
> This makes it the **preferred** command for removing directories in scripts where safety matters.

---

*Notes compiled for Ubuntu/Linux command reference.*
