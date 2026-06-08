
# `rm` Command in Ubuntu

## Overview

`rm` stands for **remove**.

The `rm` command is used in Ubuntu/Linux to delete files and directories from the command line.

It is one of the most powerful and dangerous basic commands because deleted files usually do **not** go to the Trash. In most cases, they are removed immediately.

---

## Basic Syntax

```bash
rm [options] FILE...
```

Example:

```bash
rm notes.txt
```

This deletes `notes.txt`.

`FILE...` means you can give one file or many files.

Example:

```bash
rm file1.txt file2.txt file3.txt
```

---

## Important Warning

The `rm` command can permanently delete data.

Unlike deleting files from a graphical file manager, `rm` usually does not move files to Trash.

Before running `rm`, check:

```bash
pwd
ls
```

This helps confirm your current directory and the files inside it.

---

## Delete a Single File

```bash
rm file.txt
```

This removes `file.txt`.

Example:

```bash
rm notes.txt
```

---

## Delete Multiple Files

```bash
rm file1.txt file2.txt file3.txt
```

Example:

```bash
rm old.txt temp.txt backup.txt
```

This deletes all listed files.

---

## Delete Files With Confirmation

Use `-i` for interactive mode:

```bash
rm -i file.txt
```

Nano asks before deleting:

```text
rm: remove regular file 'file.txt'?
```

Press:

```text
y
```

to delete.

Press:

```text
n
```

to cancel.

This is safer when learning.

---

## Delete Without Asking

Use `-f`:

```bash
rm -f file.txt
```

`-f` means **force**.

It removes files without asking for confirmation.

It also ignores missing files.

Example:

```bash
rm -f missing-file.txt
```

This does not show an error if the file does not exist.

---

## Delete an Empty Directory

`rm` alone cannot remove directories.

Wrong:

```bash
rm myfolder
```

You may get:

```text
rm: cannot remove 'myfolder': Is a directory
```

To remove an empty directory, use:

```bash
rmdir myfolder
```

Or use:

```bash
rm -d myfolder
```

---

## Delete a Directory and Its Contents

Use `-r` or `-R`:

```bash
rm -r directory
```

Example:

```bash
rm -r old_project
```

This deletes the directory and everything inside it.

`-r` means **recursive**.

Recursive means it goes inside subdirectories and removes their contents too.

---

## Force Delete a Directory

```bash
rm -rf directory
```

This is very powerful and dangerous.

Meaning:

| Option | Meaning |
|---|---|
| `-r` | Delete recursively |
| `-f` | Force delete without asking |

Example:

```bash
rm -rf old_project
```

This deletes `old_project` and all files/subdirectories inside it without confirmation.

---

## Safer Recursive Delete

Use:

```bash
rm -ri directory
```

This asks before deleting files and directories.

Example:

```bash
rm -ri old_project
```

Useful when deleting folders that may contain important files.

---

## Verbose Delete

Use `-v` to show what is being removed:

```bash
rm -v file.txt
```

Example output:

```text
removed 'file.txt'
```

For a directory:

```bash
rm -rv old_project
```

This shows each removed file.

---

## Delete Files by Pattern

You can use wildcards.

Delete all `.txt` files:

```bash
rm *.txt
```

Delete all `.log` files:

```bash
rm *.log
```

Delete files starting with `temp`:

```bash
rm temp*
```

Delete files ending with `.bak`:

```bash
rm *.bak
```

Be careful with wildcards.

Before deleting, preview with `ls`:

```bash
ls *.txt
```

Then delete:

```bash
rm *.txt
```

---

## Delete Hidden Files

Hidden files start with a dot `.`.

Example:

```bash
.hiddenfile
```

Delete one hidden file:

```bash
rm .hiddenfile
```

Delete hidden files matching pattern:

```bash
rm .*.bak
```

Be extremely careful with patterns like:

```bash
rm -rf .*
```

This can match important parent directory entries or hidden configuration files depending on shell behavior and command context.

A safer way is to inspect first:

```bash
ls -la
```

Then delete specific hidden files by name.

---

## Delete File Names With Spaces

Use quotes:

```bash
rm "my file.txt"
```

Or escape the space:

```bash
rm my\ file.txt
```

Example:

```bash
rm "old report.pdf"
```

---

## Delete File Names Starting With `-`

If a filename starts with a dash, `rm` may think it is an option.

Example file:

```text
-file.txt
```

Use `--` to stop option parsing:

```bash
rm -- -file.txt
```

Or use a path:

```bash
rm ./-file.txt
```

---

## Delete Using Full Path

```bash
rm /home/user/Documents/file.txt
```

Example:

```bash
rm /home/vipin/Downloads/test.iso
```

Using full paths helps when deleting files outside the current directory, but it also increases risk if the path is wrong.

---

## Delete All Files in Current Directory

```bash
rm *
```

This deletes visible files in the current directory.

It usually does not delete hidden files.

It also does not delete directories unless recursive option is used.

Very dangerous:

```bash
rm -rf *
```

This deletes visible files and directories in the current directory.

Always check first:

```bash
pwd
ls
```

---

## Delete Everything Inside a Directory But Keep the Directory

```bash
rm -r directory/*
```

Example:

```bash
rm -r cache/*
```

This deletes visible contents inside `cache`, but keeps the `cache` directory itself.

Hidden files are not removed by `*`.

Check first:

```bash
ls -la cache
```

---

## Prompt Once Before Many Deletes

Use `-I`:

```bash
rm -I *.txt
```

