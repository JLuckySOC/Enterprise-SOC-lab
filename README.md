# Enterprise-SOC-lab
Enterprise SOC Lab -- Personal Project 2025

This project is a hands-on SOC (Security Operations Center) simulation lab I built to practice enterprise-style detection and monitoring.
It uses a segmented virtual environment with Windows, Active Directory, Splunk, and pfSense to generate and analyze security events.

Lab Architecture

* pfSense Firewall – Provides segmentation between internal LAN (192.168.56.0/24) and DMZ (192.168.57.0/24).
* Windows Server 2022 DC – Domain Controller for unlucky.local, runs DNS/AD DS.
* Windows 11 Workstation – Domain-joined endpoint for user activity.
* Kali Linux Attacker – Simulated adversary, used for scanning/brute force attempts.
* Splunk – Centralized logging, ingestion from Splunk Universal Forwarder, detection dashboards.

Authentication & Account Activity

* Tracks failed vs. successful logons in real time
* Highlights top failed accounts and sources
* Displays new account creation events
* Provides log volume trends by sourcetype

Security Event Volumes

* Hourly visualization of Windows Security EventCodes
* Detection of brute force / credential stuffing attempts

Simulated Attacks

* Brute Force Attempts – Multiple failed logons to simulate credential guessing.
* Reconnaissance – nmap and ICMP scans from Kali Linux.
* Persistence Tests – New account creation for red team activity simulation.

Repo Structure
soc-lab-simulation/
│

├── images/

│   ├── diagrams/          # Network architecture diagrams

│   └── screenshots/       # Splunk dashboards, firewall rules, AD proof

│

├── docs/

│   └── setup-notes.md     # Configs, steps, troubleshooting (in progress)

│

└── README.md              # You are here
