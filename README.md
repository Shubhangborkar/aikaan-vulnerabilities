# AiKaan IoT Platform — Vulnerability Report Collection

This repository contains responsible-disclosure technical advisories for multiple security issues discovered in AiKaan (https://www.aikaan.io) IoT Platform (v3.25.0325-5-g2e9c59796 and earlier). These advisories are intended as public references for CVE requests and coordinated disclosure.

Repository contents:
- cve1-shared-ssh-key.md        — Shared SSH private key used across devices (CVE candidate)
- cve2-proxyuser-shell.md       — Interactive shell access for tunnel user (CVE candidate)
- cve3-activation-link-password.md — Initial account password exposed in activation link (CVE candidate)
- cve4-signup-api-bypass.md     — Unauthenticated account creation via exposed sign-up API (CVE candidate)
- cve5-department-switch.md     — Unauthorized Elevation to Department Admin via API Manipulation (CVE candidate)


Author / Reporter:
- Shubhang Borkar — https://shubhangborkar.medium.com

Disclosure timeline:
- Discovery: 16 Feb 2025
- Vendor notified: 7 May 2025
- Public disclosure: 8 Aug 2025

Notes:
- Sensitive artifacts have been redacted. No production private keys or customer-sensitive data are published here.
- You may use these advisories as public references for CVE requests. Each CVE request should link to the specific markdown file addressing that vulnerability.
