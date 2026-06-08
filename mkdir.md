# `mkdir` — Make Directory

## Overview

The `mkdir` command stands for **Make Directory**. It is used to **create one or more new directories** in the Linux/Ubuntu filesystem. It is a standard Unix utility available on all Linux distributions.

---

## Basic Syntax

```bash
mkdir [OPTIONS] DIRECTORY_NAME...
```

- `OPTIONS` — Flags that modify behavior.
- `DIRECTORY_NAME` — Name(s) of the directory/directories to create. You can specify **multiple** at once.

---

## Basic Usage

### Create a Single Directory
```bash
mkdir myfolder
```
Creates a directory named `myfolder` in the **current working directory**.

---

### Create Multiple Directories at Once
```bash
mkdir folder1 folder2 folder3
```
Creates three directories simultaneously in the current directory.

---

### Create a Directory at a Specific Path
```bash
mkdir /home/alice/Documents/projects
```
Creates the `projects` directory inside `/home/alice/Documents/` (the parent must already exist).

---

## Options (Flags)

### `-p` — Create Parent Directories as Needed
```bash
mkdir -p /home/alice/projects/2024/june
```
Creates the **entire path**, including any missing intermediate directories.

Without `-p`, if `/home/alice/projects/` doesn't exist, the command **fails**:
```
mkdir: cannot create directory '/home/alice/projects/2024/june': No such file or directory
```

With `-p`, all missing parent directories are created automatically.

> ✅ `-p` also **suppresses errors** if the directory already exists — making it safe to use in scripts.

---

### `-m` — Set Permissions (Mode) at Creation
```bash
mkdir -m 755 myfolder
```
Creates the directory with specific **permissions** at the time of creation, instead of using the default `umask`.

Permission values follow the **octal notation**:

| Value | Permissions |
|---|---|
| `777` | rwxrwxrwx (full for all) |
| `755` | rwxr-xr-x (owner full, others read+execute) |
| `700` | rwx------ (owner only) |
| `644` | rw-r--r-- (owner read+write, others read) |

Example:
```bash
mkdir -m 700 private_folder
```
Only the owner can access `private_folder`.

---

### `-v` — Verbose Output
```bash
mkdir -v folder1 folder2
```
Prints a message for **each directory created**:
```
mkdir: created directory 'folder1'
mkdir: created directory 'folder2'
```
Useful for confirming what was created, especially in scripts.

---

### Combining Options
```bash
mkdir -pv /home/alice/projects/2024/june
```
Creates the full path **and** prints each directory as it's created:
```
mkdir: created directory '/home/alice/projects'
mkdir: created directory '/home/alice/projects/2024'
mkdir: created directory '/home/alice/projects/2024/june'
```

```bash
mkdir -pm 755 /var/www/mysite
```
Creates the full path with `755` permissions on the final directory.

---

## Creating Directories with Spaces in Names

### Using Quotes
```bash
mkdir "My Projects"
mkdir 'My Documents'
```

### Using Backslash Escape
```bash
mkdir My\ Projects
```

> ⚠️ Avoid spaces in directory names when possible — they require escaping every time you reference them.

---

## Using Brace Expansion to Create Multiple Directories

Bash **brace expansion** is a powerful way to create multiple related directories in one command.

### Create Multiple Sibling Directories
```bash
mkdir -p project/{src,bin,docs,tests}
```
Creates:
```
project/
├── src/
├── bin/
├── docs/
└── tests/
```

### Create Nested Structures
```bash
mkdir -p project/{src/{main,utils},docs/{api,guides},tests}
```
Creates:
```
project/
├── src/
│   ├── main/
│   └── utils/
├── docs/
│   ├── api/
│   └── guides/
└── tests/
```

### Create Numbered Directories
```bash
mkdir week{1..5}
```
Creates: `week1`, `week2`, `week3`, `week4`, `week5`

```bash
mkdir -p backup/2024/{jan,feb,mar,apr,may,jun,jul,aug,sep,oct,nov,dec}
```
Creates a full year of monthly backup folders.

---

## Default Permissions and `umask`

