# OverTheWire: Bandit Wargame Write-up

**Author:** Ghazal Dib  
**Platform:** OverTheWire — Bandit  
**Levels Completed:** 0 → 15  
**Focus:** Linux fundamentals, file manipulation, SSH, encoding, networking

---

## Level 0 → 1

**Connection:**
```
ssh bandit0@bandit.labs.overthewire.org -p 2220
password: bandit0
```

**Solution:**
```bash
ls
cat readme
```

**What I learned:** Basic SSH connection and reading files with `cat`.

---

## Level 1 → 2

**Connection:**
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
cat ./-
# Alternative:
cat -- -
```

**What I learned:** When a filename starts with `-`, the terminal treats it as a flag/argument. Using `./` tells the terminal it's a file path, not an argument.

---

## Level 2 → 3

**Connection:**
```
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
cat "spaces in this filename"
```

**What I learned:** Filenames with spaces must be wrapped in quotes, otherwise the terminal treats each word as a separate argument.

---

## Level 3 → 4

**Connection:**
```
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
ls -la
cd inhere
cat ...Hiding-From-You
```

**What I learned:** Hidden files in Linux start with `.` — using `ls -la` reveals all hidden files including ones with unusual names.

---

## Level 4 → 5

**Connection:**
```
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
file -- *
```

**What I learned:** The `file` command identifies the type of each file. We search for human-readable (ASCII text) files because the password won't be in binary files.

---

## Level 5 → 6

**Connection:**
```
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
find . -type f -size 1033c ! -executable
```

**What I learned:** `find` can filter files by size (`-size 1033c` = 1033 bytes) and exclude executable files (`! -executable`). Powerful for locating specific files among many.

---

## Level 6 → 7

**Connection:**
```
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

**What I learned:** Searching the entire filesystem (`/`) by owner, group, and size. `2>/dev/null` hides permission errors to clean up the output.

---

## Level 7 → 8

**Connection:**
```
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
grep millionth data.txt
```

**What I learned:** `grep` searches for a specific string inside a file — essential for finding data in large files quickly.

---

## Level 8 → 9

**Connection:**
```
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
sort data.txt | uniq -u
```

**What I learned:** `sort` organizes lines alphabetically, then `uniq -u` shows only lines that appear exactly once. Piping commands together is a core Linux skill.

---

## Level 9 → 10

**Connection:**
```
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
strings data.txt | grep "===="
```

**What I learned:** `strings` extracts human-readable text from binary files. Combined with `grep`, we can find specific patterns inside any file.

---

## Level 10 → 11

**Connection:**
```
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
base64 -d data.txt
```

**What I learned:** Base64 is an encoding method (not encryption). The `-d` flag decodes it back to plain text. Commonly used in web and security contexts.

---

## Level 11 → 12

**Connection:**
```
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

**What I learned:** ROT13 is a simple Caesar cipher that shifts letters by 13 positions. The `tr` command translates characters — useful for basic decoding.

---

## Level 12 → 13

**Connection:**
```
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
mktemp -d
cd /tmp/tmp.CwuXHUWdeR
cp ~/data.txt .
xxd -r data.txt > file
file file
# Then identify and decompress repeatedly:
mv file file.gz && gunzip file.gz
# or
mv file file.bz2 && bunzip2 file.bz2
# or
mv file file.tar && tar -xf file.tar
```

**What I learned:** A hexdump can be reversed with `xxd -r`. Files can be compressed multiple times with different formats (gzip, bzip2, tar). Always use `file` to identify the type before decompressing.

---

## Level 13 → 14

**Connection:**
```
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
# Copy content of sshkey.private
# Logout from bandit13, then:
nano sshkey.private   # paste the key
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit14
```

**What I learned:** SSH key authentication — more secure than passwords. `chmod 600` sets the key to owner-read-only, which SSH requires for security.

---

## Level 14 → 15

**Connection:**
```
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
nc localhost 30000
# Submit current password
```

**What I learned:** `nc` (netcat) is a networking tool for sending/receiving data over TCP connections. Essential tool for security testing and CTFs.

---

## Level 15 → 16

**Connection:**
```
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

**Solution:**
```bash
openssl s_client -connect localhost:30001 -quiet
# Submit current password
```

**What I learned:** OpenSSL can establish encrypted SSL/TLS connections. `-quiet` reduces verbose output. Understanding SSL/TLS is critical for cybersecurity work.

---

## Skills Demonstrated

| Skill | Levels |
|---|---|
| SSH connection and key authentication | 0, 13 |
| Linux file navigation and hidden files | 0, 3 |
| Special filename handling | 1, 2 |
| File type identification | 4, 12 |
| Advanced file search with find | 5, 6 |
| Text searching with grep | 7, 9 |
| Piping and chaining commands | 8, 9 |
| Encoding/Decoding — Base64, ROT13 | 10, 11 |
| File compression formats | 12 |
| Networking — Netcat, OpenSSL | 14, 15 |

---

*This write-up is part of my cybersecurity learning journey.*  
*Next: TryHackMe SOC Level 1 Path*
*
