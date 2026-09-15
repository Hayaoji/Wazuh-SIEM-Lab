# Lab Architecture

## Overview

This document describes the architecture of the Wazuh security monitoring lab.

The lab was designed as a controlled virtual environment for monitoring Windows and Debian Linux endpoints, collecting security events, detecting security-related activity, and analyzing alerts through the Wazuh platform.

The environment was hosted on a Windows system using Oracle VirtualBox.

---

## Architecture Components

The lab consisted of the following main components:

| Component | Role |
|---|---|
| Wazuh Manager | Receives and processes security data from monitored agents and generates alerts |
| Wazuh Indexer | Stores and indexes security events |
| Wazuh Dashboard | Provides the web interface for monitoring agents, alerts, vulnerabilities, and security events |
| Windows Agent | Windows endpoint monitored by Wazuh |
| Debian Linux Agent | Linux endpoint monitored by Wazuh |
| Suricata | Network intrusion detection component deployed on the Debian Linux agent |

---

## High-Level Architecture

```text
                         Wazuh Platform
                              │
                ┌─────────────┼─────────────┐
                │             │             │
                ▼             ▼             ▼
        Wazuh Manager   Wazuh Indexer   Wazuh Dashboard
                ▲             ▲
                │             │
                │             │
        ┌───────┴───────┐     │
        │               │     │
        │               │     │
        ▼               ▼     │
 Windows Agent    Debian Linux Agent
                        │
                        ▼
                    Suricata
````

The Windows and Debian Linux agents collected security-related data and communicated with the Wazuh Manager.

The Wazuh Manager processed the collected data and generated alerts. Security events were stored and indexed by the Wazuh Indexer and made available through the Wazuh Dashboard for monitoring and analysis.

---

## Endpoint Monitoring

### Windows Endpoint

The Windows virtual machine was enrolled as a Wazuh agent.

The Windows endpoint was used for:

* File Integrity Monitoring (FIM)
* Security Configuration Assessment (SCA)
* Vulnerability Detection
* Windows security event collection
* Failed login testing
* Endpoint activity monitoring

The Wazuh agent collected relevant security events and sent them to the Wazuh Manager for processing.

---

### Debian Linux Endpoint

The Debian Linux virtual machine was enrolled as a Wazuh agent and used as the primary Linux endpoint for the lab.

The Debian Linux endpoint was used for:

* File Integrity Monitoring (FIM)
* Security Configuration Assessment (SCA)
* Vulnerability Detection
* Linux security log collection
* Failed sudo authentication testing
* Alert analysis
* Wazuh rule tuning
* Suricata integration

---

## Suricata Integration

Suricata was deployed on the Debian Linux endpoint to provide network intrusion detection.

The Suricata integration followed this flow:

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
Debian Wazuh Agent
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

Suricata generated network security events in EVE JSON format.

The Wazuh agent was configured to collect the Suricata EVE JSON log and forward the events to the Wazuh Manager.

The main Suricata log used for the integration was:

```text
/var/log/suricata/eve.json
```

The integration was validated by generating controlled network traffic and confirming that the resulting Suricata alert was visible in the Wazuh Dashboard.

---

## Data Flow

The general security monitoring flow was:

```text
Windows Agent ────────┐
                      │
                      ▼
                Wazuh Manager
                      │
                      ▼
                Wazuh Indexer
                      │
                      ▼
                Wazuh Dashboard
                      ▲
                      │
Debian Agent ─────────┘
      ▲
      │
   Suricata
```

The agents collected endpoint security information, while Suricata provided network security events on the Debian Linux endpoint.

The Wazuh Manager processed the collected information and generated alerts that could then be reviewed through the Wazuh Dashboard.

---

## Security Monitoring Activities

The architecture supported the following practical security monitoring activities:

* Endpoint monitoring
* File Integrity Monitoring
* Security Configuration Assessment
* Vulnerability Detection
* Security log collection
* Alert analysis
* Basic Wazuh rule tuning
* Network intrusion detection through Suricata
* Dashboard-based security monitoring

These activities were performed within the controlled virtual lab environment.

---

## Architecture Design

The architecture separated the monitored endpoints from the central Wazuh monitoring components.

This design allowed Windows and Debian Linux systems to act as monitored endpoints while the Wazuh platform provided centralized processing, storage, and visualization of security events.

Adding Suricata to the Debian Linux endpoint extended the monitoring capability to include network-based security detection in addition to endpoint monitoring.

---

## Architecture Summary

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
    └── Debian Linux VM
        ├── Wazuh Agent
        └── Suricata
```

This architecture provided a controlled environment for practicing centralized security monitoring, endpoint detection, vulnerability monitoring, log analysis, rule tuning, and network intrusion detection.
