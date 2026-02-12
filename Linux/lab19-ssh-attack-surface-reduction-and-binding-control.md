# SSH Attack Surface Reduction & Service Binding Control

Configured SSH service binding to control which network interfaces accept connections, reducing external attack surface. Demonstrated how systemd socket activation and SSH daemon configuration impact service exposure.

## Objective

To understand and implement SSH exposure control by modifying service binding behavior, validating access restrictions, and safely restoring connectivity while maintaining hardened configurations.

## Environment

Target Machine: Ubuntu Server

Attacker / Client: Kali Linux

Network Type: Host-Only + NAT

Service: OpenSSH Server

Interface Tools: CLI-based verification

## Commands Used & Purpose (One-Line Explanation)
Service & Network Inspection
ss -tulpn


→ Displays active listening ports and confirms SSH exposure level.

ip a


→ Identifies available network interfaces and IP addresses for binding validation.

ps -ef | grep sshd


→ Confirms SSH daemon process is running.

SSH Configuration Management
sudo nano /etc/ssh/sshd_config


→ Used to modify SSH service binding and listening behavior.

ListenAddress 127.0.0.1


→ Restricts SSH access to local machine only, removing network exposure.

ListenAddress 0.0.0.0


→ Allows SSH to listen on all network interfaces, restoring remote connectivity.

ListenAddress ::


→ Enables SSH listening on IPv6 interfaces.

AddressFamily any


→ Ensures SSH supports both IPv4 and IPv6 connections.

Service Control & Validation
sudo systemctl restart ssh


→ Applies configuration changes by restarting SSH service.

sudo systemctl status ssh


→ Verifies SSH service operational state.

sudo sshd -t


→ Validates SSH configuration syntax before restarting service.

Socket Activation Control
sudo systemctl stop ssh.socket


→ Stops systemd socket from controlling SSH service binding.

sudo systemctl disable ssh.socket


→ Prevents socket activation from overriding manual SSH configuration.

Access Verification
ssh user@localhost


→ Confirms SSH functionality remains available locally after restriction.

ssh user@<Ubuntu-IP>


→ Tests remote SSH accessibility from Kali after binding adjustments.

## Observations

SSH binding to 127.0.0.1 successfully blocked remote access while preserving local administrative control.

systemd socket activation overrides SSH binding settings if not disabled.

Incorrect or invalid binding configurations can prevent SSH daemon from starting.

Dual-stack binding (0.0.0.0 and ::) ensures full network compatibility.

## Analysis

Service-level binding provides stronger security control than firewall filtering because it eliminates exposed listening services entirely. Proper validation using diagnostic tools prevents accidental service lockouts during configuration changes.

## Security Takeaway

Reducing attack surface by restricting service binding significantly lowers external exposure risk and enforces defense-in-depth beyond traditional firewall protections.
