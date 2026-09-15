# Wazuh SIEM Lab

A hands-on cybersecurity lab focused on deploying, configuring, and using Wazuh for centralized security monitoring, endpoint detection, vulnerability monitoring, log analysis, incident investigation, and network intrusion detection.

The project was built in a controlled virtual environment using Oracle VirtualBox, with Windows and Debian Linux endpoints monitored through Wazuh.

---

## Project Overview

This project documents practical work performed while building and operating a Wazuh security monitoring environment.

The lab covers the deployment of Wazuh's core components, endpoint enrollment, security monitoring, detection and analysis of simulated security events, vulnerability identification and remediation, basic rule tuning, incident response exercises, troubleshooting, security hardening, and Suricata IDS integration.

The objective was to gain practical experience with how security events are collected, processed, detected, investigated, and visualized in a centralized SIEM environment.

---

## Environment

| Component | Details |
|---|---|
| Virtualization Platform | Oracle VirtualBox |
| Host Operating System | Windows |
| Wazuh Deployment | Wazuh 4.12 OVA |
| Monitored Windows Endpoint | Windows virtual machine |
| Monitored Linux Endpoint | Debian Linux virtual machine |
| Network IDS | Suricata on Debian Linux |

The lab used separate virtual machines for the Wazuh environment and monitored endpoints.

Debian Linux was used as the primary Linux endpoint for the hands-on security monitoring activities.

---

## Wazuh Architecture

The Wazuh environment consisted of the following core components:

- **Wazuh Manager** — Processes security data received from agents and generates alerts.
- **Wazuh Indexer** — Stores and indexes security events.
- **Wazuh Dashboard** — Provides the interface for monitoring agents, alerts, vulnerabilities, and security events.
- **Wazuh Agents** — Collect security data from monitored Windows and Debian Linux endpoints.

High-level data flow:

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
Debian Linux Agent ───┘
          ▲
          │
       Suricata
````

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

---

## Security Monitoring Capabilities

The lab included practical work with the following Wazuh capabilities:

### File Integrity Monitoring (FIM)

Configured and tested FIM across both Windows and Debian Linux endpoints.

Examples included:

* Monitoring `/etc/passwd` on Debian Linux
* Monitoring `C:\Windows\System32\drivers\etc\hosts` on Windows
* Simulating controlled file modifications
* Verifying Wazuh integrity alerts
* Analyzing checksum and metadata changes
* Working with Wazuh Rule ID `550`

[View FIM Documentation](file-integrity-monitoring.md)

---

### Security Configuration Assessment (SCA)

Used Wazuh SCA to identify configuration weaknesses and verify remediation.

Examples included:

* Debian Linux `cramfs` configuration
* Windows `Enforce password history` policy
* Remediating the identified configurations
* Verifying the transition from **Failed** to **Passed**
* Working with Rule IDs `33000` and `26000`

[View SCA Documentation](security-configuration-assessment.md)

---

### Vulnerability Detection

Used Wazuh Vulnerability Detection to identify vulnerable software and verify remediation.

Examples included:

* Identifying low-severity package vulnerabilities on Debian Linux
* Identifying a high-severity vulnerability in Microsoft Visual Studio Code on Windows
* CVE-2025-21264 affecting Visual Studio Code version 1.99.3
* Updating the affected software
* Verifying that the vulnerable version was no longer listed in Wazuh

[View Vulnerability Detection Documentation](vulnerability-detection.md)

---

### Log Data Collection & Alert Analysis

Analyzed security events collected from both Linux and Windows endpoints.

Linux analysis included:

* Failed `sudo` authentication attempts
* Journald log collection
* Sudo decoder analysis
* Wazuh Rule ID `5404`
* User and target account investigation

Windows analysis included:

* Failed login attempts
* Windows EventChannel log collection
* Authentication failure analysis
* Wazuh Rule ID `60122`
* Investigation of the affected user account

[View Log Analysis Documentation](log-analysis.md)

---

### Basic Wazuh Rule Tuning

Performed basic rule customization to reduce alert noise.

A local Wazuh rule with ID `100001` was modified in `local_rules.xml` to lower its alert level to `5` for repeated SSH authentication failures.

The Wazuh Manager was restarted to apply the change, and the resulting alerts were verified with the updated severity level.

[View Rule Tuning Documentation](rule-tuning.md)

---

## Incident Response & Detection Exercises

The lab included controlled security event simulations to practice incident detection and investigation.

### Authentication Attack Simulation

A controlled brute-force-style scenario was simulated against the Debian Linux environment.

Multiple failed `sudo` authentication attempts were generated and detected by Wazuh through Rule ID `5404`.

The resulting alerts were analyzed through the Wazuh Dashboard to understand the relationship between the activity, the generated alert, the affected user, and the target account.

A Windows failed-login scenario was also performed using intentionally incorrect credentials, generating authentication failure alerts through the Windows EventChannel.

---

### Active Response Concept

The Wazuh `firewall-drop` Active Response capability was researched to understand how automated defensive actions can interact with the agent firewall.

This part of the work focused on understanding the concept and configuration rather than presenting Active Response as a production or fully deployed automated blocking mechanism.

