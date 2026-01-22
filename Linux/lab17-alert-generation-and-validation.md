# Alert Generation & Validation

Validated Wazuh SIEM alerting by intentionally generating authentication failures, privilege escalation attempts, enumeration activity, and file integrity changes. Confirmed end-to-end detection from host logs to Wazuh alerts using CLI only.

## Objective

To verify that security-relevant host activities are correctly detected, classified, and triaged by the SIEM, and to understand alert severity, context, and response logic from a SOC perspective.

## Environment

Agent: Ubuntu Linux (monitored endpoint)

SIEM Manager: Kali Linux (Wazuh Manager, Indexer, Dashboard backend)

Approach: CLI-only, no UI dependency

# Commands Used & Meaning (one line each)

ssh invaliduser@localhost
→ Generates failed authentication events for brute-force detection.

sudo su (wrong password)
→ Simulates failed privilege escalation attempt.

uname -a, id, whoami, cat /etc/passwd
→ Represents post-access system enumeration activity.

sudo nano /etc/passwd
→ Triggers file integrity monitoring on a critical authentication file.

sudo grep -i syscheck /var/ossec/logs/ossec.log
→ Confirms FIM detection on the agent side.

sudo grep -i passwd /var/ossec/logs/alerts/alerts.json
→ Verifies alert generation on the Wazuh manager.

## Observations

Single authentication failures triggered Rule 5402 (Level 3) indicating low-risk activity.

Enumeration combined with sudo failure escalated alert severity to Level 7 due to suspicious behavior correlation.

Modification of /etc/passwd triggered Rule 510 (Level 7) after scheduled FIM scan (~2 minutes delay).

Alert latency matched configured syscheck frequency, confirming expected detection behavior.

## Analysis

Alerts represent state changes and patterns, not confirmed attacks.

Severity reflects risk potential, not certainty.

Rule 510 requires escalation for validation but may be closed if the change is authorized and uncorrelated.

## Security Takeaway

SIEM effectiveness depends on proper coverage, timing awareness, and human triage; high-severity alerts must be investigated in context to distinguish legitimate administrative activity from real compromise.
