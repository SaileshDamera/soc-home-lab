\# Investigation 001 — Nmap Port Scan



\## Summary

Nmap SYN scan performed from Kali Linux 

against Windows 10 VM to simulate attacker 

reconnaissance activity. Wazuh successfully 

detected the scan and generated security alerts.



\## Environment

| Detail | Value |

|---|---|

| Attacker IP | 192.168.1.138 (Kali VM) |

| Target IP | 192.168.1.100 (Windows VM) |

| Date | 27-06-2026 |

| Time | 14:59 |

| Tool | Nmap 7.99 |

| OS Attacked | Windows 10 Pro |



\## MITRE ATT\&CK

| Field | Value |

|---|---|

| Tactic | Discovery |

| Technique | T1046 - Network Service Discovery |

| Sub-technique | None |



\## Attack Performed

Command run on Kali:

nmap -sS 192.168.1.100



Result:

\- Host is up (0.00084s latency)

\- 1000 ports scanned

\- MAC Address: 08:00:27:7F:4D:01



\## Wazuh Detection

| Field | Value |

|---|---|

| SIEM | Wazuh v4.7.5 |

| Events Generated | 42 pages |

| MITRE Detected | T1078 |

| Alert Level | Medium |



\## Timeline

| Time | Event |

|---|---|

| 14:59:00 | Nmap SYN scan started from Kali |

| 14:59:22 | Scan completed (21.92 seconds) |

| 14:59:58 | Wazuh security events triggered |

| 14:59:58 | Alerts visible on dashboard |



\## Evidence

Screenshots attached in evidence folder.



\## Impact Assessment

| Factor | Status |

|---|---|

| Attack Successful | Partial |

| Ports Found Open | None (filtered) |

| Data Compromised | No |

| Service Disrupted | No |



\## Recommendations

1\. Enable IDS rules for port scan detection

2\. Alert when 100+ ports scanned in 1 minute

3\. Block IPs doing reconnaissance

4\. Implement network segmentation

5\. Monitor for follow-up attacks after scan



\## Lessons Learned

\- Port scanning is the first step of any attack

\- Attackers use Nmap to find open services

\- Early detection stops attack chain

\- Even filtered ports reveal host is alive

\- SOC should alert on scanning behavior

