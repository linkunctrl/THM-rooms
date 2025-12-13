- **Hydra (FTP password guessing)** — a network login cracker that automates credential guessing against services (use with a username list and a wordlist to test FTP logins);
    
- **Binwalk** — firmware and binary analysis tool that scans files for embedded files, compressed data, and signatures so you can extract and inspect components of firmware images;
    
- **John (John the Ripper)** — password-hash cracker for offline cracking of hashed passwords (feed it hashes and wordlists/rules to attempt recovery);
    
- **7z (7-Zip)** — file archiver/extractor that opens, tests, and can brute-force or try passwords on compressed archives (use it to list/extract archive contents or attempt password recovery with a wordlist tool);
    
- **Steghide** — steganography utility to hide or extract data inside images/audio using a passphrase (attempt extraction when you suspect hidden data with the correct passphrase);
    
- **Google for CVE finding** — use targeted search queries and vendor/security sites (e.g., “CVE <product> <version>”, vendor advisories, NVD) to find known vulnerabilities and patch details;
    
**Payload I used — `sudo -u#-1 /bin/bash`** — attempts to run a shell as UID `-1` (which some systems treat as UID `65535` or map to root), commonly seen in privilege-escalation/CTF contexts; treat carefully and only test on authorized targets.