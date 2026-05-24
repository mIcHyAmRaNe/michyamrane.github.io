---
tags:
  - CTF
  - Pentest
  - Steganography
  - Forensics
  - Reverse Engineering
---

!!! warning "Educational purposes only"
    These notes are written strictly for **CTF (Capture The Flag) challenges** and educational learning.
    Do **not** use these techniques against systems you do not own or have explicit written permission to test.
    The author does not endorse or support any illegal or unauthorized activity.

### Pictures

```bash
exiftool $FILENAME

steghide info $FILENAME
steghide extract -sf $FILENAME

stegsolve 
```

### Binary Files

```bash
# Analyze to find host
strings filename | grep 'host'

# Analyze to find source filename 
strings filename | grep '\.c'

# To find for which distro version the binary is compiled on
## we see that it s compiled on gnu , means with gnu compiler
file filename
strings -a filename | grep 'gcc'
strings -a filename | grep 'GCC' 

# To find which funtion is called when it runs main()
## open the file with "ghidra" then "Display Function Call Trees" then "expand Nodes to Depth Limit"
```
