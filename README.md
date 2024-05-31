# Soc-Honeynet

# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

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

## Azure Sentinel Before Hardening / Security Controls

<img width="1142" alt="MS Sentinel Incidents (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/459b627c-0911-458c-b530-e054112b3572">

<img width="1450" alt="Incidents (Before)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/520eef67-6b98-4188-86b1-69e480d31780">

## Attack Maps Before Hardening / Security Controls
<img width="1303" alt="2  nsg-malicious-allowed-in (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/49a6dc55-8f79-4521-b0ff-edc2d63f505e">

<img width="1115" alt="1  mssql-auth-fail (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/916bc573-4975-4679-af10-e70f639d112f">

<img width="1111" alt="3  windows-rdp-auth-fail (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/f7788213-b187-4eec-a093-a40e35213d68">

<img width="1240" alt="4  linux-ssh-auth-fail (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/15234aa1-c447-4e8d-bb12-db454ca969ae">

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-05-29 19:56:02
Stop Time 2024-05-30 19:56:02

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 54051
| Syslog                   | 4825
| SecurityAlert            | 30
| SecurityIncident         | 237
| AzureNetworkAnalytics_CL | 2192


## Azure Sentinel After Hardening / Security Controls
<img width="1488" alt="MS Sentinel Incidents AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/46805b22-6699-410d-87ef-33dfa7ae536c">


## MS Defender for Cloud After NIST 800 53 R5 Regulatory Compliance Application
<img width="1494" alt="NIST" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/a4d2969e-130e-4b4e-9e86-92b566c24dc6">

<img width="1340" alt="MS Defender" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/283e2ef2-bbbb-4201-9a52-10a8dd1b287f">


## Attack Maps After Hardening / Security Controls
<img width="1139" alt="2a  nsg AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/c57f8211-a899-4ecc-a1aa-cde09b6b795e">

<img width="893" alt="1a  mssql AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/62dad4f3-8135-4951-b9f7-98826a799498">

<img width="966" alt="3a  windows AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/55946c00-e449-48d7-b956-8c5f8fcf116f">

<img width="834" alt="4a  linux AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/10a7cba6-cacf-4206-9cec-935a85262ebd">

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-05-30 19:55:14
Stop Time	2024-05-31 19:55:14

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 26093
| Syslog                   | 43
| SecurityAlert            | 6
| SecurityIncident         | 27
| AzureNetworkAnalytics_CL | 138

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
