# CVE-2025-57605: Privilege Escalation to Admin of Other Departments Through Department-Assignment APIs (AiKaan IoT Platform)

| Field | Value |
|---|---|
| CVE ID | [CVE-2025-57605](https://www.cve.org/CVERecord?id=CVE-2025-57605) |
| Status | **Published** (22 Sep 2025) |
| Vendor | AiKaan Labs Pvt Ltd (aikaan.io) |
| Product | AiKaan IoT management platform |
| Affected version | v3.25.0325-5-g2e9c59796 and earlier |
| Fixed version | None published by the vendor |
| Weakness | CWE-862: Missing Authorization |
| CVSS v3.1 | 8.8 High |
| Attack type | Remote, authenticated |
| Reporter | Shubhang Borkar |

## Summary

A user who signs up through the dashboard automatically becomes admin of their own department. The APIs that assign department admins do not check whether the caller has authority over the target department. An authenticated user can read other departments' IDs from the UI, put them in the admin-assignment API request, and make themselves admin of those departments.

## Affected Component

The API endpoints that handle department switching and department-admin assignment.

## Impact

- Privilege escalation from a self-registered user to admin of any department.
- Control over the devices, users and settings of those departments.

## Proof of Concept (Sanitized)

1. Sign up through the dashboard. You become admin of your own department.
2. Find another department's ID in the UI.
3. Send the department-admin assignment API request with that ID.
4. You are now admin of the other department.

## Root Cause

There is no server-side authorization check on department-admin assignment. The server trusts the department ID the client sends.

## Remediation

- On the server, check that the caller is already an admin of the target department, or holds a global admin role.
- Do not expose other departments' IDs to users who have no access to them.
- Write an audit log of role and department changes, and alert on them.

## Timeline

- **16 Feb 2025**: Vulnerability discovered; vendor first contacted.
- **07 May 2025**: Full technical details sent to the vendor. No response received.
- **08 Aug 2025**: Public advisory published.
- **11 Sep 2025**: CVE-2025-57605 reserved by MITRE.
- **22 Sep 2025**: CVE record published.

## Vendor Status

The vendor was notified and did not respond. No fix has been confirmed.

## Related

- [CVE-2025-52352](cve4-signup-api-bypass.md): unauthenticated sign-up, which gives an attacker the first account.

## Credits

Discovered and reported by Shubhang Borkar ([LinkedIn](https://www.linkedin.com/in/shubhangborkar), [Medium](https://shubhangborkar.medium.com)).

## References

- https://www.cve.org/CVERecord?id=CVE-2025-57605
- https://nvd.nist.gov/vuln/detail/CVE-2025-57605
- https://cwe.mitre.org/data/definitions/862.html
