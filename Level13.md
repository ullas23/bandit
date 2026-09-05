# Bandit Level 13 -> Level 14

## Level Goal

The password for the next level is stored in `/etc/bandit_pass/bandit14` and can only be read by user `bandit14`. For this level, you don't get the next password directly, but you get a private SSH key that can be used to log into the next level.

## Terminal Session

```bash
bandit13@bandit:~$ ls
HINT  sshkey.private

bandit13@bandit:~$ realpath sshkey.private
/home/bandit13/sshkey.private
```

The `sshkey.private` file is an OpenSSH private key. It is used to authenticate as `bandit14` without entering the bandit14 password.

First, exit the Bandit server and return to the local Kali machine.

```bash
bandit13@bandit:~$ exit
```

From Kali, copy the private key from the Bandit server:

`scp` — securely copies files across Remote and Local hosts.

```bash
┌──(ullas23㉿KALI)-[~/Downloads]
└─$ scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private ~/Downloads/
```

Enter the `bandit13` password when prompted.

The key is copied successfully:

```bash
sshkey.private                                          100% 2602     5.9KB/s   00:00
```

Check the file permissions:

```bash
┌──(ullas23㉿KALI)-[~/Downloads]
└─$ ls -l ~/Downloads/sshkey.private
-rw-r----- 1 ullas23 ullas23 2602 Sep  6 00:40 /home/ullas23/Downloads/sshkey.private
```

SSH private keys should have restrictive permissions, so change them to read/write only for the owner:

```bash
┌──(ullas23㉿KALI)-[~/Downloads]
└─$ chmod 600 sshkey.private
```

Verify:

```bash
┌──(ullas23㉿KALI)-[~/Downloads]
└─$ ls -l ~/Downloads/sshkey.private
-rw------- 1 ullas23 ullas23 2602 Sep  6 00:40 /home/ullas23/Downloads/sshkey.private
```

Now use the private key to log in as `bandit14`:

```bash
┌──(ullas23㉿KALI)-[~/Downloads]
└─$ ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

After successfully logging in:

```bash
bandit14@bandit:~$ cd /etc/bandit_pass
bandit14@bandit:/etc/bandit_pass$ ls -la
```

The password files are owned individually by their corresponding users:

```text
-r--------   1 bandit13 bandit13 33 Jun 24 14:58 bandit13
-r--------   1 bandit14 bandit14 33 Jun 24 14:58 bandit14
-r--------   1 bandit15 bandit15 33 Jun 24 14:58 bandit15
```

Check the path permissions:

```bash
bandit14@bandit:/etc/bandit_pass$ namei -l /etc/bandit_pass/bandit14
```

Output:

```bash
f: /etc/bandit_pass/bandit14
drwxr-xr-x root     root     /
drwxr-xr-x root     root     etc
drwxr-xr-x root     root     bandit_pass
-r-------- bandit14 bandit14 bandit14
```

The final file has:

```text
-r--------
```

which means only the owner has read permission. Since we are now logged in as `bandit14`, we can read it:

```bash
bandit14@bandit:/etc/bandit_pass$ cat bandit14
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit13

**Retrieved Password:** `aaWecNkG4FhxJQxz07uiwzVP6bJiYS65`

**Key Concept:** SSH public/private key authentication

**Commands Learnt:**

* `realpath` — displays the absolute path of a file.
* `scp -P 2220` — securely copies files over SSH using a specified port.
* `chmod 600` — gives the file owner read/write permissions while removing permissions for group and others.
* `ssh -i keyfile` — uses a specified private key for SSH authentication.
* `namei -l` — displays permissions for every component of a file path.
