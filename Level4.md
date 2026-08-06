# Bandit Level 4 -> Level 5

## Terminal Session

```bash
# Connect to the Level 4 target server
ssh bandit.labs.overthewire.org -p 2220 -l bandit4

# List the contents of the home directory
bandit4@bandit:~$ ls
inhere

# Enter the directory
bandit4@bandit:~$ cd inhere

# List all files
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09

# Attempting to read a file beginning with '-' without escaping it
bandit4@bandit:~/inhere$ cat -file07

error: unexpected argument '-f' found

  tip: to pass '-f' as a value, use '-- -f'

Usage: cat [OPTION]... [FILE]...

# Read the file correctly using '--' to indicate the end of options
bandit4@bandit:~/inhere$ cat -- "-file07"
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

# Exit after obtaining the password
bandit4@bandit:~/inhere$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit4

**Retrieved Password:** `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`

**Key Concept:** When a filename begins with a hyphen (`-`), many commands interpret it as a command-line option. Use `--` to mark the end of command options so that the filename is treated as a regular file. Alternatively, prefix the filename with `./` (e.g., `cat ./-file07`) to access it safely.
