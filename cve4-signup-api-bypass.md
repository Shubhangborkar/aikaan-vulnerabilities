# CVE Candidate: Sign-Up API Bypass

## Title
Unauthenticated Account Creation via Exposed Sign-Up API Endpoint

## Description
AiKaan Cloud Controller exposes a sign-up API endpoint that allows unauthenticated account creation even when public sign-up is disabled via the web UI. Missing server-side authorization checks enable attackers to programmatically create accounts without administrative approval. This can be used to create multiple accounts to access restricted functionality or for fraud.

## Affected Systems
- AiKaan IoT Platform v3.25.0325-5-g2e9c59796 and earlier

## Root Cause
Lack of server-side access control for the registration endpoint

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
