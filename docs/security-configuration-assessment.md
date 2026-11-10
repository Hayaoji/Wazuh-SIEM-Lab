# Security Configuration Assessment (SCA)

## Objective

Evaluate system security configurations using Wazuh Security Configuration Assessment (SCA), remediate non-compliant settings, and verify compliance after applying security recommendations.

## Software Used

| Software | Purpose |
|----------|---------|
| Wazuh Dashboard         | Displayed SCA policy results and compliance status. |
| Debian Virtual Machine | Tested Linux security configuration compliance. |
| Windows 11 Host Machine | Tested Windows security policy compliance.  |
| Wazuh SCA Module | Evaluated security configurations against predefined policies. |

## Implementation

Security Configuration Assessment (SCA) was performed on both Linux and Windows systems to identify security misconfigurations and verify compliance after remediation.

The following tasks were completed:

- Evaluated the Linux system against the Wazuh SCA policy.
- Disabled the `cramfs` filesystem module to reduce the attack surface.
- Re-ran the SCA assessment after applying the remediation.
- Evaluated the Windows password history policy.
- Updated the **Enforce password history** policy to require a minimum of 24 previous passwords.

## Verification

The Security Configuration Assessment results were verified by confirming that remediation actions changed the compliance status from **Failed** to **Passed**.

The following checks were performed:

- Verified that **Check ID 33000** changed to **Passed** after disabling the `cramfs` filesystem module.
- Verified that **Check ID 26000** changed to **Passed** after updating the Windows password history policy.
- Confirmed that Wazuh re-evaluated both systems and reported the updated compliance status in the SCA module.

## Commands Used

Disable the `cramfs` filesystem module on Debian:

```
sudo nano /etc/modprobe.d/cramfs.conf
```

The file contained:

```
install cramfs /bin/true
```

Unload the module (if loaded) and verify the configuration:

```
sudo rmmod cramfs
grep cramfs /etc/modprobe.d/*.conf
lsmod | grep cramfs
```

`rmmod` reported that the `cramfs` module was not currently loaded, so the configuration file was the effective remediation.

Set the Windows password history policy:

```
net accounts /uniquepw:24
```

## Evidence

### Linux SCA – Initial Compliance Failure

The initial SCA assessment identified the `cramfs` configuration as non-compliant under **Check ID 33000**.

![Initial SCA Result - cramfs Module Enabled](../images/security-configuration-assessment/linux-sca-initial-failed.png)

### Linux SCA – Compliance Passed After Remediation

After disabling the `cramfs` filesystem module, Wazuh re-evaluated the configuration and reported **Check ID 33000** as **Passed**.

![Post-Remediation SCA Result - Linux](../images/security-configuration-assessment/linux-sca-post-remediation-passed.png)

### Windows SCA – Initial Compliance Failure

The initial SCA assessment identified the **Enforce password history** setting as non-compliant under **Check ID 26000**.

![Initial SCA Result - Weak Password History Policy](../images/security-configuration-assessment/windows-sca-initial-failed.png)

### Windows SCA – Compliance Passed After Remediation

After updating the password history policy to the recommended value, Wazuh re-evaluated the configuration and reported **Check ID 26000** as **Passed**.

![Post-Remediation SCA Result - Windows](../images/security-configuration-assessment/windows-sca-post-remediation-passed.png)

## Lessons Learned

- Gained practical experience using Wazuh SCA to identify security configuration weaknesses on Linux and Windows systems.
- Learned how remediation actions affect SCA compliance results.
- Improved the ability to verify security configuration changes by comparing initial and post-remediation compliance states.
