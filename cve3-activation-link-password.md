# CVE-2025-52351: Initial Account Password Sent in Plaintext and in the Activation URL (AiKaan IoT Platform)

| Field | Value |
|---|---|
| CVE ID | [CVE-2025-52351](https://www.cve.org/CVERecord?id=CVE-2025-52351) |
| Status | **Published** (21 Aug 2025) |
| Vendor | AiKaan Labs Pvt Ltd (aikaan.io) |
| Product | AiKaan IoT management platform |
| Affected version | v3.25.0325-5-g2e9c59796 and earlier |
| Fixed version | None published by the vendor |
| Weakness | CWE-319: Cleartext Transmission of Sensitive Information (see also CWE-598: Use of GET Request Method With Sensitive Query Strings) |
| CVSS v3.1 | 8.8 High, `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H` |
| Attack type | Remote |
| Reporter | Shubhang Borkar |

## Summary

During onboarding, the platform emails each new user their generated password in plaintext. The same password is also placed as a query parameter in the account-activation URL. Browser history, proxy and server access logs, referrer headers and email caches can all keep copies of it, so anyone who can read those logs or caches can recover the password and take over the account.

## Affected Component

The user-onboarding and account-activation flow (the email template and the activation endpoint).

## Impact

- The credentials of newly onboarded users, including administrators, are exposed.
- Full account takeover for anyone who can read the relevant logs, caches or mailbox.

## Proof of Concept (Sanitized)

1. Have an administrator invite a new user.
2. The invitation email shows the generated password in plaintext, and the activation link contains the same password as a query parameter.
3. Open the link. The full URL, password included, is recorded in browser history and in the access logs of any proxy or web server on the path.

## Root Cause

A credential is sent through channels that keep it (email body, URL query string) instead of through a single-use, short-lived activation token.

## Remediation

- Send a single-use, time-limited activation token and have the user choose their own password at first login.
- Never put credentials or secrets in URLs. Send sensitive values in POST bodies over TLS.
- Expire any password that was delivered by email, and force a reset at first login.

## Timeline

- **16 Feb 2025**: Vulnerability discovered; vendor first contacted.
- **07 May 2025**: Full technical details sent to the vendor. No response received.
- **12 Jun 2025**: CVE requested; CVE-2025-52351 reserved by MITRE.
- **08 Aug 2025**: Public advisory published.
- **21 Aug 2025**: CVE record published.

## Vendor Status

The vendor was notified and did not respond. No fix has been confirmed.

## Credits

Discovered and reported by Shubhang Borkar ([LinkedIn](https://www.linkedin.com/in/shubhangborkar), [Medium](https://shubhangborkar.medium.com)).

## References

- https://www.cve.org/CVERecord?id=CVE-2025-52351
- https://nvd.nist.gov/vuln/detail/CVE-2025-52351
- https://cwe.mitre.org/data/definitions/319.html
- https://cwe.mitre.org/data/definitions/598.html
