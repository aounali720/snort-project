# SPLUNK-FORWARDER IMPLEMENTATION

## Objective
In this setup, an Ubuntu virtual machine is running on a Windows host, with Snort configured as an Intrusion Detection System (IDS) to monitor TCP and ICMP network traffic. The goal is to detect suspicious activities and generate alerts. These alerts are forwarded to Splunk Enterprise using splunk forwarder for centralized alert collection and analysis.
As in the previous project done in configuring Snort <a href="https://github.com/aounali720/snort-project/blob/main/README.md">Project Snort </a>

### Skills Learned
- Splunk Universal Forwarder Installation:
- Knowledge of downloading, installing, and setting up the Splunk Universal Forwarder on Linux systems (e.g., Ubuntu).
- Familiarity with using command-line utilities to manage Splunk services and configurations.
- Log Forwarding Configuration:
  - Ability to configure the Universal Forwarder to send logs and data to a remote Splunk Enterprise server.
Understanding how to specify log sources and directories to monitor (e.g., Snort logs).
- Splunk Enterprise Setup:
  - Competence in configuring Splunk Enterprise to receive forwarded logs by enabling listening on a specific port.
  - Skills in searching, indexing, and managing forwarded logs for real-time data analysis.
- Snort and Log Monitoring:
  - Expertise in monitoring network traffic using Snort and identifying critical log files that need to be forwarded to a central log management system.
  - Ability to integrate Snort with Splunk for centralized alert and log analysis.
- Network and Security Skills:
  - Knowledge of detecting and analyzing network traffic, particularly TCP and ICMP, using Snort.
  - Familiarity with network security practices by monitoring and responding to Snort-generated alerts in a SIEM system like Splunk.
- System Administration and Troubleshooting:
  - Experience in managing and troubleshooting a Linux-based environment.
  - Familiarity with configuring system logs, services, and monitoring processes.
  - Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
- Splunk Universal Forwarder:
  - A lightweight tool used to forward logs and data from a machine (Ubuntu VM in this case) to a Splunk Enterprise server for centralized log management and analysis.
- Splunk Enterprise:
  - A Security Information and Event Management (SIEM) system used for log aggregation, indexing, searching, and visualizing data. It receives and processes the alerts and logs forwarded by the Universal Forwarder.
-Snort:
  - An open-source Intrusion Detection System (IDS) that monitors network traffic and generates alerts based on predefined rules. These alerts are forwarded to Splunk for further analysis.
- Ubuntu (Linux OS):
  - The operating system running on the virtual machine, used to install and configure both Snort and the Splunk Universal Forwarder.
- VirtualBox/VMware:
   - Virtualization software used to run an Ubuntu virtual machine on a Windows host, allowing you to set up a sandbox environment for security monitoring.
- Syslog:
  - A logging protocol used to forward logs (e.g., Snort alerts) from the local machine (Ubuntu VM) to Splunk, often leveraged within the Universal Forwarder configuration.
- Terminal (Command Line Interface):
  - Used for installing, configuring, and managing Snort, Splunk Universal Forwarder, and Ubuntu services. Key in executing setup and monitoring commands.


## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*
