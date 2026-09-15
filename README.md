# Wazuh SIEM Lab

> A hands-on cybersecurity lab focused on SIEM deployment, endpoint monitoring, security detection, alert investigation, and network intrusion detection.

This repository documents the practical work performed while building and operating a **Wazuh-based security monitoring environment** in a controlled virtual lab.

The project combines **Windows and Debian Linux endpoint monitoring** with security detection, investigation, remediation, rule tuning, and **Suricata IDS integration**.

---

##  What I Built

The lab was designed to simulate core activities performed in a security monitoring environment:

- Deployed and configured Wazuh for centralized security monitoring
- Enrolled and monitored Windows and Debian Linux endpoints
- Configured and tested File Integrity Monitoring (FIM)
- Assessed endpoint security configurations using SCA
- Identified and investigated software vulnerabilities
- Collected and analyzed security logs and authentication events
- Tuned Wazuh rules to reduce alert severity and noise
- Performed controlled security incident and authentication-failure exercises
- Built a security incident monitoring dashboard
- Integrated Suricata IDS with Wazuh
- Troubleshot agent connectivity, network, firewall, and event-processing issues
- Applied basic security hardening to the monitoring environment

---

##  Lab Environment

| Component | Technology |
|---|---|
| Virtualization | Oracle VirtualBox |
| Host | Windows |
| SIEM | Wazuh 4.12 |
| Windows Endpoint | Windows VM + Wazuh Agent |
| Linux Endpoint | Debian Linux VM + Wazuh Agent |
| Network IDS | Suricata |

### High-Level Architecture

```text
 Windows Endpoint
       │
       │ Wazuh Agent
       ▼
 ┌─────────────────┐
 │  Wazuh Manager  │
 └────────┬────────┘
          │
          ▼
 ┌─────────────────┐
 │  Wazuh Indexer  │
 └────────┬────────┘
          │
          ▼
 ┌─────────────────┐
 │ Wazuh Dashboard │
 └─────────────────┘
          ▲
          │
    Debian Endpoint
          ▲
          │
       Suricata
````

For the network detection component:

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
 Wazuh Dashboard
```

[View the full lab architecture →](docs/architecture.md)

---

## Security Capabilities

### Endpoint Security

**File Integrity Monitoring**

Monitored critical files on both Windows and Debian Linux, generated controlled modifications, and investigated the resulting integrity alerts.

[Explore FIM →](docs/file-integrity-monitoring.md)

**Security Configuration Assessment**

Identified configuration weaknesses on Windows and Debian Linux, applied remediation, and verified the resulting security status.

[Explore SCA →](docs/security-configuration-assessment.md)

**Vulnerability Detection**

Used Wazuh to identify vulnerable software, investigated findings including **CVE-2025-21264**, performed remediation, and verified the resulting vulnerability status.

[Explore Vulnerability Detection →](docs/vulnerability-detection.md)

---

###  Detection & Investigation

**Log Analysis**

Analyzed authentication-related security events from both Linux and Windows endpoints, including failed `sudo` authentication and Windows login failures.

[Explore Log Analysis →](docs/log-analysis.md)

**Rule Tuning**

Created and tested a custom Wazuh local rule to adjust alert severity for repeated SSH authentication failures.

[Explore Rule Tuning →](docs/rule-tuning.md)

**Incident Response**

Performed controlled authentication-failure exercises and investigated the resulting alerts through Wazuh.

A custom **Security Incident Overview** dashboard was also created to improve visibility into security events.

[Explore Incident Response →](docs/incident-response.md)

---

###  Network Detection

**Suricata IDS Integration**

Integrated Suricata with Wazuh to extend the lab from endpoint monitoring to network-based intrusion detection.

The integration was validated end-to-end:

```text
Suricata → EVE JSON → Wazuh Agent → Wazuh Manager → Wazuh Dashboard
```

A controlled test successfully generated and detected a `TestMyIDS.com Detect` alert in Wazuh.

