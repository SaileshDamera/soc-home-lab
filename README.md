🛡️ Home SOC Lab


## Overview
A home Security Operations Center (SOC) lab built to simulate real-world cyber attacks and practice threat detection, log analysis, and incident response using industry standard tools.


## 👨‍💻 Author

**Sailesh Damera**
- Aspiring SOC Analyst
- Email: damerasailesh@gmail.com


## 🏗️ Lab Architecture

| Component | Details |
|---|---|
| Host Machine | HP Pavilion Gaming Laptop |
| Host RAM | 16GB (13.9GB usable) |
| Storage | 1TB |
| Hypervisor | Oracle VirtualBox |
| Attacker VM | Kali Linux 2026.1 — 192.168.1.138 |
| Target VM | Windows 10 Pro — 192.168.1.100 |
| SIEM | Wazuh v4.7.5 |
| Network | Bridged Adapter |


## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Wazuh SIEM | Log collection, alerting and threat detection |
| Nmap | Network reconnaissance and port scanning |
| Hydra | Brute force attack simulation |
| Metasploit | Exploitation and reverse shell simulation |
| Wireshark | Network traffic capture and analysis |
| Oracle VirtualBox | Virtualization platform |
| Git | Version control and documentation |


## 📁 Repository Structure

soc-home-lab/
├── README.md
├── lab-setup/
│   └── setup.md
├── investigations/
│   ├── 001-nmap-port-scan/
│   │   ├── findings.md
│   │   └── evidence/
│   ├── 002-rdp-brute-force/
│   │   ├── findings.md
│   │   └── evidence/
│   ├── 003-failed-logins/
│   │   ├── findings.md
│   │   └── evidence/
│   ├── 004-reverse-shell/
│   │   ├── findings.md
│   │   └── evidence/
│   └── 005-eicar-malware/
│       ├── findings.md
│       └── evidence/
├── playbooks/
│   └── incident-response.md
└── tools/
└── configs/


## 🔍 Investigations

| # | Attack Type | MITRE Technique | Severity | Status |
|---|---|---|---|---|
| 001 | Nmap Port Scan | T1046 - Network Service Discovery | Medium | ✅ Complete |
| 002 | RDP Brute Force | T1110 - Brute Force | High | ⬜ Pending |
| 003 | Failed Login Attempts | T1110.001 - Password Guessing | Medium | ⬜ Pending |
| 004 | Reverse Shell | T1059 - Command and Scripting | Critical | ⬜ Pending |
| 005 | EICAR Malware Test | T1204 - User Execution | High | ⬜ Pending |
| 006 | Privilege Escalation | T1068 - Exploitation for Privilege | Critical | ⬜ Pending |
| 007 | File Integrity Monitor | T1565 - Data Manipulation | High | ⬜ Pending |
| 008 | PowerShell Attack | T1059.001 - PowerShell | High | ⬜ Pending |


## 📊 What I Observe in Every Attack

As a SOC analyst I document the following for every investigation:
| # | Observable | Description |
|---|---|---|
| 1 | Source IP | Where the attack came from |
| 2 | Destination IP | What was targeted |
| 3 | Attack Tool | Tool used by attacker |
| 4 | MITRE Technique | ATT&CK framework mapping |
| 5 | Wazuh Rule ID | Which rule detected it |
| 6 | Windows Event ID | Corresponding Windows log |
| 7 | Alert Severity | Low, Medium, High, Critical |
| 8 | Timeline | Chronological order of events |
| 9 | Impact | Was attack successful |
| 10 | Recommendations | How to prevent recurrence |


## 🧠 Skills Demonstrated

- SIEM Configuration and Management (Wazuh)
- Threat Detection and Alert Analysis
- Incident Response and Documentation
- MITRE ATT&CK Framework Mapping
- Network Traffic Analysis
- Windows Log Analysis
- Attack Simulation and Red Teaming
- Vulnerability Assessment
- Security Hardening Recommendations
- GitHub Documentation


## 🚨 Key Findings So Far

- Windows 10 VM CIS Benchmark score below 50% indicating poor security posture
- Port scanning activity detected by Wazuh Rule 533
- MITRE T1078 technique automatically mapped by Wazuh
- Default Windows configurations create significant security risk
- Wazuh successfully detected all simulated attacks


## 🔧 Lab Setup Summary

**Step 1 — Virtualization**
- Installed Oracle VirtualBox on Windows host
- Created Kali Linux VM with 4GB RAM
- Created Windows 10 VM with 4GB RAM
- Configured Bridged Adapter networking

**Step 2 — SIEM Setup**
- Installed Wazuh Manager on Kali Linux
- Installed Wazuh Dashboard on Kali Linux
- Installed Wazuh Agent on Windows 10 VM
- Verified agent connection on dashboard

**Step 3 — Attack Simulation**
- Used Kali Linux as attacker machine
- Used Windows 10 as target machine
- Monitored all alerts on Wazuh dashboard
- Documented findings in GitHub


## 📚 References

- [Wazuh Documentation](https://documentation.wazuh.com)
- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [Kali Linux Tools](https://www.kali.org/tools)
- [Oracle VirtualBox](https://www.virtualbox.org)
- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
