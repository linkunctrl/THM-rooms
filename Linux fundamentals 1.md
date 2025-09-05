### `echo`

- Prints text/variables to the terminal.
    
- **Example:** `echo hello` → prints _hello_
    
- **Parameters:**
    
    - `-n` → no new line
        
    - `-e` → enable escape characters (e.g. `\n`, `\t`)
        

---

### `whoami`

- Shows the current logged-in user.
    
- **Example:** `whoami` → outputs _root_ or _user_
    

---

### `ls`

- Lists files and directories in current folder.
    
- **Parameters:**
    
    - `-l` → long format (permissions, size, date)
        
    - `-a` → show hidden files (`.` prefix)
        
    - `-h` → human-readable sizes (e.g. KB, MB)
        

---

### `cd`

- Change directory.
    
- **Examples:**
    
    - `cd /home/user` → go to path
        
    - `cd ..` → go up one folder
        
    - `cd ~` → go to home directory
        

---

### `cat`

- Displays content of a file.
    
- **Examples:**
    
    - `cat file.txt` → show file contents
        
    - `cat file1 file2` → show multiple files together
        

---

### `pwd`

- Prints the current working directory (your location).
    
- **Example:** `pwd` → `/home/user/Desktop`
    

---

### `find`

- Searches for files/directories by name, type, or size.
    
- **Examples:**
    
    - `find / -name file.txt` → search by name
        
    - `find . -type d` → find directories in current path
        
    - `find . -size +10M` → files larger than 10MB
        

---

### `grep`

- Searches for text patterns inside files.
    
- **Examples:**
    
    - `grep hello file.txt` → find “hello” in file
        
    - `grep -i hello file.txt` → case-insensitive
        
    - `grep -r hello /path` → search recursively in folder
        

---

### `wc` (word count)

- Counts lines, words, and characters in files.
    
- **Examples:**
    
    - `wc file.txt` → shows lines, words, chars
        
    - `wc -l file.txt` → count lines only
        
    - `wc -w file.txt` → count words only