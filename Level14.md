# Bandit Level 14 -> Level 15

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## Terminal Session

I first tried to identify the service running on port `30000` using `ss`, `lsof`, `nmap`, and `netstat`. I couldn't find the exact process because the service was hosted by another user and normal users cannot see services run by other users without root privileges.

```bash
bandit14@bandit:~$ ss -tulpn | grep :30000

#The command returned nothing. ss -tulpn is used to display listening TCP/UDP sockets
#and the processes associated with them.

bandit14@bandit:~$ lsof -i :30000

#This also returned nothing. lsof -i can be used to identify processes using a particular network port.

bandit14@bandit:~$ nmap -sV -p 30000 localhost
Starting Nmap 7.98 (https://nmap.org) at 2026-09-06 15:31 +0000
^C

bandit14@bandit:~$ nmap -Pn -p 30000 localhost
Starting Nmap 7.98 (https://nmap.org) at 2026-09-06 15:31 +0000
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000017s latency).
Other addresses for localhost (not scanned): ::1
PORT      STATE SERVICE
30000/tcp open  ndmps
Nmap done: 1 IP address (1 host up) scanned in 0.05s

#nmap -Pn -p 30000 localhost confirmed that port 30000 is open on localhost.
#-Pn skips host discovery and -p specifies the port to scan.

bandit14@bandit:~$ netstat -tulpn | grep :30000
(No info could be read for "-p": geteuid()=11014 but you should be root.)
netstat: no support for `AF INET (tcp)` on this system.

#netstat could not provide the process information because the current user does not have root privileges.
#Since the service is running under another user, its process information cannot be viewed by bandit14.
```

I then directly connected to port `30000` using `nc`. With `nc -v`, I confirmed that the connection was successful and submitted the current password: `aaWecNkG4FhxJQxz07uiwzVP6bJiYS65`

```bash
bandit14@bandit:~$ nc localhost 30000
^C

#By default, Netcat is completely silent. If you don't use -v (Verbose),
#Netcat connects to the port and just sits there with a blinking cursor.
#It won't tell you if the connection was successful, if it failed, or if it timed out.

bandit14@bandit:~$ nc -v localhost 30000
Connection to localhost (127.0.0.1) 30000 port [tcp/*] succeeded!
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
^C

#I also verified the same process using `telnet`, which returned the same password.

bandit14@bandit:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
Connection closed by foreign host.
```

Both the services, `nc` and `telnet` responded with:

```text
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit14

**Retrieved Password:** `pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7`

**Key Concept:** Connecting to a TCP service running on localhost and submitting the current password to retrieve the next password.

**Commands Learnt:**

* `ss -tulpn` — displays listening TCP/UDP sockets and associated processes.
* `lsof -i :30000` — checks network connections associated with port `30000`.
* `nmap -sV -p 30000 localhost` — scans port `30000` and attempts to identify the service.
* `nmap -Pn -p 30000 localhost` — scans port `30000` without performing host discovery.
* `netstat -tulpn` — displays network connections and listening ports.
* `nc localhost 30000` — connects to the TCP service using Netcat.
* `nc -v localhost 30000` — connects using Netcat verbose mode.
* `telnet localhost 30000` — connects to the TCP service using Telnet.
