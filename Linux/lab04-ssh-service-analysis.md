# Lab 04 – SSH Service Exposure and Session Monitoring

Shows how network exposure is created and removed by starting and stopping services, reinforcing that processes—not ports—create attack surface.

## Objective
The objective of this lab was to observe how enabling and disabling the SSH service affects system exposure, and how TCP connection states can be used to monitor active SSH sessions.

## Commands Used
- systemctl status ssh
- systemctl start ssh
- systemctl stop ssh
- ss -tlnp | grep 22
- ssh localhost
- ss -tanp | grep 22

## Observations
- When the SSH service was inactive, no process was listening on port 22.
- Starting the SSH service created a listening TCP port, exposing the system to remote connections.
- Establishing an SSH session resulted in an ESTABLISHED TCP connection visible using ss.
- Stopping the SSH service immediately removed the listening port and terminated exposure.


## Security Takeaway
SSH is a secure protocol by design, but enabling it unnecessarily creates a highly visible and frequently targeted attack surface that must be strictly controlled and monitored.
