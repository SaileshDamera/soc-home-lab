\# Investigation 003 — Failed Login Attempts



\## Summary

Multiple failed login attempts simulated on Windows 10 VM 

by entering wrong passwords on the lock screen to replicate 

an insider threat or unauthorized local access scenario. 

Wazuh SIEM successfully detected all failed attempts in 

real time and mapped them to MITRE ATT\&CK framework.



\## Environment

| Detail | Value |

|---|---|

| Attack Type | Local failed login simulation |

| Target Account | labuser |

| Target Machine | Windows 10 Pro (Windows-Lab) |

| Target IP | 192.168.1.100 |

| Date | 28-06-2026 |

| Start Time | 14:25:10 |

| End Time | 14:25:23 |

| Duration | 13 seconds |

| Method | Manual wrong password entries on lock screen |

| Agent ID | 001 |



\## MITRE ATT\&CK

| Field | Value |

|---|---|

| Tactic | Defense Evasion, Persistence, Privilege Escalation, Initial Access, Impact |

| Technique | T1078 - Valid Accounts |

| Sub-technique | T1531 - Account Access Removal |

| Additional Technique | T1110 - Brute Force |

| Sub-technique | T1110.001 - Password Guessing |



\## Attack Method

Windows lock screen used to simulate unauthorized 

login attempts. Wrong passwords entered repeatedly 

to trigger failed logon events. This simulates:

\- Insider threat scenario

\- Physical access attack

\- Unauthorized workstation access attempt



\## Wazuh Alerts Observed

| Time | Rule ID | Description | Level | Techniques |

|---|---|---|---|---|

| 14:25:10 | 60122 | Logon failure - Unknown user or bad password | 5 | T1078, T1531 |

| 14:25:14 | 60122 | Logon failure - Unknown user or bad password | 5 | T1078, T1531 |

| 14:25:16 | 60122 | Logon failure - Unknown user or bad password | 5 | T1078, T1531 |

| 14:25:19 | 60642 | Software protection service scheduled | 3 | None |

| 14:25:19 | 60122 | Logon failure - Unknown user or bad password | 5 | T1078, T1531 |

| 14:25:21 | 60122 | Logon failure - Unknown user or bad password | 5 | T1078, T1531 |

| 14:25:23 | 60122 | Logon failure - Unknown user or bad password | 5 | T1078, T1531 |



\## Windows Event IDs

| Event ID | Description | Count |

|---|---|---|

| 4625 | Failed logon attempt | 6 |

| 4625 | Logon type 2 - Interactive | 6 |



\## MITRE Techniques Detected

| Technique | Name | Description |

|---|---|---|

| T1078 | Valid Accounts | Attacker used valid account name |

| T1531 | Account Access Removal | Multiple failures risk account lockout |

| T1110 | Brute Force | Repeated login attempts |



\## Timeline

| Time | Event |

|---|---|

| 14:25:10 | First failed login attempt detected |

| 14:25:14 | Second failed login attempt |

| 14:25:16 | Third failed login attempt |

| 14:25:19 | Fourth failed login + software protection alert |

| 14:25:21 | Fifth failed login attempt |

| 14:25:23 | Sixth failed login attempt |

| 14:25:23 | Wazuh Rule 60122 triggered 6 times |



\## Interesting Observation

Rule 60642 fired at 14:25:19 during the attack:

\- Description: Software protection service scheduled

\- This is Windows background activity

\- Appeared between failed login attempts

\- SOC analysts must distinguish between:

&#x20; → Attack-related alerts (60122) ✅

&#x20; → Background noise alerts (60642) ℹ️

\- Context and timing help identify real threats



\## Comparison with Attack 002

| Factor | Attack 002 RDP Brute | Attack 003 Failed Logins |

|---|---|---|

| Source | External Kali VM | Local lock screen |

| Protocol | RDP port 3389 | Interactive logon |

| Tool | Hydra | Manual/Script |

| Detection | Same Rule 60122 | Same Rule 60122 |

| Scenario | External attacker | Insider threat |

| Prevention | Block RDP | Physical security |



\## Impact Assessment

| Factor | Status |

|---|---|

| Attack Successful | No |

| Account Locked | No (threshold not reached) |

| Data Compromised | No |

| Service Disrupted | No |

| Insider Threat Risk | High |

| Physical Security Risk | High |



\## Key Findings

1\. Wazuh detected all 6 failed attempts in real time

2\. Multiple MITRE techniques mapped automatically

3\. T1078 and T1531 both triggered by same event

4\. Background noise (60642) appeared during attack

5\. Local attacks generate same alerts as network attacks

6\. 13 second window generated 6 security events

7\. Alert level 5 for each failed attempt



\## Recommendations

1\. Set account lockout threshold to 3 attempts

2\. Alert SOC immediately on any 4625 event

3\. Implement physical security controls

4\. Use screen lock with short timeout

5\. Monitor failed logins during off-hours

6\. Correlate multiple 60122 alerts as attack pattern

7\. Implement MFA for all local accounts

8\. Security awareness training for employees

9\. CCTV monitoring for physical workstations

10\. Alert on repeated lockouts for same account



\## Lessons Learned

\- Local failed logins are as dangerous as network attacks

\- Insider threats bypass most network security controls

\- Physical access to machine = high risk

\- Wazuh detects both local and network authentication failures

\- Background alerts (60642) create noise during investigation

\- SOC analysts must filter signal from noise

\- Timestamps help correlate attack sequence

\- 13 seconds is enough time for Wazuh to detect pattern

\- Account lockout policy is critical first line of defense

\- Off-hours login failures should trigger immediate alerts

