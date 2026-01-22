# SIEM Deployment Using Wazuh (Manager, Indexer, Agent Integration)


In this lab, a centralized SIEM solution using Wazuh was deployed to collect, analyze, and correlate security logs from multiple systems. The lab focused on backend SIEM architecture, agent enrollment, and log flow verification rather than UI visualization.

## Objective

Understand how a SIEM works internally (agent → manager → indexer).

Deploy Wazuh Manager, Indexer, and Dashboard.

Enroll an Ubuntu system as a Wazuh agent.

Verify log ingestion and alert generation via CLI.

Learn the difference between events, alerts, and incidents.

## Environment

SIEM Server

OS: Kali Linux

IP: 192.168.56.101

### Components:

Wazuh Manager

Wazuh Indexer (OpenSearch)

Wazuh Dashboard

Monitored System (Agent)

OS: Ubuntu Server 24.04

Hostname: zaid735

IP: 192.168.56.102

Role: Log source (SSH, system logs)

### Network

VirtualBox Host-only Network

Tools & Components Used

Wazuh Manager

Wazuh Indexer (OpenSearch)

Wazuh Dashboard

Wazuh Agent

systemd

OpenSearch Dashboards

Linux CLI tools (ss, journalctl, agent_control, wazuh-control)

## Commands Used (with purpose)
1. Wazuh Installation (All-in-One)
curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh
sudo bash wazuh-install.sh -a -i


Purpose:
Installs Wazuh Manager, Indexer, and Dashboard in a single-node setup.

2. Verify Core Services
sudo systemctl is-active wazuh-manager wazuh-indexer wazuh-dashboard


Purpose:
Confirms whether SIEM backend services are running.

3. Verify Indexer (OpenSearch)
sudo ss -tlnp | grep 9200
curl -k https://127.0.0.1:9200


Purpose:
Ensures OpenSearch is listening and responding to requests.

4. Check Wazuh Manager Daemons
sudo /var/ossec/bin/wazuh-control status


Purpose:
Verifies internal Wazuh components like analysisd, remoted, authd, and db.

5. Install Wazuh Agent on Ubuntu
sudo apt install wazuh-agent -y


Purpose:
Installs the agent that forwards logs to the SIEM.

6. Agent Enrollment
sudo /var/ossec/bin/agent-auth -m 192.168.56.101


Purpose:
Registers the Ubuntu system with the Wazuh Manager.

7. Verify Agent Connection
sudo /var/ossec/bin/agent_control -lc


Purpose:
Lists all connected agents and confirms active status.

8. Validate Log Flow (CLI-based)
sudo tail -f /var/ossec/logs/alerts/alerts.json


Purpose:
Confirms that security events are being processed and alerts generated.

## Observations

Wazuh Manager and Indexer were successfully installed and verified running.

Ubuntu agent was enrolled and appeared as Active in agent_control.

OpenSearch was listening on port 9200 and responding correctly.

Wazuh Manager daemons (analysisd, remoted, authd, db) were running.

Alerts were generated and visible via CLI (alerts.json).

Wazuh Dashboard UI showed API connectivity issues on Kali Linux, despite a healthy backend.

Known Issue / Limitation

The Wazuh Dashboard UI did not fully function on Kali Linux due to rolling-release compatibility issues.

Symptoms included:

“Application not found”

“API not connected”

Backend SIEM functionality was not affected.

This is a known limitation when deploying Wazuh Dashboard on non-LTS rolling distributions.

## Security Takeaways

SIEM effectiveness depends on log ingestion and correlation, not UI dashboards.

Agents forward events; managers analyze them; indexers store them — dashboards only visualize.

A single failed login is an event, repeated failures become an alert, correlated malicious activity becomes an incident.

Real SOC environments frequently rely on CLI and logs when dashboards fail.

Understanding backend health is more important than UI availability.
