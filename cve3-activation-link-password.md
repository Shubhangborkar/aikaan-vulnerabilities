# CVE Candidate: Password in Activation Link

## Title
Exposure of Initial Account Password in Activation Link via Query Parameter

## Description
The onboarding flow for AiKaan Cloud Controller sends initial account passwords embedded as query parameters in activation links. These links are delivered over email and, if intercepted or stored (server logs, browser history, proxy logs), expose the cleartext password. An attacker who accesses the link from logs, caches, or other stored copies can obtain the initial password and fully compromise the account.

## Affected Systems
- AiKaan IoT Platform v3.25.0325-5-g2e9c59796 and earlier

## Root Cause
Insecure credential transmission via URL query parameters; lack of single-use tokens

## Exploitability
Confirmed (tested in a controlled research environment).  

## Timeline
- **16 Feb 2025** — Vulnerability discovered  
- **07 May 2025** — Vendor notified (no response received)  
- **08 Aug 2025** — Public disclosure

## Reporter
Shubhang Borkar — [https://shubhangborkar.medium.com](https://shubhangborkar.medium.com)

## References
- This public advisory (this file)  

## Vendor Status
Vendor notified but has not responded or confirmed a fix at the time of publication.
