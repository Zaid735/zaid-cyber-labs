#Lab 01 & 02 – Network Basics and Attack Surface
## Objective
The goal of this lab was to understand basic network interfaces, connectivity, and how network services create and remove attack surface on a system.
## Environment
- OS: Kali Linux (VirtualBox)
- User: kali
- Network Mode: NAT

## Lab 1 – Establishing a Baseline
### Commands Used
- ip a
- ping 8.8.8.8
- ping google.com
- ss -tulnp
- nmap -sS -p 1-1000 127.0.0.1

### Observations
- The system had two main interfaces: loopback (127.0.0.1) and eth0 (10.0.2.15).
- Internet connectivity worked, and DNS resolution was verified by comparing ping to an IP address and a domain name.
- No TCP ports were listening on localhost, indicating no active network services.
## Security Takeaway
A system with no listening services has no network attack surface, meaning there are no entry points for remote connections.

## Lab 2 – Creating and Observing an Open Port

### Commands Used
- ncat -lvp 4444
- ncat 127.0.0.1 4444
- ss -tulnp | grep 4444
- nmap -p 4444 127.0.0.1
### What Happened
- A listening service was created on port 4444 using ncat.
- A client connected to the listening service, and data was successfully exchanged.
- While the service was running, the port appeared as open in both ss and nmap.
- After stopping the service, the port immediately closed.
### Security Takeaway
Network attack surface exists only while a service is actively listening. Stopping the responsible process immediately removes the exposure.

## Conclusion
This lab demonstrated how network exposure is created and removed by running services. By comparing a baseline system with no open ports to a system running a listener, it became clear that security depends on controlling processes, not just scanning ports.
