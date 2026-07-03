# Network Attack Analysis — SYN Flood Attack Report

## What's this?

This is a cybersecurity incident report I completed as part of the Google
Cybersecurity Professional Certificate. The activity involved analyzing
Wireshark TCP/HTTP logs to identify a network attack that was causing a
company's web server to go down.

**Type of attack:** DoS SYN Flood Attack  
**Tools used:** Wireshark (network protocol analyzer)

---

## Scenario Summary

I work as a security analyst for a travel agency. One afternoon, an automated
alert came in saying there was a problem with the web server. When I tried to
visit the company's website, I got a connection timeout error. I used a packet
sniffer to capture the traffic going to and from the web server and spotted a
massive number of TCP SYN requests coming from one unfamiliar IP address. The
server was getting so overwhelmed it couldn't keep up with normal traffic anymore.

---

## Section 1: Identify the type of attack that may have caused this network interruption

One potential explanation for the website's connection timeout error is a DoS
SYN flood attack. The logs show that starting around log entry 52, a single IP
address (203.0.113.0) began sending a huge and continuous stream of TCP SYN
requests to the web server at 192.0.2.1 on port 443. Unlike normal visitors
who complete the full three-way handshake, this IP just kept hammering the
server with SYN packets without ever finishing the connection. By log entry 125,
the server had completely stopped responding to legitimate employee traffic and
was only logging the attacker's requests. This event is a direct DoS SYN flood
attack since it's coming from a single source IP address rather than multiple
locations.

---

## Section 2: Explain how the attack is causing the website to malfunction

When website visitors try to connect to the web server, a three-way handshake
happens using the TCP protocol. First, the visitor's browser sends a SYN packet
to the server to request a connection. Second, the server responds with a SYN-ACK
packet, basically saying "okay, I got your request, let's connect" and reserves
resources for that connection. Third, the visitor sends back an ACK packet to
confirm the connection is established and they can start communicating.

What happens when a malicious actor sends a massive number of SYN packets all
at once is that the server tries to respond to every single one of them with a
SYN-ACK and reserves resources for each connection, waiting for the final ACK
that never comes. The server's resources get eaten up fast because it's holding
open all these half-finished connections while still getting bombarded with more
SYN requests.

The logs show exactly this happening in real time. Early on, the attacker's SYN
requests were being answered normally by the server (log entries 52-54) and
legitimate employees could still connect and load the sales page just fine. But
as the attack kept going, the server started struggling to handle both the flood
of fake SYN requests and real employee traffic at the same time. By log entry 73,
legitimate visitors started getting RST-ACK packets and 504 Gateway Timeout errors
instead of actually loading the page. From log entry 125 onwards, the server
completely stopped responding to anyone except logging the attacker's SYN packets
coming in. The web server was fully overwhelmed and employees could no longer
access the company website at all.

---

## What I Learned

This activity showed me how a SYN flood attack works in practice by actually
reading through the Wireshark logs and watching the attack unfold entry by entry.
It also reinforced why monitoring tools and automated alerts are so important —
the attack was caught because of an automated alert, not someone manually noticing
the site was down. Without that, the server could have been down way longer before
anyone noticed.
