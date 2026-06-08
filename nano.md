
# `nano` Command in Ubuntu

## Overview

`nano` is a simple command-line text editor used in Ubuntu/Linux to create and edit text files directly from the terminal.

It is beginner-friendly because common shortcuts are displayed at the bottom of the editor window.

---

## Basic Syntax


nano [options] filename
```

Example:
nano file.txt
```

If `file.txt` exists, nano opens it for editing.

If it does not exist, nano creates it when you save.

---

## Install Nano

Nano is usually pre-installed on Ubuntu.

Check version:

```bash
nano --version
```

Install nano:

```bash
sudo apt update
sudo apt install nano
```

---

## Open or Create a File

```bash
nano notes.txt
```

This opens `notes.txt`.

If the file does not exist, nano opens a blank editor and creates the file after saving.

---

## Edit a System File

Some files require administrator permission.

```bash
sudo nano /etc/hosts
```

Example:

```bash
sudo nano /etc/ssh/sshd_config
```

Be careful with system configuration files. Wrong changes can stop services from working.

---

## Important Nano Shortcuts

In nano, the `^` symbol means `Ctrl`.

So:

```text
^X = Ctrl + X
```

| Shortcut | Meaning |
|---|---|
| `Ctrl + O` | Save file |
| `Enter` | Confirm filename while saving |
| `Ctrl + X` | Exit nano |
| `Ctrl + W` | Search text |
| `Ctrl + K` | Cut current line |
| `Ctrl + U` | Paste cut text |
| `Ctrl + G` | Open help |
| `Ctrl + C` | Show cursor position |
| `Ctrl + _` | Go to specific line |
| `Alt + U` | Undo |
| `Alt + E` | Redo |
| `Alt + A` | Start selecting text |
| `Alt + 6` | Copy selected text |

---

## Save a File

Press:

```text
Ctrl + O
```

Nano shows:

```text
File Name to Write:
```

Press:

```text
Enter
```

The file is saved.

---

## Exit Nano

Press:

```text
Ctrl + X
```

If the file has unsaved changes, nano asks:

```text
Save modified buffer?
```

Options:

| Key | Meaning |
|---|---|
| `Y` | Save changes |
| `N` | Exit without saving |
| `Ctrl + C` | Cancel exit |

---

## Save and Exit

Use this sequence:

```text
Ctrl + O
Enter
Ctrl + X
```

This saves the file and exits nano.

---

## Exit Without Saving

Press:

```text
Ctrl + X
```

Then press:

```text
N
```

This exits and discards changes.

---

## Search Inside File

Press:

```text
Ctrl + W
```

Type the word you want to search.

Example:

```text
PermitRootLogin
```

Press:

```text
Enter
```

To find the next match:

```text
Alt + W
```

---

## Search and Replace

Press:

```text
Ctrl + \
```

Then enter the text to search for.

Then enter the replacement text.

Nano asks whether to replace each match.

| Key | Meaning |
|---|---|
| `Y` | Replace this match |
| `N` | Skip this match |
| `A` | Replace all matches |
| `Ctrl + C` | Cancel |

---

## Cut, Copy, and Paste

Cut current line:

```text
Ctrl + K
```

Paste:

```text
Ctrl + U
```

Select text:

```text
Alt + A
```

Copy selected text:

```text
Alt + 6
```

Paste copied text:

```text
Ctrl + U
```

---

## Move Around in Nano

| Shortcut | Meaning |
|---|---|
| Arrow keys | Move cursor |
| `Ctrl + A` | Beginning of line |
| `Ctrl + E` | End of line |
| `Ctrl + Y` | Page up |
| `Ctrl + V` | Page down |
| `Ctrl + _` | Go to line number |

---

## Open File at a Specific Line

```bash
nano +LINE filename
```

Example:

```bash
nano +25 app.py
```

Open at line 25.

Open at line and column:

```bash
nano +25,10 app.py
```

This opens `app.py` at line 25, column 10.

---

## Show Line Numbers

```bash
nano -l file.txt
```

or:

```bash
nano --linenumbers file.txt
```

Line numbers are useful when editing config files or following error messages.

---

## Open File in Read-Only Mode

```bash
nano -v file.txt
```

or:

```bash
nano --view file.txt
```

This lets you view the file without accidentally editing it.

---

## Disable Line Wrapping

```bash
nano -w file.txt
```

or:

```bash
nano --nowrap file.txt
```

This is useful for configuration files because unwanted line wrapping can break settings.

---

## Enable Auto Indentation

```bash
nano -i script.sh
```

This keeps indentation from the previous line.

Useful for scripts and code files.

---

## Create Backup Before Saving

```bash
nano -B file.txt
```

