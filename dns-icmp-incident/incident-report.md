# Cybersecurity Incident Report: DNS/ICMP Network Traffic Analysis

**Analyst:** Mohammad
**Incident date:** [Date of activity]
**Tool used:** tcpdump
**Affected service:** www.yummyrecipesforme.com

---

## Scenario

Customers reported they were unable to access **www.yummyrecipesforme.com**, receiving a "destination port unreachable" error after the page failed to load. As the analyst on the case, I reproduced the issue and used `tcpdump` to capture live traffic while attempting to load the page, in order to identify the root cause.

---

## Part 1: Summary of the Problem Found in the DNS and ICMP Traffic Log

**The UDP protocol reveals that:**
the browser sent a UDP packet to the DNS server (203.0.113.2) on port 53, querying for an A record to resolve the IP address of www.yummyrecipesforme.com. This query was attempted three times, each with the same result.

**This is based on the results of the network analysis, which show that the ICMP message returned the error:**
`udp port 53 unreachable`

> **Note:** the activity template refers to this as an "ICMP echo reply," but that's not technically accurate — an echo reply is the response to a ping (ICMP type 0). What the log actually shows is an ICMP **Destination Unreachable** message (type 3, code 3 — port unreachable), which is the correct term used in this report.

**The port noted in the error message is used for:**
DNS (Domain Name System) services. Port 53 is the standard port DNS servers use to receive and respond to queries.

**The most likely issue is:**
the DNS service on the server at 203.0.113.2 is down, not running, or misconfigured. The server itself is reachable on the network (it responded), but nothing is listening on port 53 to process DNS queries.

---

## Part 2: Analysis of the Data and Likely Cause of the Incident

**Time incident occurred:**
13:24:32 (1:24 p.m.), based on the first timestamp recorded in the tcpdump log.

**How the IT team became aware of the incident:**
Customers reported being unable to access www.yummyrecipesforme.com and received a "destination port unreachable" error. The analyst reproduced the issue directly and received the same error when attempting to load the site.

**Actions taken by the IT department to investigate:**
The analyst used `tcpdump` to capture live network traffic while reattempting to load the webpage, allowing inspection of the packet-level exchange between the client and the DNS server during the failed connection.

**Key findings of the investigation:**
The tcpdump log showed the client machine (192.51.100.15) sending UDP packets to the DNS server (203.0.113.2) on port 53. Instead of a normal DNS response, the server returned ICMP "destination unreachable" packets with the message `udp port 53 unreachable`, repeated across three separate query attempts. This indicates the DNS server is reachable at the network layer, but no service is bound to or listening on port 53.

**Likely cause of the incident:**
The DNS service on server 203.0.113.2 is down or improperly configured to listen on port 53 — most likely due to the DNS daemon crashing or stopping, or a firewall/configuration change blocking the port.

**Next steps:**
- Verify whether the DNS service (e.g., BIND, named) is running on 203.0.113.2
- Review service/crash logs for the DNS daemon
- Confirm firewall rules are not blocking UDP/53
- Restart or reconfigure the DNS service as needed, then re-test resolution

---

## Tools & Concepts Applied
- Packet capture and analysis with `tcpdump`
- TCP/IP model — Internet layer (IP), Transport layer (UDP)
- DNS protocol and port 53
- ICMP error messaging (Destination Unreachable, type 3 code 3)
- Network traffic-based root cause analysis
