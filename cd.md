# `cd` — Change Directory

## Overview

The `cd` command stands for **Change Directory**. It is used to **navigate between directories** in the Linux/Ubuntu filesystem. It is a **shell built-in command** (not an external program), meaning it is handled directly by the shell (bash, zsh, etc.) rather than as a separate executable.

> Since `cd` changes the state of the current shell session, it **must** be a built-in — an external program cannot change the working directory of the parent shell process.

---

## Basic Syntax

```bash
cd [DIRECTORY]
```

- `DIRECTORY` — The target path to navigate to.
- If no argument is given, `cd` takes you to the **home directory**.

---

## Understanding the Linux Directory Structure

Before diving in, it helps to know key directory symbols:

| Symbol | Meaning |
|---|---|
| `/` | Root directory (top of the filesystem) |
| `~` | Home directory of the current user |
| `.` | Current directory |
| `..` | Parent directory (one level up) |
| `-` | Previous working directory |

---

## Basic Usage

### Go to a Specific Directory
```bash
cd /home/user/Documents
```
Navigates to the absolute path `/home/user/Documents`.

---

### Go to Home Directory
```bash
cd
```
or
```bash
cd ~
```
Both take you to your **home directory** (e.g., `/home/alice`).

---

### Go Up One Level (Parent Directory)
```bash
cd ..
```
Moves one directory **up** in the hierarchy.

Example:
```
Current: /home/alice/Documents
After cd ..: /home/alice
```

---

### Go Up Two Levels
```bash
cd ../..
```
Moves two directories up.

Example:
```
Current: /home/alice/Documents/Projects
After cd ../.. : /home/alice
```

---

### Go to Root Directory
```bash
cd /
```
Takes you to the **root** of the entire filesystem.

---

### Go to Previous Directory
```bash
cd -
```
Switches back to the **last directory you were in** — like an undo for navigation.

Example:
```bash
cd /var/log
cd /etc
cd -        # Goes back to /var/log
```
It also **prints** the directory it switched to.

---

## Absolute vs Relative Paths

### Absolute Path
Starts from the **root** `/`. Always works regardless of where you currently are.
```bash
cd /home/alice/Music
```

### Relative Path
Starts from the **current directory**. Depends on where you are now.
```bash
cd Documents/Projects
```
If you're in `/home/alice`, this takes you to `/home/alice/Documents/Projects`.

---

## Navigating with `~` (Tilde Expansion)

The `~` symbol always expands to the current user's home directory:

```bash
cd ~/Downloads
```
Equivalent to:
```bash
cd /home/alice/Downloads
```

You can also navigate to another user's home directory (if you have permission):
```bash
cd ~bob
```
Takes you to `/home/bob`.

---

## Navigating with Spaces in Directory Names

If a directory name contains **spaces**, handle it in one of two ways:

### Using Quotes
```bash
cd "My Documents"
cd 'My Documents'
```

### Using Backslash Escape
```bash
cd My\ Documents
```

---

## Navigating with Special Characters

Some directory names may contain special characters. Always **quote** or **escape** them:
```bash
cd "project (2024)"
cd project\ \(2024\)
```

---

## `cd` with Environment Variables

You can use environment variables as part of the path:

```bash
cd $HOME
```
Same as `cd ~` — navigates to the home directory.

```bash
cd $HOME/Documents
```

```bash
echo $HOME    # prints /home/alice
```

---

## Checking Where You Are — `pwd`

After using `cd`, confirm your location with `pwd` (Print Working Directory):
```bash
cd /var/log
pwd
# Output: /var/log
```

---

## `cd` and the `CDPATH` Variable

`CDPATH` is an environment variable that defines **additional base directories** for `cd` to search in — similar to `PATH` for executables.

```bash
export CDPATH=/home/alice:/var:/etc
```

Now if you type:
```bash
cd log
```
The shell searches for `log` in `/home/alice`, `/var`, and `/etc` — and finds `/var/log`.

---

## `cd` in Shell Scripts

In scripts, `cd` works, but you should **always check if it succeeded** before running further commands:

```bash
cd /some/directory || exit 1
```
or
```bash
if cd /some/directory; then
    echo "Changed directory successfully"
else
    echo "Failed to change directory"
    exit 1
fi
```

> ⚠️ In scripts, a failed `cd` without error handling can cause subsequent commands to run in the **wrong directory**, leading to dangerous operations.

---

## Common Errors

### `No such file or directory`
```bash
cd /home/alice/Documnets
# bash: cd: /home/alice/Documnets: No such file or directory
```
- Check spelling.
- Verify the path exists with `ls`.

---

### `Not a directory`
```bash
cd notes.txt
# bash: cd: notes.txt: Not a directory
```
- `cd` only works on **directories**, not files.

---

### `Permission denied`
```bash
cd /root
# bash: cd: /root: Permission denied
```
- You don't have permission to access that directory.
- Use `sudo -i` or `sudo su` to switch to root if needed.

---

## Useful `cd` Tricks

### Jump to Home from Anywhere
```bash
cd
# or
cd ~
```

---

### Toggle Between Two Directories
```bash
cd /var/log
cd /etc/nginx
cd -    # back to /var/log
cd -    # back to /etc/nginx
```

---

### Navigate Deep Paths Quickly with Tab Completion
```bash
cd /ho<TAB>/al<TAB>/Do<TAB>
```
Press `Tab` to auto-complete directory names. If multiple matches exist, press `Tab` twice to see all options.

---

### Using `pushd` and `popd` (Directory Stack)

These are related built-ins that extend `cd` with a **stack-based navigation** system:

```bash
pushd /var/log    # Go to /var/log AND save current dir on stack
pushd /etc        # Go to /etc AND save /var/log on stack
popd              # Return to /var/log
popd              # Return to original directory
```

- `dirs` — Shows the current directory stack.

---

## `cd` vs `pushd`/`popd`

| Feature | `cd` | `pushd`/`popd` |
|---|---|---|
| Navigate to directory | ✅ | ✅ |
| Remember history (stack) | ❌ (only one previous) | ✅ (multiple) |
| Return to previous | `cd -` (one level) | `popd` (full stack) |
| Use case | Simple navigation | Complex multi-dir workflows |

---

## Summary of `cd` Shortcuts

| Command | Action |
|---|---|
| `cd` | Go to home directory |
| `cd ~` | Go to home directory |
| `cd /` | Go to root directory |
| `cd ..` | Go up one level |
| `cd ../..` | Go up two levels |
| `cd -` | Go to previous directory |
| `cd ~/Documents` | Go to Documents in home |
| `cd /absolute/path` | Navigate via absolute path |
| `cd relative/path` | Navigate via relative path |
| `cd "dir with spaces"` | Handle spaces in names |
| `cd ~username` | Go to another user's home |

---

## Quick Reference — Path Symbols

| Symbol | Expands To |
|---|---|
| `~` | `/home/currentuser` |
| `.` | Current directory |
| `..` | Parent directory |
| `-` | Previous directory (`$OLDPWD`) |
| `/` | Root directory |

---

## Related Commands

| Command | Description |
|---|---|
| `pwd` | Print current working directory |
| `ls` | List contents of a directory |
| `pushd` | Change directory and push to stack |
| `popd` | Return to directory from stack |
| `dirs` | Display directory stack |
| `find` | Search for files/directories |
| `tree` | Display directory tree visually |

---

*Notes compiled for Ubuntu/Linux command reference.*
