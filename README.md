# Linux SSH Hardening Project

## Project Overview
This project demonstrates SSH hardening and authentication control on a Linux system.
The lab focuses on verifying SSH service availability, enforcing PAM authentication rules,
and validating successful user access after remediation.

The work reflects a real-world troubleshooting and security-hardening scenario commonly
encountered in system administration and security operations.

---

## Technologies Used
- Kali Linux
- OpenSSH
- PAM (Pluggable Authentication Modules)
- systemctl
- faillock

---

## Security Objectives
- Verify SSH service status
- Enforce PAM-based authentication controls
- Reduce brute-force login attempts
- Restore legitimate user access securely

---

## Evidence and Results

### SSH Service Status
This screenshot confirms that the SSH service is running and properly managed by systemd.

![SSH Status](screenshots/ssh status.png)

---

### PAM SSH Configuration
This screenshot shows the PAM configuration applied to SSH authentication.

![PAM SSHD](screenshots/pam sshd.png)

---

### Successful SSH Authentication
This screenshot confirms successful SSH login after correcting authentication
and user environment issues.

![SSH Success](screenshots/ssh success.png)

---

## Outcome
- SSH service verified and operational
- PAM authentication rules correctly applied
- User login successfully restored
- System hardened against repeated authentication failures

---

## Skills Demonstrated
- Linux system administration
- SSH configuration and troubleshooting
- PAM authentication management
- Security hardening fundamentals
- Incident-style problem solving
