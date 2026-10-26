# NETWORK-SCANNING (NETWORK-DISCOVERY-DETECTION-PROJECT) 

THIS IS MY NETWORK DISCOVERY DETECTION HANDS ON PRACTICAL PROJECT WITH TRYHACKME

Network Scanning & Threat Detection Lab: Internal, External, Horizontal & Vertical Scanning Analysis. A hands-on threat detection and log analysis project focusing on identifying network discovery tactics, distinguishing between internal and external scanning vectors, and analyzing port scan behaviors using Linux command-line utilities.

Table of Contents
Project Overview
Network Scanning Classification
Tools & Technologies Used
Key Investigation Areas
Conclusion

📌 Project Overview

Network discovery detection involves analyzing log files to identify active scanning activity, which often marks the early stages of an attack lifecycle. This project focuses on analyzing session log files to detect internal and external reconnaissance techniques, map activity to the MITRE ATT&CK framework, and differentiate between horizontal and vertical network scans.

⚙️ Network Scanning Classification

Scanning Vectors & MITRE ATT&CK Mapping:

Internal Network Scanning: Occurs when a system inside the internal network probes other internal assets to discover live hosts, open ports, and active services. Maps to the Discovery (TA0007) tactic in MITRE ATT&CK.

External Network Scanning: Occurs when an external source probes public-facing IP addresses to discover exposed services. Maps to the Reconnaissance (TA0043) tactic in MITRE ATT&CK.

Horizontal Network Scanning: Occurs when a single source IP scans a single specific port across multiple target IP addresses to locate hosts running a specific service.

Vertical Network Scanning: Occurs when a single source IP scans multiple ports on a single target IP address to profile open services on that host.

🛠️ Tools & Technologies Used

Linux CLI Utility Suite: (cat, cut, grep, head, ls, uniq, sort) for rapid log parsing, field filtering, frequency counting, and parameter redirection.

CSV Log Analysis: Parsing session records (log-session-0.csv, log-session-2.csv, etc.) using command-line delimiters.

🔍 Key Investigation Areas

Internal vs. External Scanning Detection: Filtering log session files for RFC 1918 private IP ranges (e.g., 192.168.X.X) to separate internal insider scanning (log-session-2.csv) from external reconnaissance (203.0.113.25).

Log Entry Frequency & Volume Analysis: Utilizing field extraction (cut -d ',' -f3) and occurrence counting (uniq -c) to quantify the exact number of probe attempts performed by scanning hosts (e.g., 2,276 log entries).

Horizontal Scan Analysis: Isolating session records where a single target port is sequentially probed across an entire CIDR subnet range (e.g., 203.0.113.0/24).

Vertical Scan Analysis: Identifying single host target IPs (192.168.230.145) subjected to rapid multi-port scanning across consecutive port ranges.

Targeted Service Port Identification: Isolating selective port probing activity on specific hosts to discover scans targeted at critical infrastructure services (HTTP/80, SMB/445, RDP/3389).

🛡️ Conclusion

Detecting network scanning patterns is vital for identifying adversarial discovery tactics before an attack escalates to exploitation. Utilizing Linux command-line utilities enables security analysts to efficiently process log files, categorize scanning behaviors (horizontal vs. vertical), and distinguish internal compromise indicators from external reconnaissance threats.
