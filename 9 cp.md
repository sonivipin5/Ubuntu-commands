# cp Command - Complete Ubuntu Guide

## Overview

The `cp` (copy) command is a fundamental UNIX/Linux utility used for **creating duplicate copies of files and directories** in the filesystem. Unlike `mv`, it creates a new copy while keeping the original intact.

**Key Behavior:**
- ✅ Creates duplicate files/directories
- ✅ Original file remains unchanged
- ✅ Can copy to different locations or rename during copy
- ✅ Works recursively for directories (with `-r` option)
- ✅ Preserves permissions, timestamps, and attributes (with options)

**Primary Use Cases:**
- Creating backup copies of files
- Copying files between directories
- Distributing files to multiple locations
- Copying entire directory structures
- Preserving file attributes during copy

---

## Syntax

**General syntax:**
```bash
cp [OPTIONS] SOURCE DESTINATION
```

**Parameters:**
- `OPTIONS`: Command-line flags to customize behavior
- `SOURCE`: The file or directory to copy (can be multiple files)
- `DESTINATION`: The target location (directory path or new filename)

**Two usage patterns:**

### Pattern 1: Copy to Directory
```bash
cp [options] file.txt /path/to/destination/
```
Copies `file.txt` into the destination directory, keeping the same filename.

### Pattern 2: Copy and Rename
```bash
cp [options] old_name.txt new_name.txt
```
Creates a copy with a new name (`new_name.txt`).

**Example:**
```bash
cp document.txt /home/user/Documents/
cp config.json config_backup.json
```

---

## All Options and Flags

### Table of Options

| Option | Long Option | Description | Use Case |
|--------|-------------|-------------|----------|
| `-r` | `--recursive` | Copy directories recursively | Essential for folders |
| `-R` | `--recursive` | Same as `-r` | Alternative |
| `-i` | `--interactive` | Ask before overwriting | Safety |
| `-n` | `--no-clobber` | Never overwrite | Very safe |
| `-v` | `--verbose` | Show what's being copied | Verification |
| `-a` | `--archive` | Archive mode (-d -p -r) | Full preservation |
| `-p` | `--preserve` | Preserve attributes | Attributes |
| `-P` | `--no-dereference` | Don't follow symlinks | Symlinks |
| `-d` | `-` | Same as `-p --no-dereference` | Symlinks |
| `-l` | `--link` | Create hard links instead | Fast copies |
| `-s` | `--symbolic-link` | Create symlinks instead | Links |
| `-u` | `--update` | Copy only if newer | Smart copies |
| `-b` | `--backup` | Create backup before overwrite | Safety |
| `-f` | `--force` | Remove destination before copy | Force mode |
| `-L` | `--dereference` | Follow symlinks | Content |
| `-H` | `-` | Follow symlinks in args | Args |
| `-S` | `--suffix` | Backup suffix (with `-b`) | Backup |
| `-t` | `--target-directory` | Specify target explicitly | Convenience |
| `--parents` | `-` | Create parent directories | Structure |
| `--verbose` | `-` | Same as `-v` | Info |
| `--sparse` | `-` | Handle sparse files | Efficiency |

---

## Essential Usage Examples

### 1. Copy a Single File (Basic Usage)

**Basic copy:**
```bash
cp document.txt /home/user/Documents/
```

**What happens:**
- Creates duplicate in `/home/user/Documents/`
- Original stays in source location
- Filename remains `document.txt`

**Real examples:**
```bash
cp report.pdf ~/Documents/
cp config.json /etc/myapp/
cp image.jpg ~/Pictures/
```

---

### 2. Copy and Rename File

**Copy with new name:**
```bash
cp config.json config_backup.json
```

**What happens:**
- Creates `config_backup.json` in current directory
- Original `config.json` remains unchanged
- Two identical files exist

**Real examples:**
```bash
cp main.js main_v2.js
cp photo.jpg photo_edited.jpg
cp index.html index_old.html
```

---

### 3. Copy File to Directory with New Name

**Copy and rename simultaneously:**
```bash
cp file.txt /destination/new_name.txt
```

