# Security Hardening

## Overview

This document describes the basic security hardening activities performed during the Wazuh lab.

The hardening activities focused on reducing unnecessary exposure, securing the Wazuh environment, reviewing system updates, and validating Wazuh rules and log processing.

---

## Hardening Objectives

The hardening activities focused on:

- Securing default Wazuh credentials
- Restricting network access to required ports
- Reviewing Wazuh release and update information
- Testing Wazuh rules and log processing
- Applying basic security practices within the lab environment

---

## Wazuh Credential Hardening

The default Wazuh passwords were changed as part of the security hardening activities.

This reduced the risk associated with leaving default credentials unchanged within the Wazuh environment.

Credential changes were performed as part of the initial security configuration of the Wazuh deployment.

---

## Firewall Configuration

UFW (Uncomplicated Firewall) was used to restrict network access to required Wazuh ports.

The firewall configuration was reviewed to limit access to trusted IP addresses rather than allowing unnecessary network exposure.

This provided an additional layer of protection for the Wazuh environment.

---

## System and Wazuh Updates

Wazuh release information and update recommendations were reviewed during the lab.

Keeping the security monitoring environment updated helps ensure that the deployed components remain aligned with available releases and security improvements.

Updates were considered as part of the ongoing maintenance and hardening process.

---

## Wazuh Log Testing

The Wazuh `logtest` utility was used to test how log entries are processed and which rules are triggered.

The following command was used:

```bash
sudo /var/ossec/bin/wazuh-logtest
````

The tool provided a way to validate log decoding and rule matching before relying on the resulting alerts during monitoring activities.

This was particularly useful when working with Wazuh rules and analyzing security events.

---

## Hardening Approach

The hardening activities followed a basic security approach:

```text
Review Configuration
        │
        ▼
Secure Credentials
        │
        ▼
Restrict Network Access
        │
        ▼
Review Updates
        │
        ▼
Test Log Processing
```

The objective was to improve the security of the monitoring environment while maintaining the functionality required for the lab exercises.

---

## Key Lessons Learned

The hardening activities demonstrated the importance of:

* Avoiding default credentials in security monitoring environments
* Restricting network access to required services
* Keeping security infrastructure reviewed and updated
* Testing rules and log processing before relying on generated alerts
* Combining configuration hardening with continuous monitoring

These practices helped strengthen the Wazuh lab environment and provided practical experience with basic security hardening.