`-I` asks once before deleting many files.

This is less annoying than `-i`, which asks for every file.

Example:

```bash
rm -I *.log
```

---

## Remove Empty Directory With `rm -d`

```bash
rm -d empty_folder
```

This removes an empty directory only.

If the directory contains files, it fails.

---

## Common Options

| Option | Long Option | Meaning |
|---|---|---|
| `-f` | `--force` | Ignore missing files and never prompt |
| `-i` |  | Ask before every removal |
| `-I` |  | Ask once before removing many files |
| `-r` | `--recursive` | Remove directories and contents recursively |
| `-R` | `--recursive` | Same as `-r` |
| `-d` | `--dir` | Remove empty directories |
| `-v` | `--verbose` | Show what is removed |
| `--` |  | Stop reading options |

---

## Common Examples

### Remove One File

```bash
rm file.txt
```

### Remove Multiple Files

```bash
rm file1.txt file2.txt
```

### Remove With Confirmation

```bash
rm -i file.txt
```

### Remove All Log Files

```bash
rm *.log
```

### Remove Empty Directory

```bash
rm -d emptydir
```

### Remove Directory Recursively

```bash
rm -r olddir
```

### Force Remove Directory

```bash
rm -rf olddir
```

### Verbose Recursive Remove

```bash
rm -rv olddir
```

### Remove File Starting With Dash

```bash
rm -- -file.txt
```

---

## `rm` vs `rmdir`

| Command | Use |
|---|---|
| `rm file.txt` | Delete file |
| `rm -r folder` | Delete folder and contents |
| `rmdir folder` | Delete empty folder only |
| `rm -d folder` | Delete empty folder only |

Use `rmdir` when you only want to remove an empty directory safely.

---

## `rm` vs Trash

`rm` permanently removes files from the filesystem.

It does not usually move them to Trash.

Graphical delete:

```text
Moves file to Trash
```

Terminal `rm`:

```text
Deletes file directly
```

If you want safer trash behavior from terminal, you can install `trash-cli`:

```bash
sudo apt install trash-cli
```

Then use:

```bash
trash-put file.txt
```

List trash:

```bash
trash-list
```

Restore from trash:

```bash
trash-restore
```

Empty trash:

```bash
trash-empty
```

---

## Dangerous Commands to Avoid

Be extremely careful with commands like:

```bash
rm -rf /
```

```bash
rm -rf /*
```

```bash
rm -rf ~
```

```bash
rm -rf $HOME
```

```bash
rm -rf *
```

```bash
sudo rm -rf /important/path
```

These can destroy important files, user data, or the operating system.

Modern GNU `rm` has some protection for root directory deletion, but you should never rely on that protection.

---

## `sudo rm`

Using `sudo rm` gives the command administrator permission.

Example:

```bash
sudo rm protected-file
```

Be very careful.

`sudo rm -rf` can delete system files and break Ubuntu.

Use `sudo` only when you are sure the file belongs to root or requires administrator permission.

---

## Check Before Removing

Good habit:

```bash
pwd
ls -la
```

If deleting by pattern, preview first:

```bash
ls *.log
```

Then:

```bash
rm *.log
```

For directories:

```bash
ls -la old_project
```

Then:

```bash
rm -r old_project
```

---

## Recovering Deleted Files

Files deleted with `rm` are difficult to recover.

Possible recovery depends on:

- Filesystem type
- Disk activity after deletion
- Whether backups exist
- Whether snapshots are enabled

If you accidentally delete important files:

1. Stop using the disk immediately.
2. Do not create new files.
3. Check backups.
4. Consider recovery tools such as `testdisk` or `extundelete`.

Example install:

```bash
sudo apt install testdisk
```

Recovery is not guaranteed.

---

## Best Practices

Use `rm -i` while learning:

```bash
rm -i file.txt
```

Use `rm -I` for many files:

```bash
rm -I *.log
```

Preview wildcards with `ls`:

```bash
ls *.tmp
```

Avoid unnecessary `sudo`.

Avoid using `rm -rf` unless you fully understand the path.

Use backups before deleting important folders.

Use `trash-cli` if you want safer deletion.

---

## Related Commands

| Command | Purpose |
|---|---|
| `rmdir` | Remove empty directories |
| `unlink` | Remove a single file name |
| `find` | Search files and delete matching files |
| `trash-put` | Move files to trash using `trash-cli` |
| `ls` | List files before deleting |
| `pwd` | Show current directory |
| `cp` | Copy files before deleting |
| `mv` | Move or rename files |
| `shred` | Overwrite files before deleting |

---

## Using `find` With `rm`

Delete files found by `find`:

```bash
find . -name "*.log" -type f -delete
```

This deletes `.log` files under the current directory.

Safer preview first:

```bash
find . -name "*.log" -type f
```

Then delete:

```bash
find . -name "*.log" -type f -delete
```

You can also use:

```bash
find . -name "*.tmp" -type f -exec rm {} \;
```

But `-delete` is simpler for many cases.

---

## Summary

`rm` is used to delete files and directories in Ubuntu.

Basic file deletion:

```bash
rm file.txt
```

Delete with confirmation:

```bash
rm -i file.txt
```

Delete directory recursively:

```bash
rm -r folder
```

Force delete directory:

```bash
rm -rf folder
```

Most important safety habit:

```bash
pwd
ls -la
```

Check where you are and what you are deleting before running `rm`.

Remember:

```text
rm does not usually send files to Trash.
```

Once removed, files may be very hard or impossible to recover.
```
