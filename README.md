# Honeypot-Splunk-Lab  

Honeypot (Cowrie) with Splunk Enterprise for log monitoring and network traffic analysis in a VMware lab environment.  

---

## Project Overview  

- Deploy a **Cowrie honeypot** to simulate vulnerable services  
- Capture malicious activity directed at the honeypot  
- Forward logs into **Splunk Enterprise** for real-time monitoring and detection  
- Build dashboards and alerts to analyze attacker behavior  

👉 The goal is to show how a honeypot integrates with a SIEM for hands-on **security monitoring and threat analysis**.  

---

## Technologies Used  

- **VMware Workstation Pro** – Virtualized lab environment  
- **pfSense** – Firewall and NAT port forwarding  
- **Ubuntu** – Honeypot and Splunk host  
- **Cowrie Honeypot** – SSH/Telnet emulation  
- **Docker** – Containerized Splunk Enterprise deployment  
- **Splunk Enterprise** – Log collection, parsing, dashboards, and alerting  

---

## Lab Architecture  

[ Attacker (simulated) ]  
↓  
[ pfSense Firewall ] -- Port Forwarding (22 → 2222)  
↓  
[ Ubuntu VM: Cowrie Honeypot ]  
↓  
[ Splunk Enterprise Container ] → Dashboards & Alerts  

---

## Setup Instructions  

### 1. Configure Networking  
- Set up **pfSense VM** for NAT + port forwarding.  
- Forward traffic from **WAN → Honeypot** (SSH on port **2222**).  

---

### 2. Deploy Cowrie Honeypot  
```bash
docker run -d -p 2222:2222 cowrie/cowrie

docker run -d --name splunk \
  -p 8000:8000 -p 8089:8089 -p 9997:9997 -p 1514:1514/udp \
  -e SPLUNK_START_ARGS="--accept-license" \
  -e SPLUNK_GENERAL_TERMS=Y \
  -e SPLUNK_PASSWORD="Splunk123!" \
  splunk/splunk:latest

