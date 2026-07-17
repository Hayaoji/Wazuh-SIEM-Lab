# Wazuh-SIEM-Lab

## Project Overview
This repository documents my hands-on experience with Wazuh during a structured cybersecurity training program. Throughout this lab, I deployed and configured a Wazuh environment, connected Linux and Windows agents, monitored security events, analyzed alerts, and implemented several core security monitoring capabilities.

The project includes practical exercises on File Integrity Monitoring (FIM), Security Configuration Assessment (SCA), vulnerability detection, log analysis, dashboard customization, and basic security hardening. Every section documents tasks that I personally completed during the training and includes supporting screenshots, commands, and key observations.

## Lab Environment

The lab was built in a virtual environment using Oracle VirtualBox to simulate a security monitoring environment. Wazuh 4.12 (OVA) was deployed on Amazon Linux 2023, while both Linux and Windows systems were used as monitored endpoints through Wazuh agents.

| Component | Details |
-----------------------
| Hypervisor | Oracle VirtualBox |
| SIEM Platform | Wazuh 4.12 |
| Wazuh OVA | Amazon Linux 2023 |
| Monitored Endpoints | Linux & Windows |
| Main Components | Wazuh Manager, Indexer, Dashboard, Agents |

## Wazuh Architecture

The lab environment consists of four core Wazuh components working together to collect, process, index, and visualize security events. Linux and Windows endpoints send security data to the Wazuh Manager through installed agents, enabling centralized monitoring and alert generation.

| Component | Role |
-----------------------
| Wazuh Manager | Collects logs, analyzes events, and generates security alerts. |
| Wazuh Indexer | Stores and indexes security data for fast searching and analysis. |
| Wazuh Dashboard | Provides a web interface for monitoring alerts and managing the platform. |
| Wazuh Agents | Collect endpoint data from Linux and Windows systems and send it to the Wazuh Manager. |
