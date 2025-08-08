# CVE Candidate: proxyuser Allows Interactive Shell Access

## Title
Improper Access Control in AiKaan Cloud Controller Allows Interactive Shell Access for Reverse Tunnel User

## Description
AiKaan Cloud Controller's SSH configuration allows the `proxyuser` account, intended solely for non-interactive reverse tunneling, to obtain an interactive shell on the remote access server.  

Any actor authenticating as `proxyuser` (for example, via the shared key described in a companion advisory) can log into the server and execute arbitrary commands. This enables:

- Enumeration of authorized keys and active sessions  
- Inspection of active tunnels  
- Pivoting into connected devices  
- Disruption of remote access services

**Companion Advisory:** This issue is related to “Shared SSH Private Key Across Devices,” which describes how the `proxyuser` account can be accessed using a globally shared SSH key.

## Affected Systems
- AiKaan Cloud Controller v3.25.0325-5-g2e9c59796 and earlier

## Root Cause
SSH account intended for tunnels is granted interactive shell; no `ForceCommand`, `no-pty`, or other restrictions enforced.

## Proof of Concept (Sanitized)
1. Authenticate to the remote access server as `proxyuser` using the static private key.  
2. Observe that the account drops into an interactive shell rather than being restricted to tunneling.  
3. Execute commands, enumerate keys, and inspect active SSH tunnels.

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
