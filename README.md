# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/Scar-Op/Azure-Honeynet-Project/assets/158982947/680b9bb4-89ad-4038-ab75-79b210580057)


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/Scar-Op/Azure-Honeynet-Project/assets/158982947/51102478-f6bf-4277-9c5c-76db750cd5fe)


## Architecture After Hardening / Security Controls
![image](https://github.com/Scar-Op/Azure-Honeynet-Project/assets/158982947/543b9109-f854-4562-b600-7d80d12345f0)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![Screenshot 2024-01-27 224416](https://github.com/Scar-Op/Azure-Honeynet-Project/assets/158982947/46dbdef2-bda8-43d8-a858-68860964560f)

![Screenshot 2024-01-27 224308](https://github.com/Scar-Op/Azure-Honeynet-Project/assets/158982947/b6910756-ed6c-4721-b24b-f986e8f2954b)
![Screenshot 2024-01-27 224448](https://github.com/Scar-Op/Azure-Honeynet-Project/assets/158982947/f6442a27-fb2a-424c-92a9-5b2009b8abf2)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-01-27 4:17:46
Stop Time 2024-01-28 4:17:46

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 16850
| Syslog                   | 4658
| SecurityAlert            | 297
| SecurityIncident         | 297
| AzureNetworkAnalytics_CL | 4437

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-02-02 18:23:53
Stop Time	2024-02-03 18:23:53

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8338
| Syslog                   | 3
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
