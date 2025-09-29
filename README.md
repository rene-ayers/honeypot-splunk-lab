# 🕵️ Honeypot Project

## Overview
This project demonstrates a honeypot lab environment used to attract, log, and analyze malicious activity. The goal is to better understand attacker tactics, techniques, and procedures (TTPs) while practicing defensive monitoring.  

The lab includes:
- **pfSense** as the firewall and gateway  
- **Cowrie** as the SSH/Telnet honeypot  
- **Splunk** for centralized log ingestion and dashboards  

---

## Lab Architecture
- **Host:** VMware Workstation Pro 17  
- **VMs:** pfSense Firewall, Cowrie Honeypot, Splunk Enterprise  
- **Network:**  
  - WAN → pfSense (Internet entry point)  
  - LAN → Honeypots + Splunk  
  - Ports 22 (SSH) and 23 (Telnet) forwarded to Cowrie  

```text
[ Attacker ] → [ pfSense Firewall ] → [ Cowrie Honeypot ]
                                 ↘→ [ Splunk SIEM ]
