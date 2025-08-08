# AiKaan Cloud Controller — Vulnerability Report Collection

This repository contains responsible-disclosure technical advisories for multiple security issues discovered in AiKaan Cloud Controller (v3.25.0325-5-g2e9c59796 and earlier). These advisories are intended as public references for CVE requests and coordinated disclosure.

Repository contents:
- cve1-shared-ssh-key.md        — Shared SSH private key used across devices (CVE candidate)
- cve2-proxyuser-shell.md       — Interactive shell access for tunnel user (CVE candidate)
- cve3-activation-link-password.md — Initial account password exposed in activation link (CVE candidate)
- cve4-signup-api-bypass.md     — Unauthenticated account creation via exposed sign-up API (CVE candidate)
- poc/                          — sanitized proof-of-concept files and examples
- screenshots/                   — sanitized screenshots (redacted)

Author / Reporter:
- Shubhang Borkar (independent security researcher) — https://github.com/<your-github-username> or https://medium.com/@shubhangborkar

Disclosure timeline:
- Discovery: [INSERT DISCOVERY DATE]
- Vendor notified: [INSERT DATES and method — email/ticket]
- Public disclosure: [INSERT PUBLICATION DATE]

Notes:
- Sensitive artifacts have been redacted. No production private keys or customer-sensitive data are published here.
- You may use these advisories as public references for CVE requests. Each CVE request should link to the specific markdown file addressing that vulnerability.
