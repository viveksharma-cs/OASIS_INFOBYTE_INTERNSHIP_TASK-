# Basic Network Scanning with Nmap

## Overview
This project documents a hands-on network scanning exercise using
**Nmap** against a local Kali Linux virtual machine, covering basic
port scanning, service version detection, and OS fingerprinting,
along with a security analysis of the discovered services.

## What is Nmap?
Nmap ("Network Mapper") is a free, open-source tool used to discover
hosts and services on a computer network. It works by sending
specially crafted packets to target machines and analyzing the
responses to determine:
- Which hosts are up and reachable
- Which ports are open, closed, or filtered on those hosts
- What services and software versions are running on open ports
- What operating system a host is likely running

It's one of the most widely used tools in both offensive security
(reconnaissance) and defensive security (auditing your own network).

## Why Network Scanning Matters
Network scanning is a foundational security practice for several
reasons:
- **Asset discovery** — you can't secure what you don't know exists.
  Scanning reveals every device and service actually running on a
  network, which is often more than administrators expect.
- **Attack surface reduction** — identifying open ports and running
  services shows exactly what could potentially be attacked, so
  unnecessary services can be shut down.
- **Vulnerability assessment** — knowing the exact service and
  version running on a port lets you check it against known CVEs.
- **Configuration verification** — scanning confirms whether
  firewall rules and access controls are actually working as
  intended, rather than assuming they are.
- **Compliance and auditing** — many security standards require
  regular network scanning as part of ongoing risk management.

## Installation

Nmap comes pre-installed on Kali Linux. To verify or install it
manually on any Debian-based system:

```bash
sudo apt update
sudo apt install nmap -y
nmap --version
```

## Scans Performed

| Scan Type            | Command                    | Purpose                                      |
|-----------------------|-----------------------------|-----------------------------------------------|
| Basic scan             | `nmap 127.0.0.1`            | Identify open ports on the default top 1000  |
| Service version scan   | `nmap -sV 127.0.0.1`        | Identify the software/version behind each port |
| OS detection scan      | `sudo nmap -O 127.0.0.1`    | Fingerprint the likely operating system       |

Full output and the resulting security analysis are documented in
[`nmap_scan_results.txt`](./nmap_scan_results.txt).

## Findings Summary
Two services were found running on the target: **SSH (port 22)**
and **HTTP via Apache (port 80)**. Both are common, well-understood
services whose risk level depends heavily on configuration (e.g.
whether SSH allows password login, whether HTTP traffic is
encrypted). Full per-port analysis is in the results file.

## Screenshots
Screenshots of terminal output for each scan are included in the
`/screenshots` folder of this repository.

## ⚠️ Ethical Use Guidelines
Network scanning must only ever be performed against systems you
**own** or have **explicit, documented permission** to test.
Unauthorized scanning of networks or systems you do not control can
be illegal under computer misuse laws in most jurisdictions, even
when no damage is done.

For this project:
- Only a personally owned/controlled virtual machine (Kali Linux,
  running locally in VirtualBox) was scanned.
- No external, production, or third-party systems were scanned at
  any point.
- All scans were performed for educational purposes as part of a
  coursework assignment.

**Rule of thumb:** if you don't own it, and nobody has given you
written permission to scan it, don't scan it.