[View Incident Response Documentation](incident-response.md)

---

### Security Incident Dashboard

A custom Wazuh dashboard named **Security Incident Overview** was created to provide centralized visibility into security events.

The dashboard included visualizations covering areas such as:

* Alert severity
* Vulnerability risk levels
* MITRE ATT&CK tactics
* Top alert categories
* Users generating events
* External SSH attackers
* Recent security activity

---

## Suricata IDS Integration

Suricata was deployed on the Debian Linux endpoint to extend the lab's monitoring capabilities from endpoint events to network intrusion detection.

The integration included:

* Suricata installation and configuration
* Network interface configuration
* Emerging Threats Open ruleset
* Network traffic monitoring
* EVE JSON event generation
* Wazuh log collection of `/var/log/suricata/eve.json`
* Suricata-to-Wazuh integration
* Controlled IDS alert validation
* Verification of Suricata alerts in the Wazuh Dashboard

A controlled test generated the `TestMyIDS.com Detect` Suricata alert, which was successfully observed in the Wazuh Dashboard.

[View Suricata Integration Documentation](suricata-integration.md)

---

## Troubleshooting & System Maintenance

The lab also included practical troubleshooting and maintenance activities.

These included:

* Monitoring CPU, RAM, and disk usage
* Reviewing Wazuh analysisd health metrics
* Checking `events_dropped` and `discarded_count`
* Simulating Wazuh agent disconnections
* Restoring disconnected Windows and Debian agents
* Investigating firewall and connectivity issues
* Reviewing Wazuh release information
* Testing log processing using `wazuh-logtest`

The troubleshooting exercises provided practical experience in diagnosing agent connectivity and maintaining a healthy Wazuh environment.

[View Troubleshooting Documentation](troubleshooting.md)

---

## Security Hardening

Basic security hardening measures were applied to the Wazuh environment.

Activities included:

* Changing default Wazuh passwords
* Restricting access to Wazuh ports using UFW and trusted IP addresses
* Reviewing Wazuh release information and update importance
* Testing Wazuh decoders and rules using `wazuh-logtest`

[View Security Hardening Documentation](security-hardening.md)

---

## Skills Demonstrated

### SIEM & Security Monitoring

* Wazuh deployment
* SIEM architecture
* Centralized security monitoring
* Security event collection
* Alert investigation
* Dashboard monitoring

### Endpoint Security

* Windows endpoint monitoring
* Debian Linux endpoint monitoring
* File Integrity Monitoring
* Security Configuration Assessment
* Vulnerability Detection

### Detection & Analysis

* Authentication event analysis
* Failed login investigation
* Failed `sudo` authentication analysis
* Rule and alert analysis
* Basic alert correlation
* MITRE ATT&CK context

### Detection Engineering

* Wazuh local rule customization
* Alert severity adjustment
* Alert noise reduction
* Log and rule testing with `wazuh-logtest`

### Network Security

* Suricata IDS deployment
* Network traffic monitoring
* EVE JSON analysis
* Suricata-to-Wazuh integration
* IDS alert validation

### Security Operations

* Incident detection
* Incident investigation
* Basic incident response concepts
* Troubleshooting agent connectivity
* Security hardening
* Security monitoring maintenance

---

## Tools & Technologies

* Wazuh 4.12
* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard
* Wazuh Agents
* Suricata
* Debian Linux
* Windows
* Oracle VirtualBox
* UFW
* Journald
* EventChannel
* `wazuh-logtest`
* `local_rules.xml`

---

## Documentation

Detailed implementation notes, configurations, troubleshooting steps, and evidence are available in the project documentation.

### Environment & Architecture

* [Lab Environment](environment.md)
* [Lab Architecture](architecture.md)
* [Wazuh Installation](installation.md)
* [Agent Deployment](agent-deployment.md)

### Security Monitoring

* [File Integrity Monitoring](file-integrity-monitoring.md)
* [Security Configuration Assessment](security-configuration-assessment.md)
* [Vulnerability Detection](vulnerability-detection.md)
* [Log Analysis](log-analysis.md)
* [Rule Tuning](rule-tuning.md)

### Incident Response & Network Detection

* [Incident Response](incident-response.md)
* [Suricata IDS Integration](suricata-integration.md)

### Operations & Maintenance

* [Troubleshooting](troubleshooting.md)
* [Security Hardening](security-hardening.md)

---

## Project Structure

```text
Wazuh-SIEM-Lab/
│
├── docs/
│   ├── README.md
│   ├── agent-deployment.md
│   ├── architecture.md
│   ├── environment.md
│   ├── file-integrity-monitoring.md
│   ├── incident-response.md
│   ├── installation.md
│   ├── log-analysis.md
│   ├── rule-tuning.md
│   ├── security-configuration-assessment.md
│   ├── security-hardening.md
│   ├── suricata-integration.md
│   ├── troubleshooting.md
│   └── vulnerability-detection.md
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

## Project Focus

This repository focuses on documenting hands-on security monitoring work performed in a controlled virtual lab environment.

The documentation emphasizes practical configuration, controlled security testing, alert investigation, remediation verification, troubleshooting, and evidence-based analysis rather than theoretical descriptions alone.
