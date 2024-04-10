# Summary and Results

![image](https://github.com/Ashrafs-Tech/Summary-and-Results/assets/166546026/4623a787-f135-4e76-acf2-1dfa11cfeee2)

## Intro

For this project, I constructed a honeynet within the Azure platform and gathered log data from multiple sources into a Log Analytics workspace. This workspace serves as the foundation for Microsoft Sentinel, enabling the creation of attack maps, alert triggers, and incident reports. I conducted security metric assessments in the vulnerable environment for 24 hours, implemented security measures to fortify the environment, and subsequently reevaluated the metrics for another 24-hour period. Below, I will present the measured security metrics, which include:

AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)
SecurityAlert (Log Analytics Alerts Triggered)
SecurityEvent (Windows Event Logs)
SecurityIncident (Incidents created by Sentinel)
Syslog (Linux Event Logs)

## Azure Components, Technologies, and Regulations 

- Azure Key Vault for Secure Secrets Management
- Azure Network Security Groups (NSG)
- Azure Storage Account for Data Storage
- Azure Virtual Network (VNet)
- Command Line Interface (CLI) for System Management
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Microsoft Defender for Cloud to Protect Cloud Resources
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- NIST SP 800-53 Revision 5 for Security Controls
- NIST SP 800-61 Revision 2 for Incident Handling Guidance
- PowerShell for Automation and Configuration Management
- Virtual Machines (1 Windows VMs, 1 Linux VM)
- Windows Remote Desktop for Remote Access

## Architecture Before Hardening / Security Controls

During the initial phase of the project, an experimental environment was established and made accessible via the public Internet, inviting potential threat actors to probe and attempt unauthorized access. The purpose was to analyze the attack strategies employed by these actors by presenting seemingly vulnerable virtual machines. With this strategy in mind, a Windows virtual machine was set up to host a SQL database alongside a Linux server deployed openly. Both virtual machines had their network security groups (NSGs) configured with a policy of "Allow All" traffic. Additionally, a storage account and key vault were provisioned to further attract potential attackers, with public endpoints exposed to the internet. Throughout this phase, Microsoft Sentinel actively monitored the unsecured environment, utilizing logs aggregated by the Log Analytics workspace for analysis and detection of potential security incidents.


## windows-rdp-smb-auth-fail

![image](https://github.com/Ashrafs-Tech/Summary-and-Results/assets/166546026/c19cddb0-a5d1-4f53-bb30-ec006d23c62f)


## syslog-linux-ssh-auth-fail

![image](https://github.com/Ashrafs-Tech/Summary-and-Results/assets/166546026/805265bf-b5bc-41bd-89eb-9f61a9348fa4)



## nsg-malicious-allowed-in

![image](https://github.com/Ashrafs-Tech/Summary-and-Results/assets/166546026/9a48d946-749c-452c-a02b-d531a7492b88)





All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

## Architecture AFTER Hardening and Implementing Security Controls

In the "AFTER" phase of the project, significant efforts were made to fortify the environment and enforce stringent security measures in alignment with NIST SP 800-53 Rev5 SC-7(3) Access Points. These security enhancements included:

- Network Security Groups (NSGs): The NSGs underwent hardening procedures by implementing strict policies that blocked all inbound and outbound traffic except for specific public IP addresses authorized to access the virtual machines. This measure guaranteed that only trusted traffic from designated sources could reach the virtual machines.

- Built-in Firewalls: Azure's built-in firewalls were strategically configured on the virtual machines to establish barriers against unauthorized access and defend the resources from potential malicious connections. This configuration involved fine-tuning the firewall rules based on the function and responsibilities of each VM, effectively reducing the exposure of attack surfaces accessible to malicious actors.

- Private Endpoints: A critical step in enhancing the security posture involved replacing Public Endpoints with Private Endpoints for Azure Key Vault and Storage Containers. This transition ensured that access to these sensitive resources was confined within the virtual network, safeguarding them from exposure to the public internet and unauthorized access attempts.

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls: Start Time 2024-04-07 15:37 Stop Time 2024-04-08 15:37

| Metric                   | Count
| ------------------------ | -----
| AzureNetworkAnalytics_CL | 528
| SecurityAlert            | 52
| SecurityEvent            | 15953
| SecurityIncident         | 268
| Syslog                   | 3068


## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls: Start Time 2024-04-09 14:30 Stop Time 2024-04-10 14:30

| Metric                   | Count
| ------------------------ | -----
| AzureNetworkAnalytics_CL | 0
| SecurityAlert            | 0
| SecurityEvent            | 600
| SecurityIncident         | 0
| Syslog                   | 25


## Conclusion 

In this project, I leveraged Microsoft Azure to establish a honeynet and aggregate logs from various resources into a Log Analytics workspace. Additionally, I employed Microsoft Sentinel to generate attack maps, alerts, and incident reports. Over a span of 48 hours, I collected metrics to underscore the importance of configuring cloud assets with security as a top priority. Through the implementation of a specific section of NIST SP 800-53 Rev5, I managed to significantly decrease the frequency of security events and incidents.

It's important to note that if the network's resources were regularly accessed by ordinary users, the introduction of security controls might have led to a higher number of security events and alerts being triggered within a 24-hour timeframe.
