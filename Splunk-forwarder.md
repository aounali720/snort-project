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


# 1-Step:
Download the splunk Forwarder package from splunk website as to specfic machine .<br>
In our case we are going to use the debian package as snort was configured on ubuntu virtual machine.<br>
After downnloading the specific package we are moving it to the /opt directory.With the following command .<br>
``sudo mv /Downloads/splunkforwarder-9.3.1-0b8d769cb912-linux-2.6-amd64.deb /opt``<br>
with the package is now moved to the opt directory where all the optional software are stored.<br>
To install the package we are going to use the following command.<br>
``sudo apt install ./splunkforwarder-9.3.1-0b8d769cb912-linux-2.6-amd64.deb ``<br>
*Ref 1: intallation*
![Ubuntu 64-bit-2024-09-18-16-34-23](https://github.com/user-attachments/assets/2430620e-8fcb-41f1-8eb6-2fcf12f1b7ca)<br>

# 2-step:
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
# 3-step:
After entering the username and password.<br>
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
# 4-step:
After adding our forward server we can check if the configuration is done.<br>
we need to go into the "/opt/splunkforwarder/etc/system/local" directory using the command <br>
``cd /opt/splunkforwarder/etc/system/local`` <br>
Using any text editor like nano or vim open the outputs.conf file.<br>
``nano outputs.conf``<br>

*Ref 3: output.conf file check*
![Ubuntu 64-bit-2024-09-18-17-33-28](https://github.com/user-attachments/assets/c5bb8ee2-fd2d-40fa-8a96-c67940eea456)
<br>
As we checked the file has the correct ip-address that we added in the previous step (3).<br>
# 5-step:
Now we are going to add the file that will be forwarded to splunk enterprise using splunk forwarder.<br>
In the /opt/splunkforwarder/bin directory.<br>
Using the following command to add the file that will be monitored and forwarded by splunkforwarder.<br>
``./splunk add monitor /var/log/snort/alert ``<br>
*Ref 4: snort alert check*

![Ubuntu 64-bit-2024-09-18-17-50-38](https://github.com/user-attachments/assets/9196ecae-85c4-42eb-8cca-6e1a2f3082d8)

We can see the specific alert file that is generated by snort will be monitored and forwarded to the server.<br>
<br>
# 6-step:
We wil now go to the /opt/splunkforward/etc/apps/search/local directory.<br>
using the following command :<br>
`` cd /opt/splunkforward/etc/apps/search/local``<br>
Here we need to add the following things so the alerts that are sent to the splunk enterprise server is arranged properlly.<br>
Adding:<br>
``[Splunktcp://9997]``<br>
``connection_host="ip-address of the server"``<br>
``index = main``<br>
``sourcetype=snort_aler_full``<br>
``source=snort``<br>
After adding these configuration in the input.conf file save it .<br>
Restart splunk using the following command in the bin directory:<br>
``./splunk restart``<br>
This will apply the configuration that we have done.<br>

#7-step:
We need to install splunk enterprise where the data is going to be recieved.<br>
Go to the splunk website and downnload the software .<br>
with this complete the initial steps in the installation of the splunk enterprise software on the host machine.<br>
After the installtion is done open splunk enterprise .It will open in the web-browser on the localhost.<br>
Use the login credentials created while installing splunk enterprise .<br>
After logging in go to setting .
under the data list select the receiving and forwarding option to receive the alerts on the 9997 port that was configured on the splunkforwarder.<br>

*Ref 5: snort-enterprise receiving port*

![local host enterprise port](https://github.com/user-attachments/assets/7d7b91c7-45ad-4800-abc5-ed820b5128cf)
After opening the port go to the dashboard and click on "searching an reporting" on the left apps list.<br>
*Ref 6: searching and reporting *
![local host enterprise port](https://github.com/user-attachments/assets/261a1886-0324-4f27-92b2-9e580abb1aee)
<br>
Now click on the datasummary and go to the sourse tab <br>
Here we can see that splunk-forwarder sent the snort alerts to splunk-enterprise.<br>

*Ref 6: source-splunk*

![Screenshot 2024-09-16 225818](https://github.com/user-attachments/assets/d134304e-25a0-4c99-a4ee-a36252552245)

# 8-step:
Now we can install a plugin to visualize the alerts in a more user friendly manner.<br>
On the dashboard under the apps tab click on the find an app.<br>
Now Search for any app that is more userfriendly in our case we are going to use the " Snort alert for splunk ".<br>

*Ref 7: Snort aler app for splunk*
<br>
![snort alertapp localhost](https://github.com/user-attachments/assets/4a6dc2bd-5ba2-44e4-9ee6-17bc063576bb)
<br>
Now install the app.Splunk will ask for the user name and password<br>
After completeting the installation <br>
Go to the dashboard of splunk<br>
Here you will see the snort alert for splunk app under the app list on the left corner.<br>

*Ref 8: Snort alert app for splunk on dashboard*
<br>
![snort alertapp localhost](https://github.com/user-attachments/assets/95b31bdb-a79a-4cc1-907c-3f7908c0ba9c)
<br>
Click on the app.<br>
As we can see now the alert from snort are presented in a more user friendly way.<br>

*Ref 9: Snort alert app dashboard*
<br>

![Screenshot_16-9-2024_232339_127 0 0 1](https://github.com/user-attachments/assets/2a3f8655-865a-478e-99a2-8d4c468ebe04)
