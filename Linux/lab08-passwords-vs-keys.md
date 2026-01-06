# Lab 08 – Password Authentication vs Key-Based Authentication (SSH)

## Objective

The objective of this lab was to understand why password-based SSH authentication is inherently weak at scale, how key-based authentication works, and why replacing guessable credentials with possession-based authentication significantly reduces the attack surface.


## Command Used

sudo systemctl start ssh
ss -tlnp | grep 22
grep -E "^(PasswordAuthentication|PubkeyAuthentication)" /etc/ssh/sshd_config
ssh-keygen -t ed25519
ssh-copy-id kali@localhost
ssh kali@localhost
sudo systemctl stop ssh

## Observation

Observations

SSH was running and listening on port 22 when the service was started.

Authentication settings for password and public key authentication were commented out in sshd_config, meaning SSH was using default behavior.

Password authentication was available by default, allowing repeated login attempts.

An SSH key pair was generated locally, creating a private key (kept by the user) and a public key.

The public key was installed on the local SSH server using ssh-copy-id.

After installing the key, SSH login succeeded without requiring a password.

Stopping the SSH service immediately removed port 22 and eliminated exposure.

## Analysis
Why password authentication is weak

Password authentication relies on secrets that can be guessed, reused, leaked, or brute-forced. Attackers can automate password guessing at scale, making password-based SSH a persistent and noisy attack target.

Why key-based authentication is stronger

Key-based authentication relies on possession of a private cryptographic key. Unlike passwords, private keys cannot be guessed or brute-forced, eliminating an entire class of attacks.

Why defaults are dangerous

Although SSH is secure by design, default configurations prioritize usability over security. Allowing password authentication by default creates unnecessary exposure unless explicitly hardened.

## Security Takeaway

Password authentication scales for attackers because it relies on guessing, while key-based authentication eliminates brute-force attacks entirely by requiring possession of a private key.
