# Security Audit — Botium Toys

## Overview
Internal security audit conducted for Botium Toys, a fictional small U.S. toy company experiencing rapid online growth. The audit was completed as part of the Google Cybersecurity Certificate program.

---

## Scenario
Botium Toys operates a physical store, warehouse, and growing online presence serving customers in the U.S. and E.U. The IT manager initiated an internal audit to identify security gaps, ensure compliance, and reduce risk as the business scales.

---

## What I Did
- Reviewed the company's scope, goals, and risk assessment report
- Identified all assets managed by the IT department
- Evaluated existing controls against the NIST Cybersecurity Framework (CSF)
- Completed a controls and compliance checklist (Yes/No for each control)
- Assessed compliance with PCI DSS, GDPR, and SOC standards

---

## Key Findings

### Controls Missing
- No least privilege or separation of duties
- No encryption on customer credit card data
- No intrusion detection system (IDS)
- No disaster recovery plan
- No data backups
- Weak password policy with no centralized management system

### Controls In Place
- Firewall with defined security rules
- Antivirus software monitored regularly
- Physical locks, CCTV, and fire detection
- Legacy system monitoring
- Data integrity controls

---

## Compliance Assessment

| Standard | Status |
|---|---|
| PCI DSS | ❌ Non-compliant — no encryption, no access controls on card data |
| GDPR | ⚠️ Partial — 72hr notification plan exists but data not classified or secured |
| SOC | ⚠️ Partial — data integrity exists but PII not properly protected |

---

## Recommendations
1. Implement encryption immediately for all credit card data
2. Apply least privilege — restrict employee access to only what they need
3. Install an Intrusion Detection System (IDS)
4. Create a disaster recovery plan and set up regular data backups
5. Strengthen password policy and deploy a centralized password manager
6. Classify and inventory all assets properly

---

## Frameworks Used
- NIST Cybersecurity Framework (CSF)
- PCI DSS (Payment Card Industry Data Security Standard)
- GDPR (General Data Protection Regulation)
- SOC (System and Organizations Controls)

---

*Completed as part of the Google Cybersecurity Certificate — Course 2*
