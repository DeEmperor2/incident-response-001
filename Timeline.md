# Attack Timeline — Malvertising Infection

| Time (WAT) | Event |
| Session start | Host 10.1.17.215 joins network DHCP handshake observed |
| Early session | Kerberos authentication — user hutchens logs into BLUEMOONTUESDAY domain |
| Mid session | User searches for Google Authenticator clicks malicious advertisement |
| Packet ~24913 | HTTP session begins with 199.232.214.172 |
| Packet 24926 | Malicious .exe downloaded from au.download.windowsupdate.com (398 kB) |
| Post download | C2 communication begins with 5.252.153.241 |
| Ongoing | 9,076 packets exchanged between victim and C2 active beaconing |
