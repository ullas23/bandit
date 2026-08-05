OverTheWire: Bandit — Level 1 to Level 2
# Terminal Session
```bash
## Connect to the Level 1 target server
ssh bandit.labs.overthewire.org -p 2220 -l bandit1

## List the directory contents to find the target file 
bandit1@bandit:~$ ls
-

## Read the file named "-" using a relative path
bandit1@bandit:~$ cat ./-
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

## Close the session after capturing the password
bandit1@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

# Level Summary
### Host: bandit.labs.overthewire.org
### Port: 2220
### Username: bandit1
### Retrieved Password: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
### Key Concept: Using ./ allows cat to read a file named - without treating it as an input stream switch.