Nano creates a backup copy of the file.

Backup files usually end with:

```text
~
```

Example:

```text
file.txt~
```

---

## Set Tab Size

```bash
nano -T 4 file.txt
```

This sets tab width to 4 spaces.

---

## Use Syntax Highlighting

Nano can highlight syntax for many file types.

Example:

```bash
nano script.sh
```

Force syntax highlighting:

```bash
nano -Y sh script.txt
```

Examples of syntax names:

```text
sh
python
html
css
javascript
json
conf
```

Available syntax depends on nano configuration.

---

## Nano Configuration File

User nano settings are stored in:

```bash
~/.nanorc
```

Edit it:

```bash
nano ~/.nanorc
```

Useful settings:

```text
set linenumbers
set autoindent
set tabsize 4
set softwrap
set mouse
set backup
```

| Setting | Meaning |
|---|---|
| `set linenumbers` | Show line numbers |
| `set autoindent` | Auto-indent new lines |
| `set tabsize 4` | Set tab width to 4 |
| `set softwrap` | Visually wrap long lines |
| `set mouse` | Enable mouse support |
| `set backup` | Create backup files |

System-wide nano configuration:

```bash
/etc/nanorc
```

---

## Common Examples

Edit a text file:

```bash
nano notes.txt
```

Edit `.bashrc`:

```bash
nano ~/.bashrc
```

Apply `.bashrc` changes:

```bash
source ~/.bashrc
```

Edit hosts file:

```bash
sudo nano /etc/hosts
```

Edit SSH config:

```bash
sudo nano -w /etc/ssh/sshd_config
```

Edit crontab:

```bash
crontab -e
```

If asked to choose an editor, select nano for beginner-friendly editing.

---

## Useful Options

| Option | Meaning |
|---|---|
| `-h` | Show help |
| `--help` | Show help |
| `-V` | Show version |
| `--version` | Show version |
| `-l` | Show line numbers |
| `--linenumbers` | Show line numbers |
| `-v` | View-only mode |
| `--view` | View-only mode |
| `-w` | Disable automatic wrapping |
| `--nowrap` | Disable automatic wrapping |
| `-i` | Enable auto indentation |
| `-B` | Make backup file |
| `-T number` | Set tab size |
| `-Y syntax` | Use specific syntax highlighting |
| `+LINE` | Open file at line number |
| `+LINE,COLUMN` | Open file at line and column |

---

## Common Mistakes

### 1. Forgetting to Use `sudo`

Wrong:

```bash
nano /etc/hosts
```

Correct:

```bash
sudo nano /etc/hosts
```

Without `sudo`, you may not be able to save system files.

---

### 2. Forgetting to Save

Before exiting, save with:

```text
Ctrl + O
Enter
```

Then exit:

```text
Ctrl + X
```

---

### 3. Thinking `Ctrl + O` Exits Nano

`Ctrl + O` only saves.

To exit, use:

```text
Ctrl + X
```

---

### 4. Breaking Config Files With Wrapping

When editing configuration files, use:

```bash
nano -w file.conf
```

This prevents unwanted line wrapping.

---

## Best Practices

Before editing important files, make a backup:

```bash
sudo cp /etc/hosts /etc/hosts.backup
sudo nano /etc/hosts
```

Use line numbers:

```bash
nano -l file.txt
```

Use no wrapping for config files:

```bash
sudo nano -w /etc/ssh/sshd_config
```

For safer editing of system files, use:

```bash
sudoedit /path/to/file
```

---

## Related Commands

| Command | Purpose |
|---|---|
| `vim` | Advanced terminal editor |
| `vi` | Traditional Unix editor |
| `gedit` | Graphical text editor |
| `cat` | Display file content |
| `less` | View file page by page |
| `touch` | Create empty file |
| `cp` | Copy files |
| `mv` | Move or rename files |
| `rm` | Remove files |
| `sudoedit` | Safely edit system files |

---

## Quick Remember

The most important nano workflow is:

```text
Ctrl + O
Enter
Ctrl + X
```

Meaning:

```text
Save
Confirm
Exit
```

---

## Summary

`nano` is a simple and beginner-friendly terminal text editor in Ubuntu.

It is mainly used to create and edit text files from the command line.

Most important shortcuts:

| Shortcut | Meaning |
|---|---|
| `Ctrl + O` | Save |
| `Enter` | Confirm save |
| `Ctrl + X` | Exit |
| `Ctrl + W` | Search |
| `Ctrl + K` | Cut |
| `Ctrl + U` | Paste |
| `Ctrl + G` | Help |

Remember:

```text
Ctrl + O → Enter → Ctrl + X
```

This saves and exits nano.
```
