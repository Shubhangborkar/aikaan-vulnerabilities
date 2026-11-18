# CVE-2025-57602: Tunnel-Only `proxyuser` Account Gets an Interactive Shell on the AiKaan Remote-Access Server

| Field | Value |
|---|---|
| CVE ID | [CVE-2025-57602](https://www.cve.org/CVERecord?id=CVE-2025-57602) |
| Status | **Published** (22 Sep 2025) |
| Vendor | AiKaan Labs Pvt Ltd (aikaan.io) |
| Product | AiKaan Cloud Controller / IoT management platform |
| Affected version | v3.25.0325-5-g2e9c59796 and earlier |
| Fixed version | None published by the vendor |
| Weakness | CWE-798: Use of Hard-coded Credentials (combined with an unrestricted SSH account) |
| CVSS v3.1 | 9.8 Critical, `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| Attack type | Remote |
| Reporter | Shubhang Borkar |

## Summary

The `proxyuser` SSH account on AiKaan's remote-access server is meant only for non-interactive reverse tunnels, yet it is given a full interactive shell. Anyone who signs in as `proxyuser` with the shared key from CVE-2025-57601 can run commands on the server, inspect other customers' tunnels and pivot into their devices.

## Affected Component

The SSH configuration of the remote-access server: the `proxyuser` account and its `authorized_keys` entry.

## Impact

- Arbitrary command execution on the remote-access server.
- Enumeration of authorized keys, active sessions and live tunnels for all customers.
- Pivoting through existing tunnels into other customers' IoT and edge devices, which allows remote code execution there.
- Disruption of the remote-access service for every tenant.

## Proof of Concept (Sanitized)

1. Authenticate to the remote-access server as `proxyuser` with the shared key from CVE-2025-57601.
2. The session opens an interactive shell instead of being limited to port forwarding.
3. List the active tunnels and listening ports. Each one belongs to a connected customer device that can be reached from this shell.

Host names, keys and tenant data are not published.

## Root Cause

The tunnel account has no SSH restrictions. There is no `ForceCommand`, `no-pty`, `permitlisten`/`permitopen` limit or restricted shell, and there is no isolation between tenants.

## Remediation

- In `sshd_config` or in `authorized_keys` options, restrict the account to forwarding only: `restrict,port-forwarding,permitlisten="…"`, `ForceCommand /bin/false` (or a no-op), and `PermitTTY no`.
- Set the account's login shell to `nologin`.
- Separate tenants: use a dedicated tunnel endpoint or listening namespace for each customer.
- Fix CVE-2025-57601 (the shared key) at the same time.

## Timeline

- **16 Feb 2025**: Vulnerability discovered; vendor first contacted.
- **07 May 2025**: Full technical details sent to the vendor. No response received.
- **08 Aug 2025**: Public advisory published.
- **11 Sep 2025**: CVE-2025-57602 reserved by MITRE.
- **22 Sep 2025**: CVE record published.

## Vendor Status

The vendor was notified and did not respond. No fix has been confirmed.

## Related

- [CVE-2025-57601](cve1-shared-ssh-key.md): the shared hard-coded SSH key that grants `proxyuser` access.

## Credits

Discovered and reported by Shubhang Borkar ([LinkedIn](https://www.linkedin.com/in/shubhangborkar), [Medium](https://shubhangborkar.medium.com)).

## References

- https://www.cve.org/CVERecord?id=CVE-2025-57602
- https://nvd.nist.gov/vuln/detail/CVE-2025-57602
- https://cwe.mitre.org/data/definitions/798.html
