Project Type
Linux Security Hardening / Defensive Security / DFIR-Oriented Lab
Objective
The objective of this project is to secure an SSH service against brute-force attacks using
native Linux authentication and access control mechanisms, without relying on third-party
intrusion prevention tools.
The lab focuses on implementing, validating, and troubleshooting account-level protections
while maintaining system stability and recoverability.

Environment
● Operating System: Kali Linux (minimal installation)
● SSH Server: OpenSSH
● Authentication Framework: PAM (Pluggable Authentication Modules)
● Protection Mechanism: pam_faillock
● Service Manager: systemd
● Test User: testuser
● Attack Source: Localhost (127.0.0.1)

Tools and Technologies
● OpenSSH
● PAM
● pam_faillock
● systemctl
● journalctl
● Linux user and permission management utilities

Implementation Overview

1. SSH Service Configuration
The SSH service was configured to ensure proper integration with PAM authentication and
enhanced logging for security monitoring.
Key configuration aspects:
● PAM authentication enabled
● Password authentication enabled for testing
● Increased logging verbosity
Configuration file used:
/etc/ssh/sshd_config

2. PAM-Based Brute-Force Protection
Brute-force protection was implemented using the PAM module pam_faillock.
The following controls were enforced:
● Account lockout after three failed authentication attempts
● Lockout applied at the user account level
● Manual reset capability for administrative recovery
Configuration file:
/etc/pam.d/sshd
This approach ensures that protection is handled natively by the Linux authentication stack
without reliance on external monitoring services.

3. Attack Simulation
Multiple failed SSH login attempts were intentionally performed against a test user account to
simulate brute-force behavior:
ssh testuser@127.0.0.1
The SSH service correctly rejected authentication attempts after the defined threshold was
reached.

4. Detection and Verification
Authentication failures and account lockouts were verified using:
faillock
faillock --user testuser
These commands confirmed:
● Failed login attempts were recorded
● Source IP addresses were logged
● Account lockout was enforced as configured

5. Recovery and Incident Response
To simulate administrative incident response, the locked account was manually reset:
faillock --user testuser --reset
Following the reset, successful SSH authentication was verified. User identity and session
context were confirmed using:
whoami
pwd

6. Post-Incident Remediation
During testing, it was identified that the test user did not have a valid home directory, resulting in
session warnings upon login.
This issue was remediated by creating and securing the user’s home directory:
mkdir /home/testuser
chown testuser:testuser /home/testuser
chmod 700 /home/testuser
This step reflects real-world system administration tasks often encountered during incident
recovery.
Results
● SSH brute-force attempts were successfully detected and blocked
● Account lockout policies functioned as intended
● Manual recovery procedures were validated
● SSH service remained stable throughout the testing process
Key Learnings
● PAM provides robust native mechanisms for authentication hardening
● Account-level protections are effective without third-party tools
● Proper SSH and PAM configuration is critical to avoid unintended lockouts
● Incident response includes both recovery and system remediation
Relevance to DFIR and Cloud Security
This project demonstrates skills directly applicable to digital forensics and incident response,
including:
● Detection of authentication abuse
● Log-based validation of security controls
● Account containment and recovery workflows
● Linux server hardening applicable to on-premise and cloud environments
Evidence
The project is supported by screenshots demonstrating:
● SSH service status
● SSH configuration changes
● PAM configuration for brute-force protection
● Failed authentication attempts
● Account lock verification
● Account recovery and successful login
● Post-incident remediation steps
Conclusion
This project successfully demonstrates the implementation of SSH hardening and brute-force
protection using native Linux security mechanisms. The lab reflects real-world defensive
security practices, emphasizes troubleshooting and recovery, and aligns with DFIR and system
hardening principles used in production environments.
