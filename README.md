# Linux Authentication Monitoring Lab

## Overview
This project demonstrates Security Operations Center (SOC) monitoring activities using Ubuntu Linux. Authentication events were generated and analyzed to investigate failed login attempts, user account creation, and privilege escalation activity. System logs were reviewed using the Linux authentication log (/var/log/auth.log) to identify security-relevant events and verify account changes.

The lab was performed in Oracle VirtualBox using Ubuntu 26.04 LTS.

## Objectives

- Install and configure Ubuntu Linux
- Create and manage local user accounts
- Generate failed authentication events
- Analyze authentication logs
- Investigate login failures
- Simulate privilege escalation
- Verify security events in log files


## Lab Environment

### Host System
- Windows 11

### Virtualization Platform
- Oracle VirtualBox

### Guest Operating System
- Ubuntu 26.04 LTS

## Skills Demonstrated

- Linux Administration
- User Account Management
- Authentication Monitoring
- Log Analysis
- Privilege Escalation Investigation
- Security Event Analysis
- SOC Fundamentals

## Tools Used

- Ubuntu 26.04 LTS
- Oracle VirtualBox
- Terminal
- Auth Logs (/var/log/auth.log)

# Part 1: User creation
```bash
sudo adduser testuser
```
verified account creation:
```
cat /etc/passwd | grep testuser
```
<img src="screenshots/user-created.png" width="600">

# Part 2: Failed Authentication Simulation
Attempted to switch to the test account using an incorrect password multiple times: 
```bash
su testuser
```
Generated authentication failures for investigation.

<img src="screenshots/failed-login.png" width="600">

# Part 3: Authentication Log Analysis
Reviewed authentication logs:
```bash
sudo cat /var/log/auth.log | tail -20
```
Observed:
- Authentication failures
- Password check failures
- Failed SU attempts
  
<img src="screenshots/auth-log-analysis.png" width="600">

# Part 4: Privilege Escalation 
Added testuser to the sudo group:
```bash 
sudo usermod -aG sudo testuser
```
verified group membership:

```bash
groups testuser
```
output:
testuser : testuser sudo users

<img src="screenshots/privilege-escalation-log.png" width="600">

# Part 5: Privilege Escalation Investigation 
searched authentication logs:
```bash 
sudo cat /var/log/auth.log | grep usermod
```
Obderved: 
usermod: add 'testuser' to group 'sudo'
This event demonstrate how administrator privilege changes can be detected and invetigated.

<img src="screenshots/sudo-group-membership.png" width="600">

# Key Security Findings

- Failed authentication attempts were successfully recorded in auth.log
- User account creation events were verified through the Linux account database
- Privilege escalation activities generated auditable log entries
- Administrative group membership changes were detected and investigated
- Authentication logs provide valuable visibility into user activity and security events

# Technologies & Concepts

- Linux Administration
- User Account Management
- Authentication Monitoring
- Security Log Analysis
- Privilege Escalation Detection
- Event Investigation
- Ubuntu Linux
- VirtualBox
- SOC Fundamentals

# Lesson Learned 
Through this lab, I gained hands-on experience with:

- Creating and managing Linux user accounts
- Investigating failed authentication attempts
- Analyzing authentication logs for security events
- Detecting privilege escalation activities
- Using Linux command-line tools for log analysis
- Understanding how SOC analysts monitor and investigate user activity
