# Bandit Level 15 -> Level 16

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost using SSL/TLS encryption**.

## Terminal Session

```bash
#To check for command usage guides, I checked the manuals of openssl and s_client
bandit15@bandit:~$ man openssl
bandit15@bandit:~$ man s_client
bandit15@bandit:~$ openssl s_client -help
```

The **`openssl`** command is the **`"Swiss Army knife"`** of digital security and cryptography.  It is a massive utility used to handle **encryption**, **certificates**, and **network testing**.

`openssl s_client` is an SSL/TLS client that can be used to establish a secure connection to a server.
The `-connect` option is used to specify the host and port to connect to, in `host:port` format.

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
Connecting to 127.0.0.1
CONNECTED(00000003)
Cant use SSL_get_servername
depth=0 CN=SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=SnakeOil
verify return:1
---
Certificate chain
 0 s:CN=SnakeOil
   i:CN=SnakeOil
   a:PKEY: RSA, 4096 (bit); sigalg: sha256WithRSAEncryption
   v:NotBefore: Jun 10 03:59:50 2024 GMT; NotAfter: Jun  8 03:59:50 2034 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
subject=CN=SnakeOil
issuer=CN=SnakeOil
---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: rsa_pss_rsae_sha256
Negotiated TLS1.3 group: X25519MLKEM768
---
SSL handshake has read 3191 bytes and written 1613 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Protocol: TLSv1.3
Server public key is 4096 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
```

The connection was successfully established using TLS. The `self-signed certificate` warning does not prevent the connection from working because the challenge server uses a self-signed certificate.

The important part is that the connection is now open and waiting for input. I submitted the current `bandit15` password:

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

The server responded:

```bash
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

The password for `bandit16` is:

```text
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit15

**Retrieved Password:** `kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V`

**Key Concept:** Connecting to a localhost service using SSL/TLS with `openssl s_client` and submitting the current password.

**Commands Learnt:**

* `man s_client` — opens the manual page for `s_client`.
* `openssl s_client -help` — displays the available options for the OpenSSL SSL/TLS client.
* `openssl s_client -connect host:port` — establishes an SSL/TLS connection to the specified host and port.
* `-connect` — specifies the TCP host and port in `host:port` format.
* `openssl s_client` — provides an interactive SSL/TLS client for communicating with secure services.
