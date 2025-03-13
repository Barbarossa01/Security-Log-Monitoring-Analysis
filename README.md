# Security Log Monitoring Analysis using Splunk

This project demonstrates a Security Operations Center (SOC) dashboard created using **Splunk** to monitor and analyze internal system security events, such as Ransomware attack, authentication failures, brute force attack (login attempts on SSH), and the most frequently logged-in users.

## Features
- **Ransomware Attack**: Tracks and shows the paths of files with `.crypt` extensions (can be extended to other extensions such as `.encrypt`). This helps identify potential ransomware activity by monitoring file renaming events.
- **Authentication Failure Monitoring**: Displays failed authentication attempts to track potential intrusions.
- **Brute Force Attack Detection**: Identifies login attempts to root SSH accounts, helping detect brute force attacks.
- **Most Logged-In Users**: Shows the users who log in most frequently, providing insights into user activity and behavior.

## Prerequisites
- Splunk installation (or access to an existing Splunk instance).
- Access to system logs containing authentication attempts, SSH logs, and user login details.
- Basic knowledge of Splunk and its dashboarding features.

## Setup Guide

1. **Install Splunk** (if not already installed):
   Follow [this guide](https://www.splunk.com/en_us/download.html) to install Splunk on your system.

2. **Import the Dashboard**:
   - Download the dashboard configuration files from the `splunk_dashboards` directory.
   - Import the `.xml` file into your Splunk instance via **Splunk Web**.
   - Customize the dashboard if necessary to suit your log data format.

3. **Configure Data Inputs**:
   Ensure that Splunk is collecting the required data sources, including:
   - Authentication logs (e.g., `/var/log/auth.log` or similar).
   - SSH logs for login attempts.
   - System logs showing user activity.

## Usage
- After importing the dashboard into Splunk, navigate to the **Dashboard** section.
- Use the visualizations to monitor:
  - Authentication failures over time.
  - Root SSH login attempts and potential brute force indicators.
  - User login statistics to identify abnormal behavior.

## Screenshots
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/1.png" alt="dashboard1">
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/2.PNG" alt="dashboard2">

## Simulation Brute Force attack:
Let's consider the following scenario : a hacker in the LAN network trying to use hydra to guess the password for the user ubuntu, this is a photo for a successful brute force attack on ubuntu showing that the password is admin

<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/bruteForceAttack1.PNG" alt="brute1.PNG">

Luckily the ubuntu host is using splunk to monitor the ssh service and the attempts for password authentication, on the ubuntu side the logs look like the following : 

<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/bruteForceAttack2.PNG" alt="brute2.PNG">

and the SOC analyst who's using Splunk can see the logs in the dashboard, knowing that which user was under the attack, by which IP address as well and at what time 

<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/bruteForceAttack3.PNG" alt="brute3.PNG">

now since it's critical the password must be changed.

## Ransomware Showcase 
There are many techniques to detect malware on the system, one of them is to log any changed extensions for files, I create a custom SPL to detect files that changed the extension to .crypt, using the following SPL
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/ransomeware1.PNG" alt="ransom1.PNG">

and in the dashboard gonna look like the following : 
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/ransomeware2.PNG" alt="ransom2.PNG">


## Used SPL in the dashbiard
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/SPL1.PNG" alt="SPL1.PNG">
- index=* :  index where the search should look for data
- ("FAILED SU (to root)" OR "authentication failure") : search filter that looks for specific strings in the logs
- | rex field=_raw "user\s+(?<user>\S+)" : regular expression (regex) extraction from the raw log data. It is used to extract values from your logs based on a pattern.

<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/SPL2.PNG" alt="SPL2.PNG">
- This SPL query designed to detect failed SSH login attempts specifically targeting the root user
- ("Failed password" AND "root") : This filter looks for both "Failed password" and "root" in the log messages.

<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/SPL3.PNG" alt="SPL3.PNG">

##  Audit Trail : a detailed, chronological record of events and actions performed within the system
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/trail0.PNG" alt="trail0.PNG">
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/trail1.PNG" alt="trail1.PNG">
<br><img src="https://github.com/Barbarossa01/Security-Log-Monitoring-Analysis/blob/main/images/trail2.PNG" alt="trail2.PNG">
