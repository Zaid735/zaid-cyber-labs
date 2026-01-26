# Alert Correlation & Detection Engineering Limits


Validated how multiple low-to-medium severity alerts can be correlated into a single security incident using timeline and context analysis. Attempted custom correlation rule creation and identified Wazuh engine limitations that prevent deep multi-stage correlation.

## Objective

To determine when isolated alerts collectively indicate malicious behavior and to understand practical limitations of SIEM-based correlation versus analyst-driven incident detection.

## Environment

Endpoint (Agent): Ubuntu Linux

SIEM Manager: Kali Linux (Wazuh Manager & Indexer)

Interface: CLI only (no dashboard dependency)

## Commands Used & Meaning (one line each)

ssh invaliduser@localhost
→ Generates repeated authentication failures.

ssh zaid735@localhost
→ Simulates successful access after failed attempts.

whoami, id, uname -a, cat /etc/passwd
→ Represents post-access system enumeration.

sudo su (wrong password)
→ Simulates failed privilege escalation attempt.

sudo tail -f /var/ossec/logs/alerts/alerts.json
→ Observes alert sequence and timing in real time.

sudo nano /var/ossec/etc/rules/local_rules.xml
→ Used to attempt custom correlation rule creation.

sudo /var/ossec/bin/wazuh-analysisd -t
→ Validates rule syntax and engine compatibility.

## Observations

Individual alerts (authentication failure, enumeration, sudo failure) were generated successfully.

Alerts occurred within the same host, user context, and time window.

Custom correlation rules loaded but did not trigger due to Wazuh correlation constraints on authentication-related rules.

Analysis

Although no single alert confirmed compromise, the sequence of access attempts, reconnaissance, and privilege escalation attempts formed a complete attack chain. Wazuh detected each stage but did not natively correlate them into one incident, requiring analyst-level correlation.

## Security Takeaway

SIEM tools detect events, not incidents; effective incident detection depends on contextual correlation, timeline analysis, and understanding platform limitations rather than relying solely on automated correlation rules.
