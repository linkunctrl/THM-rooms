1. **Finding specific files in root**
    
    `find / -type f \( -name 8V2L -o -name bny0 -o -name ... \) 2>/dev/null`
    
    - `find /` → start searching from the root (`/`) directory.
        
    - `-type f` → only look for **files** (not directories).
        
    - `\( ... -o ... \)` → list of file names to match (`-o` = OR).
        
    - `2>/dev/null` → hides **error messages** (like "Permission denied") by redirecting errors (file descriptor `2`) to `/dev/null` (a “black hole” for unwanted output).  
        ✅ Result: Prints the path of files that match the names.
        

---

2. **Finding which file contains an IP address**
    
    `find / -type f \( -name ... \) -exec grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' {} + 2>/dev/null`
    
    - `-exec grep ... {} +` → run `grep` on the files found.
        
    - `-Eo` → use extended regex (`-E`) and only print the match itself (`-o`).
        
    - Regex: `'([0-9]{1,3}\.){3}[0-9]{1,3}'` → looks for IPv4 addresses.  
        ✅ Result: Prints IPs found inside those files.
        

---

3. **Finding file with exact number of lines**
    
    `find / -type f \( -name ... \) -exec wc -l {} + 2>/dev/null`
    
    - `wc -l` → counts the **number of lines** in a file.
        
    - Output format:
        
        `230 /path/to/file`
        
    
    ✅ You can check which file has exactly 230 lines.
    

---

4. **Finding file by owner (UID)**
    
    `find / -type f \( -name ... \) -uid 502 2>/dev/null`
    
    - `-uid 502` → only show files owned by user with ID `502`.  
        ✅ Useful when the question asks: "Which file belongs to user X?"
        

---

### 🔑 Key Takeaway

- You always:
    
    1. **Locate the file(s)** with `find / -type f -name ...`.
        
    2. **Apply a command** (`grep`, `wc`, `sha1sum`, etc.) using `-exec`.
        
    3. **Filter/Check output** to match what the question asks (IP, hash, line count, UID, etc.).
        
- `2>/dev/null` is important because without it, the screen will fill with **permission denied errors** from scanning system directories.