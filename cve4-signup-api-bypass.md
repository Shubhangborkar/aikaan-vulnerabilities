# CVE-2025-52352: Unauthenticated Account Creation Through the Sign-up API When Sign-up Is Disabled (AiKaan IoT Platform)

| Field | Value |
|---|---|
| CVE ID | [CVE-2025-52352](https://www.cve.org/CVERecord?id=CVE-2025-52352) |
| Status | **Published** (21 Aug 2025) |
| Vendor | AiKaan Labs Pvt Ltd (aikaan.io) |
| Product | AiKaan IoT management platform |
| Affected version | v3.25.0325-5-g2e9c59796 and earlier |
| Fixed version | None published by the vendor |
| Weakness | CWE-862: Missing Authorization |
| CVSS v3.1 | 9.8 Critical, `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| Attack type | Remote, unauthenticated |
| Reporter | Shubhang Borkar |

## Summary

Operators of distributed deployments can "disable" public sign-up. The setting only hides the sign-up option on the login page; the sign-up API endpoint stays reachable and working. An unauthenticated attacker can call it directly to register accounts on admin portals that are meant to be closed, without any administrator approval.

## Affected Component

The user sign-up API endpoint and the server-side authorization logic behind it.

## Impact

- Unauthorized accounts on restricted admin portals.
- A foothold for further abuse. Accounts created this way can be chained with CVE-2025-57605 to take admin rights over other departments.
- Scripted mass registration of accounts.

## Proof of Concept (Sanitized)

1. Choose a deployment where sign-up is turned off (the login page shows no sign-up option).
2. Send a registration request straight to the sign-up API endpoint.
3. The account is created and can sign in to the portal.

## Root Cause

The sign-up setting is enforced only in the user interface. The server never checks it.

## Remediation

- Check the sign-up setting on the server and reject registration requests when it is off.
- Require invitation tokens or administrator approval for new accounts on restricted deployments.
- Add rate limiting and anti-automation to registration.

## Timeline

- **16 Feb 2025**: Vulnerability discovered; vendor first contacted.
- **07 May 2025**: Full technical details sent to the vendor. No response received.
- **12 Jun 2025**: CVE requested; CVE-2025-52352 reserved by MITRE.
- **08 Aug 2025**: Public advisory published.
- **21 Aug 2025**: CVE record published.

## Vendor Status

The vendor was notified and did not respond. No fix has been confirmed.

## Related

- [CVE-2025-57605](cve5-department-switch.md): escalation to admin of other departments.

## Credits

Discovered and reported by Shubhang Borkar ([LinkedIn](https://www.linkedin.com/in/shubhangborkar), [Medium](https://shubhangborkar.medium.com)).

## References

- https://www.cve.org/CVERecord?id=CVE-2025-52352
- https://nvd.nist.gov/vuln/detail/CVE-2025-52352
- https://cwe.mitre.org/data/definitions/862.html
