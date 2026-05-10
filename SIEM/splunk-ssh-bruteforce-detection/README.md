
# Splunk SSH Brute Force Detection

## Objective

Simulate SSH brute-force activity and detect suspicious authentication behavior using Splunk SIEM and SPL queries.

---

## Lab Environment

| System | Role |
|---|---|
| Kali Linux | Attacker |
| Ubuntu Server | Target |
| Splunk Enterprise | SIEM Platform |

---

## Attack Simulation

Hydra was used to simulate repeated SSH authentication failures against the Ubuntu target.

Example:

hydra -l fakeuser -P /usr/share/wordlists/rockyou.txt ssh://192.168.56.102

## Log Ingestion

Authentication logs were continuously monitored in Splunk using:

/var/log/auth.log

Splunk was configured to ingest and index SSH authentication events for investigation.

## SPL Queries Used
Failed SSH Logins
source="/var/log/auth.log" "Failed password"
### Extract Source IPs
source="/var/log/auth.log" "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
### Threshold-Based Brute Force Detection
source="/var/log/auth.log" "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| bucket _time span=1m
| stats count by _time, src_ip
| where count > 5
### Timeline Visualization
source="/var/log/auth.log" "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| timechart count by src_ip
### Investigation Findings
Kali Linux IP (192.168.56.101) generated multiple failed SSH authentication attempts
Splunk successfully extracted and correlated source IP activity
Timeline analysis identified spikes in brute-force behavior
Fail2Ban initially reduced event visibility by blocking attack traffic early

## Key Learning

This lab demonstrated:

SIEM log ingestion
SPL query development
Regex-based field extraction
Threshold-based detection logic
Timeline analysis and attack visualization
Relationship between prevention controls and telemetry visibility

## Screenshots
### Failed SSH Events
![Failed SSH](/failed-ssh.png)

### SPL Regex Extraction
![Regex Extraction](/regex-extraction.png)

### Brute Force Detection
![Brute Force Detection](/bruteforce-detection.png)

### Timeline Visualization

![Timeline](/timeline-visualization.png)

## Conclusion

This lab simulated SSH brute-force activity in a controlled environment and demonstrated how Splunk SIEM can ingest, parse, correlate, and visualize authentication-based attacks using SPL.
