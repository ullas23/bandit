# Bandit Level 8 -> Level 9

## Level Goal

The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once.

## Terminal Session

```bash
# List the contents of the home directory
bandit8@bandit:~$ ls
data.txt

# List files with detailed information and check the size of data.txt
bandit8@bandit:~$ ls -la
total 56
drwxr-xr-x   2 root    root     4096 Jun 24 14:59 .
drwxr-xr-x 150 root    root     4096 Jun 24 15:02 ..
-rw-r--r--   1 root    root      220 Feb 13  2026 .bash_logout
-rw-r--r--   1 root    root     3851 Jun 24 14:50 .bashrc
-rw-r--r--   1 root    root      807 Feb 13  2026 .profile
-rw-r-----   1 bandit9 bandit8 33033 Jun 24 14:59 data.txt

# Sort the contents and count how many times each line occurs
bandit8@bandit:~$ sort data.txt | uniq -c
     10 0LTDNpAmqqfuE0FlE0ksGf6c0Kraspzs
     10 1cKKjk7M0Pl2cPUbYgc9W4307bYC0ohF
     10 1PesxCa7cihwvCvzBeKAcjKkjUwp7i2z
     10 1QDbI0z3b488UD7pbhxxzAscVKVGJIqi
     ...
      1 EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
     ...
     10 ZpnAurXvto4z1V8ySf59BjY2Ieq2xa7y

# Find the only line that occurs exactly once
bandit8@bandit:~$ sort data.txt | uniq -u
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit8

**Retrieved Password:** `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl`

**Key Concept:** Use `sort` and `uniq` together to identify lines based on their frequency. `sort data.txt | uniq -c` sorts the file and displays the number of occurrences of each line. The `uniq -u` option then displays only lines that occur exactly once. Since the challenge states that the password is the only line appearing once, `sort data.txt | uniq -u` directly reveals the password.

**Additional Commands Learned:**

- `sort data.txt` — Sorts the lines of a file.
- `uniq data.txt` — Removes consecutive duplicate lines.
- `uniq -c` — Counts how many times each line occurs.
- `uniq -d` — Displays only duplicated lines.
- `uniq -u` — Displays only lines that occur exactly once.
- `sort -u data.txt` — Sorts the file and removes duplicate lines, but does **not** identify lines occurring only once.
