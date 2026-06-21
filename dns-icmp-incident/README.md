# DNS/ICMP Network Traffic Analysis

## Overview
This project is a network traffic analysis exercise completed as part of the Google Cybersecurity Certificate (Networking course). Using `tcpdump` packet capture data, I investigated a real-world style incident where customers were unable to reach a company website, diagnosed the root cause from the protocol-level evidence, and documented findings in a formal incident report.

## Scenario
A client company's website (www.yummyrecipesforme.com) became unreachable for customers, who received a "destination port unreachable" error. I analyzed the corresponding `tcpdump` log to determine which protocol and service were affected and identify the likely root cause.

## Skills Demonstrated
- Reading and interpreting `tcpdump` packet capture output
- Differentiating UDP query traffic from ICMP error responses
- Identifying DNS (port 53) as the affected service
- Correctly distinguishing ICMP message types (Destination Unreachable vs. Echo Reply)
- Root cause analysis and incident documentation

## Files
- [`incident-report.md`](./incident-report.md) — full written incident analysis
- [`incident-report.pdf`](./incident-report.pdf) — PDF version of the same report

## Key Finding
The DNS server (203.0.113.2) was reachable on the network, but had no service listening on UDP port 53 — meaning the DNS service itself was down or misconfigured, not a connectivity/routing issue. This was confirmed by repeated ICMP "port unreachable" responses to outbound DNS queries.
