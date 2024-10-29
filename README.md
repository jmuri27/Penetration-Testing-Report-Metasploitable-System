# Penetration Testing Report: Metasploitable System

This project contains a detailed report on a penetration test performed on a Metasploitable system within a VirtualBox lab environment. The test demonstrates the process of identifying and exploiting system vulnerabilities, elevating privileges, and performing post-exploitation activities to assess security weaknesses.

## Table of Contents
- [Objective](#objective)
- [Tools Used](#tools-used)
- [Methodology](#methodology)
  - [Network Scanning](#network-scanning)
  - [Exploiting vsftpd 2.3.4 Backdoor](#exploiting-vsftpd-234-backdoor)
  - [Post-Exploit Enumeration](#post-exploit-enumeration)
  - [Cracking Passwords with John the Ripper](#cracking-passwords-with-john-the-ripper)
  - [SSH Access](#ssh-access)
  - [Privilege Escalation](#privilege-escalation)
  - [Post-Exploitation](#post-exploitation)
- [Conclusion](#conclusion)
- [Recommendations](#recommendations)

## Objective

The primary goal of this penetration test was to evaluate the security posture of the Metasploitable system (IP: 192.168.56.104) by identifying and exploiting vulnerabilities to gain unauthorized access and perform post-exploitation actions. This exercise highlights potential security risks and serves as a hands-on demonstration of penetration testing techniques.

## Tools Used
- **Kali Linux**: The attacker machine used for conducting the test.
- **Nmap**: Network scanning tool to identify open ports and running services.
- **Metasploit Framework**: Used for exploiting known vulnerabilities.
- **John the Ripper**: Password-cracking tool for recovering weak passwords.
- **SSH**: Secure Shell for remote access.
- **Linux Utilities**: Commands for exploring files and logs.

## Methodology

### Network Scanning
- **Objective**: Identify open ports and services on the target.
- **Command**: `nmap -A 192.168.56.104`
- **Results**: Nmap revealed critical services:
  - FTP (vsftpd 2.3.4), SSH (OpenSSH 4.7p1), Telnet, Samba, PostgreSQL, MySQL, VNC, Apache Tomcat, IRC (UnrealIRCd)

### Exploiting vsftpd 2.3.4 Backdoor
- **Objective**: Exploit a backdoor vulnerability in the vsftpd 2.3.4 service.
- **Result**: Successfully opened a root shell on the target, gaining root access.

### Post-Exploit Enumeration
- **Objective**: Gather system information and retrieve user account data.
- **Commands**: Basic Linux commands were used to explore the system.
- **Result**: Extracted user account information and password hashes from `/etc/shadow`.

### Cracking Passwords with John the Ripper
- **Objective**: Crack user passwords to facilitate further access.
- **Commands**: Used `john` to crack saved hashes.
- **Result**: Recovered the following passwords:
  - `postgres: postgres`
  - `user: user`
  - `msfadmin: msfadmin`
  - `service: service`
  - `klog: 123456789`
  - `sys: batman`

### SSH Access
- **Objective**: Log into the target system with cracked credentials.
- **Command**: `ssh msfadmin@192.168.56.104`
- **Result**: Successfully accessed the system as the user `msfadmin`.

### Privilege Escalation
- **Objective**: Gain root privileges through sudo rights.
- **Command**: `sudo -l` confirmed full sudo rights for `msfadmin`.
- **Result**: Achieved full root access, allowing complete control over the system.

### Post-Exploitation
- **Objective**: Investigate sensitive files and logs as root.
- **Findings**:
  - Discovered SSH keys in `/root/.ssh`.
  - Reviewed system logs to assess unauthorized access attempts and cron jobs.

## Conclusion
The penetration test successfully demonstrated multiple vulnerabilities in the Metasploitable system:
1. Exploitable **vsftpd 2.3.4** backdoor.
2. Weak password policy, with several easily crackable passwords.
3. Improper sudo configuration, allowing privilege escalation for `msfadmin`.

## Recommendations
- **Update or disable** the vsftpd service to prevent exploitation.
- **Implement stronger password policies** to secure accounts.
- **Limit sudo privileges** to necessary users to mitigate privilege escalation risks.

---

This project serves as a practical example of penetration testing, showcasing key techniques for identifying, exploiting, and securing against vulnerabilities.
