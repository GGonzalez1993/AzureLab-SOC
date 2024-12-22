# AzureLab-SOC
# Building a SOC + Honeynet in Azure (Live Traffic)
![Lab Overview - Gabriel Gonzalez](https://github.com/user-attachments/assets/4675afdd-ad8c-4012-8af4-0031f12edcce)


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which Microsoft Sentinel then uses to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, applied some security controls to harden the environment, measured metrics for another 24 hours, and then showed the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Before Hardening _ Security Controls - Gabriel Gonzalez](https://github.com/user-attachments/assets/352cd2a0-b795-4587-97c7-c5af8e8e12d3)


## Architecture After Hardening / Security Controls
![Architecture After Hardening _ Security Controls - Gabriel Gonzalez](https://github.com/user-attachments/assets/a4ef06dc-a2d9-406d-8299-4a7b871ad4d2)


I used the following components in my mini honeynet within the Azure environment:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open to attack, and all other resources were deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic except my admin workstation, and all other resources were protected by their built-in firewalls and Private Endpoint.

## Attack Maps Before Hardening / Security Controls
![Before_NSG Malicious Allowed - 24hr - Gabriel Gonzalez](https://github.com/user-attachments/assets/bfd6e03e-5018-4254-9b61-45a92878ffe5)<br>
![Before_Linux SSH Auth Fail - 24hr - Gabriel Gonzalez](https://github.com/user-attachments/assets/facc7cf6-ef6b-4f7c-b1b2-150343da5326)<br>
![Before_Windows RDP Auth Fail - 24hrs - Gabriel Gonzalez](https://github.com/user-attachments/assets/91440d8a-5ef3-4e63-9418-a81dc86f8e8d)<br>
![Before_MySQLAuthFails-24hrs-Gabriel Gonzalez](https://github.com/user-attachments/assets/b86d2961-7b74-4901-9710-532d22a7bc59)<br>


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-12-15 16:41
Stop Time 2024-12-16 16:41

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 28873
| Syslog                   | 47314
| SecurityAlert            | 0
| SecurityIncident         | 283
| AzureNetworkAnalytics_CL | 3549

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24-hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we applied security controls:
Start Time 2024-12-20 10:49
Stop Time	2024-12-20 10:49

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 612
| Syslog                   | 8
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

This project involved building a small honeynet in Microsoft Azure and integrating log sources into a workspace for Log Analytics. Microsoft Sentinel triggered alerts and created incidents based on the ingested logs. Furthermore, metrics were assessed in the unsecured environment before the security controls were applied and subsequently re-evaluated after security measures were implemented. Notably, the number of security events and incidents was drastically reduced after the security controls were applied, demonstrating their effectiveness.

If regular users heavily utilized the resources within the network, more security events and alerts may likely have been generated within the 24-hour period following the implementation of the security controls.
