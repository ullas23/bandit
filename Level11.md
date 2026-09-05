# Bandit Level 11 → Level 12

## Level Goal

The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

## Terminal Session

```bash
bandit11@bandit:~$ ls
data.txt

bandit11@bandit:~$ file -i -b data.txt
text/plain; charset=us-ascii

bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf TEBbmJCB8DlA0zTewHxVQ0JPLxMvDkeA

bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

```

The text is encoded using **ROT13**, where each letter is shifted 13 positions through the alphabet.

The `tr` command performs the ROT13 transformation:

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

* `A-Z` → uppercase letters
* `a-z` → lowercase letters
* `N-ZA-M` → uppercase ROT13 mapping
* `n-za-m` → lowercase ROT13 mapping

The decoded output reveals the password:

```text
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit11

**Retrieved Password:** `GROozWPO8QyN0mGrjUkID0WCYkZiQxrN`

**Key Concept:** ROT13 character substitution

**Commands Learnt:**

* `file -i -b` — identify a file's MIME type and character encoding
* `tr` — translate or substitute characters
* `tr 'A-Za-z' 'N-ZA-Mn-za-m'` — perform ROT13 decoding
