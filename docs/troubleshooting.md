# Troubleshooting

## Overview

This document describes the troubleshooting activities performed during the Wazuh lab.

The troubleshooting work focused on monitoring the health of the Wazuh environment, investigating agent connectivity issues, checking system and Wazuh processing metrics, resolving network and firewall-related issues, and validating Wazuh log processing.

All troubleshooting activities were performed within the controlled virtual lab environment.

---

## Troubleshooting Objectives

The troubleshooting activities focused on:

* Monitoring CPU, RAM, and disk usage
* Reviewing Wazuh analysis engine health
* Checking `analysisd.state`
* Monitoring `events_dropped` and `discarded_count`
* Simulating Wazuh agent disconnections
* Restoring Windows and Debian Linux agent connectivity
* Investigating firewall and network connectivity issues
* Reviewing Wazuh release information
* Testing log processing using `wazuh-logtest`

---

## System Resource Monitoring

System resources were monitored during the lab to help identify potential performance-related issues.

The following resources were reviewed:

* CPU usage
* RAM usage
* Disk usage

Monitoring these resources provided visibility into the overall health of the virtual machines and the Wazuh environment.

---

## Wazuh Analysis Engine Monitoring

Wazuh Manager processing activity was reviewed using the `analysisd.state` file.

The review included monitoring processing-related values such as:

```text
events_dropped
discarded_count
```

These metrics were used to check whether security events were being dropped or discarded during processing.

Monitoring these values provided an additional way to assess the health of Wazuh event processing.

---

## Agent Connectivity Troubleshooting

Agent connectivity was tested by intentionally stopping Wazuh agents and observing their status in the Wazuh Dashboard.

This was performed with both the Debian Linux and Windows agents.

The purpose was to understand how an agent disconnection appears in Wazuh and to verify that connectivity could be restored after restarting the agent service.

---

### Debian Linux Agent

The Wazuh agent service on the Debian Linux endpoint was stopped to simulate an agent disconnection.

The service was then started again to restore communication with the Wazuh Manager.

The following commands were used:

```bash
sudo systemctl stop wazuh-agent
```

```bash
sudo systemctl start wazuh-agent
```

The service status was checked using:

```bash
sudo systemctl status wazuh-agent
```

After restarting the service, the agent status was checked in the Wazuh Dashboard to verify that communication had been restored.

---

### Windows Agent

The Windows Wazuh agent was also stopped to simulate an endpoint disconnection.

The Windows service was then started again to restore communication with the Wazuh Manager.

The following PowerShell commands were used:

```powershell
Stop-Service -Name WazuhSvc
```

```powershell
Start-Service -Name WazuhSvc
```

The agent status was then reviewed in the Wazuh Dashboard to verify that the Windows endpoint had returned to an active state.

---

## Network and Firewall Troubleshooting

Network connectivity and firewall configuration were reviewed during the lab when investigating communication issues between the virtual machines and Wazuh components.

Different VirtualBox network configurations were tested, including:

* NAT
* Bridged Adapter

The network configuration was adjusted when required to establish stable communication between the virtual machines.

Firewall configuration was also reviewed when investigating connectivity problems.

The troubleshooting process included checking:

1. Virtual machine network configuration
2. Network connectivity
3. Firewall configuration
4. Wazuh service status
5. Agent connectivity

---

## Wazuh Release Information

Wazuh release information was reviewed as part of the troubleshooting and maintenance activities.

Reviewing the deployed Wazuh version and available release information helped provide awareness of updates and changes relevant to the Wazuh environment.

The Wazuh version used in the lab was:

```text
Wazuh 4.12
```

---

## Log Processing Troubleshooting

The Wazuh `logtest` utility was used to test log processing and investigate how Wazuh decodes logs and applies rules.

The following command was used:

```bash
sudo /var/ossec/bin/wazuh-logtest
```

The tool was used to review:

* Log pre-decoding
* Log decoding
* Rule matching
* Rule ID
* Alert level
* Extracted event information

This was particularly useful when working with Wazuh rules and analyzing security events.

Wazuh documentation describes `wazuh-logtest` as a tool for testing and verifying decoders and rules against supplied log samples. ([Wazuh Documentation][1])

---

## Troubleshooting Workflow

The troubleshooting process used during the lab can be summarized as:

```text
Identify the Problem
        │
        ▼
Check Service Status
        │
        ▼
Check Network Connectivity
        │
        ▼
Review Firewall Configuration
        │
        ▼
Review System / Wazuh Health
        │
        ▼
Test Log Processing
        │
        ▼
Apply the Fix
        │
        ▼
Verify the Result
```

The final verification step was used to confirm that the affected service, agent, or monitoring function had returned to the expected state.

---

## Troubleshooting Examples

### Example 1: Debian Agent Disconnection

**Problem:**

The Debian Wazuh agent was intentionally stopped to simulate an agent connectivity issue.

**Investigation:**

The agent status was reviewed in the Wazuh Dashboard and the Wazuh agent service was checked on the Debian endpoint.

**Resolution:**

The Wazuh agent service was started again.

**Verification:**

The agent status was checked to confirm that communication with the Wazuh Manager had been restored.

---

### Example 2: Windows Agent Disconnection

**Problem:**

The Windows Wazuh agent was intentionally stopped to simulate an endpoint disconnection.

**Investigation:**

The Windows agent status was reviewed in the Wazuh Dashboard.

**Resolution:**

The `WazuhSvc` service was started again using PowerShell.

**Verification:**

The Windows agent status was checked to confirm that the endpoint had returned to an active state.

---

### Example 3: Wazuh Log Processing

**Problem:**

A log entry needed to be tested to understand how Wazuh processed the event.

**Investigation:**

`wazuh-logtest` was used to process the log and review the decoding and rule-matching results.

**Resolution:**

The resulting decoder and rule information was reviewed to understand how Wazuh interpreted the event.

**Verification:**

The processing output was reviewed to confirm the rule and alert information generated from the tested log.

---

## Key Lessons Learned

The troubleshooting activities demonstrated the importance of following a structured approach when diagnosing security monitoring issues.

Key lessons included:

* Check service status before making configuration changes.
* Verify network connectivity when agents cannot communicate with the Wazuh Manager.
* Review firewall configuration when network communication is restricted.
* Monitor CPU, RAM, and disk usage when investigating system health.
* Review `analysisd.state` and processing metrics such as `events_dropped` and `discarded_count`.
* Use `wazuh-logtest` to validate log decoding and rule matching.
* Verify the final system state after applying a fix.
* Use controlled disconnection tests to understand agent connectivity behavior.

---

## Practical Outcome

The troubleshooting exercises provided practical experience with maintaining and diagnosing a Wazuh monitoring environment.

The activities covered:

* Wazuh agent connectivity
* Windows and Debian Linux agent recovery
* Virtual machine networking
* Firewall-related connectivity
* System resource monitoring
* Wazuh analysis engine monitoring
* Log decoding and rule testing
* Wazuh release awareness

These exercises helped develop a structured approach to troubleshooting security monitoring infrastructure in a controlled lab environment.
