#### `/etc/passwd`

- A text file on Linux.
    
- Stores **user account info** (username, user ID, group ID, home folder, default shell).
    
- Example line:
    
    `root:x:0:0:root:/root:/bin/bash`
    
    - `root` = username
        
    - `x` = password stored elsewhere (/etc/shadow)
        
    - `0` = user ID (UID)
        
    - `/root` = home folder
        
    - `/bin/bash` = shell
        

 Used for: seeing who the users are on the system.

---

#### `../`

- Means **“go up one folder”** (parent directory).
    
- Example:
    
    `/home/user/docs/../`
    
    → goes back to `/home/user/`.
    

 Used in **directory traversal attacks** to escape the current folder.