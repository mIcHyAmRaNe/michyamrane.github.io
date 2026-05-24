---
tags:
  - CTF
  - Pentest
  - Passwords
  - Hashes
  - Cryptography
  - Brute-force
---

!!! warning "Educational purposes only"
    These notes are written strictly for **CTF (Capture The Flag) challenges** and educational learning.
    Do **not** use these techniques against systems you do not own or have explicit written permission to test.
    The author does not endorse or support any illegal or unauthorized activity.

### Base64

```bash
# Encode
echo '$TEXT' | base64

# Decode
echo '$TEXT' | base64 -d 
```

### Python converts

```python
# Decimal => Hex => Ascii
hex("DECIMAL NUMBER")
b = bytes.fromhex("HEX NUMBER")
print(b.decode("ASCII"))
```

### Find the format of the hash
```bash
# bash
for i in descrypt bsdicrypt md5crypt bcrypt LM AFS tripcode dummy crypt;
	do john --format=$i yourfile
done
```
```shell
# fish
for i in descrypt bsdicrypt md5crypt bcrypt LM AFS tripcode dummy crypt
    echo $i
    john --format=$i unshadow.txt 
end
```

### Bruteforce SSH

```bash
hydra -l $USER -P /usr/share/wordlists/rockyou.txt $IP ssh -t 10
hydra -l $USER -P /usr/share/wordlists/rockyou.txt ftp://$IP
hydra -l $USER -P /usr/share/wordlists/rockyou.txt $IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```
