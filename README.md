# Benign

## Objective
Investigate a suspected LOLBin (Living Off the Land Binary) abuse on a corporate Windows workstation using Splunk. The goal was to detect the use of certutil.exe to download a malicious payload from a C2 server, leveraging Windows event logs.

### Skills Learned
- LOLBin abuse detection (certutil.exe)
- Splunk SPL query writing for Windows event log analysis
- Process execution chain reconstruction
- C2 download detection via command-line argument analysis
- MITRE ATT&CK T1105 (Ingress Tool Transfer) mapping

### Tools Used
- Splunk SIEM (SPL queries)
- Windows Security Event Logs (Event ID 4688)
- Sysmon logs (Event ID 1 - Process Creation)
- MITRE ATT&CK framework

## Steps
Investigation began by querying Splunk for process creation events (Sysmon Event ID 1) on the HR workstation. SPL was used to filter on certutil.exe execution and inspect the full command-line arguments. The command revealed a download cradle fetching a payload from an external C2 server. The parent process was identified to reconstruct the execution chain. The technique was mapped to MITRE ATT&CK T1105. IOCs including the C2 URL and payload filename were documented.

*Ref 1: Splunk SPL query isolating certutil.exe execution with malicious command-line arguments*

<img width="1561" height="601" alt="p1" src="https://github.com/user-attachments/assets/6a6853c3-cebf-4372-a7e8-27fa9f3eee93" />

*Ref 2: Process execution chain from parent process to certutil C2 download*

<img width="912" height="582" alt="P2" src="https://github.com/user-attachments/assets/9fd4fa67-bdc6-408d-be32-5bf906df6d78" />



