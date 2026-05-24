---
tags:
  - CTF
  - Pentest
  - Networking
  - Nmap
  - Recon
  - Web
---

!!! warning "Educational purposes only"
    These notes are written strictly for **CTF (Capture The Flag) challenges** and educational learning.
    Do **not** use these techniques against systems you do not own or have explicit written permission to test.
    The author does not endorse or support any illegal or unauthorized activity.

### Nmap

```bash
sudo nmap -p1-65535 $IP
sudo nmap --top-ports 65535 $IP
sudo nmap -sS -sC -sV -Pn -p- -T4 -A -vv $IP -oA scanresult
sudo nmap -p- -sVC --min-rate 5000 $IP

# for firewall evasion, we add: -sN -sF -sX
sudo nmap -sS -sC -sV -Pn -p- -T4 -A -sN -sF -sX $IP
```

### FTP (21)
```bash
# Do not forget to activate the binary mode if necessary.
ftp $IP
Name (IP): anonymous
Password: anonymous
ftp> pwd
ftp> cd docs
ftp> ls 
ftp> bin
ftp> get flag.txt
ftp> put backdoor.php
ftp> bye
```
### SSH (22)
```bash
# Login with password
ssh user@$IP

# Login with private key
ssh -i id_rsa user@$IP

# Note that the private key should only be read by its owner
chmod 600 id_rsa
```
### HTTP (80)
```bash
# contains a list of the resources of the site that are not supposed to be indexed by search engine spiders
http://$IP/robots.txt

# Check comments in source code
# Check for hidden elements
# Directories and files bruteforce
```

### Smb server (445)

```bash
# Use enum4linux tool to enumerate users and folders
enum4linux $IP
```

### WFuzz, Gobuster, Feroxbuster

```bash
# list of directories/filenames
/usr/share/wordlists/dirb/common.txt   # Small well-constructed list
/usr/share/wordlists/seclists/Discovery/Web-Content/big.txt
/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt   # Best for CTFs.

gobuster dir -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt --no-error -x "html,php,txt,bak,git" -u "http://$IP"

# Fuzz a parameter name
gobuster fuzz -w /usr/share/wordlists/seclists/Discovery/Web-Content/burp-parameter-names.txt --no-error -u "http://$IP/action.php?FUZZ=whoami"

# Fuzz the value of a url parameter
gobuster fuzz -w /usr/share/wordlists/seclists/Discovery/Web-Content/burp-parameter-names.txt --no-error -u "http://$IP/action.php?command=FUZZ"

# Fuzz subdomain
gobuster dns -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt --no-error -d "$IP"

# Fuzz an id from 0 to 20
wfuzz -c -z range,000-020 http://$IP/user.php?id=FUZZ

# Directories
wfuzz -c -z file,/usr/share/wordlists/seclists/Discovery/Web-Content/big.txt --sc 200,202,204,301,302,307,403 http://$IP/FUZZ

# Subdomain
wfuzz -c --hw 977 -w /usr/share/wfuzz/wordlist/general/common.txt -u http://URL -H "Host: FUZZ.URL" --hc 400

# Files
gobuster dir -u $IP -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x "html,php,txt"

# BOTH
dirsearch http://$IP
feroxbuster -x js html php txt json bkp git --depth 2 --silent -u http://$IP
```
