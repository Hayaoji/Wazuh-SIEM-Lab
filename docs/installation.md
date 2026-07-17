# Wazuh Installation

## Objective

Deploy the official Wazuh 4.12 OVA in Oracle VirtualBox and prepare the environment for security monitoring and agent deployment.

## Software Used

| Software | Purpose |
|----------|---------|
| Oracle VirtualBox | Hosted the Wazuh virtual machine. |
| Wazuh OVA 4.12 | Provided the pre-configured Wazuh environment. |
| Amazon Linux 2023 | Operating system running the Wazuh platform. |

## Implementation

The installation process followed the official Wazuh deployment approach using the Wazuh 4.12 OVA image.

The following tasks were completed:

- Installed Oracle VirtualBox on the Windows host machine.
- Downloaded the official Wazuh 4.12 OVA for Amazon Linux 2023.
- Imported the OVA into Oracle VirtualBox.
- Created the virtual machine and completed the initial configuration.
- Configured the virtual network to establish communication between the host system and the virtual machine.

## Verification

After completing the installation, the Wazuh services were verified using `systemctl status` to confirm that the platform was running correctly.

Command used to verify the service status:

```bash
sudo systemctl status wazuh-manager
```

The screenshot below shows the Wazuh Manager service in an active (running) state, confirming that the installation was successful and the service was operating correctly.

## Evidence

The following screenshot shows the Wazuh Manager service running successfully after the installation.

### Service Status Verification

## Lessons Learned

- Learned the deployment workflow using the official Wazuh 4.12 OVA.
- Understood the importance of verifying service status before accessing the Wazuh Dashboard.
- Gained practical experience configuring a virtual machine using Oracle VirtualBox.

The following screenshot shows the Wazuh Manager service running successfully after the installation.
