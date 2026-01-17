# Lab 15: Centralized Logging Using rsyslog

Centralized logging was implemented by forwarding system and security logs from an Ubuntu server to a Kali Linux log collector using rsyslog. This setup ensures log availability and visibility for security monitoring.

## Objective

To configure and verify centralized log forwarding from an Ubuntu server to a remote log collector in order to improve detection capability and prevent log tampering.

## Environment

Log Source: Ubuntu Server 24.04 (192.168.56.102)

Log Collector: Kali Linux (192.168.56.101)

Network Type: VirtualBox Host-only

Logging Service: rsyslog

Log Transport: TCP (Port 514)

## Commands Used

### Ubuntu (Log Source)
sudo nano /etc/systemd/journald.conf


→ Edits the journald configuration to enable forwarding logs to the syslog service.

sudo systemctl restart systemd-journald


→ Restarts journald so the new configuration (ForwardToSyslog) takes effect.

sudo nano /etc/rsyslog.conf


→ Configures rsyslog to forward system logs to the remote log collector.

sudo systemctl restart rsyslog


→ Restarts rsyslog to apply log forwarding and processing rules.

logger "Centralized logging test from Ubuntu"


→ Generates a test log entry to verify local logging and remote log forwarding.

### Kali (Log Collector)
sudo apt install rsyslog -y


→ Installs rsyslog on Kali to enable log collection and storage.

sudo nano /etc/rsyslog.conf


→ Enables rsyslog to listen for incoming logs over the network (TCP/UDP).

sudo nano /etc/rsyslog.d/10-remote.conf


→ Defines a template and rule to store incoming remote logs in /var/log/remote/.

sudo systemctl restart rsyslog


→ Restarts rsyslog to activate network listening and remote log rules.

sudo ufw allow 514/tcp


→ Allows incoming TCP log traffic on port 514 through the firewall.

sudo tcpdump -n -i eth1 tcp port 514


→ Captures network traffic on the host-only interface to verify logs are received over TCP.

ls /var/log/remote


→ Lists centralized log files received from remote systems.

sudo tail /var/log/remote/ubuntu.log


→ Displays recent log entries forwarded from the Ubuntu server.

## Observations

Ubuntu system logs were successfully generated and forwarded using rsyslog over TCP.

TCP traffic on port 514 was verified using packet capture.

Logs from the Ubuntu server were received and stored centrally on Kali in /var/log/remote/ubuntu.log.

Centralized logging confirmed end-to-end visibility of remote system events.

## Security Takeaway

Centralized logging improves security monitoring by ensuring logs are preserved outside the source system, enabling SOC teams to detect, investigate, and respond to security events without relying on local host access.
