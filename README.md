# Building a SOC + Honeynet in Azure (Live Traffic)
<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/4d134bd0-74ef-4482-8cc3-0d2f2088b9d1">



## Introduction

In this project, I set up a mini honeynet in Azure and configured it to send log data from various resources into a Log Analytics workspace. This data was then utilized by Microsoft Sentinel to generate attack maps, trigger alerts, and create incidents. To evaluate the security of the environment, I first measured key security metrics over a 24-hour period with minimal security controls. After implementing enhanced security measures to harden the environment, I measured the same metrics for another 24 hours. Below, I present the results of these measurements. The metrics included are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/036d87a2-193b-404b-b655-2cfb436a2198">


## Architecture After Hardening / Security Controls
<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/df5ae031-f740-4004-95e7-550ad0e640ef">


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed and exposed to the internet. The Virtual Machines had their Network Security Groups and built-in firewalls fully open, and all other resources were accessible via public endpoints, with no Private Endpoints in use.

For the "AFTER" metrics, I enhanced security by hardening the Network Security Groups to block all traffic except from my admin workstation. Additionally, all other resources were secured using their built-in firewalls and Private Endpoints.

## Attack Maps Before Hardening / Security Controls
<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/0fd60437-a548-470e-bd3e-6b7fea7ff2dc">

<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/01aa4dff-9b07-4a53-9865-dbeddca66237">


<img width="893" alt="image" src="https://github.com/AuvyuanDumas/Azure-SOC/assets/148530581/58928675-fa20-478d-96f5-ef32ac01f400">


## Metrics Before Hardening / Security Controls

The following table shows the metrics I measured in my insecure environment for 24 hours:
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

```All map queries returned no results, indicating no instances of malicious activity were detected during the 24-hour period following the hardening of the environment.```

## Metrics After Hardening / Security Controls

The following table shows the metrics I measured in my environment for another 24 hours, but after I have applied security controls:
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

In this project, I set up a mini honeynet in Microsoft Azure and integrated log sources into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Initially, I measured metrics in the unsecured environment before applying security controls. After implementing these controls, I measured the metrics again. The results demonstrated a substantial reduction in security events and incidents, highlighting the effectiveness of the security measures.

It’s important to note that if the network resources had been heavily utilized by regular users, more security events and alerts might have been generated during the 24-hour period after the security controls were applied.

# Azure-SOC
