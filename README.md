# Mapping My Network Path (Campus Network)

## Goal
Trace and document the path my laptop's traffic takes to reach the internet
while connected to Algonquin College's WiFi, using only passive, read-only
tools. Since this is a shared network I don't administer, I intentionally
avoided active scanning tools (like nmap) that probe other devices.

## Tools Used
- `ipconfig /all` — laptop's own IP and default gateway
- `arp -a` — locally cached device info (read-only, no probing)
- `tracert 8.8.8.8` — hop-by-hop path to Google's public DNS

## What I Found
My laptop's traffic reaches the campus gateway (`10.70.192.1`), then
Algonquin College's own border router (`205.211.42.150`), then passes
through 8 hops that don't reply to the trace — those routers are
configured to silently drop ICMP probes rather than respond, which is
normal behavior and doesn't mean the path is broken. Traffic successfully
reaches the destination, `dns.google` (`8.8.8.8`), at hop 11.



## What I Learned
- The difference between passive tools (arp, ipconfig) and active ones
  (nmap) 
- A `*` timeout in traceroute doesn't mean a router is broken — many
  routers just don't respond to ICMP by policy, while still forwarding
  real traffic fine.
- How to read a full ipconfig/tracert output and turn it into a diagram.
