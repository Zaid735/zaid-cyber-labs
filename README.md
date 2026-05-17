# 🛡️ Zaid Akbar Sayyed — Cybersecurity Home Lab

> BSc IT Graduate | Aspiring SOC Analyst (L1) | Blue Team | Detection Engineering
> 
> 📍 Mumbai, India | 📧 sayyedzaidakbar1121@gmail.com | 🔗 [LinkedIn](https://www.linkedin.com/in/zaid-sayyed-6a6588305/)

---

## About This Repository

This repository documents my hands-on cybersecurity lab work — built to develop
real SOC analyst skills through attack simulation, log analysis, SIEM detection,
and endpoint telemetry investigation.

The goal is not just running commands — it's understanding:
- How attackers think and operate
- How detection gaps are created
- How defenders build visibility and response workflows

---

## 🔬 Featured Projects

---

### 🥇 Splunk + Sysmon Mini SOC Lab
**[View Project →](https://github.com/Zaid735/zaid-cyber-labs/tree/main/splunk-sysmon-soc-lab)**

Built a fully functional mini SOC environment integrating Windows endpoint
telemetry with Splunk Enterprise SIEM.

**Architecture:**
Windows 11 (Sysmon) → Splunk Universal Forwarder → Splunk Enterprise (Ubuntu Server)

**Simulated attacker techniques:**
- Encoded PowerShell execution (`powershell -enc`)
- LOLBin abuse — `certutil.exe`, `regsvr32.exe`
- DNS queries and network reconnaissance
- System enumeration (`whoami`, `net user`, `tasklist`, `ipconfig`)

**Detected via Sysmon Event IDs:**
| Event ID | Description | What I Found |
|----------|-------------|--------------|
| 1 | Process Creation | PowerShell, certutil, regsvr32, tasklist |
| 3 | Network Connections | Outbound connections from endpoint |
| 11 | File Creation | Suspicious file drops |
| 22 | DNS Queries | google.com, example.com, wpad lookups |

**MITRE ATT&CK Mapping:**
- T1059 — Command and Scripting Interpreter (PowerShell)
- T1218 — System Binary Proxy Execution (LOLBins)
- T1071 — Application Layer Protocol (DNS)

**Tools:** Splunk Enterprise | Sysmon | Splunk Universal Forwarder | Windows 11 | Ubuntu Server | SPL

---

### 🥈 SSH Brute Force Detection — Splunk Enterprise
**[View Project →](https://github.com/Zaid735/zaid-cyber-labs/tree/main/SIEM/splunk-ssh-bruteforce-detection)**

Simulated SSH brute-force attack and detected it using custom SPL queries in
Splunk Enterprise.

**Key Work:**
- Ingested `/var/log/auth.log` into Splunk — identified 19 failed SSH events
- Built regex-based field extraction using `rex` to isolate attacker IPs
- Wrote threshold detection: `bucket _time span=1m | where count > 5`
- Created `timechart` visualisation — identified attack spike of 15 attempts/min
- Documented Fail2Ban's impact on SIEM telemetry visibility

**MITRE ATT&CK:** T1110 — Brute Force

**Tools:** Splunk Enterprise | SPL | Hydra | Ubuntu Server | Kali Linux | Fail2Ban

---

### 🥉 SSH Brute Force Detection — Wazuh SIEM
**[View Project →](https://github.com/Zaid735/wazuh-ssh-bruteforce-detection)**

Detected and escalated a live SSH brute-force attack using Wazuh SIEM.

**Key Work:**
- Escalated alerts from Level 5 (individual failures) → Level 8 (brute-force pattern)
- Analysed 500+ auth.log entries to build attacker IP timeline
- Wrote custom Wazuh detection rule to flag repeated failures from single IP
- Mapped full attack chain to MITRE ATT&CK T1110
- Documented IoCs for incident report

**Tools:** Wazuh SIEM | Hydra | Ubuntu Server | Kali Linux | Fail2Ban

---

## 📚 Learning Focus Areas

### 🔹 Endpoint Detection & Telemetry
- Sysmon configuration and Event ID analysis
- Log forwarding via Splunk Universal Forwarder
- Windows process creation and LOLBin detection
- DNS anomaly detection

### 🔹 SIEM & Detection Engineering
- Splunk SPL — rex, stats, timechart, bucket, where
- Wazuh rule configuration and alert escalation
- Threshold-based detection logic
- Log correlation across multiple sources

### 🔹 Attack Simulation
- SSH brute-force using Hydra
- Encoded PowerShell execution
- LOLBin abuse (certutil, regsvr32)
- Network reconnaissance and enumeration

### 🔹 System Hardening & Defence
- SSH hardening — key-based auth, password login disabled
- UFW firewall rule configuration
- Fail2Ban intrusion prevention
- Analysing trade-off between prevention and detection visibility

### 🔹 Frameworks
- MITRE ATT&CK mapping — T1059, T1110, T1218, T1071
- IoC documentation
- Incident report writing

---

## 🛠️ Tools & Technologies

| Category | Tools |
|----------|-------|
| SIEM | Splunk Enterprise, Wazuh |
| Endpoint | Sysmon, Splunk Universal Forwarder |
| Attack Tools | Hydra, Nmap, Wireshark |
| Defence | Fail2Ban, UFW |
| OS | Kali Linux, Ubuntu Server, Windows 11 |
| Virtualization | VirtualBox |
| Query Language | SPL (Splunk Processing Language) |

---

## 📈 What This Repository Demonstrates

- Ability to build and operate a functioning SIEM detection environment
- Hands-on experience with both Linux and Windows endpoint telemetry
- Detection engineering — writing queries that catch real attack techniques
- Security reasoning aligned with SOC L1 analyst responsibilities
- Understanding of attacker techniques mapped to MITRE ATT&CK

---

*All labs performed in isolated VirtualBox environments for ethical and legal safety.*
