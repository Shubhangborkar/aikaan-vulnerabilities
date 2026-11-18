# AiKaan IoT Platform: Security Advisories

Coordinated-disclosure advisories for vulnerabilities found in the **AiKaan IoT / edge device management platform** (AiKaan Cloud Controller), v3.25.0325-5-g2e9c59796 and earlier. Each file is the public reference for its CVE record.

| CVE | Advisory | Weakness | CVSS v3.1 | Status |
|---|---|---|---|---|
| CVE-2025-57601 | [Shared hard-coded SSH private key enables device impersonation](cve1-shared-ssh-key.md) | CWE-798 | 9.8 Critical | Published 22 Sep 2025 |
| CVE-2025-57602 | [Tunnel-only `proxyuser` account gets an interactive shell](cve2-proxyuser-shell.md) | CWE-798 | 9.8 Critical | Published 22 Sep 2025 |
| CVE-2025-52351 | [Initial password sent in plaintext and in the activation URL](cve3-activation-link-password.md) | CWE-319 | 8.8 High | Published 21 Aug 2025 |
| CVE-2025-52352 | [Unauthenticated account creation through the sign-up API](cve4-signup-api-bypass.md) | CWE-862 | 9.8 Critical | Published 21 Aug 2025 |
| CVE-2025-57605 | [Escalation to admin of other departments through APIs](cve5-department-switch.md) | CWE-862 | 8.8 High | Published 22 Sep 2025 |

## Attack Chains

- **Unauthenticated user to admin of any department:** CVE-2025-52352 (register when sign-up is disabled), then CVE-2025-57605 (make yourself admin of other departments).
- **Remote access to other customers' devices:** CVE-2025-57601 (shared `proxyuser` key), then CVE-2025-57602 (interactive shell on the remote-access server and a pivot through other customers' tunnels).

## Disclosure Timeline

- **16 Feb 2025**: Vulnerabilities discovered; vendor first contacted.
- **07 May 2025**: Full technical details sent to the vendor. No response received.
- **12 Jun 2025**: First CVE requests filed with MITRE.
- **08 Aug 2025**: Public advisories published (more than 90 days after the vendor was notified).
- **21 Aug – 22 Sep 2025**: All five CVE records published.

## Guidance for Operators

No vendor fix has been confirmed. If you run AiKaan:

- Treat the `proxyuser` key as compromised.
- Restrict access to the remote-access server.
- Block the sign-up API at your reverse proxy if you don't use it.
- Review department-admin assignments for changes you didn't make.

## Responsible Disclosure Notes

- No private keys, host names, working exploits or customer data are published here.
- Testing was done in a controlled research environment, with no more access than needed to confirm each issue.

## Reporter

Shubhang Borkar: [LinkedIn](https://www.linkedin.com/in/shubhangborkar) · [Medium](https://shubhangborkar.medium.com)

## License

[MIT](LICENSE)
