# Brute Force Attack & Malicious Redirect Incident Analysis

## Overview
This project is an incident analysis exercise completed as part of the Google Cybersecurity Certificate. Using a tcpdump packet capture log and a detailed incident scenario, I investigated how a former employee used a brute force attack to compromise a website's admin panel, injected malicious code to redirect visitors to a fake site, and documented the full incident with a root-cause-based remediation recommendation.

## Scenario
A former employee gained access to the yummyrecipesforme.com admin panel by brute-forcing a default administrative password, then injected malicious JavaScript that redirected visitors to a fake malware-hosting site (greatrecipesforme.com). I analyzed the tcpdump log to identify the network protocols involved, documented the full incident timeline from available evidence, and recommended a targeted security control.

## Skills Demonstrated
- Reading tcpdump logs to identify DNS, TCP handshake, and HTTP traffic
- Reconstructing a multi-stage incident timeline from log evidence and scenario reporting
- Distinguishing a captured log's scope (the symptom) from the actual root cause (the prior compromise)
- Mapping a security control recommendation directly to a root cause rather than a generic best practice
- Objective, fact-based incident documentation (avoiding emotional language, citing sources)

## Files
- [`incident-report.md`](./incident-report.md) — full written incident analysis
- [`incident-report.pdf`](./incident-report.pdf) — PDF version of the same report

## Key Finding
The compromise was made possible because the website's administrative account was left on its default password, allowing a brute force attack using commonly known default credentials. Once inside, the attacker injected malicious JavaScript to redirect visitors to a fraudulent domain hosting malware. The recommended remediation — enforcing strong, unique passwords and disallowing default credentials — targets this specific root cause directly, rather than only making the attack harder to execute.
