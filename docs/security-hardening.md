# Security Hardening

## Overview

This document describes the basic security hardening activities performed during the Wazuh lab and the additional hardening steps recommended for the monitoring environment.

The document separates the activities that were performed from the recommendations that were reviewed but not implemented in this lab.

---

## Hardening Objectives

The hardening activities focused on:

- Changing a default credential in the Wazuh environment
- Reviewing Wazuh release and update information
- Reviewing recommended network access restrictions for Wazuh components

---

## Implemented Hardening

### Credential Hardening

A default credential in the Wazuh environment was changed as part of the basic security hardening.

Leaving default credentials unchanged is a common weakness in security monitoring deployments, since default accounts are publicly documented.

### Release and Update Review

Wazuh release information was reviewed during the lab.

The deployed version was Wazuh 4.12. Reviewing release notes helps identify security fixes and compatibility changes that should be considered when maintaining a monitoring environment.

---

## Recommended Hardening (Not Implemented in This Lab)

### Network Access Restriction

A recommended hardening step for a Wazuh deployment is to restrict access to its network services so that only the required hosts can reach them.

| Service | Port | Typical Access |
|---------|------|----------------|
| Agent connection service | 1514/TCP | Wazuh agents |
| Agent enrollment service | 1515/TCP | Wazuh agents (during enrollment) |
| Wazuh server API | 55000/TCP | Administrators |
| Wazuh indexer API | 9200/TCP | Wazuh server and administrators |
| Wazuh Dashboard | 443/TCP | Administrators |

This restriction can be applied with the host firewall available on the Wazuh server operating system. It was reviewed as a recommendation and was not implemented or validated in this lab.

---

## Hardening Approach

The basic approach followed during the lab was:

1. Secure default credentials.
2. Review release and update information.
3. Identify further access restrictions for future hardening.

The objective was to improve the security of the monitoring environment while maintaining the functionality required for the lab exercises.

---

## Key Lessons Learned

The hardening activities demonstrated the importance of:

- Avoiding default credentials in security monitoring environments
- Restricting network access to required services
- Keeping security infrastructure reviewed and updated
- Recording each hardening change with its command and a screenshot so it can be verified later
