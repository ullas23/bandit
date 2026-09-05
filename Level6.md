# Bandit Level 6 -> Level 7

## Terminal Session

```bash
# Show the current working directory
bandit6@bandit:~$ pwd
/home/bandit6

# List the contents of the home directory
bandit6@bandit:~$ ls

# Search the entire filesystem for a 33-byte file
# owned by bandit7 and belonging to the bandit6 group
# Suppress permission-denied errors
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password

# Read the password file
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit6

**Retrieved Password:** `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`

**Key Concept:** Use the `find` command to search the entire filesystem based on multiple file attributes. In this level, `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null` located the only 33-byte file owned by `bandit7` and belonging to the `bandit6` group. Redirecting errors to `/dev/null` suppressed permission-denied messages, and `cat` was then used to display the password.
