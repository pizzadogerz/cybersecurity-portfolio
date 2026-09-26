# Linux File Permissions

## What's this?
This is a hands on Linux file permissions review I did as part of my cybersecurity home lab practice. I audited a Linux system (my Kali VM) for messed up file permissions and ownership, the kind of thing that can lead to privilege escalation or someone getting access to stuff they shouldn't, and fixed them using basic CLI tools.

**Tools used:** `ls -l`, `chmod`, `chown`, `stat`

## Scenario Summary
While going through a Linux system as part of a security audit, I found a few files with permissions that didn't make sense from a security standpoint. There was a script anyone on the system could write to, a config file owned by the wrong user, and an SSH private key that was way too open. I found each issue and fixed it.

## Part 1: Finding the issues

I used `ls -l` to check permissions and ownership in the target directory:

```
[ ls -l ]
```

**What I found:**
- `[filename]` had permissions `777` (world writable), so basically anyone on the system could modify or run it
- `[filename]` was owned by `[wrong user]` instead of `[correct user]`, which gave the wrong person access to it
- `id_rsa` (SSH private key) had permissions `644` instead of `600`. SSH actually refuses to use a key if the permissions are this loose

## Part 2: Fixing the issues

**Removing world writable access:**
```bash
chmod 755 [filename]
```
This makes it so only the owner can write to it, while others can still read or run it if they need to.

**Fixing ownership:**
```bash
chown [correct_user]:[correct_group] [filename]
```
This makes sure only the right user (and group) actually controls the file.

**Locking down the SSH key:**
```bash
chmod 600 id_rsa
```
This limits the key to read/write for the owner only, which is what SSH requires.

## Part 3: Checking my work
```
[ ls -l]
```

## Why it matters
Bad file permissions are a super common real world attack vector. A world writable script can get modified by any local user to escalate privileges, and an exposed SSH key can let someone get into a system they have no business being in. This exercise showed me how something as simple as `chmod` and `chown` is actually one of the first things you check when hardening a system.
