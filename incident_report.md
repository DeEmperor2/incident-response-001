# Incident Report — Malvertising / Malware Infection
**Date of Analysis:** June 2026  
**Analyst:** Emmanuel Edwin Jimmy 
**Severity:** High  
**Status:** Contained (lab environment)

---

## Executive Summary
A Windows workstation (DESKTOP-L8C5GSJ) was infected after its user 
searched for Google Authenticator and clicked a malicious advertisement. 
The attacker used a fake download domain disguised as Windows Update 
infrastructure to deliver a payload. The infected machine subsequently 
established persistent communication with a confirmed malicious C2 server 
(5.252.153.241), exchanging over 9,000 packets.

---

## Victim Identification
| Field | Value |
| IP Address | 10.1.17.215 |
| MAC Address | 00:d0:b7:26:4a:74 |
| Hostname | DESKTOP-L8C5GSJ |
| Domain | BLUEMOONTUESDAY |
| User Account | hutchens |

**Method:** Victim identified via Statistics → Endpoints. Host 10.1.17.215 
generated 39,045 of 39,427 total packets far exceeding all other hosts. 
Hostname confirmed via NBNS traffic. MAC address extracted from early DHCP 
packets. Username confirmed via Kerberos AS-REQ packet 258, cname string field.

---

## Attack Vector
The user searched for Google Authenticator and clicked a malicious 
advertisement. This redirected the browser to attacker controlled 
infrastructure. A file was delivered via a domain impersonating 
Microsoft Windows Update:

**Delivery Domain:** au.download.windowsupdate.com  
**Filename:** am_delta_patch_1.421.1491.0_c8e6042b36d8f357a8e298b6f9f2fcde561c2e02.exe  
**File Size:** 398 kB  
**VirusTotal Result:** 0/70 legitimate Microsoft binary used as decoy  

The file itself is a genuine Windows Defender signature update, indicating 
the attacker used a legitimate binary to avoid detection while delivering 
the actual payload through a separate mechanism.

---

## C2 Communication
Following infection, the host established persistent communication with:

**C2 IP:** 5.252.153.241  
**ASN:** AS205775 Neon Core Network LLC  
**Country:** Panama  
**VirusTotal:** 15/91 vendors flagged as malicious  
**Vendors:** BitDefender (Phishing), Kaspersky (Malware), ESET (Malware), 
Fortinet (Malware), Dr.Web (Malicious), SOCRadar (Phishing)  
**Packets exchanged:** 9,076  
**Community Score:** -59  

The volume of traffic (9,076 packets) between the victim and C2 server 
indicates active beaconing behaviour consistent with an established 
malware implant awaiting instructions.

---

## Detection Method
Traffic anomaly detected via Wireshark Statistics → Conversations. 
The connection between 10.1.17.215 and 5.252.153.241 represented the 
largest single conversation in the capture by a significant margin, 
immediately flagging it for investigation.

---

## Defensive Recommendations
1. **Ad blocking at DNS/gateway level** malvertising relies on ads 
   loading in the browser; blocking at network level removes the vector
2. **Web proxy with URL categorisation** would have blocked the fake 
   download domain before the file reached the host
3. **EDR on endpoints** behavioural detection would catch the C2 
   beaconing even if the initial file evaded AV
4. **Network monitoring** anomalous outbound connection volumes should 
   trigger automated alerts
5. **User awareness training** users should download software only from 
   official vendor websites, never via search ads

---

## Lessons Learned
This investigation demonstrated that malware can evade antivirus detection 
by using legitimate binaries as decoys. The real indicator of compromise 
was not the file but the network behaviour persistent high-volume 
communication with an external IP. This reinforces the value of network 
traffic analysis alongside endpoint detection in a SOC environment.
