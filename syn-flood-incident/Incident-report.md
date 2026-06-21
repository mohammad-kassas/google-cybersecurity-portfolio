# Cybersecurity Incident Report: SYN Flood (DoS) Attack Analysis

**Analyst:** Mohammad
**Tool used:** Wireshark (TCP/HTTP packet log)
**Affected system:** Company travel agency web server (192.0.2.1), sales webpage

---

## Scenario

Employees and customers reported a connection timeout error when trying to access the company's sales webpage. An automated monitoring alert had already flagged a problem with the web server. As the analyst, I captured and analyzed TCP/HTTP traffic to and from the server using Wireshark to identify the cause.

---

## Section 1: Identify the Type of Attack

**One potential explanation for the website's connection timeout error message is:**
the web server is overwhelmed by a flood of incomplete TCP connection requests, leaving it unable to respond to legitimate traffic in time.

**The logs show that:**
the source IP `203.0.113.0` sent **139 SYN packets** to the server (`192.0.2.1`) on port 443, but never once completed the handshake by sending the final ACK. The server attempted to respond with **2 SYN-ACK** packets and eventually sent **8 RST,ACK** packets to forcibly close several of the abandoned half-open connections — but the flood of new SYN packets continued regardless.

**This event could be:**
a **Denial of Service (DoS) attack — specifically a SYN flood** — originating from a single source IP address (`203.0.113.0`) rather than a distributed network of attackers. Because the flood comes from one IP, this is classified as DoS rather than DDoS.

---

## Section 2: Explain How the Attack Is Causing the Website to Malfunction

**The three steps of a normal TCP handshake:**
1. The client sends a **SYN** packet to the server, requesting to start a connection.
2. The server responds with a **SYN-ACK** packet, acknowledging the request and agreeing to connect.
3. The client sends a final **ACK** packet back to the server, confirming the connection — at which point the connection is fully established.

**What happens when a malicious actor sends a large number of SYN packets all at once:**
The server receives each SYN packet and, following normal protocol, responds with a SYN-ACK and reserves a slot in memory to hold that connection open while it waits for the final ACK. Because the malicious actor never sends that ACK, each of these connections stays in a "half-open" state. The server has only a limited number of slots available for pending connections, so as the attacker keeps sending more SYN packets, those slots fill up faster than they can expire and be freed — eventually leaving no room for genuine connection attempts.

**What the logs indicate and how that affects the server:**
The logs show `203.0.113.0` repeatedly sending SYN packets to port 443 without ever completing the handshake, while the server attempts to keep up by issuing SYN-ACK replies and eventually RST,ACK resets. Meanwhile, legitimate users — such as the request from `198.51.100.5` — experienced a **504 Gateway Time-out**, because the server's resources were consumed managing the flood of fake half-open connections instead of being available to process real visitor requests. This is what caused the website to become unreachable and produce the connection timeout error reported in the original alert.

---

## Consequences for the Organization
- Employees and customers were unable to access the sales webpage, directly disrupting business operations.
- Potential lost sales and customer trust due to the visible outage.
- IT team resources diverted to incident response (taking the server offline, blocking the offending IP) rather than other planned work.

## Recommended Mitigation Steps
- **SYN cookies**: a server-side defense that avoids reserving memory for a connection until the handshake is cryptographically verified, preventing half-open connections from consuming resources.
- **Rate limiting**: restrict the number of SYN packets accepted per source IP within a given time window.
- **Stateful firewall / IDS tuning**: configure detection rules for abnormal patterns of incomplete handshakes from a single source.
- **IP blocking is a short-term measure only**: as noted in the original scenario, attackers can spoof or rotate IP addresses to bypass a simple block, so this should be paired with the defenses above rather than relied on alone.

---

## Tools & Concepts Applied
- TCP three-way handshake (SYN, SYN-ACK, ACK)
- Packet capture and analysis with Wireshark
- DoS vs. DDoS classification based on source IP count
- Server resource exhaustion as an attack mechanism
- Incident root cause analysis and mitigation planning