[Explore Suricata Integration →](docs/suricata-integration.md)

---

##  Operations & Security

The project also includes practical work beyond detection:

* Wazuh agent connectivity troubleshooting
* Windows and Debian agent recovery
* Network and firewall troubleshooting
* Wazuh processing health monitoring
* `analysisd.state` review
* `events_dropped` and `discarded_count` monitoring
* `wazuh-logtest` usage
* Basic Wazuh environment hardening
* Credential and firewall configuration

[Explore Troubleshooting →](docs/troubleshooting.md)

[Explore Security Hardening →](docs/security-hardening.md)

---

##  Skills Demonstrated

**SIEM & Security Monitoring**

* Wazuh
* Centralized event monitoring
* Alert investigation
* Security dashboards

**Endpoint Security**

* Windows monitoring
* Linux monitoring
* FIM
* SCA
* Vulnerability Detection

**Detection Engineering**

* Wazuh rules
* Local rule customization
* Alert severity tuning
* `wazuh-logtest`

**Incident Investigation**

* Authentication event analysis
* Failed login investigation
* Alert analysis
* MITRE ATT&CK context

**Network Security**

* Suricata IDS
* EVE JSON
* Network traffic monitoring
* IDS alert validation

**Security Operations**

* Troubleshooting
* Agent connectivity
* Firewall configuration
* Basic security hardening

---

##  Explore the Documentation

The repository contains detailed documentation for each stage of the lab, including implementation steps, configurations, troubleshooting, analysis, and supporting evidence.

| Area                  | Documentation                                                                  |
| --------------------- | ------------------------------------------------------------------------------ |
| Environment           | [Lab Environment](docs/environment.md)                                         |
| Architecture          | [Lab Architecture](docs/architecture.md)                                       |
| Deployment            | [Wazuh Installation](docs/installation.md)                                     |
| Endpoints             | [Agent Deployment](docs/agent-deployment.md)                                   |
| Monitoring            | [File Integrity Monitoring](docs/file-integrity-monitoring.md)                 |
| Configuration         | [Security Configuration Assessment](docs/security-configuration-assessment.md) |
| Vulnerabilities       | [Vulnerability Detection](docs/vulnerability-detection.md)                     |
| Detection             | [Log Analysis](docs/log-analysis.md)                                           |
| Detection Engineering | [Rule Tuning](docs/rule-tuning.md)                                             |
| Incident Response     | [Incident Response](docs/incident-response.md)                                 |
| Network Security      | [Suricata IDS Integration](docs/suricata-integration.md)                       |
| Operations            | [Troubleshooting](docs/troubleshooting.md)                                     |
| Hardening             | [Security Hardening](docs/security-hardening.md)                               |

---

##  Repository Structure

```text
Wazuh-SIEM-Lab/
│
├── README.md
│
├── docs/
│   ├── README.md
│   ├── installation.md
│   ├── agent-deployment.md
│   ├── architecture.md
│   ├── environment.md
│   ├── file-integrity-monitoring.md
│   ├── security-configuration-assessment.md
│   ├── vulnerability-detection.md
│   ├── log-analysis.md
│   ├── rule-tuning.md
│   ├── incident-response.md
│   ├── suricata-integration.md
│   ├── troubleshooting.md
│   └── security-hardening.md
│
└── images/
    ├── agent-deployment/
    ├── file-integrity-monitoring/
    ├── installation/
    ├── log-analysis/
    ├── rule-tuning/
    ├── security-configuration-assessment/
    ├── suricata/
    └── vulnerability-detection/
```

---

##  Project Focus

This project emphasizes **hands-on cybersecurity practice** rather than theoretical configuration alone.

The documentation focuses on:

* Practical deployment
* Controlled security testing
* Detection and alert analysis
* Remediation verification
* Detection engineering
* Network intrusion detection
* Troubleshooting
* Evidence-based documentation

---

##  Detailed Documentation

For the complete documentation index:

**[→ Open the Documentation Hub](docs/README.md)**
