# Network Structure & Security Analysis

# Network Traffic Analysis — Cybersecurity Incident Report

## What's this?

This is a cybersecurity incident report I completed as part of the Google 
Cybersecurity Professional Certificate. The activity involved analyzing 
tcpdump network logs to identify which protocols were affected during a 
real-world style security incident.

**Protocols involved:** UDP, ICMP, DNS  
**Tools used:** tcpdump (network protocol analyzer)

---

## Scenario Summary

A client company's website (www.yummyrecipesforme.com) went down and customers 
were getting a "destination port unreachable" error. As the cybersecurity analyst 
on the case, I used tcpdump to capture and analyze the network traffic to figure 
out what was going on.

---

## Part 1: Provide a summary of the problem found in the DNS and ICMP traffic log

The UDP protocol reveals that the browser wasn't able to reach the DNS server at 203.0.113.2 on port 53. This is based on the results of the network analysis, which show that the ICMP echo reply returned the error message "udp port 53 unreachable." The port noted in the error message is used for DNS service, which is basically what translates domain names like www.yummyrecipesforme.com into IP addresses so the browser knows where to go. The most likely issue is that the DNS service on port 53 either crashed or got blocked somehow, which meant no DNS lookups could go through and the website became completely inaccessible to everyone trying to visit it.

---

## Part 2: Explain your analysis of the data and provide at least one cause of the incident

The incident occurred at 1:24 PM (13:24:32) when multiple customers started reporting that they couldn't access www.yummyrecipesforme.com and kept getting a "destination port unreachable" error. The IT team became aware of the incident through those customer reports and confirmed it when the analyst tried visiting the website themselves and got the exact same error. To investigate, the IT department loaded up tcpdump to capture and analyze the network traffic while attempting to access the site. What they found was that every UDP packet sent to the DNS server at 203.0.113.2 on port 53 kept coming back with an ICMP error message saying "udp port 53 unreachable" and this happened three times consistently in the logs, so it wasn't just a random one-time glitch. The most likely cause of the incident is that the DNS service on the server crashed or stopped running completely, which left port 53 with nothing listening on it. Another possibility is that a firewall rule got changed and started blocking incoming traffic on port 53, which would have the same effect.

