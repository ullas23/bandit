# Bandit Level 12 → Level 13

## Level Goal

The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under `/tmp` in which you can work. Use `mkdir` with a hard to guess directory name. Or better, use the command `mktemp -d`. Then copy the datafile using `cp`, and rename it using `mv` (read the manpages!).

## Terminal Session

```bash
bandit12@bandit:~$ pwd
/home/bandit12

bandit12@bandit:~$ ls
data.txt

bandit12@bandit:~$ file -i data.txt
data.txt: text/plain; charset=us-ascii

bandit12@bandit:~$ cat data.txt
00000000: 1f8b 0808 a6f0 3b6a 0203 6461 7461 322e  ......;j..data2.
00000010: 6269 6e00 0144 02bb fd42 5a68 3931 4159  bin..D...BZh91AY
00000020: 2653 5904 ab91 e100 001c 7fff fffb bebf  &SY.............
00000030: f1fb dfbb be7f f57d fef5 5f8f ffcd b7b6  .......}.._.....
00000040: 19ff f6df af7f feae fff6 7fff 3001 3b6d  ............0.;m
00000050: 5b10 0000 001a 341a 34f5 000d 0068 0000  [.....4.4....h..
00000060: 0000 0683 2068 1ea0 3400 0d1e a034 19a8  .... h..4....4..
00000070: 0680 3d4d 00d0 69ea 69a6 0f54 41a0 00d1  ..=M..i.i..TA...
00000080: a034 d0c8 f506 8c86 8068 1a32 01a0 c40c  .4.......h.2....
00000090: 8323 40c8 0681 8803 4d32 1a34 0320 0000  .#@.....M2.4....
000000a0: 0d19 00d0 1a7a 834d 0ca6 8343 4000 00d1  .....z.M...C@...
000000b0: a006 87a8 0064 0003 41ea 321a 0321 91ea  .....d..A.2..!..
000000c0: 001a 3403 4686 81ea 0069 a680 0d3d 434d  ..4.F....i...=CM
000000d0: 0003 201e a687 21c0 488e 0290 095a 3e86  .. ...!.H....Z>.
000000e0: 15f5 36e7 cde1 c0a6 6618 63cd b8f0 63ef  ..6.....f.c...c.
000000f0: c79a d24a 84c8 a6ce 178f cb25 70ec 85a8  ..J.......%p... 
00000100: ca3e a695 c48f 63d0 116e 8bb2 4c01 11ee  .>....c..n..L...
00000110: e859 c127 9c43 5d46 adcd f083 1fd6 9c89  .Y.'.C]F........
00000120: f4cd 2dcb 4c94 133b 9845 6506 39e4 066c  ..-.L..;.Ee9..l
00000130: e84b 7292 86b9 83cb 4cc5 06b6 bbc2 0be3  .Kr.....L.......
00000140: 45f7 d0a2 f33d 5e21 e3ae 5636 d65c f20a  E....=^!..V6.\..
00000150: dd0a 527e 1bd2 d0c4 07d4 2905 cdc2 214d  ..R~......)...!M
00000160: cd24 464b 1b79 2165 218b a0e2 0c9c f1d3  .$FK.y!e!.......
00000170: 823d 6c2a 4acb 6c50 d11b a702 d33a 28c5  .=l*J.lP.....:(
00000180: 2df2 7d47 b3c4 3d41 1268 0e84 6280 1f1d  -.}G..=A.h..b...
00000190: a361 7bf7 1841 d56e 18e7 c416 fe1a 4a94  .a{..A.n......J.
000001a0: 6978 74a7 0b53 a10b 1fec 8221 bb20 871a  ixt..S.....!....
000001b0: 8f98 b993 459e 8e21 ca67 26bf f599 67e2  ....E..!.g&...g
000001c0: b74b 17ac ac63 0172 3ca0 005f e6e0 ca84  .K...c.r<.._....
000001d0: bcba 40aa aca8 0565 c111 1570 9e84 1127  ..@....e...p...'
000001e0: 8426 1a74 ca3c cf43 6100 7865 4a10 e1d7  .&.t.<.Ca.xeJ...
000001f0: 6d32 fd7e 8947 ec20 093b d503 ccf4 833c  m2.~.G. .;.....<
00000200: b6c7 1583 b688 4610 e191 244f e412 9ced  ......F...$O....
00000210: 27a7 71ac 6a6b ba1d 54e8 be4e 8fe1 744f  '.q.jk..T..N...O
00000220: b562 b142 33e9 fd09 194b 09de 54de 2de2  .b.B3....K..T.-.
00000230: 0934 7a39 638a 9941 4fe0 ea53 1103 4007  .4z9c..AO..S..@.
00000240: 52ea d2d6 00c3 6d4b c97a 2006 242f 4bb1  R.....mK.z .$/K.
00000250: 4003 fc5d c914 e142 4012 ae47 84df c445  @..]...B@..G...E
00000260: ad44 0200 00                             .D...
```

