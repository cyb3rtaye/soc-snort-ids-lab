# SOC Snort IDS Detection Engineering Lab

This project demonstrates the design, implementation and validation of custom intrusion detection rules using **Snort IDS** to detect simulated adversary activity in a controlled lab environment.

## Project Overview

The lab simulates a multi-stage cyber attack against a monitored system and adapts detection logic aligned with **MITRE ATT&CK techniques**.

The goal is to demonstrate practical SOC detection engineering skills including:

- Network traffic analysis
- Signature development
- Threat detection mapping
- Attack simulation
- Detection validation

## Lab Architecture

+------------------+
| Attacker System  |
| Windows VM       |
| (Nmap + Ncat)    |
+--------+---------+
         |
         | Attack Traffic
         v
+---------------------------+
| Target Server             |
| Ubuntu VM                 |
| Python Web Server :8080   |
| Snort IDS Sensor          |
+---------------------------+

## SOC Dashboard (Detection Coverage)

![SOC Detection Coverage Dashboard](assets/diagrams/soc-detection-dashboard.png)

## Attack Chain (End-to-End)

![Attack Chain Diagram](assets/diagrams/attack-chain-diagram.png)

## Simulated Attack Scenarios

The following adversary behaviours were simulated and detected:

| Attack Simulation             | Detection                         |
|-------------------------------|-----------------------------------|
ICMP Host Discovery             | Snort ICMP rule                   |
Port Scanning                   | SYN scan detection                |
Admin Panel Enumeration         | HTTP request inspection           |
Web Login Brute Force           | POST threshold detection          |
Reverse Shell Command & Control | Outbound TCP connection detection |

## MITRE ATT&CK Coverage

| Tactic          | Technique                               |
|-----------------|-----------------------------------------|
Reconnaissance    | T1595 Active Scanning                   |
Reconnaissance    | T1046 Network Service Discovery         |
Initial Access    | T1190 Exploit Public Facing Application |
Credential Access | T1110 Brute Force                       |
Command & Control | T1071 Application Layer Protocol        |

## Detection Validation

All detection rules were validated using controlled attack simulations and confirmed via Snort alert logs.

Example detection:

[1:1000008:7] SOC-LAB Reverse Shell Outbound Connection
{TCP} 192.168.1.3 -> 192.168.1.4:4444

## Skills Demonstrated

- Intrusion Detection Engineering
- Network Traffic Analysis
- Snort Rule Development
- Threat Detection Mapping (MITRE ATT&CK)
- Attack Simulation
- Security Monitoring

## Future Improvements

- Integration with SIEM (Elastic / Splunk)
- PCAP analysis with Wireshark
- Detection tuning and false positive reduction
- Threat hunting workflows