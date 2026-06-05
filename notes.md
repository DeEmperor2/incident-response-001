# Analyst Notes

## Key Decision Points
- Host identified by packet volume anomaly 39,045 of 39,427 total packets
- Username found in Kerberos AS-REQ packet 258, cname-string field
- C2 confirmed via VirusTotal 15/91 detections, community score -59
- Downloaded file was clean (0/70) attacker used legitimate binary as decoy
- Real compromise evidence was network behaviour, not file detection

## What I Would Do Next In a Real Incident
1. Isolate 10.1.17.215 from the network immediately
2. Preserve full disk image before any remediation
3. Submit 5.252.153.241 to threat intel platforms for wider blocking
4. Check all other hosts for connections to 5.252.153.241
5. Pull EDR logs from DESKTOP-L8C5GSJ for process execution history
6. Notify hutchens and reset all credentials

## Tools Used
- Wireshark 
- VirusTotal
- Statistics → Endpoints, Conversations, Protocol Hierarchy
- HTTP Object Export
- Kerberos traffic analysis

## PCAP Source
malware-traffic-analysis.net — 2025-01-22 traffic analysis exercise
