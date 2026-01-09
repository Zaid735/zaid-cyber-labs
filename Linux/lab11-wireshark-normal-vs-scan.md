# Lab 11 – Wireshark: Normal Traffic vs Scan Traffic

Normal traffic is predictable and limited, while scan traffic is bursty and repetitive, making reconnaissance detectable even when connections fail

## Objective

The objective of this lab was to capture and analyze network traffic using Wireshark in order to understand the behavioral differences between normal user-generated traffic and scan-generated traffic, from a defender’s detection perspective.

## Command Used

sudo wireshark
ping -c 5 8.8.8.8
nmap -p 1-100 8.8.8.8
ip route

## Procedure Summary

Wireshark was started with root privileges to allow packet capture.

Traffic capture was performed on the active network interface (eth0).

Normal traffic was generated using a limited ICMP ping command.

Scan traffic was generated using an Nmap TCP port scan.

Separate packet captures were saved for normal and scan traffic.

Traffic patterns were compared based on timing, volume, and behavior

## Observations

### Normal Traffic (Ping)

Traffic consisted of ICMP echo requests and replies.

Packets were evenly spaced over time.

Communication targeted a single destination.

Behavior appeared predictable and human-initiated.

Even when the destination was unreachable, ICMP error messages were generated and visible.

### Scan Traffic (Nmap)

Traffic consisted of multiple TCP SYN packets.

Destination ports changed rapidly.

Packets were sent in short bursts with minimal delay.

Behavior was repetitive and mechanically generated.

Scan patterns were clearly distinguishable regardless of scan success.

## Analysis

### Behavioral Differences

Normal network traffic is typically:

low volume

predictable

directed at specific services

Scan traffic is typically:

bursty

repetitive

distributed across many ports

generated faster than human interaction

### Why Failed Traffic Still Matters

Even when network destinations are unreachable, traffic attempts still generate packets and error responses. These attempts reveal timing, frequency, and destination patterns that defenders can analyze.

Detection does not depend on successful connections; it depends on observable behavior

## Security Takeaway

Network detection relies on traffic patterns rather than payload content. Even unsuccessful communication attempts produce detectable signals that allow defenders to identify reconnaissance and scanning behavior.
