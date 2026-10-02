# Cybersecurity Home Lab

![Splunk](https://img.shields.io/badge/Splunk-000000?style=for-the-badge&logo=splunk&logoColor=white)
![Security Onion](https://img.shields.io/badge/Security%20Onion-8B0000?style=for-the-badge)
![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-000000?style=for-the-badge)
![pfSense](https://img.shields.io/badge/pfSense-212121?style=for-the-badge)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## Executive Summary

A dedicated, self-built cybersecurity lab for practicing real SOC analyst workflows end to end: log aggregation and alerting with Splunk SIEM, network security monitoring with Security Onion, packet-level analysis with Wireshark, structured vulnerability assessments with Nessus and Nmap, web application testing with Burp Suite, and perimeter defense with pfSense — all running on virtualized infrastructure with documented hardening and incident investigation procedures.

## Project Overview

This lab is a working defensive-security environment, not a demo. It ingests logs from virtual machines, monitors network traffic, runs scheduled vulnerability scans, and produces alerts that get triaged and documented the way a Tier 1 SOC analyst would handle them.

## Objective

Build and operate a realistic security operations environment to develop hands-on skills in SIEM operations, vulnerability management, threat detection, and network forensics — the day-to-day work of a SOC analyst.

## Environment

| Component | Detail |
|---|---|
| Virtualization | Virtual machines on a local hypervisor |
| Network | Segmented lab network behind pfSense firewall |
| SIEM | Splunk (log aggregation, dashboards, alerting) |
| NSM | Security Onion (network security monitoring) |
| Analysis | Wireshark (packet capture and traffic analysis) |
| Scanning | Nessus, Nmap |
| Web testing | Burp Suite |

> **To document:** hypervisor choice and version, host hardware specs, Splunk deployment size.

## Technologies

| Technology | Role |
|---|---|
| Splunk | SIEM — log aggregation, custom dashboards, automated alerting |
| Security Onion | Network security monitoring and alert triage |
| Wireshark | Packet capture and protocol-level traffic analysis |
| Nessus | Credentialed and network vulnerability scanning |
| Nmap | Network discovery, port scanning, service enumeration |
| Burp Suite | Web application security testing |
| pfSense | Lab perimeter firewall and traffic control |
| Linux | Underlying OS for lab systems |

## Architecture

Traffic from lab VMs flows through the pfSense firewall, which also feeds Security Onion's monitoring interfaces. System and application logs forward to Splunk, where saved searches drive dashboards and alerts. Nessus and Nmap run from a dedicated scanning VM against lab targets on a schedule; Burp Suite is used from an analyst workstation VM against intentionally vulnerable lab web applications.

```text
[Lab VMs] ---> [pfSense Firewall] ---> [Security Onion (NSM)]
     |                                         |
     +---- logs ----> [Splunk SIEM] <-----------+
                           |
                    [Dashboards + Alerts]
                           |
                   [Analyst Workstation]
              (Wireshark / Nmap / Nessus / Burp)
```

*Diagram is a recreated visual of the documented architecture.*

## Implementation

- Deployed Splunk and configured log ingestion from lab systems; built custom dashboards for authentication events, network anomalies, and system errors; created saved searches with automated alerting thresholds.
- Deployed Security Onion for full-packet capture and IDS alerting; tuned alert rules to reduce noise while keeping true positives visible.
- Ran structured vulnerability assessments with Nessus (scheduled scans, report review, prioritization by severity) and Nmap (discovery sweeps, service version detection).
- Performed web application security testing with Burp Suite against lab targets: request interception, parameter fuzzing, and session handling review.
- Practiced system hardening on lab VMs (unnecessary service removal, patch management, baseline configuration) and wrote incident investigation documentation for findings.

## Security

- The lab is fully isolated from production/home networks by the pfSense firewall; no lab traffic routes to the internet except controlled updates.
- All scanning and testing targets are lab-owned systems — nothing external is ever scanned or probed.
- Credentials used in the lab are lab-only and never reused elsewhere.

## Challenges

- **Alert noise:** out-of-the-box IDS and SIEM rules generated high false-positive volume.
- **Log volume:** ingesting everything quickly became unmanageable to review.
- **Scan safety:** ensuring vulnerability scans stayed contained to lab targets.

> **To document:** specific tuning examples and before/after alert counts.

## Solutions

- Tuned Security Onion rules and Splunk saved searches iteratively, suppressing known-benign patterns and focusing alerts on high-fidelity detections.
- Filtered log sources to security-relevant events and built summary dashboards instead of reviewing raw logs.
- Ran all scans from the dedicated scanning VM against an explicit target list on the isolated lab network.

## Results

- A working SOC-style pipeline: logs in, detections out, alerts triaged, findings documented.
- Repeatable vulnerability assessment workflow: scan, prioritize, remediate, rescan.
- Documented incident investigation notes for lab findings, building the write-up habit real SOC roles require.

## Screenshots

Screenshots are being added. Planned captures:

| Filename | Content |
|---|---|
| `splunk-dashboard.png` | Splunk security dashboard with authentication and anomaly panels |
| `security-onion-alerts.png` | Security Onion alert console showing triaged IDS alerts |
| `wireshark-capture.png` | Wireshark packet capture with protocol analysis visible |
| `nessus-scan-report.png` | Nessus scan results with severity breakdown |
| `nmap-scan-output.png` | Nmap discovery sweep output in terminal |
| `pfsense-firewall-rules.png` | pfSense firewall rule set for the lab network |

Capture instructions are in [`screenshots/README.md`](screenshots/README.md).

## Lessons Learned

- A SIEM is only as good as its tuning — default rules drown you in noise; the real skill is shaping detections to the environment.
- Defense in depth matters even in a lab: firewall segmentation caught misconfigurations that host hardening alone would have missed.
- Writing up findings forces rigor — an alert you can't explain in a paragraph isn't understood yet.

## Future Improvements

- Add SOAR-style automated response playbooks for common alert types.
- Expand log sources to cloud-style audit logs for hybrid visibility.
- Build a detection-engineering notebook tracking each rule's precision over time.

---

*Built and documented by Christopher Bias — hands-on systems, security, and automation work.*