```bash
bandit12@bandit:~$ mktemp -d /tmp/TempXX
mktemp: too few Xs in template '/tmp/TempXX'

bandit12@bandit:~$ mktemp -d /tmp/TempXXX
/tmp/TempSe8

bandit12@bandit:~$ cp data.txt /tmp/TempSe8
bandit12@bandit:~$ cd /tmp/TempSe8
bandit12@bandit:/tmp/TempSe8$ ls
data.txt
```

The `data.txt` file is a hexdump, so the first step is to reconstruct the original binary file using `xxd -r`.

```bash
bandit12@bandit:/tmp/TempSe8$ xxd -r data.txt ogfile
bandit12@bandit:/tmp/TempSe8$ ls
data.txt  ogfile

bandit12@bandit:/tmp/TempSe8$ file -i ogfile
ogfile: application/gzip; charset=binary
```

The reconstructed file is identified as a gzip archive. Since `gunzip` relies on the `.gz` extension, rename it first.

```bash
bandit12@bandit:/tmp/TempSe8$ mv ogfile ogfile.gz
bandit12@bandit:/tmp/TempSe8$ gunzip ogfile.gz

bandit12@bandit:/tmp/TempSe8$ ls -la
total 8
drwx------   2 bandit12 bandit12   80 Sep  5 15:11 .
drwxrwx-wt 117 root     root     2860 Sep  5 15:11 ..
-rw-r-----   1 bandit12 bandit12 2641 Sep  5 15:08 data.txt
-rw-rw-r--   1 bandit12 bandit12  580 Sep  5 15:09 ogfile

bandit12@bandit:/tmp/TempSe8$ file -i ogfile
ogfile: application/x-bzip2; charset=binary
```

The next layer is bzip2.

```bash
bandit12@bandit:/tmp/TempSe8$ mv ogfile ogfile.bz2
bandit12@bandit:/tmp/TempSe8$ bunzip2 ogfile.bz2

bandit12@bandit:/tmp/TempSe8$ ls
data.txt  ogfile

bandit12@bandit:/tmp/TempSe8$ file -i ogfile
ogfile: application/gzip; charset=binary
```

The resulting file is gzip again.

```bash
bandit12@bandit:/tmp/TempSe8$ mv ogfile ogfile.gz
bandit12@bandit:/tmp/TempSe8$ gunzip ogfile.gz

bandit12@bandit:/tmp/TempSe8$ file -i ogfile
ogfile: application/x-tar; charset=binary
```

The file is now a tar archive. Extract it.

```bash
bandit12@bandit:/tmp/TempSe8$ tar -xf ogfile

bandit12@bandit:/tmp/TempSe8$ ls
data.txt  data5.bin  ogfile

bandit12@bandit:/tmp/TempSe8$ file -i data5.bin
data5.bin: application/x-tar; charset=binary

bandit12@bandit:/tmp/TempSe8$ tar -xf data5.bin

bandit12@bandit:/tmp/TempSe8$ ls
data.txt  data5.bin  data6.bin  ogfile

bandit12@bandit:/tmp/TempSe8$ file -i data6.bin
data6.bin: application/x-bzip2; charset=binary
```

The next layer is bzip2.

```bash
bandit12@bandit:/tmp/TempSe8$ mv data6.bin data6.bin.bz2
bandit12@bandit:/tmp/TempSe8$ bunzip2 data6.bin.bz2

bandit12@bandit:/tmp/TempSe8$ file -i data6.bin
data6.bin: application/x-tar; charset=binary

bandit12@bandit:/tmp/TempSe8$ tar -xf data6.bin

bandit12@bandit:/tmp/TempSe8$ ls
data.txt  data5.bin  data6.bin  data8.bin  ogfile

bandit12@bandit:/tmp/TempSe8$ file -i data8.bin
data8.bin: application/gzip; charset=binary
```

The final compressed layer is gzip.

```bash
bandit12@bandit:/tmp/TempSe8$ mv data8.bin data8.bin.gz
bandit12@bandit:/tmp/TempSe8$ gunzip data8.bin.gz

bandit12@bandit:/tmp/TempSe8$ file -i data8.bin
data8.bin: text/plain; charset=us-ascii

bandit12@bandit:/tmp/TempSe8$ cat data8.bin
The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

## Level Summary

**Host:** bandit.labs.overthewire.org

**Port:** 2220

**Username:** bandit12

**Retrieved Password:** `qQYQiHOBPR8zR61qxYqX45quvihF2uzk`

**Key Concept:** Reversing a hexdump and repeatedly identifying and decompressing nested gzip, bzip2, and tar layers.

**Commands Learnt:**

* `mktemp -d` — create a temporary directory with a randomized name
* `cp` — copy files
* `xxd -r` — reverse a hexdump back into its original binary form
* `file -i` — identify a file's MIME type and encoding
* `mv` — used for both **moving files** to a different location and **renaming files**, especially when a decompression utility requires a specific extension
* `gunzip` — decompress gzip files (.gz files)
* `bunzip2` — decompress bzip2 files (.bz2 files)
* `tar -xf` — extract tar archives
