# Network-Services-Configuration-in-Linux
Configuration of a Corporate and Caching DNS Server Using BIND and Unbound
# DNS Lab: Bind9 and Unbound

## Project Description

In this project, I deployed and configured a DNS infrastructure on Linux consisting of an authoritative DNS server using Bind9 and a caching DNS server using Unbound, and verified their operation from client machines.

## What Was Done

### Bind9 (Authoritative DNS)

- Installed and configured Bind9
- Created a DNS zone:
  ```
  <>.local
  ```
- Configured a reverse lookup zone for the VM subnet
- Added DNS records:
  - A record: `www.<>.local` → web server IP
  - PTR record: reverse DNS for the web server IP
- Started a web server on the second VM:
  ```bash
  python3 -m http.server
  ```
- Configured the client machine to use the Bind server as its DNS resolver
- Verified DNS resolution using a browser and nslookup

### Unbound (Caching DNS)

- Installed and configured Unbound
- Created the configuration file:
  ```
  /etc/unbound/unbound.conf.d/main.conf
  ```
- Freed port 53 by disabling the systemd-resolved DNS stub listener
- Configured:
  - DNS query caching
  - IPv4-based resolution
  - Client access to the DNS server
- Tested DNS performance using dig:
  - first query — uncached (slower)
  - repeated query — cached (faster)

## Technologies Used

- Linux (Ubuntu)
- Bind9
- Unbound
- systemd-resolved
- dig / nslookup
- DNS, TCP/IP

## Result

Configured:
- an authoritative DNS server for an internal domain
- a caching DNS server that reduces DNS query latency for clients
