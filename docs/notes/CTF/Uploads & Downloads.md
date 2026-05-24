---
tags:
  - CTF
  - Pentest
  - File Transfer
  - FTP
  - SMB
---

!!! warning "Educational purposes only"
    These notes are written strictly for **CTF (Capture The Flag) challenges** and educational learning.
    Do **not** use these techniques against systems you do not own or have explicit written permission to test.
    The author does not endorse or support any illegal or unauthorized activity.

### Download directories
```bash
# For example
wget --mirror -I .git http://$IP/.git/
```

### FTP (21)
```bash
# Do not forget to activate the binary mode if necessary.
ftp $IP
ftp> pwd
ftp> cd docs
ftp> ls 
ftp> bin
ftp> get flag.txt
ftp> put backdoor.php
ftp> bye
```

### Smb server (445)

```bash
smbclient //$IP/tmp

# Upload files
put test.txt

# Download files
smbget --recursive smb://$IP/shares
```
