# security-incident-response



---

## 🛡️ Security Incident Report  
**Company**: yummyrecipesforme.com  
**Date**: 2025/04/05  
**Prepared by**: Kgaugelo Given Maseti

**Role**: Cybersecurity Analyst  

---

### 🛰️ Section 1: Network Protocol Identified

**Protocols observed:**

- **DNS (Domain Name System)**: Used to resolve the domain names `yummyrecipesforme.com` and `greatrecipesforme.com` to IP addresses.  
- **HTTP (Hypertext Transfer Protocol)**: Used for the web traffic between the user and both websites (`yummyrecipesforme.com` and `greatrecipesforme.com`). This protocol was used to deliver the malicious download and redirect users.

**Layer (TCP/IP Model)**:
- DNS operates at the **Application Layer**
- HTTP also operates at the **Application Layer**

**Transport Layer Protocol**:
- Both DNS and HTTP sessions occurred over **TCP** (Transmission Control Protocol), indicating reliable, connection-based communication.

---

### 🧾 Section 2: Incident Summary

**Incident Overview**:  
On investigation, it was found that the main webpage for `yummyrecipesforme.com` was compromised. Users were being prompted to download a suspicious executable file upon visiting the site, after which they were redirected to a different domain, `greatrecipesforme.com`.

**Sequence of Events (based on tcpdump logs)**:
1. **DNS Lookup** – The user’s browser requested the IP address for `yummyrecipesforme.com`.
2. **HTTP Request** – The user accessed the website, which had been altered to serve malicious JavaScript.
3. **Malicious Download** – The script forced a download of an `.exe` file, disguised as a browser update.
4. **DNS Lookup for Redirect** – The browser then queried the IP address for `greatrecipesforme.com`.
5. **HTTP Request to Malicious Site** – After resolving, the browser was redirected to the fake site hosting malware.

**Root Cause**:  
The hacker, a former employee, gained unauthorized access to the web host using a **brute force attack**. The admin password had not been changed from its default setting. Once access was gained, the attacker altered the source code and locked the legitimate owner out by resetting the admin password.

**Source of Evidence**:
- `tcpdump` logs showing DNS and HTTP traffic
- Source code review indicating inserted malicious JavaScript
- Reports from users and helpdesk complaints

---

### 🔒 Section 3: Recommendation to Prevent Future Brute Force Attacks

**Recommended Action**:  
**Implement account lockout policies and limit login attempts.**

**Why This Works**:
Limiting the number of failed login attempts deters brute force attacks by preventing continuous automated guessing. Combined with account lockout mechanisms or CAPTCHA systems, attackers are significantly hindered from using default or commonly-used passwords. This method is simple, effective, and easy to deploy via most authentication systems.

**Additional Suggestions**:
- Enforce **strong password policies**
- Enable **two-factor authentication (2FA)**
- Regularly **audit user credentials** and system access
- Monitor logs for **suspicious login behavior**

---
