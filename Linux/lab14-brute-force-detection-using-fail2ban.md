# SSH Brute-Force Detection Using Fail2Ban

Fail2Ban was deployed on an Ubuntu server to detect repeated SSH authentication failures and automatically block brute-force attempts by banning the attacker’s IP address through firewall enforcement.

## Objective

To identify and respond to SSH brute-force attacks by monitoring authentication logs and dynamically enforcing IP bans using Fail2Ban.

## Environment
Component	Details
Attacker Machine	Kali Linux
Attacker IP	192.168.56.101
Target Machine	Ubuntu Server 24.04
Target IP	192.168.56.102
Network Type	VirtualBox Host-only
Services	OpenSSH
Security Tools	Fail2Ban, UFW

## Commands Used
Install Fail2Ban
sudo apt update
sudo apt install fail2ban -y

Create Local Configuration
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

Configure SSH Jail
sudo nano /etc/fail2ban/jail.local

[sshd]
enabled = true
backend = systemd
port = ssh
maxretry = 3
findtime = 60
bantime = 600

Restart and Verify Service
sudo systemctl restart fail2ban
sudo systemctl enable fail2ban
sudo fail2ban-client status
sudo fail2ban-client status sshd

Simulate Brute-Force Attack (Kali)
ssh root@192.168.56.102


(Incorrect passwords entered multiple times)

Verify Ban Enforcement
sudo ufw status numbered
sudo journalctl -u fail2ban --no-pager | tail

## Observations

Multiple failed SSH authentication attempts were detected within a short time window.

Fail2Ban identified the attacker IP based on log analysis.

The attacker IP (192.168.56.101) was automatically banned after exceeding retry limits.

Firewall rules were dynamically added to block SSH access from the banned IP.

Subsequent SSH connection attempts from the attacker resulted in connection refusal.

## Security Takeaway

Fail2Ban provides automated detection and response against SSH brute-force attacks by correlating authentication failures from system logs and enforcing temporary firewall bans, significantly reducing the effectiveness of credential-guessing attacks.
