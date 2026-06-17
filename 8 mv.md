
# mv Command - Complete Ubuntu Guide

## Overview

The `mv` (move) command is a fundamental UNIX/Linux utility used for **renaming and relocating files and directories** in the filesystem. It serves two primary functions:

1. **Move files/directories** from one location to another
2. **Rename files/directories** by changing their names

**Key Behavior:**
- ✅ Same filesystem: Renames the file (metadata change only, very fast)
- ✅ Different filesystem: Copies file to destination, then removes original (slower)
- ✅ Overwrites destination files by default (no warning)
- ✅ Works on both files and directories

**Primary Use Cases:**
- Moving files between directories
- Renaming files and folders
- Organizing file structure
- Upgrading files (replacing old versions)
- Batch renaming with patterns

---

## Syntax

**General syntax:**
```bash
mv [OPTIONS] SOURCE DESTINATION
```

**Parameters:**
- `OPTIONS`: Command-line flags to customize behavior
- `SOURCE`: The file or directory to move (can be multiple files)
- `DESTINATION`: The target location (directory path or new filename)

**Two usage patterns:**

### Pattern 1: Move to Directory
```bash
mv [options] file.txt /path/to/destination/
```
Moves `file.txt` into the destination directory, keeping the same filename.

### Pattern 2: Rename File
```bash
mv [options] old_name.txt new_name.txt
```
Renames the file from `old_name.txt` to `new_name.txt`.

**Example:**
```bash
mv document.txt /home/user/Documents/
mv old_name.txt new_name.txt
```

---

## All Options and Flags

### Table of Options

| Option | Long Option | Description | Safety Level |
|--------|-------------|-------------|--------------|
| `-i` | `--interactive` | Ask before overwriting (prompt) | Safe |
| `-n` | `--no-clobber` | Never overwrite (skip if exists) | Very Safe |
| `-v` | `--verbose` | Show what is being done | Info |
| `-u` | `--update` | Move only if SOURCE is newer OR DEST missing | Smart |
| `-f` | `--force` | Overwrite without prompting | Risky |
| `-b` | `--backup` | Create backup of overwritten files | Safe |
| `-t` | `--target-directory` | Specify target directory explicitly | Convenience |
| `-T` | `--no-target-directory` | Treat DEST as normal file | Strict |
| `-Z` | `--context` | Set SELinux security context | Security |
| `-S` | `--suffix` | Backup suffix (with `-b`) | Backup |
| `--version-control` | `-` | Type of backups to make | Backup |

---

## Essential Usage Examples

### 1. Move a Single File to Directory

**Basic move:**
```bash
mv document.txt /home/user/Documents/
```

**What happens:**
- file moves from current directory to `/home/user/Documents/`
- Filename stays `document.txt`
- Original file is removed from source location

**Real example:**
```bash
mv report.pdf ~/Documents/
mv config.json /etc/myapp/
```

---

### 2. Rename a File (Same Directory)

**Rename file:**
```bash
mv old_name.txt new_name.txt
```

**What happens:**
- File name changes from `old_name.txt` to `new_name.txt`
- File stays in same directory
- Fast operation (only metadata change)

**Real examples:**
```bash
mv README.md README.txt
mv photo.jpg photo_renamed.jpg
mv index.js index.ts
```

---

### 3. Move and Rename at Same Time

**Move to directory with new name:**
```bash
mv file.txt /destination/new_name.txt
```

**What happens:**
- File moves to `/destination/`
- Filename changes to `new_name.txt`

**Real example:**
```bash
mv download.zip ~/backup/archive_2024.zip
mv script.py /opt/scripts/main.py
```

---

### 4. Move Multiple Files to Directory

**Move several files:**
```bash
mv file1.txt file2.txt file3.txt /destination/
```

**What happens:**
- All three files move to `/destination/`
- Filenames remain unchanged

**Real example:**
```bash
mv photo1.jpg photo2.jpg photo3.jpg ~/Pictures/
mv config.json package.json ./node_modules/
```

---

### 5. Move All Files with Pattern (Wildcard)

**Move all .txt files:**
```bash
mv *.txt /destination/
```

**What happens:**
- All files ending in `.txt` move to destination
- Shell expands `*.txt` to match all text files

**More patterns:**
```bash
mv *.jpg ~/Pictures/          # All JPEG files
mv *.log /var/logs/backup/    # All log files
mv backup_* ./archives/       # All files starting with "backup_"
```

