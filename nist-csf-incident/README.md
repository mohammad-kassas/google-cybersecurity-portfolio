# NIST CSF Incident Report Analysis: ICMP Flood DoS Attack

## Overview
This project applies the NIST Cybersecurity Framework (CSF) — Identify, Protect, Detect, Respond, Recover — to analyze a real-world style cybersecurity incident, completed as part of the Google Cybersecurity Certificate. The analysis evaluates an organization's existing incident response, classifies its remediation steps against the correct NIST function, and identifies a gap in the organization's overall security posture.

## Scenario
A multimedia company's internal network was disrupted for two hours by an ICMP flood DoS attack, made possible by an unconfigured (unfiltered) firewall. The organization implemented four remediation measures following the incident. This report applies the NIST CSF to evaluate those measures and recommend further improvements.

## Skills Demonstrated
- Applying the NIST Cybersecurity Framework's five core functions to a real incident
- Correctly classifying remediation actions by function based on their actual mechanism (active blocking vs. passive alerting), rather than by label alone
- Identifying inconsistencies in a source scenario (DoS vs. DDoS classification) and resolving them based on the actual evidence provided
- Surfacing a structural gap in an organization's security posture (heavy investment in Protect, light investment in Detect) and recommending a specific fix (SIEM, alert thresholds)
- Self-assessment against defined completion criteria

## Files
- [`incident-report-analysis.md`](./incident-report-analysis.md) — full NIST CSF incident analysis
- [`incident-report-analysis.pdf`](./incident-report-analysis.pdf) — PDF version of the same report

## Key Finding
Of the four remediation measures the organization implemented after the incident, three were Protect-category controls (active blocking) and only one was a Detect-category control (passive monitoring). This imbalance was identified as a gap worth addressing — stronger detection capability (e.g., a SIEM tool, defined alert thresholds) would allow the organization to catch similar attacks earlier, reducing both impact and resolution time in the future.
