### 1. **nmap**

- Tool to scan networks and find open ports/services.
    
- Example:
    
    `nmap -p- <IP>`
    
    → shows all open ports.
    
- Helps find where the website/app is running.
    

---

### 2. **support.websitename (URL subdomains)**

- Websites can have **subdomains** like:
    
    - `support.website.com`
        
    - `blog.website.com`
        
- Hackers check these because sometimes they are forgotten or misconfigured → possible **subdomain takeover**.
    

---

### 3. **/etc/hosts**

- File in Linux that maps IP addresses to domain names.
    
- You can add custom entries to “fake” a DNS record.
    
- Example:
    
    `sudo nano /etc/hosts`
    
    Add:
    
    `10.10.10.10 support.website.com`
    
    → Now typing `support.website.com` in browser will go to `10.10.10.10`.