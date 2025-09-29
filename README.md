🕵️ Honeypot Project
📖 Overview

This project sets up and deploys a honeypot lab environment to attract, log, and analyze malicious activity. The purpose is to better understand attacker tactics, techniques, and procedures (TTPs) while practicing defensive monitoring. The lab uses pfSense as the firewall and gateway, Cowrie as the primary honeypot, and Splunk for centralized log ingestion and visualization.

⚙️ Lab Architecture

Host Environment: VMware Workstation Pro 17

Virtual Machines:

pfSense Firewall – controls inbound/outbound traffic (NAT + port forwarding)

Cowrie Honeypot – emulates SSH and Telnet services, logs attacker sessions

Splunk Enterprise – collects and analyzes honeypot logs

Network Design:

WAN (pfSense → Internet/attacker entry point)

LAN (pfSense → Honeypots + Splunk)

Only ports 22 (SSH) and 23 (Telnet) are forwarded to the honeypot

[ Attacker ] → [ pfSense Firewall ] → [ Cowrie Honeypot ]
                                 ↘→ [ Splunk SIEM ]

🚀 Deployment Steps
1. pfSense Firewall

Create a VM for pfSense with two network adapters:

WAN: NAT

LAN: Host-only/Internal network

Configure firewall rules:

Allow inbound SSH (22) and Telnet (23)

Forward traffic on those ports to the Cowrie honeypot VM

Verify rules with a port scan from outside (e.g., nmap).

2. Cowrie Honeypot

Deploy an Ubuntu VM for Cowrie.

Install dependencies and clone Cowrie from GitHub.

Configure cowrie.cfg:

Enable SSH and Telnet listening

Configure log output (JSON and syslog)

Start Cowrie with bin/cowrie start.

Confirm Cowrie is capturing attacker login attempts and session activity.

3. Splunk Enterprise

Install Splunk Enterprise on a separate VM.

Configure Splunk inputs to ingest Cowrie logs via file monitoring or syslog.

Build dashboards to track:

Attacker IP addresses

Commands executed

Session frequency and duration

MITRE ATT&CK mapping for observed behaviors

📊 Use Cases

Detect brute-force attempts on SSH and Telnet

Analyze attacker command sequences and identify TTPs

Collect and enrich attacker IPs with OSINT (AbuseIPDB, OTX, etc.)

Visualize attack activity with Splunk dashboards

📷 Screenshots

Recommended screenshots to include:

pfSense firewall rule configuration

Cowrie session logs

Splunk dashboards

🔒 Security Considerations

Run honeypots in an isolated lab environment only

Do not expose directly to production networks

Use pfSense segmentation to block attacker pivoting

Rotate logs and monitor system resources

📝 Future Enhancements

Add Dionaea or HoneyDB honeypots for malware collection

Automate IOC enrichment with Python scripts and APIs

Integrate with SOAR tools for automated alerting

Expand SIEM coverage to Elastic or QRadar

📚 References

Cowrie Honeypot

pfSense Documentation

Splunk Enterprise

MITRE ATT&CK
