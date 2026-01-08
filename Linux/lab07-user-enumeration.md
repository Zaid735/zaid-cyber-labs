# Lab 07 – User Enumeration via SSH

Demonstrates how authentication responses can leak valid usernames and why enumeration precedes brute-force attacks.

## Objective

The objective of this lab was to understand what user enumeration is, how authentication mechanisms can leak information about valid usernames, and why attackers perform enumeration before attempting password attacks.

## Commands

sudo systemctl start ssh
ss -tlnp | grep 22
ssh kali@localhost
ssh notarealuser@localhost
sudo journalctl -u ssh --no-pager | tail -40
sudo systemctl stop ssh

## Observations

When attempting SSH login with a valid username and wrong password, the system responded with a generic authentication failure.

When attempting SSH login with a non-existent username, the system generated log entries indicating an Invalid user.

SSH logs clearly differentiated between invalid users and failed password attempts for valid users.

These differences were observable even though no successful authentication occurred.

The SSH service exposed this information without requiring any credentials.


## Analysis
Why attackers perform user enumeration

Attackers enumerate users to identify valid accounts so that subsequent password attacks are focused only on real users, improving efficiency and increasing the chance of success.

Why enumeration reduces brute-force effort

Brute-forcing non-existent users wastes time and resources, while targeting only valid usernames allows attackers to scale attacks more effectively.

Why error message differences are dangerous

Different error messages and log entries leak information about whether a username exists, enabling attackers to confirm valid accounts without authentication.

## Security Takeaway

User enumeration allows attackers to identify valid usernames through authentication failures, significantly increasing the effectiveness of password attacks even when no login succeeds.
