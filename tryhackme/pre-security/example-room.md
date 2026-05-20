# Example Room (delete this file once you write your first real one)

**Platform:** TryHackMe
**Path:** Pre Security
**Difficulty:** Easy
**Date:** 2026-05-20
**Tags:** `networking` `linux` `beginner`

---

## Overview

This is an example writeup showing the structure I follow. Replace this file with your actual writeups as you complete rooms.

The goal of writing these is not just to document solutions — it's to force myself to understand what I did and why it worked.

## Tools Used

- nmap
- bash
- Firefox

---

## Reconnaissance

Started with a basic port scan to see what's running on the target.

```bash
nmap -sV -sC <target-ip>
```

**Findings:**
- Port 80: HTTP server

---

## Exploitation

### Step 1: Visit the web server

Navigated to the IP in the browser and found a basic webpage.

### Step 2: Find the flag

The flag was hidden in the page source.

---

## Root Cause

Sensitive information was exposed in HTML comments — a common beginner mistake when developers leave debug info in production code.

---

## Mitigation

- Never store secrets, flags, or sensitive data in client-side code
- Review HTML/JS before deploying to production
- Use proper environment variables for configuration

---

## Lessons Learned

- Always check page source (`Ctrl+U`) and developer tools
- Recon is the most important phase — most findings come from careful enumeration
- Question to explore: how do real-world attackers automate this kind of source inspection?

---

## References

- [TryHackMe](https://tryhackme.com)
