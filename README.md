# Building a SOC + Honeynet in Azure (Live Traffic)
<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/96168922-5fd6-4264-8751-58c98ef19661">


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

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
<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/0fd60437-a548-470e-bd3e-6b7fea7ff2dc">

<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/01aa4dff-9b07-4a53-9865-dbeddca66237">


<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/58928675-fa20-478d-96f5-ef32ac01f400">


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-06-12 11:46:22 AM
Stop Time 2024-06-13 11:46:22 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 20980
| Syslog                   |9556
| SecurityAlert            | 3
| SecurityIncident         | 355
| AzureNetworkAnalytics_CL | 1427

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-06-14 2:49:27 PM
Stop Time	2024-06-15 2:49:27 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8454
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
# Azure-SOC
