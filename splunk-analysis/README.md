## Set Up a Monitoring Environment:
A SIEM solution (Splunk Free) was installed and configured. It was connected to a virtual machine to ingest test log files, including Windows, Linux, SSH, DNS, and FTP logs. Sample logs were uploaded and indexed under Splunk's 'main' index for analysis.
<img width="825" height="385" alt="image" src="https://github.com/user-attachments/assets/b9c21077-63c6-44ac-83dc-57be621ce1e3" />

## Threat Detection
Several queries were created to simulate detection of common attacks and suspicious behaviors. These include brute-force login attempts, unusual DNS requests, suspicious FTP activity, and SSH intrusion attempts.
### Windows Logs - Event Spikes:
<img width="900" height="180" alt="image" src="https://github.com/user-attachments/assets/0368b755-38db-44ed-be55-0f3f49487f6a" />

The query shows spikes of Windows log activity within 5-minute intervals, indicating possible brute force or malware activity.

### Linux Logs - Failed Logins:
<img width="900" height="188" alt="image" src="https://github.com/user-attachments/assets/79db2b9a-bffd-4aa6-9a52-aa72b5be326a" />

Analysis of Linux logs revealed repeated failed login attempts for accounts like 'root' and 'guest', which indicates brute-force attempts.

### SSH Logs - Suspicious IPs:
<img width="900" height="293" alt="image" src="https://github.com/user-attachments/assets/8eb4942b-f448-4c7a-9c59-074852f95edf" />

Top IPs attempting SSH logins were identified. High frequency from specific IPs suggests brute-force attempts.

### DNS Logs - Top Queried Domains:
<img width="900" height="300" alt="image" src="https://github.com/user-attachments/assets/35f5c633-805d-4c54-8a61-323f29519d28" />

DNS analysis showed top queried domains. While many were legitimate (Google, Apple, Microsoft), monitoring unusual or unknown domains is critical for detecting C2 or malware activity.

### FTP Logs - Top IPs:
<img width="900" height="307" alt="image" src="https://github.com/user-attachments/assets/3abb8bef-3b77-4c97-8d97-58c3c361e93c" />

FTP log analysis revealed one IP generating 94% of traffic. This is highly suspicious and suggests exfiltration or abuse of the FTP service.

## Incident Response
Sample incidents were triaged based on findings:
- Classification: Brute-force login attempts (Linux/SSH), abnormal FTP traffic, potential malware traffic in Windows logs.
- Containment: Block offending IP addresses at the firewall, disable suspicious accounts (guest/test).
- Eradication: Patch vulnerable services, reset affected credentials, and remove malicious files.
- Recovery: Restore normal services, re-enable legitimate accounts, and re-monitor for recurrence.

##Documentation
Screenshots of Splunk queries and outputs are included as evidence of detection and analysis. Detection capabilities can be improved by:
- Enabling more field extractions for structured logs.
- Creating real-time alerts for failed logins, large FTP transfers, or unusual DNS queries.
- Building dashboards to monitor key metrics across multiple log sources.
- Integrating Splunk with automated response tools (SOAR) for faster containment.
