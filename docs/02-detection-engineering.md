# Detection Engineering — Baseline ICMP Rule

## Rule

alert icmp any any -> $HOME_NET any (msg:"SOC-LAB ICMP Ping Detected"; sid:1000001; rev:1;)

## Purpose

This rule was created to validate:

- Sensor visibility
- HOME_NET configuration
- Alert logging functionality
- Source and destination attribution

## Test Procedure

1. Snort launched in fast alert mode:
   sudo snort -q -A fast -l /var/log/snort -c /etc/snort/snort.conf -i enp0s3

2. From Windows 10:
   ping 192.168.1.3

## Observed Output

Alert entries written to:
  /var/log/snort/alert

Example:
[1:1000001:1] SOC-LAB ICMP Ping Detected {ICMP} 192.168.1.4 -> 192.168.1.3

## Analysis

- Source IP correctly identified as Windows host (192.168.1.4)
- Destination IP correctly identified as Ubuntu sensor (192.168.1.3)
- Reverse ICMP reply traffic also logged
- Confirms correct HOME_NET scoping (192.168.1.0/24)

## Conclusion

Sensor successfully detects and logs baseline ICMP activity.
This establishes operational readiness for more advanced detection rules.
