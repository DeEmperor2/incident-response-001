# Malware Traffic Analysis — Google Authenticator Malvertising Campaign

## Overview
A Windows workstation was compromised after a user searched for Google 
Authenticator and clicked a malicious advertisement. This investigation 
analyses the full network traffic capture to identify the infected host, 
malware delivery mechanism, and C2 infrastructure.

## Tools Used
- Wireshark — packet capture analysis
- VirusTotal — IOC reputation checks
- Statistics → Endpoints / Conversations host identification
- Kerberos traffic analysis user account identification
- HTTP Object Export — malware delivery identification

## Key Findings
- Infected host: DESKTOP-L8C5GSJ (10.1.17.215)
- User account: BLUEMOONTUESDAY\hutchens
- Malware delivery via: au.download.windowsupdate.com
- C2 server: 5.252.153.241 (15/91 vendors flagged malicious)
- 9,076 packets exchanged between victim and C2

## Files
- [Incident Report](./incident_report.md)
- [Timeline](./timeline.md)
- [IOC Table](./ioc_table.csv)
- [MITRE ATT&CK Mapping](./mitre_mapping.md)
- [Analyst Notes](./notes.md)
- [Screenshots](./screenshots/)
