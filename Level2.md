Bandit Level 2 -> Level 3
# Terminal Session
```bash
# Connect to the Level 1 target server
ssh bandit.labs.overthewire.org -p 2220 -l bandit2

# List the directory contents to find the target file
bandit2@bandit:~$ ls
--spaces in this filename--

# Read the file named "--spaces in this filename--" using a relative path
bandit2@bandit:~$ cat -- "--spaces in this filename--"
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

# Close the session after capturing the password
bandit2@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```
# Level Summary
Host: bandit.labs.overthewire.org

Port: 2220User

name: bandit2

Retrieved Password: **7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME**

Key Concept: Using cat -- "file name" or cat "./file name" to read files with spaces and special chars in the name.
