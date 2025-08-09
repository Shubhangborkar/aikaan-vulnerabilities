# CVE Candidate: Department Admin Privilege Escalation via API

## Title
Unauthorized Elevation to Department Admin via API Manipulation

## Description
AiKaan IoT Platform allows users who sign up via the dashboard to be automatically assigned as admin of their own department. However, by abusing exposed APIs, an authenticated user can obtain the ID of other departments from the UI and manipulate the API to transfer themselves as admin of those departments without authorization. This lack of server-side validation permits privilege escalation across departments.

## Affected Systems
- AiKaan IoT Platform v3.25.0325-5-g2e9c59796 and earlier

## Root Cause
Missing server-side authorization checks on API endpoints handling department admin assignments

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
