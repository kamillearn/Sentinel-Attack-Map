# Azure Sentinel Threat Hunting with Honeypots

In this lab, I created a vulnerable virtual machine (VM) to serve as a honeypot, attracting and capturing malicious activity, primarily RDP brute force attempts. I set up a log analytics workspace using Microsoft Sentinel to ingest logs from the VM. By downloading a custom PowerShell script, I was able to input IP addresses found in the VM’s Event Viewer under “Failed_RDP” into the script. The script then took these IP addresses and queried https://ipgeolocation.io/ to determine the geolocation of the attackers. The resulting data was copied onto my main computer and inserted into the log analytics workspace. Using these logs, I created a query in Sentinel to visualize the geographic locations of the attacks on an interactive Azure Sentinel map, providing a clear and insightful picture of the attack landscape and demonstrating the power of Azure Sentinel for security monitoring and threat hunting.


# Learning Objectives:
- Configuration & Deployment of Azure resources such as virtual machines, Log Analytics Workspaces, and Azure Sentinel
- Hands-on experience and working knowledge of a SIEM Log Management Tool (Microsoft's Azure Sentinel)
- Understand Windows Security Event logs
- Utilization of KQL to query logs
- Display attack data on a dashboard with Workbooks (World Map)

# Languages and Utilities Used
- PowerShell
- Services within Azure: Log Analytics Workspace and Sentinel (Mircosoft's SIEM)
- Kusto Query Language (KQL - Used to build world map)
- Remote Desktop Protocol (RDP)
- 3rd Party API: ipgeolocation.io
- Event Viewer
- Custom [Powershell Script](https://github.com/kamillearn/Threat-Hunting-with-Honeypots/blob/main/Log_exporter.ps1) written by [Josh Madakor](https://github.com/joshmadakor1)

# Demonstration
### Powershell
#### The PowerShell script in this lab serves several purposes:

- **Extract IP Addresses**: The script extracts IP addresses from the VM's Event Viewer logs, specifically under **"Audit Failure"** entries, which indicate failed Remote Desktop Protocol (RDP) login attempts.
![Screenshot 2024-06-01 200709](https://github.com/kamillearn/Sentinel-Attack-Map/assets/107491029/95336891-5294-4ea6-a890-42619cb6788c)

- **Geolocation Lookup**: The script then takes these extracted IP addresses and queries the https://ipgeolocation.io/ service to obtain geolocation data for each IP address. This includes information such as the **country, region, city,** and possibly the coordinates (**latitude and longitude**) associated with each IP address.
![image](https://github.com/kamillearn/Sentinel-Attack-Map/assets/107491029/6fe5488a-db67-43cd-a2fd-0f7d72aba591)
![Screenshot 2024-06-01 195015](https://github.com/kamillearn/Sentinel-Attack-Map/assets/107491029/86c2c132-0d65-4fad-8225-1a4c2b70610c)


- **File Creation**: The script compiles these attackers geolocation data into a custom log file called **failed_rdp**. This file is then copied onto the main computer for further processing.
![Screenshot 2024-06-01 201313](https://github.com/kamillearn/Sentinel-Attack-Map/assets/107491029/27602b0d-6946-44b1-a833-d7522894848e)

- **Log Analytics Insertion**: Finally, the script ensures that this geolocation data is inserted into the log analytics workspace in Microsoft Sentinel. This enables the visualization and analysis of attack data within Sentinel.
![image](https://github.com/kamillearn/Sentinel-Attack-Map/assets/107491029/209f494e-0b08-460f-a042-a755f130b950)

### Sentinel 

#### Sentinel purposes in this lab:

- **Ingestion of Logs**: Sentinel ingests logs from our poor vulnerable Virtual Machines's custom log **"Failed_RDP"** created by the powershell from the Event Viewer **"Audit Failure"** entries or attempts.

- **Visualization of Attack Data**: Using the geolocation data such as **country, region, city,** and coordinates (**latitude and longitude**) associated with each IP address obtained from the PowerShell script, Sentinel visualizes the geographic locations of the attackers on an interactive map. This visualization provides insights into the origin and distribution of attack attempts.

*World map showing the amount of attackers utilizing RDP brute force and where they are from*
![Screenshot 2024-06-01 183806](https://github.com/kamillearn/Sentinel-Attack-Map/assets/107491029/177dfd9e-7734-4fb2-a239-eeb095c2525e)

