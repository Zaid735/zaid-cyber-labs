# 📄 Lab 06 – Authentication Failure Patterns (SSH)

## Objective

The objective of this lab was to understand how failed SSH authentication attempts reveal attacker behavior, why brute-force attacks are still effective even when they fail, and how defenders use authentication logs to detect malicious activity early.

##Command Used

sudo systemctl start ssh
ssh localhost
sudo journalctl -u ssh --no-pager | tail -30
sudo systemctl stop ssh

## Observations

Starting the SSH service exposed TCP port 22, allowing authentication attempts.

Multiple incorrect password attempts generated log entries such as Failed password and authentication failure.

Each failed attempt recorded valuable details including timestamp, username, and source address.

Authentication failures were logged even though no successful login occurred.

Stopping the SSH service immediately stopped further authentication attempts and logging activity

## Analysis
Why attackers brute-force SSH even when attempts fail

Attackers perform brute-force attempts to gather intelligence, such as identifying valid usernames, understanding authentication behavior, and determining whether defensive controls like rate limiting or monitoring are in place.

Why defenders focus on patterns rather than single failures

Single authentication failures are often caused by user mistakes, while repeated failures over time indicate automated or malicious behavior that requires investigation or response.

Why SSH brute-force is noisy but still effective

SSH brute-force attacks generate logs and are easy to detect, but they remain effective because many systems use weak credentials and lack active monitoring or timely response to suspicious activity.

## Security Takeaway

Failed authentication attempts are not meaningless errors; they provide attackers with reconnaissance data and provide defenders with early warning signals that allow detection and response before a compromise occurs.
