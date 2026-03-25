# Interact with file and directory on linux by command
<img width="1168" height="784" alt="image" src="https://github.com/user-attachments/assets/b60c9053-70ac-4190-a50d-a8f097d335c4" />

## 1. Create new folder
```
mkdir my_folder/
mkdir -p path/to/deep/folder
```
The -p flag is a lifesaver; it creates all parent directories if they don't exist yet

## 2. Create new file
```
touch my_file_01.conf
```

## 3. Copy file to other folder
```
cp /home/my_folder/my_file_01.conf /home/my_folder/backup/
```

## 4. Copy folder to other folder
```
cp -r /home/my_folder /home/backup_folder
```
- The -r (recursive) flag is mandatory for copying folders.
- If backup_folder exists, the above commadn will copy folder my_folder to folder backup_folder => new directory is /home/backup_folder/my_folder/*
- If backup_folder does not exists, the above commadn will copy all files and folder in the my_folder folder to folder backup_folder => new directory is /home/backup_folder/*

## 5. Move/Rename
```
# Rename
mv old_name.txt new_name.txt

# Move
mv file.txt /tmp/
```

## 6. Find and replace content in file (The "Ctrl + H" Alternative)
```
sed -i 's/old_string/new_string/g' filename.txt
```
- -i: Stands for "in-place" (saves the changes to the file).
- s: Stands for "substitute."
- g: Stands for "global" (replaces all occurrences in a line, not just the first one).

## Advanced (Stream Editor)
```
# Multiple replacements in one command
sed -i -e 's/old1/new1/g' -e 's/old2/new2/g' filename.txt

# Use different delimiter for paths (easier to read)
# Hard to read (Standard):
sed -i 's/\/var\/www\/html/\/opt\/app\/data/g' config.js
# Easy to read (Using # or :):
sed -i 's#/var/www/html#/opt/app/data#g' config.js

# Insert a line to the beginning of the file
sed -i '1i your_new_line_content' filename.txt

# Append to the End of a file
sed -i '$a your_new_line_content' filename.txt
# OR use echo command
echo "your_new_line_content" >> filename.txt

# Delete all commented lines (start with #)
sed -i '/^#/d' server.conf

# Delete all empty lines
sed -i '/^$/d' server.conf
```
## 7. Directory Navigation
```
# Navigate to the parent directory of current directory
cd ..

# Navigate to the previous directory
cd -

# Navigate to the user's home directory
cd ~
# OR simply
cd 
```

## 8. Find folders, Files
```
# Find file by name (using Wildcards)
find /home -type f -name "my_file.txt"
find . -type f -name "project_*"

# Find with Case-Insensitivity (matches: My_Folder, MY_FOLDER, etc.)
find . -iname "my_folder"

# Find folder (directory) by name
find . -type d -name "my_folder"
find . -type d -iname "my_folder"

# Limit searching scope (Depth)
# (maxdepth 1 = current folder only | maxdepth 2 = current + 1 level below)
find . -maxdepth 2 -type d -name "my_folder"

# Find file with modified time
find /var/log/myapp -type f -mtime +30 -name "*.log"
# +30: Older than 30 days

# Find and delete file
find /var/log/myapp -type f -mtime +30 -name "*.log" -delete
# -delete: This is much faster than piping to rm
# Warning: Always run the command without -delete first to see what it would delete!
```

## 9. Quick Viewers (No Editing Needed)
```
# Dumps the whole file to your screen (good for short files).
cat filename.txt

# Opens the file in a scrollable view. Press q to exit. You can search inside less by typing / followed by your keyword
less  filename.txt

# Essential for DevOps! It follows a log file in real-time as it updates
tail -f filename.txt
```

## 10. File Permissions & Ownership (The "Properties" Alternative)
```
# View detailed info (Permissions, Owner, Size, Date)
ls -lh

# Change ownership (User:Group)
chown username:group_name my_file.conf

# Change permissions (r=4, w=2, x=1)
chmod 644 config.xml
chmod +x script.sh
```

## 11. Disk Space & Folder Size (The "Folder Info" Alternative)
```
# Check overall disk space on the server
df -h

# Check size of folders in current directory (1 level deep)
du -sh * --max-depth=1 | sort -h
# sort -h: Puts the biggest folders at the bottom so you see them last
```

# END



