# Bandit Level 7 -> Level 8

## Level Goal

The password for the next level is stored in the file `data.txt` next to the word `millionth`.

## Terminal Session

```bash
# List the contents of the home directory
bandit7@bandit:~$ ls
data.txt

# Check the exact size of data.txt in bytes
bandit7@bandit:~$ wc -c data.txt
4184396 data.txt

# Alternate method,
# List all files with detailed information and human-readable file sizes
bandit7@bandit:~$ ls -la
total 4108
drwxr-xr-x   2 root    root       4096 Jun 24 14:59 .
drwxr-xr-x 150 root    root       4096 Jun 24 15:02 ..
-rw-r--r--   1 root    root        220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root    root       3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root        807 Feb 13  2026 .profile
-rw-r-----   1 bandit8 bandit7 4184396 Jun 24 14:59 data.txt

# Search data.txt for the word "millionth"
bandit7@bandit:~$ grep 'millionth' data.txt
millionth       VR1ljMayciFxbnUokuQmJFw6QC9VKtub

# Extract only the second field (the password) using awk
bandit7@bandit:~$ awk '$1=="millionth" {print $2}' data.txt
VR1ljMayciFxbnUokuQmJFw6QC9VKtub

# Sort the contents of the file alphabetically
bandit7@bandit:~$ sort data.txt

# Remove duplicate consecutive lines
bandit7@bandit:~$ uniq data.txt

# Sort the file and remove duplicates at the same time
bandit7@bandit:~$ sort -u data.txt
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit7

**Retrieved Password:** `VR1ljMayciFxbnUokuQmJFw6QC9VKtub`

**Key Concept:** Use `grep` to search a large text file for a specific word. In this level, `grep 'millionth' data.txt` located the line containing the password. `awk '$1=="millionth" {print $2}' data.txt` can be used to extract only the password from the second field.

**Additional Commands Learned:**

- `wc -c data.txt` — Displays the exact file size in bytes.
- `grep` — Searches for matching text within a file.
- `awk` — Processes text by fields and can extract specific columns.
- `sort data.txt` — Sorts the lines of a file.
- `uniq data.txt` — Removes consecutive duplicate lines.
- `sort -u data.txt` — Sorts the lines and removes duplicates in one command.
