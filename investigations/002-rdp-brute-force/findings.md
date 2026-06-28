\# Investigation 002 — RDP Brute Force



\## Summary

Hydra brute force tool used from Kali Linux

to simulate RDP password attack against

Windows 10 VM. Windows account lockout

policy triggered successfully blocking

the attack. Wazuh SIEM detected the activity.



\## Environment

| Detail | Value |

|---|---|

| Attacker IP | 192.168.1.138 (Kali VM) |

| Target IP | 192.168.1.100 (Windows VM) |

| Date | 28-06-2026 |

| Start Time | 07:34:29 |

| End Time | 07:35:02 |

| Duration | 33 seconds |

| Tool | Hydra v9.7 |

| Target Service | RDP Port 3389 |

| Wordlist | rockyou.txt (14,344,399 passwords) |



\## MITRE ATT\&CK

| Field | Value |

|---|---|

| Tactic | Credential Access |

| Technique | T1110 - Brute Force |

| Sub-technique | T1110.001 - Password Guessing |



\## Attack Command

hydra -l labuser -P /usr/share/wordlists/rockyou.txt

rdp://192.168.1.100 -t 4 -W 3 -v



\## Wazuh Alerts Observed

| Rule ID | Description | Level |

|---|---|---|

| 60122 | Logon failure - Unknown user or bad password | 5 |

| 60204 | Multiple Windows logon failures | 10 |

| 60115 | User account locked out (multiple login errors) | 9 |



\## Windows Event IDs

| Event ID | Description | Count |

|---|---|---|

| 4625 | Failed logon attempt | 3576 |

| 4740 | Account locked out | 3584 |



\## Timeline

| Time | Event |

|---|---|

| 07:34:29 | Hydra brute force started |

| 07:34:30 | First failed RDP attempt |

| 07:34:35 | Account lockout triggered |

| 07:35:02 | Hydra stopped due to lockouts |



\## Key Findings

1\. Windows account lockout policy activated

2\. labuser account was locked automatically

3\. Hydra disabled all threads due to lockouts

4\. 0 valid passwords found in 33 seconds

5\. Attack was blocked by Windows defense



\## Impact Assessment

| Factor | Status |

|---|---|

| Attack Successful | No — blocked by lockout |

| Password Found | No |

| Account Locked | Yes — labuser locked |

| Service Disrupted | Partial |



\## Recommendations

1\. Account lockout policy already working ✅

2\. Set lockout threshold to 3 attempts

3\. Alert SOC immediately on lockout events

4\. Block attacker IP after lockout triggered

5\. Disable RDP if not required

6\. Use Network Level Authentication (NLA)

7\. Implement MFA for all RDP access

8\. Never expose RDP directly to internet

9\. Change RDP from default port 3389



\## Lessons Learned

\- Account lockout is effective first defense

\- Brute force attacks are easily detectable

\- Even 33 seconds generates many alerts

\- SIEM alerting on 4740 is critical

\- Default RDP is a major attack surface

\- Attackers use real leaked password lists



\## Interesting Finding — Logon Success During Attack



At 07:34:48 a Windows logon success

(Rule 60106, T1078) appeared during

the brute force attack.



Investigation revealed:

→ Logon type is 5, which is a normal windows activity

→ 127.0.0.1, which is a local windows service

→ Account name is "System", which means alert got triggered but it's just a normal windows activity

→ It concludes that Hydra didn't succeed and it's just a Windows Service alert



This demonstrates why SOC analysts must:

→ Never ignore success events during attacks

→ Investigate ALL anomalies in context

→ Correlate events with timeline

→ Not assume — always verify



\## Key Finding — Account Lockout Behavior



labuser account was locked by Hydra brute force.



Observed behavior:

→ Network RDP access: BLOCKED ❌

→ Local VM console access: ALLOWED ✅



This is expected Windows behavior:

→ Network lockout prevents remote attacks

→ Local console access remains for admin

→ In real world, physical access = full control

→ This is why physical security matters



Lockout confirmed via:

→ net user labuser command

→ Account locked: Yes and attached screenshot in evidence section

→ Wazuh Rule 60115 fired

→ Event ID 4740 generated

