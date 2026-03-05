AI-powered tutorial for analyzing IIS logs, Windows event logs, and detecting brute force attacks.


# Log Analysis Security Tutorial

This repository demonstrates how to analyze system and web server logs to detect common security threats.

The tutorial focuses on three common investigation scenarios security teams encounter:

- Detecting brute force attacks in IIS logs  
- Analyzing Windows authentication failures  
- Investigating suspicious login activity  

These techniques are commonly used by **security analysts, SOC teams, system administrators, and MSPs** to identify unauthorized access attempts and potential compromises.

---

# Detecting Brute Force Attacks in IIS Logs

Brute force attacks occur when an attacker repeatedly attempts to guess credentials by submitting multiple login requests.

IIS logs record every request made to the web server and are often the first place these attacks appear.

## Indicators of a Brute Force Attack

Common patterns include:

- Many login attempts from a **single IP address**
- Multiple **401 Unauthorized** responses
- Rapid repeated requests to login endpoints
- Attempts against multiple usernames

Example pattern in IIS logs:

```
2026-03-05 12:02:10 192.168.1.25 POST /login.aspx 401
2026-03-05 12:02:11 192.168.1.25 POST /login.aspx 401
2026-03-05 12:02:12 192.168.1.25 POST /login.aspx 401
2026-03-05 12:02:13 192.168.1.25 POST /login.aspx 401
```

### Investigation Steps

1. Identify IP addresses generating large numbers of failed login attempts.
2. Review request frequency within short time windows.
3. Check if the same IP is attempting multiple accounts.
4. Cross-reference the IP with firewall or IDS alerts.

### Mitigation Strategies

- Enable account lockout policies
- Implement login rate limiting
- Block malicious IP addresses
- Enforce multi-factor authentication (MFA)

---

# Analyzing Windows Authentication Failures

Windows Security Event Logs record authentication activity that can reveal attempted intrusions.

One of the most important events to monitor is **Event ID 4625**, which represents a failed login.

## Important Windows Security Event IDs

| Event ID | Description |
|--------|-------------|
| 4624 | Successful login |
| 4625 | Failed login |
| 4672 | Special privileges assigned |
| 4648 | Explicit credentials used |

Example failed authentication log:

```
EventID: 4625
Account Name: administrator
Failure Reason: Unknown user name or bad password
Source IP: 10.0.0.45
```

### Investigation Steps

1. Identify accounts experiencing repeated failed logins.
2. Analyze the source IP address.
3. Look for login attempts outside normal business hours.
4. Determine if multiple accounts are targeted from the same source.

### Mitigation Strategies

- Enforce strong password policies
- Configure account lockout thresholds
- Monitor privileged account activity
- Enable MFA for administrative accounts

---

# Investigating Suspicious Login Activity

Not all threats appear as brute force attacks. Sometimes attackers successfully authenticate and then escalate privileges or execute malicious commands.

## Indicators of Suspicious Activity

Look for login sequences that include:

- Successful authentication followed by privilege escalation
- Unusual login locations
- Logins outside typical working hours
- New processes launched immediately after login

Example sequence:

```
4624 Successful login
4672 Special privileges assigned
4688 New process created (PowerShell)
```

This pattern may indicate a compromised account performing post-exploitation activity.

### Investigation Steps

1. Compare login timestamps against normal user behavior.
2. Review source IP addresses and geolocation.
3. Look for privilege escalation events.
4. Identify new processes launched immediately after login.

### Mitigation Strategies

- Implement behavioral monitoring
- Use SIEM alerting for abnormal login activity
- Enforce least-privilege access
- Regularly audit privileged accounts

---

# How to Analyze Logs with LogAnalyzer.AI in 30 Seconds

This repository includes sample log files that can be used to test log analysis techniques.

You can analyze these logs instantly using **LogAnalyzer.AI**.

### Steps

1. Visit the tool  
   https://loganalyzer.ai

2. Open the **Smart Scan** feature.

3. Browse a log file from this repository.

4. Click Analyze to Run the scan.

Within seconds, the platform automatically identifies:

- Security anomalies  
- Authentication failures  
- Suspicious activity patterns  
- Potential indicators of compromise  

The system generates an **Investigation Report** summarizing the findings and recommended actions.

---

# Tool Used

Log analysis in this tutorial was performed using:

**LogAnalyzer.AI**

AI-powered log analysis designed to quickly identify anomalies, security threats, and operational issues within log files.

https://loganalyzer.ai