---

### 6. Interactive Mode (Ask Before Overwrite)

**Safe move with prompt:**
```bash
mv -i file.txt /destination/file.txt
```

**If destination exists:**
```
mv: replace '/destination/file.txt'? 
```

**Respond:**
- Type `y` and press `Enter` to overwrite
- Type `n` and press `Enter` to skip

**Real example:**
```bash
mv -i config.json ./backup/config.json
```

**Useful for:**
- Preventing accidental overwrites
- Moving files to directories with existing names
- Safety when working with important files

---

### 7. No-Clobber Mode (Never Overwrite)

**Skip if destination exists:**
```bash
mv -n file.txt /destination/file.txt
```

**If destination exists:**
- File is NOT moved
- No error, no prompt
- Silent skip

**Real example:**
```bash
mv -n *.png ./images/
```

**Useful for:**
- Batch operations where duplicates are acceptable
- Scripts that shouldn't fail on existing files
- Safe bulk moves

---

### 8. Verbose Mode (Show Progress)

**See what's happening:**
```bash
mv -v file.txt /destination/
```

**Output:**
```
'myfile.txt' -> '/destination/myfile.txt'
```

**Multiple files:**
```bash
mv -v file1.txt file2.txt file3.txt ./backup/
```

**Output:**
```
'file1.txt' -> './backup/file1.txt'
'file2.txt' -> './backup/file2.txt'
'file3.txt' -> './backup/file3.txt'
```

**Useful for:**
- Verifying moves completed correctly
- Debugging move operations
- Script logging
- Understanding what mv is doing

---

### 9. Update Mode (Move Only If Newer)

**Smart move with `-u`:**
```bash
mv -u source.txt /destination/source.txt
```

