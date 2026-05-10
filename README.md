# Zaid Sayyed — Cybersecurity Learning Labs

## About This Repository

This repository contains hands-on cybersecurity labs focused on understanding how systems are exposed, attacked, and defended.

The goal is not just running commands, but analyzing:
- How attack surfaces are created
- How attackers exploit weak configurations
- How defenders detect and reduce risk

---

## Learning Focus Areas

### 🔹 Network & Service Exposure
- Port scanning and service visibility
- TCP vs UDP behavior
- Identifying exposed services
- Service lifecycle and attack surface

---

### 🔹 Authentication & Attack Surface
- SSH as an attack vector
- User enumeration techniques
- Password-based vs key-based authentication
- Brute-force attack behavior

---

### 🔹 System Hardening & Defense
- SSH hardening techniques
- Configuration precedence
- Firewall (UFW) rules and exposure control
- Fail2Ban for intrusion prevention

---

### 🔹 Detection & Monitoring (SIEM)
- Log analysis (auth.log, system logs)
- SSH attack detection patterns
- Brute-force detection using Wazuh
- Correlation of repeated events

---

## Featured Project

🔹 **SSH Brute Force Detection using Wazuh SIEM**  
- Simulated attack using Hydra  
- Detected failed login attempts and escalation  
- Observed transition from Level 5 → Level 8 alerts  
- Mapped to MITRE ATT&CK (T1110 - Brute Force)  
- Analyzed interaction between detection (Wazuh) and prevention (Fail2Ban)

👉 [View Full Project](ADD_YOUR_NEW_REPO_LINK_HERE)

  ### Splunk SSH Brute Force Detection

Ingested Linux authentication logs into Splunk
Parsed SSH events using SPL and regex extraction
Simulated brute-force activity from Kali Linux
Built threshold-based detection logic for failed logins
Visualized attack timelines and source IP activity
Investigated the impact of Fail2Ban on telemetry visibility
  -

---

## What This Repository Demonstrates

- Understanding of attack surface creation and reduction
- Ability to analyze authentication failures and attack patterns
- Practical system hardening techniques
- Basic SIEM-based detection and log analysis
- Security reasoning beyond tool usage

---

## Tools Used

- Kali Linux
- Ubuntu Linux
- SSH
- Hydra
- Wazuh SIEM
- Fail2Ban
- UFW Firewall
- Nmap
- Wireshark

---

## Note

This repository represents foundational learning.  
Focused project-based work (real attack + detection scenarios) is maintained in separate repositories.
