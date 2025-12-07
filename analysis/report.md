# SOC Incident Report - SSH Brute Force Attack Simulation
**Analyst: Agam
**Date: Dec 07 2025
**Enviroment: Kali Linux (Local VM)
**Attack Type: SSH Brute Force
**Status: Successfully Detected & Contained

=====Summary====
On December 7th, a brute-force attack simulation was executed against the local linux system (127.0.0.1).
The attacker attempted multiple SSH password-authentication logins using the username invaliduser from the local host 127.0.0.1.  
A total of 18 failed login attempts were detected over a period of 5 minutes and 30 seconds.
No successful authentication attempts occurred.

====Indicators=====
Source IP: 127.0.0.1 (simulated attacker)
Username targetetd: invaliduser
Service: sshd
Method: SSH Password Authentication.
Authentication Method: password
Event Type: "Failed password"
Total Atttempts: 18
Status: All attempts failed

====Evidence (log excerpts)====
Dec 07 03:31:29 kali sshd-session[3401]: Failed password for invalid user invaliduser from 127.0.0.1 port 47526 ssh2
Dec 07 03:31:37 kali sshd-session[3401]: Failed password for invalid user invaliduser from 127.0.0.1 port 47526 ssh2
Dec 07 03:31:44 kali sshd-session[3401]: Failed password for invalid user invaliduser from 127.0.0.1 port 47526 ssh2
Dec 07 03:31:56 kali sshd-session[3772]: Failed password for invalid user invaliduser from 127.0.0.1 port 47172 ssh2
Dec 07 03:32:01 kali sshd-session[3772]: Failed password for invalid user invaliduser from 127.0.0.1 port 47172 ssh2
Dec 07 03:32:06 kali sshd-session[3772]: Failed password for invalid user invaliduser from 127.0.0.1 port 47172 ssh2
Dec 07 03:32:10 kali sshd-session[3943]: Failed password for invalid user invaliduser from 127.0.0.1 port 41432 ssh2
Dec 07 03:32:13 kali sshd-session[3943]: Failed password for invalid user invaliduser from 127.0.0.1 port 41432 ssh2
Dec 07 03:32:17 kali sshd-session[3943]: Failed password for invalid user invaliduser from 127.0.0.1 port 41432 ssh2
Dec 07 03:32:20 kali sshd-session[4034]: Failed password for invalid user invaliduser from 127.0.0.1 port 57824 ssh2
Dec 07 03:32:24 kali sshd-session[4034]: Failed password for invalid user invaliduser from 127.0.0.1 port 57824 ssh2
Dec 07 03:32:28 kali sshd-session[4034]: Failed password for invalid user invaliduser from 127.0.0.1 port 57824 ssh2
Dec 07 03:32:32 kali sshd-session[4137]: Failed password for invalid user invaliduser from 127.0.0.1 port 41588 ssh2
Dec 07 03:32:36 kali sshd-session[4137]: Failed password for invalid user invaliduser from 127.0.0.1 port 41588 ssh2
Dec 07 03:32:41 kali sshd-session[4137]: Failed password for invalid user invaliduser from 127.0.0.1 port 41588 ssh2
Dec 07 03:32:46 kali sshd-session[4244]: Failed password for invalid user invaliduser from 127.0.0.1 port 57374 ssh2
Dec 07 03:32:50 kali sshd-session[4244]: Failed password for invalid user invaliduser from 127.0.0.1 port 57374 ssh2
Dec 07 03:36:59 kali sshd-session[6360]: Failed password for invalid user invaliduser from 127.0.0.1 port 38444 ssh2

====TimeLine=====
Start: Dec 07 03:31:29 
End: Dec 07 03:36:59 
Duration: 00:05:30 (hh:mm:ss)

=====Detection Method==== 
sudo journalctl -u ssh | grep "Failed password"
sudo journalctl -u ssh | grep "Failed password" | awk '{print $13}' | sort | uniq -c | sort -nr

====Mitigation Recommendation====
Enable fail2ban
Enforce SSH key authentication
Disable password authentication
Change SSH port
Limit rate of authenticaion attempts
Enable rsyslog for permanent logging
Disable root login over SSH	
Use firewall rules to restrict SSH access

====Conclusion====
This simulation demonstrates how SSH brute-force attempts are logged and analyzed using journald.
The system correctly recorded failed login attempts and no unauthorized access was gained.
