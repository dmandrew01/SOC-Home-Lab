# SOC Home Lab Build – Wazuh & pfSense, Security Onion, Elastic

## Objective
The goal of this project is to build a **fully functional Security Operations Center (SOC) home lab** that simulates an enterprise environment for hands-on cybersecurity monitoring, detection, and response.  

This lab provides a safe, isolated environment to collect, analyze, and alert on both **network** and **endpoint telemetry**, using industry-grade tools such as **Security Onion**, **Elastic Stack**, **Wazuh**, and **pfSense**.  

The objective is to gain real-world experience with SIEM, IDS/IPS, EDR, and firewall technologies while learning to hunt and respond to threats using open-source security tools.

## Skills Learned
- SIEM deployment and management (Wazuh, Security Onion, Elastic)
- IDS/IPS configuration using Zeek and Suricata
- Endpoint telemetry and agent management (Wazuh Agent, Sysmon, Elastic Agent)
- Log ingestion, normalization, and analysis across Windows and Linux systems
- Network segmentation and routing with pfSense
- Writing and tuning detection rules for Sysmon and Suricata
- Threat hunting using KQL and dashboard correlation
- MITRE ATT&CK mapping and adversary emulation (Atomic Red Team, CALDERA)
- Network traffic capture and flow analysis (Zeek conn.log, Suricata eve.json)
- Virtualization and network design using VirtualBox/KVM

## Tools Used

### SIEM & Detection
- **Wazuh** – SIEM + EDR platform
- **Sysmon** – Endpoint process and telemetry monitoring (SwiftOnSecurity config)
- **Security Onion 2.4** – Includes Zeek, Suricata, Elastic, SOC UI
- **Elastic Stack** – Elasticsearch, Kibana, Fleet

### Endpoints
- **Windows 10/11 VM** – Sysmon + Elastic/Wazuh Agent
- **Ubuntu Server VM** – Linux telemetry + Elastic Agent
- **Kali Linux VM** – Traffic generation, benign + offensive simulation

### Network & Firewall
- **pfSense Firewall** – Network segmentation, routing, logging
- VirtualBox Host-only, NAT, and Internal networks

### Adversary Emulation
- **Atomic Red Team** – Safe MITRE ATT&CK test execution
- **MITRE CALDERA** – Autonomous multi-stage adversary simulation
- **OWASP Juice Shop** – Web application traffic generation

### Virtualization
- **VirtualBox / KVM** – Isolated lab environment

## Steps

### **Planned & Designed the SOC Architecture**
- Created virtual networks:
  - **Management (Host-only)** – For admin access  
  - **Monitored (Internal Network)** – For IDS/IPS visibility  
  - **NAT Network** – For Internet access  
- Designed topology for Security Onion, pfSense, and endpoints to communicate safely within isolated subnets.

### **Deployed Wazuh Server and pfsense Server**
- Created a new VM with:
  - **RAM:** 12 GB  
  - **CPU:** 6 vCPUs  
  - **Disk:** 200 GB  
- Attached two NICs:
  - Adapter 1 → Host-only (Management)  
  - Adapter 2 → Internal Network “MONITORED”  
- Installed Wazuh from ISO.
- Assigned Adapter 1 as management and Adapter 2 as sniffing interface.
- Completed setup and accessed the SOC UI via browser (HTTPS on mgmt IP).

### **Deployed Wazuh agent and Configured Endpoint Monitoring**
#### Windows Endpoint
- Installed Wazuh agent on Ubuntu 22.04 and Windows 10/11 VM connected to the monitored network.
- Installed **Sysmon** using SwiftOnSecurity config:
  ```powershell
  .\sysmon64.exe -accepteula -i sysmonconfig-export.xml

## Screenshots
- <a href="https://github.com/dmandrew01/portfolio/blob/main/images/SOC%20HomeLab%20VMs.png">Screenshot of VMs I am using in my SOC Home Lab</a>
- <a href="https://github.com/dmandrew01/portfolio/blob/main/images/wazuh%20active%20agents.png">Screenshot of active agents (Ubuntu and Windows 11 VMs)</a>
- <a href="https://github.com/dmandrew01/portfolio/blob/main/images/wazuh%20agent%20dashboard.png">Screenshot of Wazuh Dashboard on Ubuntu and Windows 11 VMs</a>
- <a href="https://github.com/dmandrew01/portfolio/blob/main/images/wazuh%20agent%20dashboard2.png">Screenshot of Wazuh Dasboard showing active alerts and Threat Monitoring Dashboard</a>
- <a href="https://github.com/dmandrew01/portfolio/blob/main/images/wazuh%20vm.png">Screenshot of the main Wazuh Management Server showing Wazuh is actively running</a>
- <a href="https://github.com/dmandrew01/portfolio/blob/main/images/pfsense%20vm.png">Screenshot of pfsense Server running</a>
