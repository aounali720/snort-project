# Snort — rule configuration and traffic test

This lab runs Snort on an Ubuntu VM to see how IDS rules react to selected TCP and ICMP traffic. The screenshots and commands below document the setup I used.

**What I tested:** installing Snort, setting its monitored network, adding local rules, and generating traffic that would appear in the alert output. This is a learning environment, not evidence that an IDS was deployed on a production network.

**Environment:** Ubuntu VM, Snort, local rule file (`/etc/snort/rules/local.rules`), terminal tools. Splunk integration is documented in the other files in this repository.

The original instructions below are kept as a lab record. Check commands and package versions against current official documentation before repeating the setup.

## 1-Step Installing snort 
The initial step is to intall snort in our virtual machine using the terminal the command is:<br>
       ```
        sudo apt-get install snort
        ```
<br>During installation, you’ll be prompted to configure the network. Set your HOME_NET to the network you want to monitor.<br>
As in our case we are going to keep it as is for sniffing any packet on the network
<br>
## 2-step configuring snort 
After the installion of snort is complete we can define the source ip and port , the destination port on which snort monitors but in our case we want it to mmonitor the whole network <br>
For the configuration of source and destination ip of a network we can modify the snort.confi file <br>
This file can be found in the
**/etc/snort/snort.conf** 
path<br>
## 3-Step adding customs rules and testing
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
## 4-STEP Running snort
In this step we are going to check if snort is working properly using the following command.<br>
``sudo snort -q -l /var/log/snort -i ens33 -A console -c /etc/snort/snort.conf ``

*Ref 3: snort running*

![Ubuntu 64-bit-2024-09-16-02-24-54](https://github.com/user-attachments/assets/d5465914-56d3-4012-82ac-f4d459d4fe82)

Using another virtual machine we tried to ping the ubuntu machine on which the snort was running .<br>
And with another machine we tried to establish a connection to the ubuntu machine using ssh .<br>
With this the alerts were generated and can be seen on the terminal.<br>
In the above used command -l is used for loging the packets.<br>
Logged packets are saved in the /var/log/snort also <br>
*Ref 4: snort log file*
![Ubuntu 64-bit-2024-09-17-23-49-03](https://github.com/user-attachments/assets/b07828f8-fac8-4e06-9427-d1fc56902dfe)


# Conclusion
- The Detection Lab project provided valuable hands-on experience in setting up and configuring Snort as an Intrusion Detection System (IDS) and integrating it with Splunk Enterprise for centralized log monitoring and analysis. By focusing on detecting TCP and ICMP traffic, we were able to generate real-time alerts, simulating network threats within a controlled environment.

- Throughout the project, we gained practical skills in network traffic analysis, SIEM integration, and Linux system administration. We learned how to monitor suspicious activities using custom Snort rules, forward alerts to a SIEM system using Splunk Universal Forwarder, and analyze network threats in a centralized platform. These skills are crucial for understanding and mitigating network security threats, recognizing attack patterns, and utilizing effective defense strategies in a real-world environment.

- By successfully implementing Snort and forwarding alerts to Splunk, this project highlighted the importance of using open-source tools for network security, detection, and response, while also emphasizing the role of centralized log management in cybersecurity operations.









