# Bandit Level 3 -> Level 4

# Terminal Session

```bash
## Connect to the Level 3 target server
ssh bandit.labs.overthewire.org -p 2220 -l bandit3

## Enter the directory
bandit3@bandit:~$ ls
inhere

bandit3@bandit:~$ cd inhere

## Hidden files are not shown by default
bandit3@bandit:~/inhere$ ls
### (no output)

## Display all files, including hidden ones
bandit3@bandit:~/inhere$ ls -al
total 12
drwxr-xr-x 2 root    root    4096 Jun 24 14:59 .
drwxr-xr-x 3 root    root    4096 Jun 24 14:59 ..
-rw-r----- 1 bandit4 bandit3   33 Jun 24 14:59 ...Hiding-From-You

## (Optional) Check the file type
bandit3@bandit:~/inhere$ file ...Hiding-From-You
...Hiding-From-You: MGR bitmap, old format, 1-bit deep, 32-bit aligned

## Read the hidden file
bandit3@bandit:~/inhere$ less ...Hiding-From-You
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

## Exit after obtaining the password
bandit3@bandit:~/inhere$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

# Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit3

**Retrieved Password:** `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`

**Key Concept:** Hidden files (those beginning with `.`) are not displayed by the default `ls` command. Use `ls -a` or `ls -al` to reveal hidden files, then read them using commands such as `cat`, `less`, or `more`.
