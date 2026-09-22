# Bandit Level 16 &rarr; Level 17

## Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range **31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

**Helpful note:** Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the **CONNECTED COMMANDS** section in the manpage.

## Terminal Session

### 1. Discovering Ports in the 31000–32000 Range and Identifying Listening Services.

`netstat -tln | grep :31` checks for TCP ports in the target range that are listening. It found ports 31960, 31046, and 31691, although the command only displayed IPv6 listeners.

```bash
bandit16@bandit:~$ netstat -tln | grep :31
netstat: no support for `AF INET (tcp)` on this system.
tcp6       0      0 :::31960                :::*                    LISTEN
tcp6       0      0 :::31046                :::*                    LISTEN
tcp6       0      0 :::31691                :::*                    LISTEN
```

`nmap -p 31000-32000 localhost` scans every TCP port from 31000 through 32000 on localhost and identifies which ports are open. This revealed five listening ports: 31046, 31518, 31691, 31790, and 31960.

```bash
bandit16@bandit:~$ nmap -p 31000-32000 localhost
Starting Nmap 7.98 ( https://nmap.org ) at 2026-09-22 05:56 +0000
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0037s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.10 seconds
```

`nmap -sV` performs service/version detection on the open ports.

```bash
bandit16@bandit:~$ nmap -sV -p 31000-32000 localhost
Starting Nmap 7.98 ( https://nmap.org ) at 2026-09-22 05:57 +0000
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00015s latency).
Other addresses for localhost (not scanned): ::1
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
```

The important result is that only ports **31518** and **31790** were identified as SSL/TLS services.

### 2. Connecting to the SSL/TLS servers to fetch the credential.

> [!NOTE]
> `openssl s_client -connect localhost:31518` connects to the SSL/TLS service on port 31518. The connection established successfully, but the normal OpenSSL output included `read R BLOCK` and a TLS `KEYUPDATE` message before closing. <br>
> ```bash
> read R BLOCK
> kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
> KEYUPDATE
> closed
> ```

> [!TIP]
> To make the interaction cleaner, use the -quiet option. This suppresses most of the SSL/TLS session details and leaves the actual application data visible.

`openssl s_client -connect localhost:31518 -quiet` establishes an SSL/TLS connection to port 31518. The service simply echoed the submitted password back, confirming that this was the SSL echo service rather than the credential server.

```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31518 -quiet
Connecting to 127.0.0.1
Cant use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
^C
```

`openssl s_client -connect localhost:31790 -quiet` connects to the second SSL/TLS service. After submitting the current password, the server responded with `Correct!` and returned the **bandit17 private SSH key**.

```bash
bandit16@bandit:~$ openssl s_client -connect localhost:31790 -quiet
Connecting to 127.0.0.1
Cant use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
Correct!
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
...
-----END OPENSSH PRIVATE KEY-----
```

### 3. Starting SSH session to bandit17.

`nano b17.private` was used to save the private key returned by port 31790.

`chmod 600 b17.private` restricts the key file so only owner can read/write, nobody else has permissions, which is required by SSH.

Finally, `ssh -i b17.private -p 2220` uses the recovered private key to authenticate as `bandit17`.

```bash
bandit16@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.

┌──(ullas23㉿KALI)-[~/Documents/Bandit]
└─$ nano b17.private

┌──(ullas23㉿KALI)-[~/Documents/Bandit]
└─$ chmod 600 b17.private

┌──(ullas23㉿KALI)-[~/Documents/Bandit]
└─$ ssh -i b17.private -p 2220 bandit17@bandit.labs.overthewire.org

...

bandit17@bandit:~$
```

**Successfully reaching the `bandit17` shell confirms that the Level 16 → Level 17 challenge is complete.**

## Level Summary

**Host:** `bandit.labs.overthewire.org`

**Port:** `2220`

**Username:** `bandit16`

**Retrieved Credential:** `bandit17` private SSH key

**Key Concept:** Port scanning, service/version detection, SSL/TLS connections, and SSH private-key authentication

**Commands Learnt:**
* `netstat -tln` – Lists TCP ports that are currently listening.
* `nmap -p` – Scans a specified port or range of ports to find open ports.
* `nmap -sV` – Detects the services and versions running on open ports.
* `openssl s_client -connect host:port -quiet` – Establishes an SSL/TLS connection to a specified host and port with minimal output.
* `chmod` – Changes the permissions of a file or directory.
* `ssh -i` – Connects to an SSH server using a specified private key file.