**What happens:**
- File copies to `/destination/`
- New filename is `new_name.txt`

**Real example:**
```bash
cp report.pdf ~/backup/report_2024.pdf
cp app.js /var/www/html/app_production.js
```

---

### 4. Copy Multiple Files to Directory

**Copy several files:**
```bash
cp file1.txt file2.txt file3.txt /destination/
```

**What happens:**
- All three files copy to `/destination/`
- Filenames remain unchanged
- Originals stay in source

**Real example:**
```bash
cp photo1.jpg photo2.jpg photo3.jpg ~/Pictures/
cp config.json package.json ./node_modules/
```

---

### 5. Copy All Files with Pattern (Wildcard)

**Copy all .txt files:**
```bash
cp *.txt /destination/
```

**What happens:**
- All files ending in `.txt` copy to destination
- Shell expands `*.txt` to match all text files

**More patterns:**
```bash
cp *.jpg ~/Pictures/           # All JPEG files
cp *.log /var/logs/backup/     # All log files
cp backup_* ./archives/        # All files starting with "backup_"
cp *.py ./python_scripts/      # All Python files
```

---

### 6. Copy Directory (Folder) - Recursive

**Copy entire directory (requires `-r`):**
```bash
cp -r myfolder/ /destination/
```

**What happens:**
- Entire folder copies (including all contents)
- Recursive operation (all subdirectories)
- Permissions preserved

**Copy and rename directory:**
```bash
cp -r old_folder/ /destination/new_folder/
```

**Real examples:**
```bash
cp -r project_files/ ~/Documents/
cp -r downloads/ ./backup/2024/
cp -r website/ /var/www/html/
cp -r src/ ./dist/src/
```

**⚠️ Important:** Without `-r`, copying directories fails with error.

---

### 7. Interactive Mode (Ask Before Overwrite)

**Safe copy with prompt:**
```bash
cp -i file.txt /destination/file.txt
```

**If destination exists:**
```
cp: overwrite '/destination/file.txt'? 
```

**Respond:**
- Type `y` and press `Enter` to overwrite
- Type `n` and press `Enter` to skip

**Real example:**
```bash
cp -i config.json ./backup/config.json
```

**Useful for:**
- Preventing accidental overwrites
- Copying to directories with existing names
- Safety when working with important files

---

### 8. No-Clobber Mode (Never Overwrite)

**Skip if destination exists:**
```bash
cp -n file.txt /destination/file.txt
```

**If destination exists:**
- File is NOT copied
- No error, no prompt
- Silent skip

**Real example:**
```bash
cp -n *.png ./images/
```

**Useful for:**
- Batch operations where duplicates are acceptable
- Scripts that shouldn't fail on existing files
- Safe bulk copies

---

### 9. Verbose Mode (Show Progress)

**See what's happening:**
```bash
cp -v file.txt /destination/
```

**Output:**
```
'document.txt' -> '/destination/document.txt'
```

**Multiple files:**
```bash
cp -v file1.txt file2.txt file3.txt ./backup/
```

**Output:**
```
'file1.txt' -> './backup/file1.txt'
'file2.txt' -> './backup/file2.txt'
'file3.txt' -> './backup/file3.txt'
```

**Directory copy:**
```bash
cp -vr project/ ./backup/
```

**Output:**
```
'project/' -> './backup/project/'
'project/file1.txt' -> './backup/project/file1.txt'
'project/file2.txt' -> './backup/project/file2.txt'
```

**Useful for:**
- Verifying copies completed correctly
- Debugging copy operations
- Script logging
- Understanding what cp is doing

---

### 10. Archive Mode (Full Preservation)

**Complete archive copy:**
```bash
cp -a source.txt /destination/source.txt
```

