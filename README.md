<<<<<<< HEAD
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
=======
# CyberPath Advisor — Full Project

Two separate folders, two separate servers:

```
cyberpath-backend/     Express API (port 5000) — scoring, career mapping, AI features
cyberpath-frontend/    Next.js + Tailwind app (port 3000) — all 8 screens + mascot
```

## Quick start (two terminals)

**Terminal 1 — backend:**
```bash
cd cyberpath-backend
npm install
cp .env.example .env
# edit .env — add your ANTHROPIC_API_KEY
npm run dev
```
Runs at `http://localhost:5000`. Check `curl http://localhost:5000/api/health`.

**Terminal 2 — frontend:**
```bash
cd cyberpath-frontend
npm install
cp .env.local.example .env.local
npm run dev
```
Runs at `http://localhost:3000`. The `NEXT_PUBLIC_API_URL` in `.env.local`
already points at `http://localhost:5000` — change it if you deploy the
backend somewhere else.

**Backend must be running before you open the frontend** — the assessment
page fetches quiz questions from it on load.

## The 8 screens (all built)

| Screen | Route | What it does |
|---|---|---|
| Landing | `/` | Hero + mascot greeting + "Get started" |
| Registration | `/register` | Name + email, saved locally |
| Interest Selection | `/interests` | Pick a track (or "not sure") |
| Assessment | `/assessment` | Step-through quiz, pulled live from the backend |
| Dashboard | `/dashboard` | Score bars across all 5 tracks |
| Career Recommendation | `/recommendation` | Best-fit role + AI explanation |
| Roadmap | `/roadmap` | Weekly plan + certificate generation |
| Mentor | `/mentor` | Curated free communities |

Data flows through the pages via `localStorage` (see `lib/storage.js`) —
no auth, no database needed, which keeps this buildable in a few hours.

## The mascot

`components/Mascot.js` — "Cy" is a hand-built SVG character (no image
assets to manage) that pops in with a bounce, waves continuously, and
opens a speech bubble with a page-specific message a moment after landing.
Click Cy anytime to reopen the bubble if dismissed.

It's on every page with a message tuned to that screen — encouragement
during the assessment, a personalized greeting on the dashboard once the
student's name is known, etc. This is the one deliberately playful,
high-motion element; everything else in the design stays calm around it
so Cy is what people remember.

## Design system

Rounded, warm, "student-friendly" — not the generic AI-app look:
- **Palette:** soft off-white background, navy for headings/dark panels,
  coral for primary actions, mint/sky/lilac/amber for track-score variety
- **Type:** Fredoka (rounded, friendly) for headings, Inter for body text
- **Shape language:** big radius corners, soft shadows, chip-style buttons

## Known simplifications (call these out if judges ask)

- **Auth:** none — state lives in the browser via `localStorage`. Fine for
  a demo; would need real accounts for production.
- **Resume upload:** the backend has `/api/resume-analysis` ready, but
  it's not wired into a frontend screen yet — parsing PDFs client-side
  was cut for time. Paste-box text input would be the fastest way to add
  it if there's time left.
- **Known skills for gap analysis:** currently passed as an empty list
  (`knownSkills: []`) when building the roadmap, so the AI works from the
  track's full requirement list. A nice next step: derive known skills
  from quiz answers with a strong score in a category.
- **Certificate:** SVG, not PDF — intentional, keeps the build dependency-free.

## Testing the backend independently

```bash
curl http://localhost:5000/api/quiz
curl -X POST http://localhost:5000/api/score \
  -H "Content-Type: application/json" \
  -d '{"answers":[{"questionId":"q1","optionIndex":2}]}'
```
>>>>>>> 532bde40b018f521bd0ede426319a5ce0eda54fc
