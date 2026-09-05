# Bandit Level 9 -> Level 10

## Level Goal

The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several `=` characters.

## Terminal Session

```bash
# List the contents of the home directory
bandit9@bandit:~$ ls
data.txt

# Determine the type of the file
bandit9@bandit:~$ file data.txt
data.txt: data

# Check the MIME type of the file
bandit9@bandit:~$ file -i data.txt
data.txt: application/octet-stream; charset=binary

# Extract human-readable strings from the binary data
bandit9@bandit:~$ strings data.txt
v 9m
~.[o
7cb'
?+APs
qDa%;
DpxVr^>
========== the
...
```
```bash
# Search the extracted strings for lines containing "="
bandit9@bandit:~$ strings data.txt | grep '='
========== the
[==p+
=zW}
========== password
Y========== is
k8c=
yo=-
=A@.
.=O],
=l"C"m
j=9$
========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
'=5G
```
```text
# Therefore, the password is B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit9

**Retrieved Password:** `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG`

**Key Concept:** The `file` command identified `data.txt` as generic binary data, so `strings` was used to extract the human-readable portions of the file. Since the level specifies that the password is one of the human-readable strings preceded by several `=` characters, `strings data.txt | grep '='` filters the output to strings containing `=`. Among the results, `========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG` matches the challenge description and reveals the password.

**Additional Commands Learnt:**

- `file data.txt` — Determines the type of a file.
- `file -i data.txt` — Displays the MIME type and character encoding.
- `strings data.txt` — Extracts printable human-readable strings from binary data.
- `grep '='` — Searches input for lines containing the specified character or pattern.
- `strings data.txt | grep '='` — Extracts human-readable strings and filters them for strings containing `=`.
