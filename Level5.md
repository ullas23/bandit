# Bandit Level 5 -> Level 6

## Terminal Session

```bash
# Connect to the Level 5 target server
ssh bandit.labs.overthewire.org -p 2220 -l bandit5

# List the contents of the home directory
bandit5@bandit:~$ ls
inhere

# Enter the target directory
bandit5@bandit:~$ cd inhere

# View the directory structure
bandit5@bandit:~/inhere$ ls -al
total 88
drwxr-x--- 22 root bandit5 4096 Jun 24 14:59 .
drwxr-xr-x  3 root root    4096 Jun 24 14:59 ..
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere00
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere01
...
drwxr-x---  2 root bandit5 4096 Jun 24 14:59 maybehere19

# Search recursively for a regular file that is exactly 1033 bytes
bandit5@bandit:~/inhere$ find . -type f -size 1033c
./maybehere07/.file2

# Verify that the file is human-readable
bandit5@bandit:~/inhere$ file ./maybehere07/.file2
./maybehere07/.file2: ASCII text, with very long lines (1000)

# Read the contents of the file
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

# Exit after obtaining the password
bandit5@bandit:~/inhere$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit5

**Retrieved Password:** `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`

**Key Concept:** Use the `find` command to search recursively based on specific file attributes. In this level, `find . -type f -size 1033c` located the only regular file that matched the required size. The `file` command was then used to verify it was human-readable (ASCII text), and `cat` displayed the password.
