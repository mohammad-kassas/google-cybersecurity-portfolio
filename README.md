# Mohammad — Cybersecurity Portfolio

Hi, I'm Mohammad. I'm working through the **Google Cybersecurity Certificate**, with a focus on **cloud security**, and building toward roles in the **Gulf job market**. This repository contains incident reports and security analyses completed as hands-on practice throughout the certificate, using packet capture analysis, recognized industry frameworks, and real-world attack scenarios.

Each project below includes a full written report, a README explaining the scenario and skills demonstrated, and a PDF version of the findings.

📫 **Contact:** [LinkedIn](www.linkedin.com/in/mohammad-kassas-298a39372) 
---

## Projects

### [DNS/ICMP Network Traffic Analysis](./dns-icmp-incident)
Diagnosed a DNS service outage using `tcpdump` packet capture analysis, correctly identifying an ICMP "port unreachable" error as proof the DNS server was reachable but its service was down — not a network connectivity failure.

### [SYN Flood (DoS) Attack Analysis](./syn-flood-incident)
Analyzed a raw Wireshark traffic log to independently identify a single-source SYN flood attack — counting 139 SYN packets with zero completed handshakes from one IP — and distinguished it from a distributed (DDoS) attack based on source count.

### [Brute Force Attack & Malicious Redirect](./brute-force-incident)
Reconstructed a multi-stage incident: a default admin password enabled a brute force attack, leading to malicious JavaScript injection and a redirect to a fake site distributing malware. Recommended a root-cause-targeted remediation (strong password enforcement) over a more general fix.

### [Security Risk Assessment: Network Hardening](./risk-assessment)
Matched four identified organizational vulnerabilities to the correct network hardening tools (MFA, Password Policies, Firewall Maintenance) by verifying each tool's actual function against its source documentation, rather than relying on name-matching alone.

### [NIST CSF Incident Report Analysis: ICMP Flood DoS Attack](./nist-csf-incident)
Applied the NIST Cybersecurity Framework (Identify, Protect, Detect, Respond, Recover) to a DoS incident caused by an unconfigured firewall. Identified a structural gap in the organization's response — three of four remediation measures strengthened *Protect*, with only one strengthening *Detect* — and recommended specific improvements (SIEM, alert thresholds) to close it.

---

## Skills Demonstrated Across This Portfolio
- Packet capture analysis (`tcpdump`, Wireshark) — reading raw TCP/UDP/ICMP traffic and identifying attack signatures
- TCP/IP model, DNS, and firewall fundamentals applied to real diagnostic scenarios
- Attack classification: DoS vs. DDoS, SYN flood, ICMP flood, Smurf attack, brute force
- Root-cause analysis and remediation planning, distinguishing direct fixes from general best practices
- Applying recognized frameworks (NIST CSF) to structure incident response and identify gaps
- Clear, factual incident documentation suitable for technical and non-technical stakeholders

## About This Certificate
Currently progressing through the Google Cybersecurity Certificate (Course 4: network hardening, IDS/IPS/SIEM, cloud security, and vulnerability assessment), building toward a cloud security specialization.
