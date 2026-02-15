# End-to-End SSH Security Review


Validated the complete SSH security lifecycle by simulating an attack and verifying exposure, logging, detection, automated blocking, and network enforcement.
Proved that security controls must be measurable through commands, not assumptions.

## Objective

Perform a full threat-to-defense validation of SSH by testing exposure, attack simulation, detection visibility, automated response, firewall enforcement, and architectural boundaries.

## Environment

Target: Ubuntu Server (SSH enabled, Fail2Ban installed, UFW active)

Attacker: Kali Linux

Networking: NAT + Host-Only

SSH bound to 0.0.0.0

systemd socket activation disabled

## Commands Used 
sudo systemctl restart ssh


Restarts SSH to ensure clean baseline state.

sudo systemctl restart fail2ban


Resets Fail2Ban counters and active bans.

sudo ufw reload


Reapplies firewall rules to confirm enforcement is active.

ss -tulpn | grep ssh


Confirms SSH listening address and exposure scope.

nmap -p 22 <ubuntu_ip>


Verifies external network reachability of SSH port.

hydra -l fakeuser -P /usr/share/wordlists/rockyou.txt ssh://<ubuntu_ip> -t 4 -V


Simulates brute-force authentication attempts.

sudo journalctl -u ssh --since "5 minutes ago"


Displays recent SSH authentication logs.

sudo fail2ban-client status sshd


Shows Fail2Ban jail status and banned IP list.

ssh fakeuser@<ubuntu_ip>


Tests whether the attacking IP is blocked.

sudo ufw status numbered


Displays active firewall rules and enforcement state.

ip a


Lists network interfaces to verify segmentation boundaries.

sudo systemctl stop fail2ban


Disables automated response to observe security degradation.

## Observations

SSH was reachable on port 22 from Kali.

Brute-force attempts generated multiple failed authentication logs.

Fail2Ban detected repeated failures and banned the attacker IP.

SSH access from banned IP was blocked.

Firewall rules remained active and visible.

When Fail2Ban was stopped, brute-force attempts were no longer blocked.

Logs continued even when automated response was disabled.

## Security Takeaway

Security is a chain, not a single control.

Exposure exists if service listens on all interfaces.

Logging alone does not stop attacks.

Detection without automated enforcement is incomplete defense.

Firewall + Fail2Ban create layered protection.

Architecture (network segmentation + interface binding) determines real attack surface.