**Behavior:**
- If destination doesn exist: **Moves** the file
- If destination exists AND is newer: **Skips** (doesn't move)
- If destination exists AND is older: **Moves** (overwrites)

**Real examples:**
```bash
mv -u *.jpg ~/Pictures/         # Move only newer images
mv -u document.pdf ./backup/    # Update backup if newer
```

**Useful for:**
- Incremental backups
- Syncing files without unnecessary copies
- Updating configuration files
- Efficient file organization

---

### 10. Force Mode (Overwrite Without Prompt)

**Overwrite aggressively:**
```bash
mv -f file.txt /destination/file.txt
```

**Behavior:**
- Overwrites destination without asking
- Removes read-only files if needed
- No warnings

**Real example:**
```bash
mv -f old_config.json /etc/app/config.json
```

**⚠️ Warning:** Use carefully - no safety checks!

**When to use:**
- Scripts where you control the flow
- When you know overwrites are intentional
- Removing lock files or temporary files

---

### 11. Backup Mode (Create Backups Before Overwrite)

**Create backup automatically:**
```bash
mv -b file.txt /destination/file.txt
```

**If destination exists:**
- Original becomes: `file.txt~` (with default suffix)
- New file moves in as `file.txt`

**Custom backup suffix:**
```bash
mv -b -S '.bak' file.txt /destination/file.txt
```

**Result:**
- Backup: `file.txt.bak`
- New: `file.txt`

**Real example:**
```bash
mv -b config.json ./backup/config.json
```

**Useful for:**
- Safely replacing important files
- Configuration file updates
- Preventing accidental data loss

---

### 12. Move Directory (Folder)

**Move entire directory:**
```bash
mv myfolder/ /destination/
```

**What happens:**
- Entire folder moves (including all contents)
- Recursive operation
- Permissions preserved

**Move and rename directory:**
```bash
mv old_folder/ /destination/new_folder/
```

**Real examples:**
```bash
mv project_files/ ~/Documents/
mv downloads/ ./backup/2024/
mv website/ /var/www/html/
```

---

### 13. Move Using Absolute and Relative Paths

**Absolute path (from root):**
```bash
mv /home/user/files/document.txt /var/data/
```

**Relative path (from current):**
```bash
mv documents/report.txt ../backup/
```

**Using `~` (home directory):**
```bash
mv file.txt ~/Documents/
mv ~/Downloads/image.jpg ~/Pictures/
```

**Using `.` (current directory):**
```bash
mv file.txt ./backup/
mv src/main.js ./dist/
```

**Using `..` (parent directory):**
```bash
mv file.txt ../
mv config.json ../../settings/
```

---

### 14. Target Directory Option (-t)

**Explicit target syntax:**
```bash
mv -t /destination/ file.txt
```

**Alternative to:**
```bash
mv file.txt /destination/
```

**Multiple files:**
```bash
mv -t ./backup/ file1.txt file2.txt file3.txt
```

**Useful for:**
- Consistent syntax in scripts
- Readability when destination is complex
- Batch operations

---

### 15. Combine Multiple Options

**Verbose + Interactive:**
```bash
mv -iv file.txt /destination/
```

**Shows:**
```
'myfile.txt' -> '/destination/myfile.txt'
mv: replace '/destination/myfile.txt'? 
```

**Verbose + Update:**
```bash
mv -vu *.jpg ./Pictures/
```

**Verbose + Backup:**
```bash
mv -vb config.json /etc/app/config.json
```

**All safe options:**
```bash
mv -ivn file.txt /dest/    # Note: -n overrides -i
```

---

## Practical Real-World Examples

### Example 1: Organizing Downloads
```bash
mv ~/Downloads/*.pdf ~/Documents/
mv ~/Downloads/*.jpg ~/Pictures/
mv ~/Downloads/*.zip ./archives/
```

### Example 2: Updating Configuration
```bash
mv -b config.json /etc/myapp/config.json
```
Creates backup before replacing system config.

### Example 3: Moving Project Files
```bash
mv project/ ~/Documents/work/
mv project/src/ ~/Documents/work/project/src/
```

### Example 4: Renaming Files for Consistency
```bash
mv IMG_001.jpg photo_001.jpg
mv IMG_002.jpg photo_002.jpg
mv IMG_003.jpg photo_003.jpg
```

### Example 5: Backup Important Files
```bash
mv -b database.sql ./backup/database.sql
mv -v important_doc.pdf ~/backup/
```

### Example 6: Moving Log Files
```bash
mv -u /var/log/app.log ./logs/
mv *.log /var/log/archive/
```

### Example 7: Git File Management
```bash
mv src/old_file.js src/new_file.js
git add src/new_file.js
git rm src/old_file.js
```

### Example 8: Batch Rename with Pattern
```bash
mv photo_2023_01.jpg photo_jan_01.jpg
mv photo_2023_02.jpg photo_jan_02.jpg
```

### Example 9: Move to Remote-Safe Location
```bash
mv sensitive_data.txt ~/Private/
mv private_keys/ ~/.ssh/
```

### Example 10: Deployment Files
```bash
mv dist/* /var/www/html/
mv build/app.js /opt/application/
```

---

## Common Pitfalls and Warnings

### ⚠️ 1. Overwriting Files Without Warning

**Dangerous:**
```bash
mv file.txt /destination/file.txt  # Overwrites if exists!
```

**Safe:**
```bash
mv -i file.txt /destination/file.txt  # Prompts first
mv -n file.txt /destination/file.txt  # Skips if exists
```

### ⚠️ 2. Moving to Non-Existent Directory

**Error:**
```bash
mv file.txt /nonexistent/dir/
# mv: cannot move 'file.txt' to '/nonexistent/dir/file.txt': No such file or directory
```

**Solution:**
```bash
mkdir -p /nonexistent/dir/
mv file.txt /nonexistent/dir/
```

### ⚠️ 3. Moving File to Same Name

**Unexpected result:**
```bash
mv file.txt ./file.txt  # File becomes empty!
```

**Why:** Creates new file, then removes old

**Check first:**
```bash
ls -l file.txt ./file.txt  # Verify they're different
```

### ⚠️ 4. Moving Directory Without Contents

**Misconception:**
```bash
mv folder/ ./dest/  # Moves entire folder with contents
```

**This IS correct:** Moves entire directory recursively

**If you want only contents:**
```bash
mv folder/* ./dest/  # Moves files inside, not folder itself
```

### ⚠️ 5. Permission Issues

**Error:**
```bash
mv file.txt /root/protected/
# mv: cannot move 'file.txt': Permission denied
```

**Solution:**
```bash
sudo mv file.txt /root/protected/
```

### ⚠️ 6. Moving Read-Only Files

**Error:**
```bash
mv -i readonly.txt ./backup/
# May fail without -f
```

**Solution:**
```bash
mv -f readonly.txt ./backup/
```

---

## Related Commands

| Command | Purpose | Difference from mv |
|---------|---------|-------------------|
| `cp` | Copy files | Creates duplicate, original stays |
| `rm` | Remove files | Deletes, doesn't relocate |
| `rename` | Batch rename | Renames multiple files with patterns |
| `ln` | Create links | Creates reference, not move |
| `rsync` | Sync files | Advanced copy with verification |
| `dd` | Copy raw data | Low-level copying |
| `find` | Search files | Find then move with `-exec` |
| `touch` | Change timestamps | Modify metadata only |

### Comparison Examples:
```bash
# Copy (original stays):
cp file.txt ./backup/

# Move (original removed):
mv file.txt ./backup/

# Move with verification:
rsync -av file.txt ./backup/ && rm file.txt

# Find and move:
find . -name "*.log" -exec mv {} ./logs/ \;

# Batch rename:
rename 's/old/new/' *.txt
```

---

## Best Practices

### ✅ 1. Use `-i` for Important Files
```bash
mv -i config.json /etc/app/  # Safe for critical files
```

### ✅ 2. Use `-v` for Verification
```bash
mv -v *.txt ./backup/  # See what moved
```

### ✅ 3. Use `-u` for Backups
```bash
mv -u document.pdf ./backup/  # Only update if newer
```

### ✅ 4. Check Destination First
```bash
ls -l /destination/  # Verify before moving
```

### ✅ 5. Use Absolute Paths for System Files
```bash
mv file.txt /etc/app/config.json  # Clear location
```

### ✅ 6. Create Directory Before Move
```bash
mkdir -p ./backup/
mv file.txt ./backup/
```

### ✅ 7. Use `-b` for Config Updates
```bash
mv -b app.conf /etc/app/app.conf  # Auto-backup
```

### ✅ 8. Test with Wildcards Carefully
```bash
ls *.txt  # Check what matches first
mv *.txt ./backup/
```

---

## Advanced Tips

### Tip 1: Move with find Command
```bash
find . -name "*.tmp" -exec mv {} ./temp/ \;
```

### Tip 2: Move Based on Age
```bash
find . -mtime +30 -name "*.log" -exec mv {} ./old_logs/ \;
```

### Tip 3: Rename Multiple Files
```bash
for file in IMG_*.jpg; do mv "$file" "photo_$file"; done
```

### Tip 4: Move to Timestamped Directory
```bash
mv file.txt ./backup/$(date +%Y%m%d)/
```

### Tip 5: Safe Move Script
```bash
mv_safe() {
    if [ -f "$2" ]; then
        echo "Destination exists: $2"
        return 1
    fi
    mv "$1" "$2"
}
```

### Tip 6: Move and Verify
```bash
mv file.txt ./backup/
cmp file.txt ./backup/file.txt  # Verify integrity
```

---

## Summary

The `mv` command is essential for:
- ✅ Moving files between directories
- ✅ Renaming files and folders
- ✅ Organizing file structure
- ✅ Updating files safely with `-u`
- ✅ Creating backups automatically with `-b`
- ✅ Preventing overwrites with `-i` or `-n`

**Remember:**
- Use `-i` for interactive (prompt before overwrite)
- Use `-n` for no-clobber (skip if exists)
- Use `-v` for verbose (see what's happening)
- Use `-u` for update (move only if newer)
- Use `-f` for force (overwrite without prompt)
- Use `-b` for backup (auto-backup overwritten files)
- Same filesystem = rename (fast)
- Different filesystem = copy + delete (slower)
- Always check permissions before moving system files
- Use absolute paths for clarity with system directories

---

**Quick Reference Card:**
```bash
mv file.txt ./dest/           # Move file
mv old.txt new.txt            # Rename file
mv file.txt ./new.txt         # Move + rename
mv *.txt ./backup/            # Move all .txt files
mv -i file.txt ./dest/        # Safe (prompt)
mv -n file.txt ./dest/        # Skip if exists
mv -v file.txt ./dest/        # Show progress
mv -u file.txt ./dest/        # Update if newer
mv -b file.txt ./dest/        # Auto-backup
mv -f file.txt ./dest/        # Force overwrite
mv -t ./dest/ file.txt        # Target directory
mv folder/ ./dest/            # Move directory
sudo mv file.txt /root/       # Move with sudo
```
```
