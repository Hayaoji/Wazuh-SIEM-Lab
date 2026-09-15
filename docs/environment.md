# Lab Environment

## Overview

This document describes the virtual lab environment used during the Wazuh training and security monitoring activities.

The environment was designed to provide a controlled setup for deploying Wazuh, monitoring Windows and Linux endpoints, collecting security events, testing detection capabilities, and performing security monitoring exercises.

The lab was built using virtual machines hosted on a Windows system with Oracle VirtualBox.

---

## Virtualization Platform

| Component | Details |
|---|---|
| Virtualization Platform | Oracle VirtualBox |
| Host Operating System | Windows |
| Wazuh Deployment | Wazuh 4.12 OVA |
| Linux Endpoint | Debian Linux virtual machine |
| Windows Endpoint | Windows virtual machine |

The Wazuh environment was deployed using the Wazuh 4.12 OVA and hosted within Oracle VirtualBox.

During the initial setup, different network configurations were tested, including NAT and Bridged Adapter, to establish stable communication between the host and virtual machines.

---

## Wazuh Central Environment

The Wazuh environment consisted of the main components required for centralized security monitoring.

| Component | Role |
|---|---|
| Wazuh Manager | Processes security data received from agents and generates alerts |
| Wazuh Indexer | Stores and indexes security events |
| Wazuh Dashboard | Provides the web interface for monitoring agents, alerts, and security events |

The core Wazuh services were verified using `systemctl status` during the initial setup.

The main services verified were:

- `wazuh-manager`
- `wazuh-indexer`
- `wazuh-dashboard`

---

## Monitored Endpoints

The lab included both Windows and Linux endpoints to provide cross-platform monitoring.

### Windows Agent

A Windows virtual machine was used as a monitored endpoint.

Activities performed on the Windows agent included:

- Wazuh agent deployment and enrollment
- Security event collection
- File Integrity Monitoring (FIM)
- Security Configuration Assessment (SCA)
- Vulnerability Detection
- Failed login testing
- Endpoint activity monitoring

The Wazuh agent configuration file was reviewed at:

```text
C:\Program Files (x86)\ossec-agent\ossec.conf
````

---

### Debian Linux Agent

A Debian Linux virtual machine was used as the primary Linux endpoint in the lab.

Debian Linux was selected because the available storage space on the host system was limited, and the Debian virtual machine provided a suitable environment for the required Linux-based security monitoring activities.

Activities performed on the Debian Linux agent included:

- Wazuh agent deployment and enrollment
- Linux security log collection
- File Integrity Monitoring (FIM)
- Security Configuration Assessment (SCA)
- Vulnerability Detection
- Failed sudo authentication testing
- Alert analysis
- Basic Wazuh rule tuning
- Suricata deployment and integration

The Wazuh agent configuration file was reviewed at:

```text
/var/ossec/etc/ossec.conf
```

---

## Suricata Environment

Suricata was deployed on the Debian agent as a network intrusion detection component.

The Suricata environment was used to:

* Monitor network traffic
* Use the Emerging Threats Open ruleset
* Generate IDS alerts
* Produce EVE JSON events
* Forward Suricata events to Wazuh
* Verify Suricata alerts in the Wazuh Dashboard

The main Suricata event log used for Wazuh integration was:

```text
/var/log/suricata/eve.json
```

---

## Security Monitoring Flow

The main Wazuh monitoring flow was:

```text
Windows Agent ──┐
                ├──> Wazuh Manager ──> Wazuh Indexer ──> Wazuh Dashboard
Debian Agent ───┘
```

For the Suricata integration:

```text
Network Traffic
      │
      ▼
  Suricata
      │
      ▼
   EVE JSON
      │
      ▼
 Wazuh Agent
      │
      ▼
 Wazuh Manager
      │
      ▼
 Wazuh Indexer
      │
      ▼
 Wazuh Dashboard
```

---

## Monitoring and Security Activities

The environment supported the following documented activities:

* Wazuh deployment and service verification
* Windows and Debian agent deployment
* File Integrity Monitoring (FIM)
* Security Configuration Assessment (SCA)
* Vulnerability Detection
* Log Data Collection and Alert Analysis
* Basic Wazuh Rule Tuning
* Incident alert analysis
* Basic dashboard customization
* Agent connectivity troubleshooting
* Basic security hardening
* `wazuh-logtest` rule testing
* Suricata IDS integration

These activities were performed using controlled virtual-machine environments.

---

## Environment Design

Virtual machines were used to provide an isolated and controlled environment for security testing.

This setup allowed security events and configuration changes to be generated without directly affecting a production environment.

Using both Windows and Debian endpoints also provided practical experience with cross-platform Wazuh monitoring and the differences in agent configuration and system logs between operating systems.

---

## Environment Summary

```text
Windows Host
│
└── Oracle VirtualBox
    │
    ├── Wazuh VM
    │   ├── Wazuh Manager
    │   ├── Wazuh Indexer
    │   └── Wazuh Dashboard
    │
    ├── Windows VM
    │   └── Wazuh Agent
    │
    └── Debian VM
        ├── Wazuh Agent
        └── Suricata
```

---

## Notes

The environment described in this document represents the setup used for the documented Wazuh training activities.

Detailed implementation steps, security exercises, alert analysis, troubleshooting activities, and Suricata integration are documented separately in the project documentation.

---
