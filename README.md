# Security Log Monitoring Analysis using Splunk

This project demonstrates a Security Operations Center (SOC) dashboard created using **Splunk** to monitor and analyze internal system security events, such as authentication failures, brute force login attempts on SSH, and the most frequently logged-in users.

## Features
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
