

## 1. Scanning

- `nmap -A -T4 <IP>` — note open ports (HTTP/80).
    
- Browse to `http://<IP>/`.
    

## 2. Web triage

- Open `/login.html`.
    
- View page source → saw sus files

## 3. Static analysis (client-side)

- Found JS auth: username `h3ck3rBoi`, password is reverse of `54321@terceSrepuS` → **password** = `SuperSecret@12345`.
    
- JS builds a file path:  
    `xhttp.open("GET", "RandomLo0o0o0o0o0o0o0o0o0o0gpath12345_Flag_"+a.value+"_"+b.value+".txt", true);`
    

## 4. Craft request (Burp Repeater)

- URL-encode unsafe chars (e.g., `@` → `%40`).
    
- Repeater-ready request (exact — include blank line after headers):
    

```
GET /RandomLo0o0o0o0o0o0o0o0o0o0gpath12345_Flag_h3ck3rBoi_SuperSecret%4012345.txt HTTP/1.1
Host: 10.201.59.222
User-Agent: Mozilla/5.0
Accept: text/html
Referer: http://10.201.59.222/login.html
Connection: close

```

- Paste in Repeater → **SEND**.
    



## 5. Successful response

- The file contents returned the flag:  
    `flag{edb0be532c540b1a150c3a7e85d2466e}`
    


