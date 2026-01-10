# Lab 12 – SSH Brute Force Detection via Logs

SSH brute-force attacks are detectable through repeated authentication failures from the same source within a short time window, regardless of changing source ports or successful access.

## Objective

The objective of this lab was to analyze SSH authentication logs to understand how brute-force login attempts appear from a defender’s perspective and how repeated failed authentication attempts act as early indicators of attack activity.

## Command Used


sudo systemctl start ssh
ss -tlnp | grep 22
sudo journalctl -u ssh --no-pager
ssh fakeuser@localhost
sudo journalctl -u ssh --no-pager | tail -n 30
sudo systemctl stop ssh

## Procedure Summary

SSH service was started in a controlled environment.

SSH listening status was verified on port 22.

SSH authentication logs were inspected using journalctl.

Multiple failed login attempts were generated using a non-existent user.

Logs were reviewed again to identify authentication failure patterns.

SSH service was stopped after analysis to remove exposure.

## Observations
SSH Log Behavior

Each failed login attempt generated log entries such as:

Failed password for invalid user

PAM authentication failure

Source address appeared as ::1, which represents the IPv6 localhost.

Source ports changed between attempts due to ephemeral port allocation.

Destination service remained constant (sshd on port 22).

Failed attempts occurred within a short time window.

Source IP vs Source Port

The source IP remained constant because all attempts originated from the same host.

The source port changed on each attempt as the client OS assigned a new ephemeral port for every TCP connection.

Port variation does not indicate a different attacker; it is normal TCP behavior.

## Detection Indicators

From a defender’s perspective, brute-force behavior can be identified by:

Repeated failed authentication attempts

Same source IP (IPv4 or IPv6)

Short time intervals between attempts

Invalid or repeated usernames

Authentication-related error messages

Successful compromise is not required for detection.

## Security Takeaway

Repeated failed SSH authentication attempts provide early warning signals of brute-force activity. Even without a successful login, authentication logs reveal attacker behavior through consistent source addresses, rapid retry patterns, and authentication failures.
