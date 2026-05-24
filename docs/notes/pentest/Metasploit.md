---
tags:
  - CTF
  - Pentest
  - Metasploit
  - Exploitation
---

!!! warning "Educational purposes only"
    These notes are written strictly for **CTF (Capture The Flag) challenges** and educational learning.
    Do **not** use these techniques against systems you do not own or have explicit written permission to test.
    The author does not endorse or support any illegal or unauthorized activity.

### Metasploit

```bash
# Specific Search
# type:<auxiliary/exploit/post>
msf6 > search type:<type> platform:<os> cve:<year> rank:<rank> <pattern>
# example: search type:exploit platform:windows cve:2021 rank:excellent microsoft
```
