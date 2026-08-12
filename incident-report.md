Brute Force Login Attempt Incident Report

## 1. Summary
SUMMARY
On the 12th of August 2026 at 14:12, host 'target' recorded five SSH login
attempts against the 'analyst' account from 192.168.252.7
within 2.15 seconds. Four failed; the fifth succeeded. The
account is considered compromised. Recommend immediate
password reset and a block on the source IP.
REMEDIATION SOLUTIONS
1. Force a password reset on 'analyst' and review its activity.
2. Disable SSH password login; require SSH keys instead.
3. Install fail2ban to auto-block IPs after repeated failures.
4. Alert on repeated 'Failed password' events in real time

## 2. Affected assets
- Host: [192.168.252.6]
- Account: [analyst]
## 3. Indicators of compromise
- Source IP: [192.168.252.7]
- Targeted user: [analyst]
## 4. Timeline
- [14:12:58.111] First failed login from [IP]
- [14:12:58.694] Further failed attempts ([4] total)
- [14:12:56.546] Successful login from same IP <-- compromise
-Four failed attempts occur within about 0.6 seconds of each other.
## 5. Analysis
From observing the time taken between the login attempts it would strongly suggest an automated process rather than manually inputted passwords which is indicative of a Successful Brute Force attempt on the Targeted Account.
## 6. MITRE ATT&CK mapping
- T1110 Brute Force
- T1078 Valid Accounts
## 7. Impact
-Depending on the privileges that the “Analyst” account has access to the potential attacker could:
-Access files belonging or shared with “Analyst”
-Read or Modify Data
-Execute Commands
-Access Internal Services on the network
-Use the account as a means of gaining more privileges on the network
## 8. Remediation
1.  Force a password reset on 'analyst' and review its activity.
2. Disable SSH password login; require SSH keys instead.
3. Install fail2ban to auto-block IPs after repeated failures
4. Alert on repeated 'Failed password' events in real time

## 9. Lessons learned
-Creating an SSH Brute-Force Detection Rule to alert for repeated subsequential Failed SSH Authentication i.e. Alert when 5 or more failed attempts occur within a minute from the same source.
-To reflect this instance a detection rule for Failed Authentication attempts shortly following a Successful Authentication would be created 
-Monitoring Authentication Attempt speed, if more than 5 authentication attempts are made within less than 10 seconds it is more than likely an automated tool being used.
-A lock out rule or a Rate Limit Rule must be implemented on the network this will slow down the rate in which Authentication attempts are made. 
