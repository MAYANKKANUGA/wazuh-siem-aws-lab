# Wazuh SIEM Security Monitoring Lab

## Objective
The goal of this lab was to deploy a centralized Wazuh SIEM environment on AWS, enroll cross-platform endpoints, simulate a brute-force attack, and develop custom detection rules mapped to the MITRE ATT&CK framework.

## Architecture & Infrastructure
* **Wazuh Server:** Ubuntu 22.04 LTS (AWS EC2)
* **Endpoint 1:** Ubuntu 22.04 LTS (AWS EC2)
* **Endpoint 2:** Windows Server 2025 Datacenter (AWS EC2)
* **Network Security:** Configured AWS Security Groups to restrict management access to trusted IPs while allowing agent registration (Port 1515) and communication (Port 1514).

## Project Workflow

### 1. SIEM Deployment & Agent Enrollment
* Provisioned the Wazuh Manager, Indexer, and Dashboard on an Ubuntu EC2 instance.
* Successfully installed and authenticated Wazuh agents on both Linux and Windows Server environments, verifying active communication in the dashboard.

### 2. Attack Simulation (SSH Brute Force)
* Utilized `Hydra` and the `rockyou.txt` wordlist from the local attacker machine to launch a targeted SSH brute-force attack against the Linux agent.
* Verified the ingestion of Event 2501 (User authentication failure) in the Wazuh Threat Hunting dashboard.

### 3. Custom Rule Creation & MITRE Mapping
* To elevate the visibility of the attack, I navigated to `/var/ossec/etc/rules/local_rules.xml` and engineered a custom detection rule.
* **Rule Logic:** Configured a Level 15 (Critical) alert to trigger when multiple authentication failures occur from the same source IP within a 60-second timeframe.
* **MITRE ATT&CK:** Mapped the custom rule directly to **T1110 (Brute Force)**.
* **Validation:** Re-ran the Hydra simulation, successfully triggering the custom Level 15 "Critical: SSH Brute Force Attack Detected" alert.

## Skills Demonstrated
* Cloud Infrastructure Management (AWS EC2, Security Groups, SSH Key Management)
* SIEM Administration & Agent Deployment
* Log Analysis and Querying 
* Threat Simulation (Hydra)
* Detection Engineering (Custom XML rule creation mapping to MITRE ATT&CK)
