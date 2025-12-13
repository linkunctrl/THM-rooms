### 1. **Room Hashes**

Each room’s URL used an MD5 hash.

Numbers 1–13 → matched to rooms 1–13.

### 2. **Flag Location**

The actual flag was hidden in Room 0.

Needed to generate MD5 hash of 0.

### 3. **Solution Steps**

Generate hash: md5(0)

Replace the URL hash with this value.

Visit url/<md5(0)>.

→ Flag revealed.