**What `-a` does (equivalent to `-d -p -r`):**
- `-d`: Preserve symlinks (don't dereference)
- `-p`: Preserve permissions, timestamps, ownership
- `-r`: Recursive (for directories)

**Real examples:**
```bash
cp -a ~/Documents/ ./backup/Documents/
cp -a /etc/app/ /opt/app/
cp -a project/ ~/Documents/work/project/
```

**Useful for:**
- Backups requiring full attribute preservation
- Moving system configurations
- Preserving file metadata
- Creating exact replicas

---

### 11. Preserve Attributes

**Preserve specific attributes:**
```bash
cp -p source.txt /destination/source.txt
```

**What `-p` preserves:**
- Mode (permissions)
- Ownership (user/group)
- Timestamps (modification, access)
- Extended attributes
- Context (SELinux)

**Preserve specific attributes (explicit):**
```bash
cp --preserve=mode,ownership,timestamps source.txt dest.txt
```

**Real examples:**
```bash
cp -p config.json /etc/app/config.json
cp -p script.sh /usr/local/bin/script.sh
```

**Useful for:**
- System file copies
- Executable files (preserving permissions)
- Files requiring specific ownership

---

### 12. Update Mode (Copy Only If Newer)

**Smart copy with `-u`:**
```bash
cp -u source.txt /destination/source.txt
```

**Behavior:**
- If destination doesn exist: **Copies** the file
- If destination exists AND is newer: **Skips** (doesn't copy)
- If destination exists AND is older: **Copies** (overwrites)

**Real examples:**
```bash
cp -u *.jpg ~/Pictures/         # Copy only newer images
cp -u document.pdf ./backup/    # Update backup if newer
cp -ur project/ ./backup/       # Recursive update
```

**Useful for:**
- Incremental backups
- Syncing files without unnecessary copies
- Updating configuration files
- Efficient file organization

---

### 13. Create Hard Links Instead of Copy

**Create hard link:**
```bash
cp -l file.txt /destination/file.txt
```

**What happens:**
- Creates hard link (not actual copy)
- Both files share same disk data
- Very fast (no data duplication)
- Changes to one affect both

**Real example:**
```bash
cp -l database.sql ./backup/database.sql
```

**Useful for:**
- Fast "copies" (actually links)
- Saving disk space
- Temporary backups

---

### 14. Create Symbolic Links Instead

**Create symlink:**
```bash
cp -s file.txt /destination/file.txt
```

**What happens:**
- Creates symbolic link (shortcut)
- Link points to original file
- Original must exist for link to work
- Different disk location possible

**Real example:**
```bash
cp -s /opt/app/config.json ./config.json
```

**Useful for:**
- Creating shortcuts
- Linking across filesystems
- Development environments

---

### 15. Backup Before Overwrite

**Auto-backup destination:**
```bash
cp -b file.txt /destination/file.txt
```

**If destination exists:**
- Original becomes: `file.txt~` (default suffix)
- New file copies in as `file.txt`

**Custom backup suffix:**
```bash
cp -b -S '.bak' file.txt /destination/file.txt
```

**Result:**
- Backup: `file.txt.bak`
- New: `file.txt`

**Real example:**
```bash
cp -b config.json /etc/app/config.json
```

**Useful for:**
- Safely replacing important files
- Configuration file updates
- Preventing accidental data loss

---

### 16. Copy with Parent Directory Creation

**Create parents automatically:**
```bash
cp --parents file.txt ./backup/2024/documents/
```

**What happens:**
- Creates `./backup/2024/documents/` if missing
- Copies file into final directory

**Real example:**
```bash
cp --contexts file.txt ./backup/2024/config/file.txt
```

**Useful for:**
- Complex directory structures
- Scripts creating nested paths
- Automated backup systems

---

### 17. Target Directory Option (-t)

**Explicit target syntax:**
```bash
cp -t /destination/ file.txt
```

**Alternative to:**
```bash
cp file.txt /destination/
```

**Multiple files:**
```bash
cp -t ./backup/ file1.txt file2.txt file3.txt
```

**Useful for:**
- Consistent syntax in scripts
- Readability when destination is complex
- Batch operations

---

### 18. Combine Multiple Options

**Verbose + Recursive + Preserve:**
```bash
cp -vpr project/ ./backup/
```

**Archive + Verbose:**
```bash
cp -av source/ ./backup/
```

**Update + Recursive + Verbose:**
```bash
cp -urv project/ ./backup/
```

**Safe options:**
```bash
cp -ibv file.txt ./dest/    # Interactive, backup, verbose
```

---

## Practical Real-World Examples

### Example 1: Creating Backups
```bash
cp config.json config_backup.json
cp -a ~/Documents/ ./backup/Documents_2024/
cp -u important.pdf ./backup/
```

### Example 2: Updating Configuration
```bash
cp -b config.json /etc/myapp/config.json
cp -p script.sh /usr/local/bin/script.sh
```

### Example 3: Copying Project Files
```bash
cp -r project/ ~/Documents/work/
cp src/main.js ./dist/main.js
cp -r assets/ ./build/assets/
```

### Example 4: Renaming Files for Consistency
```bash
cp IMG_001.jpg photo_001.jpg
cp IMG_002.jpg photo_002.jpg
cp IMG_003.jpg photo_003.jpg
```

### Example 5: Backup Important Files
```bash
cp -a database.sql ./backup/database.sql
cp -v important_doc.pdf ~/backup/
cp -r project_files/ ./backup/
```

### Example 6: Copy Log Files
```bash
cp -u /var/log/app.log ./logs/
cp *.log /var/log/archive/
cp -r logs/ ./backup/logs_2024/
```

### Example 7: Git File Management
```bash
cp old_file.js new_file.js
git add new_file.js
```

### Example 8: Batch Copy with Pattern
```bash
cp *.jpg ~/Pictures/2024/
cp *.py ./python_scripts/
cp config_* ./configs/
```

### Example 9: Deployment Files
```bash
cp -r dist/* /var/www/html/
cp build/app.js /opt/application/
cp -av release/ /deploy/
```

### Example 10: System File Copies
```bash
cp -p /etc/nginx/nginx.conf ./backup/nginx.conf
cp -a script.sh /usr/local/bin/
cp --preserve=mode,ownership config.json /etc/app/
```

---

## Common Pitfalls and Warnings

### ⚠️ 1. Copying Directories Without -r

**Error:**
```bash
cp folder/ ./dest/
# cp: omitting directory 'folder/'
```

**Solution:**
```bash
cp -r folder/ ./dest/
```

### ⚠️ 2. Overwriting Files Without Warning

**Dangerous:**
```bash
cp file.txt /destination/file.txt  # Overwrites if exists!
```

**Safe:**
```bash
cp -i file.txt /destination/file.txt  # Prompts first
cp -n file.txt /destination/file.txt  # Skips if exists
```

### ⚠️ 3. Copying to Non-Existent Directory

**Error:**
```bash
cp file.txt /nonexistent/dir/
# cp: cannot create regular file '/nonexistent/dir/file.txt': No such file or directory
```

**Solution:**
```bash
mkdir -p /nonexistent/dir/
cp file.txt /nonexistent/dir/
```

**Or use:**
```bash
cp --parents file.txt /nonexistent/dir/file.txt
```

### ⚠️ 4. Copying Same File to Same Location

**Unexpected:**
```bash
cp file.txt ./file.txt  # May cause issues
```

**Check first:**
```bash
ls -l file.txt ./file.txt  # Verify they're different
```

### ⚠️ 5. Permission Issues

**Error:**
```bash
cp file.txt /root/protected/
# cp: cannot create regular file '/root/protected/file.txt': Permission denied
```

**Solution:**
```bash
sudo cp file.txt /root/protected/
```

### ⚠️ 6. Copying Special Files

**Problems:**
```bash
cp /dev/sda ./backup/  # May copy device, not content
cp *.特殊字符 ./dest/   # Handle carefully
```

**Solution:**
```bash
ls -l  # Check what you're copying first
```

---

## Related Commands

| Command | Purpose | Difference from cp |
|---------|---------|-------------------|
| `mv` | Move files | Removes original, doesn't duplicate |
| `rm` | Remove files | Deletes files |
| `ln` | Create links | Creates reference only |
| `rsync` | Sync files | Advanced with verification |
| `tar` | Archive files | Compresses during copy |
| `dd` | Copy raw data | Low-level copying |
| `scp` | Copy remotely | Network copy |
| `find` | Search files | Find then copy with `-exec` |

### Comparison Examples:
```bash
# Move (original removed):
mv file.txt ./backup/

# Copy (original stays):
cp file.txt ./backup/

# Sync with verification:
rsync -av file.txt ./backup/

# Create link (no copy):
ln file.txt ./backup/file.txt

# Find and copy:
find . -name "*.log" -exec cp {} ./logs/ \;
```

---

## Best Practices

### ✅ 1. Use `-i` for Important Files
```bash
cp -i config.json /etc/app/  # Safe for critical files
```

### ✅ 2. Use `-v` for Verification
```bash
cp -v *.txt ./backup/  # See what copied
```

### ✅ 3. Use `-u` for Backups
```bash
cp -u document.pdf ./backup/  # Only update if newer
```

### ✅ 4. Use `-a` for Full Backups
```bash
cp -a ~/Documents/ ./backup/  # Preserve all attributes
```

### ✅ 5. Use `-r` for Directories
```bash
cp -r project/ ./backup/  # Essential for folders
```

### ✅ 6. Check Destination First
```bash
ls -l /destination/  # Verify before copying
```

### ✅ 7. Use `-b` for Config Updates
```bash
cp -b app.conf /etc/app/app.conf  # Auto-backup
```

### ✅ 8. Test with Wildcards Carefully
```bash
ls *.txt  # Check what matches first
cp *.txt ./backup/
```

---

## Advanced Tips

### Tip 1: Copy with find Command
```bash
find . -name "*.tmp" -exec cp {} ./temp/ \;
```

### Tip 2: Copy Based on Age
```bash
find . -mtime +30 -name "*.log" -exec cp {} ./old_logs/ \;
```

### Tip 3: Copy Multiple Files with Pattern
```bash
cp photo_*.jpg ./photos/2024/
```

### Tip 4: Copy to Timestamped Directory
```bash
cp file.txt ./backup/$(date +%Y%m%d)/
```

### Tip 5: Safe Copy Script
```bash
cp_safe() {
    if [ -f "$2" ]; then
        echo "Destination exists: $2"
        return 1
    fi
    cp "$1" "$2"
}
```

### Tip 6: Copy and Verify
```bash
cp file.txt ./backup/
cmp file.txt ./backup/file.txt  # Verify integrity
```

---

## Summary

The `cp` command is essential for:
- ✅ Copying files between directories
- ✅ Creating backup copies of files
- ✅ Copying entire directory structures (`-r`)
- ✅ Updating files safely with `-u`
- ✅ Creating backups automatically with `-b`
- ✅ Preventing overwrites with `-i` or `-n`
- ✅ Preserving all attributes with `-a`

**Remember:**
- Use `-i` for interactive (prompt before overwrite)
- Use `-n` for no-clobber (skip if exists)
- Use `-v` for verbose (see what's copying)
- Use `-u` for update (copy only if newer)
- Use `-r` for recursive (essential for directories)
- Use `-a` for archive (full preservation: `-d -p -r`)
- Use `-p` to preserve attributes (permissions, timestamps, ownership)
- Use `-b` for backup (auto-backup overwritten files)
- Use `-l` for hard links (fast, same disk)
- Use `-s` for symbolic links (shortcut, different disk)
- Original file ALWAYS stays (unlike `mv`)
- Always check permissions before copying to system directories

---

**Quick Reference Card:**
```bash
cp file.txt ./dest/           # Copy file
cp file.txt new_name.txt      # Copy + rename
cp file.txt ./dest/new.txt    # Copy to dir with new name
cp *.txt ./backup/            # Copy all .txt files
cp -r folder/ ./dest/         # Copy directory
cp -i file.txt ./dest/        # Safe (prompt)
cp -n file.txt ./dest/        # Skip if exists
cp -v file.txt ./dest/        # Show progress
cp -u file.txt ./dest/        # Update if newer
cp -a source/ ./backup/       # Archive (full preserve)
cp -p file.txt ./dest/        # Preserve attributes
cp -b file.txt ./dest/        # Auto-backup
cp -t ./dest/ file.txt        # Target directory
cp --parents file.txt path/   # Create parents
sudo cp file.txt /root/       # Copy with sudo
```
```
