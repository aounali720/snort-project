## Objective


The Detection Lab project aimed to establish a controlled environment for simulating and detecting malicious network packets . The primary focus was to monitor and analyze network traffic within snort tool and forwarded the alerts using Snort-Forwarder  to a  Security Information and Event Management (SIEM) system (Splunk Enterprise), generating test telemetry to mimic real-world network scenarios. This hands-on experience was designed to deepen understanding of network security, network traffic , and defensive strategies.


### Skills Learned


- Advanced understanding of SIEM(Splunk Enterprise) concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to analyze and recognize attack signatures and patterns in network.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.
- Snort Installation and Configuration:
- Proficiency in setting up and configuring Snort as an IDS on Ubuntu.
- Ability to define network variables and write rules to detect TCP and ICMP traffic.
  
- Network Traffic Analysis
- Understanding how to monitor and analyze network traffic using Snort.
- Skill in identifying suspicious activity within TCP and ICMP protocols and generating alerts accordingly.
  
- SIEM Integration

- Experience in configuring Snort to forward alerts to Splunk Enterprise for centralized log management.
- Ability to set up data inputs in Splunk to receive and index security alerts.
- Hands-on Threat Detection:

- Practical experience in simulating and detecting real-time network threats.
- Skill in analyzing logs, events, and alerts within a SIEM system for security monitoring.
- Linux System Administration:

- Competency in using Ubuntu for security tools setup and network monitoring.
- Experience with managing system configurations, services, and logs related to Snort and Splunk.

### Tools Used


- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Snort:An open-source Intrusion Detection System (IDS) used to monitor and analyze network traffic, focusing on detecting TCP and ICMP traffic, and generating alerts based on specific rules.
- Splunk Enterprise:A powerful Security Information and Event Management (SIEM) system used for centralized log management, analysis, and real-time visualization of security events. It ingests and analyzes the alerts generated by Snort.
- Ubuntu:The Linux-based operating system used as the environment for installing and running both Snort and Splunk. It serves as the platform for network monitoring and security event analysis.
- Syslog:A logging protocol used to forward Snort alerts to Splunk Enterprise for aggregation and analysis.
- Terminal (Command Line Interface):Used for installing, configuring, and running Snort and managing the Ubuntu system, including handling logs and network configurations.
- Wireshark (Optional):A network protocol analyzer that can be used alongside Snort to visually inspect network traffic for verification and debugging purposes.


## 1-Step
The initial step is to intall snort in our virtual machine using the terminal the command is:<br>
       ```
        sudo apt-get install snort
        ```
<br>During installation, you’ll be prompted to configure the network. Set your HOME_NET to the network you want to monitor.<br>
As in our case we are going to keep it as is for sniffing any packet on the network
<br>
## 2-step
After the installion of snort is complete we can define the source ip and port , the destination port on which snort monitors but in our case we want it to mmonitor the whole network <br>
For the configuration of source and destination ip of a network we can modify the snort.confi file <br>
This file can be found in the
**/etc/snort/snort.conf** 
path<br>
## 3-Step
For writing the rules on which bases the snort will alert us can be written found in the 
<br> **/etc/snort/rules/local.rules**.<br>

Using the following command we can use nano to open this file and write our rules.<br>
``
 sudo nano /etc/snort/rules/local.rules
``<br>
*Ref 1: local rules config*

![Ubuntu 64-bit-2024-09-17-22-22-34](https://github.com/user-attachments/assets/989d64ed-f895-454c-b80a-c739cb3b4bfc)
<br>
In this we have written the rules to alert us if any tcp traffic and icmp traffic is found.<br>
with the syntax <br>
``
alert tcp any any ->  any any (msg:"icmp ping detected"; sid:302911; rev:1;)
``<br>
``
alert icmp  any any -> any any (msg:"ftp ping  detected"; sid:402020; rev:1;)
``<br>
**HERE THE SID MUST BE UNIQUE**
<br>
After saving the file we are going to check the configuration for any error .<br>
To find network interface that will be used we can use this command in the terminal.<br>
 ``ifconfig``
<br>
 Using the next command we can check if our rules are configured properly for the snort.<br>
 ``
 sudo snort -T -i ens33 -c /etc/snort/snort.conf
 ``
<br>
 
*Ref 2: snort testing*

![Ubuntu 64-bit-2024-09-17-23-00-18](https://github.com/user-attachments/assets/00f7b73a-4714-4ebe-88b3-e949b06dfc1a)


T is for snort to run in test mode.<br>
i is for the interface on which snort will monitor packet (Lan card) .<br>
c is for the configuration file used<br>
<br>
## 4-STEP
In this step we are going to check if snort is working properly using the following command.<br>
``sudo snort -q -l /var/log/snort -i ens33 -A console -c /etc/snort/snort.conf ``

*Ref 3: snort running*

![Ubuntu 64-bit-2024-09-16-02-24-54](https://github.com/user-attachments/assets/d5465914-56d3-4012-82ac-f4d459d4fe82)

