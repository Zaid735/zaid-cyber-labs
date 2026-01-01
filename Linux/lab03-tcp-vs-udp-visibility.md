# Lab 03 – TCP vs UDP Visibility and Security Implications

## Objective
The objective of this lab was to understand the behavioral differences between TCP and UDP, specifically how each protocol exposes connection information and how that affects detection and monitoring from a security perspective.

## Commands Used
- ss -tulnp
- ss -ulnp
- ss -tanp
- ncat -lvp 4444
- ncat 127.0.0.1 4444
- ncat -u -lvp 5555
- ncat -u 127.0.0.1 5555


## Observations
- TCP listeners appear in a LISTEN state and show ESTABLISHED connections when a client is connected.
- UDP listeners appear as UNCONN and do not show session or connection state even when data is exchanged.
- TCP provides clear visibility into active sessions, while UDP provides minimal visibility.

## Security Takeaway
Although both TCP and UDP can expose services, TCP provides session visibility that defenders can monitor, while UDP’s stateless nature makes activity harder to track and easier to abuse for stealthy communication.

