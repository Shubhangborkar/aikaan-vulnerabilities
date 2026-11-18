# CVE-2025-57601: Shared Hard-coded SSH Private Key in AiKaan Cloud Controller Enables Device Impersonation

| Field | Value |
|---|---|
| CVE ID | [CVE-2025-57601](https://www.cve.org/CVERecord?id=CVE-2025-57601) |
| Status | **Published** (22 Sep 2025) |
| Vendor | AiKaan Labs Pvt Ltd (aikaan.io) |
| Product | AiKaan Cloud Controller (IoT/edge device management platform) |
| Affected version | v3.25.0325-5-g2e9c59796 and earlier |
| Fixed version | None published by the vendor |
| Weakness | CWE-798: Use of Hard-coded Credentials |
| CVSS v3.1 | 9.8 Critical, `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H` |
| Attack type | Remote |
| Reporter | Shubhang Borkar |

## Summary

AiKaan Cloud Controller uses one hard-coded SSH private key, tied to the username `proxyuser`, for remote terminal access to every managed IoT and edge device. The same key is reused across all customer environments. Anyone who obtains it can impersonate any managed device and open unauthorized reverse SSH tunnels.

## Affected Component

The "Open Remote Terminal" workflow. The controller sends the same static `proxyuser` private key to the target device, and the device uses it to open a reverse SSH tunnel to the remote-access server. That tunnel is what gives the administrator browser-based SSH.

## Impact

- Impersonation of any managed device toward the remote-access server.
- Unauthorized reverse SSH tunnels to devices, without the owner's consent.
- One leaked key breaks the trust boundary between the controller and every device, across all customers.
- Combined with CVE-2025-57602, it gives an interactive shell on the remote-access server and a pivot into other customers' devices.

## Proof of Concept (Sanitized)

1. In the AiKaan dashboard, start "Open Remote Terminal" for a device you control.
2. Watch the controller send the static `proxyuser` private key to that device.
3. Do the same for a second device, or from a second tenant. The same key is delivered each time.
4. Reuse the key from any host to authenticate to the remote-access server as `proxyuser`.

The private key and server addresses are not published.

## Root Cause

A single static credential is shared by all devices and tenants. There is no per-device key, no rotation and no certificate-based scoping.

## Remediation

- Issue a unique key or short-lived SSH certificate to each device and each session, through an SSH CA with expiry and principal restrictions.
- Revoke and rotate the current `proxyuser` key on every remote-access server.
- Never send long-lived private keys to devices. Generate keys on the device and send only the public part.
- Restrict `proxyuser` to port forwarding only (see CVE-2025-57602).

## Timeline

- **16 Feb 2025**: Vulnerability discovered; vendor first contacted.
- **07 May 2025**: Full technical details sent to the vendor. No response received.
- **08 Aug 2025**: Public advisory published.
- **11 Sep 2025**: CVE-2025-57601 reserved by MITRE.
- **22 Sep 2025**: CVE record published.

## Vendor Status

The vendor was notified and did not respond. No fix has been confirmed.

## Related

- [CVE-2025-57602](cve2-proxyuser-shell.md): the `proxyuser` account gets an interactive shell.

## Credits

Discovered and reported by Shubhang Borkar ([LinkedIn](https://www.linkedin.com/in/shubhangborkar), [Medium](https://shubhangborkar.medium.com)).

## References

- https://www.cve.org/CVERecord?id=CVE-2025-57601
- https://nvd.nist.gov/vuln/detail/CVE-2025-57601
- https://cwe.mitre.org/data/definitions/798.html
