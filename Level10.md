# Bandit Level 10 -> Level 11

## Level Goal

The password for the next level is stored in the file **data.txt**, which contains Base64 encoded data.

## Terminal Session

```bash
# List the contents of the home directory
bandit10@bandit:~$ ls
data.txt

# Determine the type of the file
bandit10@bandit:~$ file data.txt
data.txt: ASCII text

# Check the size of the file in bytes
bandit10@bandit:~$ wc -c data.txt
69 data.txt

# Display the Base64 encoded contents
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIHBZZk9ZNkh3VXNEajVyTDlVdnloVTdNQ212OHZONVJvCg==

# Decode the Base64 data
bandit10@bandit:~$ base64 -d data.txt
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit10

**Retrieved Password:** `pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro`

**Key Concept:** The `file` command showed that `data.txt` contains ASCII text, and the contents were Base64 encoded. The `base64 -d` command was used to decode the contents and reveal the password. Base64 is an encoding scheme, not encryption, so it can be reversed directly when the encoded data is available.

**Commands Learnt:**
- `base64 -d data.txt` — Decodes Base64 encoded data.
- `base64 --decode data.txt` — Long-form equivalent of `base64 -d`.
