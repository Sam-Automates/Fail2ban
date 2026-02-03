
# 🔐 Fail2Ban Security Hardening (Linux Servers)

Fail2Ban is an intrusion prevention tool that protects Linux servers by
automatically blocking IPs showing malicious behavior such as
brute-force attacks and suspicious web requests.

This repository contains a **production-tested Fail2Ban setup**
with **custom jails and filters** for SSH and web security.

---

## 🚀 What This Setup Protects

- 🔑 SSH brute-force login attempts  
- 🌐 Malicious web scans (WordPress, `.env`, `.git`, phpMyAdmin, etc.)
- 🤖 Automated bot attacks on Apache access logs

---

## 📦 Installation

```bash
sudo apt update
sudo apt install fail2ban -y
📁 Configuration Files
1️⃣ Jail Configuration
📄 jail.d/custom-jail.conf

Enables SSH protection

Enables custom Apache log monitoring

Bans IP after 1 failed attempt

Ban duration is permanent

text
Copy code
custom-jail → Apache access log protection
sshd        → SSH brute-force protection
2️⃣ Custom Filter
📄 filter.d/custom-filter.conf

This filter detects requests targeting sensitive paths like:

/wp-login.php

/wp-admin/

/xmlrpc.php

/.env

/.git/config

/phpmyadmin/

Any IP matching these patterns is immediately banned.

⚙️ Apply Configuration
bash
Copy code
sudo cp jail.d/custom-jail.conf /etc/fail2ban/jail.d/
sudo cp filter.d/custom-filter.conf /etc/fail2ban/filter.d/
sudo systemctl restart fail2ban
🔍 Verify Status
bash
Copy code
sudo fail2ban-client status
sudo fail2ban-client status sshd
sudo fail2ban-client status custom-jail
🧠 Why This Matters
Most server attacks are automated bots.
Fail2Ban blocks them before they reach your application,
reducing load and improving overall security.
