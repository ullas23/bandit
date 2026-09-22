# Bandit Level 17 → Level 18

## Level Goal

There are 2 files in the home directory: **passwords.old** and **passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old** and **passwords.new**.

**NOTE:** If you have solved this level and see `Byebye!` when trying to log into bandit18, this is related to the next level, Bandit Level 18 → Level 19.

## Terminal Session

### 1. Connecting to the bandit17 account and locating the password files.

The private SSH key retrieved from the previous level can be used to authenticate as `bandit17`.

```bash
┌──(ullas23㉿KALI)-[~/Documents/Bandit]
└─$ ssh -i b17.private -p 2220 bandit17@bandit.labs.overthewire.org
bandit17@bandit:~$
```

`ls` lists the files in the current home directory. The two files required for this challenge are `passwords.old` and `passwords.new`.

```bash
bandit17@bandit:~$ ls
passwords.new  passwords.old
```

### 2. Comparing passwords.old and passwords.new.

`diff passwords.old passwords.new` compares the two files and displays the lines that are different. The `<` line belongs to `passwords.old`, while the `>` line belongs to `passwords.new`.

```bash
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
---
> OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

The output shows that line 42 was changed. Therefore, the password in `passwords.new` is:

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

`diff -u passwords.old passwords.new` displays the same difference using the unified-diff format, providing some surrounding context for the changed line.

```bash
bandit17@bandit:~$ diff -u passwords.old passwords.new
--- passwords.old       2026-06-24 14:58:52.315331770 +0000
+++ passwords.new       2026-06-24 14:58:52.323331835 +0000
@@ -39,7 +39,7 @@
 dCpvYCM0qdq9TrjpZj7YrflAUwF9GXvA
 6DtvOxp6oD5X4pmDv64fzsGHnwvpwP2m
 S1msSibMhCyxssqxe8a6dqIGcepeHwuu
-qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
+OQxXZjELndr90zuhOTDYBEomI0SZITXI
 M9PI7AAGrmH7gSFGnhXYDWFWXRbWZUqd
 DkEDNbP9brtv2ZcX0Ggk0ZnedqAYBuUd
 VNAHfTJr7rD8KwOJOS9loZRcYOt1QMu9
```

The `-` line represents the old value from `passwords.old`, while the `+` line represents the new value from `passwords.new`.

### 3. Testing the password on bandit18.

After retrieving the password, the `bandit17` session can be closed using `exit`.

```bash
bandit17@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

The retrieved password can then be used when connecting to `bandit18`.

```bash
┌──(ullas23㉿KALI)-[~/Documents/Bandit]
└─$ ssh bandit18@bandit.labs.overthewire.org -p 2220

Byebye !
Connection to bandit.labs.overthewire.org closed.
```

> [!NOTE]
> Seeing `Byebye!` does not mean that the password retrieved from `passwords.new` is incorrect. The `Byebye!` behavior is caused by the restrictions introduced in the next challenge, Bandit Level 18 → Level 19.

**Successfully identifying the only changed line and retrieving `OQxXZjELndr90zuhOTDYBEomI0SZITXI` confirms that the Level 17 → Level 18 challenge is complete.**

## Level Summary

**Host:** `bandit.labs.overthewire.org`

**Port:** `2220`

**Username:** `bandit17`

**Retrieved Password:** `OQxXZjELndr90zuhOTDYBEomI0SZITXI`

**Key Concept:** Comparing files with `diff` and identifying the only changed line

**Commands Learnt:**

- `diff` – Compares two files and displays the differences between them.
- `diff -u` – Displays differences using the unified-diff format.
