# Lab 13: SSH Exposure & Firewall Visibility


SSH access to an Ubuntu server was initially exposed to the network.
Firewall rules were applied to restrict SSH access to a trusted host and verify visibility of blocked attempts.

## Objective

To identify SSH exposure on a Linux server, restrict access using UFW, and validate firewall visibility through connection behavior and logs.

## Environment

Attacker Machine: Kali Linux

IP (Host-only): 192.168.56.101

Target Machine: Ubuntu Server 24.04

IP (Host-only): 192.168.56.102

SSH: OpenSSH

Firewall: UFW

Network: VirtualBox Host-only Adapter

## Commands Used
SSH Exposure Test (Before Firewall)
ssh <ubuntu_user>@192.168.56.102

Enable Firewall & Set Defaults
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing

Allow SSH From Trusted Host Only
sudo ufw allow from 192.168.56.101 to any port 22 proto tcp

Verify Firewall Rules
sudo ufw status numbered

Firewall Visibility (Logs)
sudo ufw logging on
sudo journalctl -u ufw --no-pager | tail -20

## Observation

SSH connection succeeded before firewall hardening.

After enabling UFW with a default-deny policy, SSH access was restricted.

SSH connections from the trusted Kali host were successful.

Unauthorized SSH attempts were silently dropped.

Blocked connection attempts were visible in firewall logs.

## Security Takeaway

SSH is a high-risk service when exposed without restrictions.

Limiting SSH access by source IP significantly reduces attack surface.

Firewall behavior (ALLOW vs DROP) directly affects attacker visibility.

Logging blocked attempts is essential for SOC monitoring and incident response.
