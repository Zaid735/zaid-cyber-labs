# Lab 09 – Secure SSH Hardening

Compares password-based and key-based authentication, showing why key-based access eliminates brute-force attacks.

## Objective

The objective of this lab was to safely harden SSH by disabling password authentication and root login, while understanding SSH configuration precedence and avoiding administrative lockout through controlled verification.

## Command Used

sudo sshd -T | grep -E "passwordauthentication|pubkeyauthentication|permitrootlogin"
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sudo nano /etc/ssh/sshd_config
ls /etc/ssh/sshd_config.d/
sudo nano /etc/ssh/sshd_config.d/99-hardening.conf
sudo sshd -t
sudo systemctl restart ssh
ssh kali@localhost

## Observations

The effective SSH configuration showed that password authentication and root login were enabled despite changes made in the main sshd_config file.

SSH was loading additional configuration files from /etc/ssh/sshd_config.d/, which overrode settings in the main configuration file.

Editing sshd_config alone did not change the effective behavior because later include files had higher precedence.

Creating a custom override file (99-hardening.conf) successfully enforced the desired hardened settings.

After restarting SSH, password-based login and root login were disabled, while key-based authentication remained functional.

SSH access was verified in a new session to ensure no lockout occurred.

## Analysis
Why main configuration edits did not apply

Modern SSH implementations load configuration in layers. Settings defined in included files under sshd_config.d/ are processed after the main configuration file and override earlier values.

Why an override file is the correct approach

Creating a custom hardening file ensures that security settings:

override vendor defaults

survive system updates

remain isolated and reversible

do not conflict with OS-managed configurations

Why hardening must follow a strict order

Authentication methods must be verified before removing weaker access options to prevent accidental loss of administrative access.


## Hardened Configuration Applied

The following settings were enforced using an override file:

PasswordAuthentication no
PubkeyAuthentication yes
PermitRootLogin no

## Security Takeaway

Effective SSH hardening depends on understanding configuration precedence and applying changes in a controlled, verifiable order to reduce attack surface without breaking access.
