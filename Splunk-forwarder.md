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


## 1-Step:
Download the splunk Forwarder package from splunk website as to specfic machine .<br>
In our case we are going to use the debian package as snort was configured on ubuntu virtual machine.<br>
After downnloading the specific package we are moving it to the /opt directory.With the following command .<br>
``sudo mv /Downloads/splunkforwarder-9.3.1-0b8d769cb912-linux-2.6-amd64.deb /opt``<br>
with the package is now moved to the opt directory where all the optional software are stored.<br>
To install the package we are going to use the following command.<br>
``sudo apt install ./splunkforwarder-9.3.1-0b8d769cb912-linux-2.6-amd64.deb ``<br>
*Ref 1: intallation*
![Ubuntu 64-bit-2024-09-18-16-34-23](https://github.com/user-attachments/assets/2430620e-8fcb-41f1-8eb6-2fcf12f1b7ca)<br>

### 2-step:
After the installation is complete we need to run splunk to get the initial credentials.<br>
we need to navigate into the splunk-forwarder/bin directory using the following command.<br>
``cd /splunkforwarder/bin``<br>
In this directory we need to run splunk using the command :<br>
``sudo ./splunk start --accept-license``<br>
with the --accept-license parameter the terms are accepted .<br>
Provide splunk with the username and password that will be used to login into splunkforwarder.<br>
*Ref 2: username and password*
![Ubuntu 64-bit-2024-09-16-17-46-43](https://github.com/user-attachments/assets/df8f4e3c-7793-4a3a-a992-4945b4217920)
<br>
#### 3-step:
After enteriing the username and password.<br>
We need to configure snortforward  and add the forward server where the snort logs and alert will be sent.<br>
In our case the splunk-enterprise is installed on the host machine running windows.<br>
The ip of the host machine where splunk-forwarder will send the logs can be found using the cmd command.<br>
``ipconfig``<br>
We need the ipv4 address to send logs.<br>
After obtaining the ip address we need to add the forwarding address in splunk-forwarder using the command :<br>
`` sudo ./splunk add forward-server "ip-address":9997``<br>
After the ip-address the specific port 9997 that is a reserved port <br>
splunk-forwarder will ask for the username and password that was created in the initial start up of splunk.<br>
with the following command we can check the list of forward server:<br>
``sudo ./splunk list forward-server``<br>



