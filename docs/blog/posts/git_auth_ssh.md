---
title: Add SSH Keys for Git Authentication
date: 2026-05-30 
categories:
  - git
---

## Windows 

### Setup SSH key

**Forge Your New SSH Key**

```powershell
ssh-keygen -t ed25519 -C "your-email@example.com"
```

**start the SSH agent**

```powershell
Set-Service -Name ssh-agent -StartupType Automatic  
Start-Service ssh-agent
```

**Add the key**
```powershell
ssh-add $HOME\.ssh\id_ed25519
```
<!-- more -->
**Grab Your Public Key**
```powershell
cat ~/.ssh/id_ed25519.pub
```


**GitHub**

- Navigate to **GitHub → Settings → SSH and GPG keys**.
- Click **New SSH Key**, paste your key, and hit save.

**GitLab**

- Go to **GitLab → Preferences → SSH Keys**.
- Paste your key and save it.

**Bitbucket**

- Head to **Bitbucket → Personal Settings → SSH Keys**.
- Click **Add Key**, paste, and save.


### Test the connection

**Github**:

```powershell
ssh -T git@github.com
```

**GitLab**

```powershell
ssh -T git@gitlab.com
```

**Bitbucket**

```powershell
ssh -T git@bitbucket.org
```

If you get this message, means all **OK** 

```bash
Hi username! You've successfully authenticated, but GitHub/GitLab/Bitbucket does not
```
