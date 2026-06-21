# SYN Flood (DoS) Network Traffic Analysis

## Overview
This project is a network traffic analysis exercise completed as part of the Google Cybersecurity Certificate (Networking course). Using a captured Wireshark TCP/HTTP log, I investigated a scenario where a company's web server became unreachable, identified the responsible attack pattern, and documented the incident with root cause and mitigation recommendations.

## Scenario
A travel agency's sales webpage became unreachable, triggering a monitoring alert and connection timeout errors for employees and customers. I analyzed the corresponding Wireshark log to identify the type of attack causing the outage and explain its mechanism.

## Skills Demonstrated
- Reading and interpreting raw Wireshark TCP packet logs
- Identifying the TCP three-way handshake (SYN / SYN-ACK / ACK) and recognizing when it fails to complete
- Distinguishing a single-source DoS attack from a distributed (DDoS) attack based on traffic patterns
- Diagnosing server resource exhaustion as an attack mechanism
- Incident documentation, including root cause analysis and mitigation recommendations

## Files
- [`incident-report.md`](./incident-report.md) — full written incident analysis
- [`incident-report.pdf`](./incident-report.pdf) — PDF version of the same report

## Key Finding
A single source IP (`203.0.113.0`) sent 139 SYN packets to the web server without ever completing a single handshake, exhausting the server's pool of available connection slots. This SYN flood — a Denial of Service (DoS) attack from one source — caused legitimate user requests to time out (504 Gateway Time-out), taking the sales webpage offline for real customers and employees.
