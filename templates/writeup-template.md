**Path:** [ OWASP Top 10]
**Difficulty:** Easy / Medium / Hard
**Date:** 
**Tags:** `tag1` `tag2` `tag3`

---

## Overview

Brief description of what this room covers. What is the goal? What technologies/vulnerabilities are involved?

## Tools Used

- 
- 
- 

---

## Reconnaissance

What did I discover first? Initial scans, exposed services, technologies in use.

```bash
# Example: nmap scan
nmap -sV -sC -oN scan.txt <target-ip>
```

**Findings:**
- Port 22: SSH
- Port 80: HTTP (Apache 2.4.x)
- ...

---

## Enumeration

Deeper investigation of the services found. Directory busting, banner grabbing, technology fingerprinting.

```bash
# Example
gobuster dir -u http://<target-ip> -w /usr/share/wordlists/dirb/common.txt
```

---

## Exploitation

Step-by-step how I solved it. Include commands, screenshots, and explanations.

### Step 1: [Action]

What I did and why.

```bash
# Command used
```

### Step 2: [Action]

What I found and how it helped.

---

## Root Cause

**Why did this vulnerability exist?** What did the developer/admin do wrong?

Understanding the root cause is more important than just exploiting it.

---

## Mitigation

How would this be prevented in a real-world scenario?

- Use parameterized queries
- Validate and sanitize input
- Apply principle of least privilege
- ...

---

## Lessons Learned

What's new for me? What concept clicked? What do I want to explore further?

- Concept 1
- Concept 2
- Question to explore: ...

---

## References

- [Official room link](https://tryhackme.com/room/...)
- [Related documentation](#)
- [Related writeup or article](#)
