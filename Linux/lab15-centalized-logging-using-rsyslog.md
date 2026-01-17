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

### Ubuntu (Log Source):

sudo nano /etc/systemd/journald.conf
sudo systemctl restart systemd-journald
sudo nano /etc/rsyslog.conf
sudo systemctl restart rsyslog
logger "Centralized logging test from Ubuntu"


### Kali (Log Collector):

sudo apt install rsyslog -y
sudo nano /etc/rsyslog.conf
sudo nano /etc/rsyslog.d/10-remote.conf
sudo systemctl restart rsyslog
sudo ufw allow 514/tcp
sudo tcpdump -n -i eth1 tcp port 514
ls /var/log/remote
sudo tail /var/log/remote/ubuntu.log

## Observations

Ubuntu system logs were successfully generated and forwarded using rsyslog over TCP.

TCP traffic on port 514 was verified using packet capture.

Logs from the Ubuntu server were received and stored centrally on Kali in /var/log/remote/ubuntu.log.

Centralized logging confirmed end-to-end visibility of remote system events.

## Security Takeaway

Centralized logging improves security monitoring by ensuring logs are preserved outside the source system, enabling SOC teams to detect, investigate, and respond to security events without relying on local host access.
