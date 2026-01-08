# Lab 05 – SSH Attack Surface Analysis

Shows how network exposure is created and removed by starting and stopping services, reinforcing that processes—not ports—create attack surface.

## Objective

To understand why SSH, despite being a secure protocol, can become a major attack surface when exposed unnecessarily, and to observe how service exposure, listening interfaces, and attacker behavior affect system security.

## Environment

OS: Kali Linux

Platform: VirtualBox (NAT)

User: kali

## Command Used

systemctl status ssh
sudo systemctl start ssh
sudo systemctl stop ssh
ss -tlnp | grep 22
ssh localhost
ss -tanp | grep 22
sudo journalctl -u ssh --no-pager | tail -20


## Observation 

Observations

When the SSH service was inactive, no process was listening on TCP port 22.

Starting the SSH service launched the sshd process and created a LISTEN socket on port 22.

SSH was observed listening on 0.0.0.0:22 and [::]:22, meaning it was exposed on all IPv4 and IPv6 interfaces.

Establishing an SSH connection to localhost created an ESTABLISHED TCP session visible using ss.

SSH logs were generated even for successful or failed connection attempts.

Stopping the SSH service immediately removed port 22 and eliminated the attack surface

## Security Takeaway

SSH is secure by design, but enabling it on all interfaces without necessity creates a persistent and highly targeted attack surface that attackers can continuously probe, brute-force, and exploit over time.
