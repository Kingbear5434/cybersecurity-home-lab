# Screenshots — Cybersecurity Home Lab

Screenshots for this project are captured from the actual lab systems and added here as they become available. Planned captures (see README for the full list):

| Filename | What to open | What should be visible | Hide / redact |
|---|---|---|---|
| `splunk-dashboard.png` | Splunk search & reporting dashboard | Authentication events panel, anomaly panel, time range | Any internal hostnames, usernames |
| `security-onion-alerts.png` | Security Onion alert console (Squert/Security Onion Console) | Triaged IDS alerts with severity | Internal IPs — replace with RFC 5737 examples (192.0.2.x) in annotations |
| `wireshark-capture.png` | Wireshark with a lab capture open | Packet list, protocol details pane | Payload contents with credentials; internal IPs |
| `nessus-scan-report.png` | Nessus scan results page | Severity breakdown, host summary | Target hostnames/IPs |
| `nmap-scan-output.png` | Terminal running an Nmap sweep | Command, open ports, service versions | Target IPs |
| `pfsense-firewall-rules.png` | pfSense firewall rules page | Lab network rule set | WAN IP, DDNS hostnames |

**Rules:** real screenshots only — never label a diagram as a screenshot. Redact before committing. PNG format, ~1600px wide where possible.
