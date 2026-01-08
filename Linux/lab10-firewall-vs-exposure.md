# Lab 10 – Firewall vs Service Exposure

Documents safe SSH hardening using configuration precedence while avoiding administrative lockout.

## Objective

The objective of this lab was to understand the difference between service hardening and network exposure, and to demonstrate how a firewall reduces attack surface by controlling reachability before authentication occurs.

## Command used

sudo systemctl start ssh
ss -tlnp | grep 22
sudo apt update
sudo apt install ufw -y
sudo ufw status
sudo ufw allow ssh
sudo ufw enable
sudo ufw status

## Observations

SSH was running and listening on port 22, indicating the service was exposed to the network stack.

Initially, the system had no firewall installed, meaning no network-level filtering was in place.

After installing UFW, the firewall was inactive by default and did not affect traffic until explicitly enabled.

SSH was explicitly allowed through the firewall to prevent administrative lockout.

Once UFW was enabled, SSH remained accessible, but traffic was now filtered according to firewall rules.

The firewall did not stop the SSH service from listening; it controlled which connections were allowed to reach it

## Security Takeaway

Service hardening protects authentication mechanisms, while firewalls reduce attack surface by limiting which systems can reach a service in the first place; both layers are required for effective defense.
