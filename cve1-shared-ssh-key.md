# CVE Candidate: Shared SSH Private Key Across Devices

## Title
Use of Shared Hardcoded SSH Private Key in AiKaan Cloud Controller Remote Access Workflow Enables Device Impersonation

## Description
AiKaan Cloud Controller uses a single hardcoded SSH private key and the username `proxyuser` for remote terminal access to all managed IoT/edge devices.

When an administrator initiates “Open Remote Terminal” from the AiKaan dashboard, the controller sends this same static private key to the target device.  
The device then uses it to establish a reverse SSH tunnel to a remote access server, enabling browser-based SSH access for the administrator.

Because the same `proxyuser` account and SSH key are reused across all customer environments:

- An attacker who obtains the key (e.g., by intercepting it in transit, extracting it from the remote access server, or from a compromised admin account) can impersonate any managed device.  
- They can establish unauthorized reverse SSH tunnels and interact with devices without the owner’s consent.

This is a design flaw in the authentication model: compromise of a single key compromises the trust boundary between the controller and devices.

**Companion Advisory:** This issue is related to “Improper Access Control in AiKaan Cloud Controller Allows Interactive Shell Access for Reverse Tunnel User,” which describes how the `proxyuser` account can be leveraged to gain an interactive shell on the remote access server.

## Affected Systems
- AiKaan Cloud Controller v3.25.0325-5-g2e9c59796 and earlier  
- All IoT/edge devices managed by affected controllers

## Root Cause
Use of a single static SSH private key for `proxyuser` across all customers and devices, with no per-device key isolation or rotation.

## Proof of Concept (Sanitized)
1. Initiate “Open Remote Terminal” from AiKaan dashboard.  
2. Observe the controller sending the static SSH private key to the device.  
3. The device establishes a reverse SSH tunnel to the remote access server.  
4. Reuse of the same key across environments allows impersonation of devices and unauthorized tunnel creation.

## Exploitability
Confirmed in a controlled research environment. 

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
