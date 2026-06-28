# Incident Report Analysis: ICMP Flood DoS Attack (NIST CSF)

**Analyst:** Mohammad
**Framework applied:** NIST Cybersecurity Framework (CSF) — Identify, Protect, Detect, Respond, Recover
**Organization:** Multimedia company (web design, graphic design, social media marketing services)

---

## Summary

The organization experienced a Denial of Service (DoS) attack that disrupted its internal network for two hours. Network services suddenly stopped responding due to an incoming flood of ICMP packets, which prevented normal internal traffic from accessing network resources. Investigation determined that a malicious actor sent the flood of ICMP pings through an unconfigured firewall, exploiting the lack of any traffic-filtering rules. The incident management team responded by blocking incoming ICMP packets, taking non-critical services offline, and restoring critical services, resolving the immediate disruption within two hours.

**Note on classification:** the scenario refers to this incident as both a "DoS attack" and a "distributed denial of service (DoS) attack." Based on the details provided — a single malicious actor, with no indication of multiple distributed source IPs — this incident is classified here as a **DoS attack**, not a DDoS attack. A true DDoS would require evidence of traffic originating from multiple distributed sources, which is not described in this scenario.

---

## Identify

**Technology/Assets affected:** The organization's firewall (which had no configured filtering rules) and the broader internal network and its connected services. The flood of ICMP traffic passed unfiltered through the firewall, consuming network resources and rendering internal services unreachable.

**Attack path:** A malicious actor sent a high volume of ICMP echo request packets into the network. Because the firewall had no rules in place to filter or rate-limit this traffic, the flood reached the internal network directly and overwhelmed it, consistent with an ICMP flood–based DoS attack.

**Business processes affected:** All internal network-dependent operations were disrupted for the duration of the incident, as normal traffic could not reach any network resources. Non-critical services were deliberately taken offline as part of the response, further limiting business operations until resolution.

**People needing access:** IT/network security staff and the incident management team required access to the firewall and network infrastructure to diagnose and resolve the issue.

---

## Protect

Three of the four remediation measures implemented after this incident are Protect-category safeguards — controls that actively block or limit malicious traffic before it can cause harm, rather than simply alerting staff to its presence:

- **Firewall rate-limiting rule:** restricts the volume of incoming ICMP packets the firewall will allow through, directly preventing a repeat flood of this scale and type.
- **Source IP address verification:** checks incoming ICMP packets for spoofed source addresses, helping block traffic from disguised or illegitimate sources before it can reach internal systems.
- **IDS/IPS filtering:** actively filters out ICMP traffic matching suspicious characteristics, preventing it from reaching the internal network — this is the IPS (prevention) function specifically, since it actively blocks traffic rather than only generating an alert.

**Additional recommended safeguard:** the root cause of this incident was an unconfigured firewall with no traffic-filtering rules in place at all. Beyond the ICMP-specific rules already implemented, the organization should conduct a full firewall configuration review and establish a documented baseline (see baselining, covered earlier in this course) to ensure no other protocols or ports are similarly left unfiltered.

---

## Detect

Only one of the four implemented measures falls into the Detect category:

- **Network monitoring software:** monitors for abnormal traffic patterns and alerts staff, rather than blocking traffic directly.

This represents a relative gap in the organization's response — three controls were added to actively block future attacks, but only one was added to help staff *notice* unusual activity early, before it escalates. To strengthen detection further, the organization should consider:
- Implementing a SIEM tool to aggregate logs from the firewall, IDS/IPS, and monitoring software into a single dashboard, making anomalies easier to spot across multiple sources at once.
- Establishing alert thresholds specifically for ICMP traffic volume, so unusual spikes trigger an immediate notification rather than relying solely on post-incident review.
- Regularly auditing firewall logs and configurations to confirm filtering rules remain correctly applied over time (tying back to the baselining concept).

---

## Respond

**Response plan for similar future incidents:**
- **Containment:** Immediately apply or verify rate-limiting and IP-verification rules on the firewall for the traffic type involved; take non-critical services offline if needed to preserve resources for critical systems, as was done in this incident.
- **Communication:** Notify IT staff and relevant stakeholders as soon as abnormal traffic is detected, and provide affected end users with status updates until service is restored.
- **Analysis:** Use firewall logs, IDS/IPS alerts, and network monitoring data to confirm the attack type (e.g., DoS vs. DDoS, protocol involved) before finalizing the response, rather than assuming based on initial symptoms alone.
- **Mitigation:** Block or rate-limit the offending traffic type at the firewall, and isolate any affected non-critical systems to prevent resource exhaustion from spreading to critical services.
- **Improvement:** After each incident, review whether existing Protect and Detect controls performed as expected, and update firewall rules, monitoring thresholds, or IDS/IPS signatures accordingly.

---

## Recover

**Recovery plan:**
- **Immediate recovery needs:** Confirm which non-critical services were taken offline during the incident and verify each one individually before restoring it, to avoid reintroducing the same vulnerability.
- **Recovery process:** Restore critical services first (as was done during this incident), followed by non-critical services once the firewall rules and filtering controls have been confirmed effective.
- **Process improvements:** Document the full incident timeline and root cause (unconfigured firewall) so future recovery efforts can reference a clear baseline of what "normal, secure" configuration should look like.
- **Communication:** Inform affected internal teams and any impacted clients once full service has been restored, along with a brief summary of the cause and the steps taken to prevent recurrence.

---

## Reflections / Notes

This incident highlights how a single missing control — firewall traffic filtering — created an exploitable gap despite the organization otherwise operating normally. Applying the NIST CSF surfaced an important imbalance in the response: three of the four new safeguards strengthen **Protect**, while only one strengthens **Detect**. Future security planning for this organization should prioritize closing that detection gap, since earlier detection could reduce both the impact and duration of similar incidents going forward.

---

## Self-Assessment

| # | Criterion | Met? |
|---|---|---|
| 1 | Includes a summary of the incident | Yes |
| 2 | Identifies the type of attack and extent of the incident, including affected devices/systems | Yes |
| 3 | Offers a plan to protect the network from future incidents | Yes |
| 4 | Describes methods for detecting security events in the future | Yes |
| 5 | Outlines a response process for similar future incidents | Yes |
| 6 | Lists procedures to recover from a similar security event | Yes |

**Result: 6/6 criteria met.**
