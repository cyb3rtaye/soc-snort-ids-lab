# SOC Snort IDS Lab — Detection Engineering & Alert Triage

A SOC-style portfolio case study demonstrating:
- deploying Snort as a network IDS sensor
- building and testing custom detection rules
- generating controlled suspicious activity inside a lab
- triaging alerts and documenting findings like a Tier1/Tier2 analyst

## Lab Environment
- Ubuntu (Sensor): 192.168.1.3 (enp0s3)
- Windows 10 (Workstation): 192.168.1.4
- Subnet: 192.168.1.0/24

## Repo Structure
soc-snort-ids-lab/
docs/ # setup + detections + investigation writeups
rules/ # custom Snort rules used in this project
artifacts/
pcaps/ # optional small captures (sanitized)
screenshots/ # evidence screenshots
assets/
diagrams/ # diagrams used in docs/README

## Documentation Index
- docs/00-scope.md
- docs/01-sensor-deployment.md
- docs/02-detection-engineering.md
- docs/03-alert-triage.md
- docs/04-incident-report.md