When you create a directory without `-m`, the permissions are determined by the **umask** value.

- Default directory permission: `777`
- Typical `umask` value: `022`
- Result: `777 - 022 = 755` (`rwxr-xr-x`)

Check your current umask:
```bash
umask
# Output: 0022
```

Change umask temporarily:
```bash
umask 027
mkdir secured_folder   # Results in 750 permissions
```

---

## `mkdir` in Shell Scripts

### Safe Directory Creation with `-p`
```bash
#!/bin/bash
mkdir -p /var/app/logs
mkdir -p /var/app/data
mkdir -p /var/app/config
```
Using `-p` ensures the script doesn't fail if directories already exist.

---

### Check if Directory Was Created Successfully
```bash
mkdir mydir
if [ $? -eq 0 ]; then
    echo "Directory created successfully."
else
    echo "Failed to create directory."
fi
```

Or more concisely:
```bash
mkdir mydir && echo "Created!" || echo "Failed!"
```

---

### Create Directory Only If It Doesn't Exist
```bash
if [ ! -d "mydir" ]; then
    mkdir mydir
fi
```
Or simply use `-p` which handles this automatically:
```bash
mkdir -p mydir
```

---

## Common Errors

### `File exists`
```bash
mkdir existingfolder
# mkdir: cannot create directory 'existingfolder': File exists
```
**Fix:** Use `-p` to suppress this error, or check with `[ -d dirname ]` first.

---

### `No such file or directory`
```bash
mkdir /nonexistent/path/newdir
# mkdir: cannot create directory '/nonexistent/path/newdir': No such file or directory
```
**Fix:** Use `-p` to create all missing parent directories automatically.

---

### `Permission denied`
```bash
mkdir /etc/newdir
# mkdir: cannot create directory '/etc/newdir': Permission denied
```
**Fix:** Use `sudo`:
```bash
sudo mkdir /etc/newdir
```

---

## Permissions After Creation

After creating a directory, you can verify and change permissions:

```bash
ls -ld myfolder
# drwxr-xr-x 2 alice alice 4096 Jun 8 10:00 myfolder
```

Change permissions later with `chmod`:
```bash
chmod 700 myfolder
```

Change ownership with `chown`:
```bash
sudo chown bob:bob myfolder
```

---

## Practical Examples

### Set Up a Web Project Structure
```bash
mkdir -p mywebsite/{html,css,js,images,fonts}
```

### Set Up a Python Project
```bash
mkdir -p myapp/{src,tests,docs,assets}
touch myapp/src/__init__.py
```

### Create Dated Backup Folders
```bash
mkdir -p /backup/$(date +%Y-%m-%d)
```
Creates a folder like `/backup/2024-06-08` using today's date.

### Create Log Directories with Restricted Permissions
```bash
mkdir -m 750 /var/log/myapp
```

---

## Quick Reference Cheat Sheet

| Command | Action |
|---|---|
| `mkdir dirname` | Create a single directory |
| `mkdir dir1 dir2 dir3` | Create multiple directories |
| `mkdir -p a/b/c` | Create full path including parents |
| `mkdir -m 755 dirname` | Create with specific permissions |
| `mkdir -v dirname` | Verbose — print what's created |
| `mkdir -pv a/b/c` | Create full path with verbose output |
| `mkdir "dir name"` | Create directory with spaces |
| `mkdir {a,b,c}` | Create multiple dirs with brace expansion |
| `mkdir dir{1..5}` | Create numbered directories |
| `sudo mkdir /etc/mydir` | Create directory requiring root access |

---

## Related Commands

| Command | Description |
|---|---|
| `rmdir` | Remove an **empty** directory |
| `rm -r` | Remove a directory and all its contents |
| `ls -l` | List directory contents with details |
| `cd` | Navigate into a directory |
| `pwd` | Print current working directory |
| `chmod` | Change directory permissions |
| `chown` | Change directory ownership |
| `tree` | Display directory structure visually |
| `find` | Search for directories/files |

---

*Notes compiled for Ubuntu/Linux command reference.*
