# Building a SOC + Honeynet in Azure (Live Traffic) :honey_pot: :lock: 
![68747470733a2f2f692e696d6775722e636f6d2f5a5778653033652e6a7067](https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/bc037cb5-677a-41b6-9389-724559b80b06)


## 🛡️ Introduction 🛡️
In this project, I constructed a mini honeynet in Azure, integrating log sources from various resources into a Log Analytics workspace. This data was utilized by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured security metrics in the initial, unsecured environment for 24 hours, then applied security controls to harden the environment, followed by another 24-hour measurement period. The results of these metrics, which are detailed below, demonstrate the impact of the applied security controls:

The metrics we will show are:
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

For the "BEFORE" metrics, all resources were initially deployed with direct exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls configured with unrestricted access, and all other resources were deployed with public endpoints visible to the internet, rendering private endpoints unnecessary.

In contrast, for the "AFTER" metrics, significant security enhancements were implemented. Network Security Groups were fortified by restricting ALL traffic except for access from designated admin workstations. Additionally, all other resources were shielded by their built-in firewalls and reinforced with the implementation of Private Endpoints.

## Azure Sentinel Before Hardening / Security Controls

<img width="1142" alt="MS Sentinel Incidents (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/459b627c-0911-458c-b530-e054112b3572">

<img width="1450" alt="Incidents (Before)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/520eef67-6b98-4188-86b1-69e480d31780">

## Attack Maps Before Hardening / Security Controls
<img width="1303" alt="2  nsg-malicious-allowed-in (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/49a6dc55-8f79-4521-b0ff-edc2d63f505e">

<img width="1115" alt="1  mssql-auth-fail (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/916bc573-4975-4679-af10-e70f639d112f">

<img width="1111" alt="3  windows-rdp-auth-fail (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/f7788213-b187-4eec-a093-a40e35213d68">

<img width="1240" alt="4  linux-ssh-auth-fail (BEFORE)" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/15234aa1-c447-4e8d-bb12-db454ca969ae">

## Metrics Before Hardening / Security Controls

The following table displays the metrics we measured in the insecure environment for 24 hours:


**Start Time 2024-05-29 19:56:02** 

**Stop Time 2024-05-30 19:56:02**

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 54051
| Syslog                   | 4825
| SecurityAlert            | 30
| SecurityIncident         | 237
| AzureNetworkAnalytics_CL | 2192


## MS Sentinel After Hardening / Security Controls
Microsoft Sentinel is important for monitoring and securing cloud environments. It provides tools to detect and respond to security threats across the organization. By collecting and analyzing data, it helps identify potential issues and offers solutions to improve security. This tool helps protect sensitive information and ensures that the organization stays secure and compliant with industry standards.

<img width="1488" alt="MS Sentinel Incidents AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/46805b22-6699-410d-87ef-33dfa7ae536c">

## NIST 800-53 Cybersecurity Framework 
![info-3-1](https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/2897197e-3eda-44ea-baff-c8466ee3df3b)

The NIST 800-53 framework is important for keeping organizations' information systems secure. It offers a set of guidelines to protect against various threats, helping organizations safeguard sensitive data and comply with regulations. By following these guidelines, organizations can identify and reduce risks, making their digital operations more secure and reliable.

## MS Defender for Cloud After NIST SP 800 53 R5 Regulatory Compliance Application
![defender-for-cloud-pillars](https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/f099ee79-833f-4437-913f-2ad20d41383d)

Microsoft Defender for Cloud is essential for keeping cloud environments secure. It helps manage security across different cloud services and protects against threats. By regularly checking the security of resources, it provides easy-to-follow recommendations and automates security practices. This tool ensures that sensitive data is protected and that the organization meets industry security standards, making cloud operations more reliable and secure.


<img width="1494" alt="NIST" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/a4d2969e-130e-4b4e-9e86-92b566c24dc6">

<img width="1340" alt="MS Defender" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/283e2ef2-bbbb-4201-9a52-10a8dd1b287f">


## Attack Maps After Hardening / Security Controls
<img width="1139" alt="2a  nsg AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/c57f8211-a899-4ecc-a1aa-cde09b6b795e">

<img width="893" alt="1a  mssql AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/62dad4f3-8135-4951-b9f7-98826a799498">

<img width="966" alt="3a  windows AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/55946c00-e449-48d7-b956-8c5f8fcf116f">

<img width="834" alt="4a  linux AFTER" src="https://github.com/TerikaJ/Soc-Honeynet/assets/136477450/10a7cba6-cacf-4206-9cec-935a85262ebd">

## Metrics After Hardening / Security Controls

The following table displays the metrics measured in the secure environment for another 24 hours. This is after the application of security controls:

**Start Time 2024-05-30 19:55:14**

**Stop Time	2024-05-31 19:55:14**

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 26093
| Syslog                   | 43
| SecurityAlert            | 6
| SecurityIncident         | 27
| AzureNetworkAnalytics_CL | 138

| Metric                   | % After Hardening Environment
| ------------------------ | -----
| SecurityEvent            | -51.73%
| Syslog                   | -99.11%
| SecurityAlert            | -80.00%
| SecurityIncident         | -88.61%
| AzureNetworkAnalytics_CL | -93.70%                       
| TOTAL AVERAGE            | -82.63%


## Conclusion

In this project, I constructed a mini honeynet in Microsoft Azure and integrated log sources into a Log Analytics workspace. Utilizing Microsoft Sentinel, I triggered alerts and created incidents based on the ingested logs. Metrics were measured in the insecure environment before applying security controls and then again after implementing these measures. The results showed a significant reduction in security events and incidents post-implementation, demonstrating the effectiveness of the security controls.

It is important to note that if the network resources had been heavily utilized by regular users, more security events and alerts might have been generated within the 24-hour period following the implementation of the security controls.

<h1><p align=center> DONE! Good job! </p></h1>

<h2><p align=center>The Next Demonstration:<br><a href="https://github.com/terikaj/Windows7-Exploit"> Exploiting Windows 7 Accessibility for Password Reset </a></p></h2>

<p align=right> Please delete & clean up your Azure resources when finished!<br>
If you're unsure of how to do this, please click <a href="https://github.com/terikaj/azure-begin?tab=readme-ov-file">HERE</a>

