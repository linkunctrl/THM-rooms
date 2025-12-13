### 1. Identify file

`file Compiled`

→ ELF 64-bit executable

---

### 2. Run binary

`./Compiled`

→ Asks for password

---

### 3. Inspect strings

`strings Compiled | less`

→ Found: `DoYouEven%sCTF`, `_init`, `Try again!`, `Correct!`

---

### 4. Behavior

- Uses `scanf("DoYouEven%sCTF")` → input replaces `%s`
    
- Compares input with `_init`
    

---

### 5. Final password

`DoYouEven_init`