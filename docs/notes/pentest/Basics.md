---
tags:
  - CTF
  - Pentest
  - Networking
  - Linux
---

!!! warning "Educational purposes only"
    These notes are written strictly for **CTF (Capture The Flag) challenges** and educational learning.
    Do **not** use these techniques against systems you do not own or have explicit written permission to test.
    The author does not endorse or support any illegal or unauthorized activity.

### Top ports

```bash
# FTP 21
# SSH 22
# HTTP 80
# Windows NETBIOS 139
# HTTPS 443
# SMB 445
```

### TCP/IP Fondamentals

```bash
# Client send "SYN" request to Server

# if connection opened
# Server answer with "SYN/ACK" request
# Client answer with "ACK" request

# if connection closed
# Client send SYN request to Server
# Server answer with RST request
```

### Interresting files

```bash
.htaccess
robots.txt
.DS_Store
css & javascript
.well-known/security.txt

# LFI
/var/log/apache2/error.log
/var/log/apache2/access.log
/.dockerenv
/etc/php/8.2/apache2/php.ini
/etc/php/8.2/cli/php.ini
```

### Read files using Python instance

```python
print open("/root/ETSCTF", "r").read()
print open("/etc/passwd", "r").read()
print open("/etc/shadow", "r").read()
```
