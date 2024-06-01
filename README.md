# Sentinel-Attack-Map

In this lab, I created a vulnerable virtual machine (VM) to serve as a honeypot, attracting and capturing malicious activity, primarily RDP brute force attempts. I set up a log analytics workspace using Microsoft Sentinel to ingest logs from the VM. By downloading a custom PowerShell script, I was able to input IP addresses found in the VM’s Event Viewer under “Failed_RDP” into the script. The script then took these IP addresses and queried https://ipgeolocation.io/ to determine the geolocation of the attackers. The resulting data was copied onto my main computer and inserted into the log analytics workspace. Using these logs, I created a query in Sentinel to visualize the geographic locations of the attacks on an interactive Azure Sentinel map, providing a clear and insightful picture of the attack landscape and demonstrating the power of Azure Sentinel for security monitoring and threat hunting.


# Learning Objectives:
- Configuration & Deployment of Azure resources such as virtual machines, Log Analytics Workspaces, and Azure Sentinel
- Hands-on experience and working knowledge of a SIEM Log Management Tool (Microsoft's Azure Sentinel)
- Understand Windows Security Event logs
- Utilization of KQL to query logs
- Display attack data on a dashboard with Workbooks (World Map)

# Languages and Utilities Used
- PowerShell
- Event Viewer
- Azure Virtual Machine
- Analytics Workspace
- Sentinel

# Demonstration
