# Security Risk Assessment: Social Media Data Breach

## Overview
This project is a security risk assessment completed as part of the Google Cybersecurity Certificate. Given a scenario where a social media organization suffered a data breach due to four identified network vulnerabilities, I selected and justified three network hardening tools to address all four weaknesses.

## Scenario
A social media organization experienced a data breach that exposed customer personal information. Inspection of the network revealed four vulnerabilities: shared employee passwords, a default database admin password, an unconfigured firewall with no traffic filtering rules, and no multifactor authentication in use anywhere on the network.

## Skills Demonstrated
- Mapping security vulnerabilities to the specific hardening tool that addresses their root cause (rather than picking tools based on surface-level name matching)
- Recognizing when a single tool (MFA) can address multiple vulnerabilities simultaneously, for an efficient and well-justified recommendation set
- Applying defense-in-depth reasoning across multiple, distinct security controls
- Referencing current password security guidance (NIST recommendations on salting/hashing vs. complexity rules)

## Files
- [`security-risk-assessment.md`](./security-risk-assessment.md) — full written risk assessment
- [`security-risk-assessment.pdf`](./security-risk-assessment.pdf) — PDF version of the same report

## Key Finding
Three hardening measures — Multifactor Authentication (MFA), Password Policies, and Firewall Maintenance — together address all four identified vulnerabilities. MFA was selected specifically because it mitigates both the password-sharing risk and the missing-MFA gap at once, making it the most efficient single control in the recommendation set.
