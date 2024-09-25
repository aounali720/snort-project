
# Splunk-Enterprise-On-Cloud

## Objective

The primary objective of this project is to migrate Splunk Enterprise from a local environment to a cloud-hosted instance. In alignment with the <a href="https://github.com/aounali720/snort-project/blob/main/Splunk-forwarder-and-splunk-enterprise.md">previous project</a>, where Snort and Splunk were deployed on an Ubuntu virtual machine to monitor ICMP and TCP packet activity, this project will also involve configuring the Splunk Forwarder. The forwarder will be set up to transmit alerts from Snort to the cloud-hosted SIEM (Security Information and Event Management) solution, ensuring efficient and centralized alert management in the cloud environment.

### Skills Learned
- **Cloud-Based SIEM Configuration**:
  - Migrating Splunk Enterprise from a local environment to a cloud-hosted instance.
  - Configuring a cloud-based SIEM system for centralized log management and analysis.

- **Splunk Forwarder Configuration**:
  - Setting up and optimizing Splunk Forwarder to transmit alerts to the cloud-hosted Splunk Enterprise.
  - Understanding data pipelines and log forwarding best practices.

- **Snort Configuration and Management**:
  - Implementing and fine-tuning Snort for real-time intrusion detection.
  - Creating Snort rules to monitor for ICMP and TCP traffic.

- **Network Traffic Monitoring and Analysis**:
  - Analyzing network traffic and identifying potential threats (ICMP and TCP) using Snort and Splunk.
  - Configuring alert mechanisms based on network activity.

- **Linux System Administration**:
  - Managing an Ubuntu-based virtual machine to host and configure Snort and Splunk Forwarder.
  - Command-line proficiency for package installation, configuration, and network troubleshooting.

- **Cloud Computing and Deployment**:
  - Understanding cloud architecture and deployment for SIEM solutions.
  - Leveraging cloud infrastructure to enhance security monitoring and scalability.

- **Log Ingestion and Management**:
  - Ingesting, parsing, and indexing logs from different sources using Splunk.
  - Configuring dashboards and visualizations to monitor network security data.

- **Incident Detection and Response**:
  - Learning to detect, analyze, and respond to security incidents in real-time.
  - Developing insights into security event correlation and threat hunting.

### Tools Used
- **Snort**:
  - Open-source network intrusion detection and prevention system (IDS/IPS).
  - Used for real-time traffic analysis and packet logging.

- **Splunk Enterprise**:
  - Data analytics and SIEM platform.
  - Used for log aggregation, monitoring, and alerting.
  
- **Splunk Universal Forwarder**:
  - Lightweight tool for sending data to Splunk Enterprise.
  - Used to forward Snort alerts and logs to the Splunk instance.

- **Cloud Infrastructure (AWS, GCP, Azure, etc.)**:
  - Cloud-hosted platform for deploying Splunk Enterprise.
  - Provides scalability and centralized management for SIEM.

- **Ubuntu (Linux)**:
  - Open-source operating system for setting up Snort and Splunk Forwarder.
  - Virtual machine used for hosting the local instance of Snort and Splunk.

- **TCP/IP Network**:
  - The network protocol stack used for monitoring and detecting ICMP and TCP packets.

- **Command Line Interface (CLI)**:
  - For configuring and managing Snort, Splunk Forwarder, and Ubuntu.
  
- **Web Browser**:
  - To access the Splunk Enterprise dashboard for log analysis and monitoring.
  
- **Cloud SIEM (Hosted Splunk Enterprise)**:
  - Cloud-based security monitoring platform.
  - Used for centralized log analysis and alert management.


## Step-1:
start your cloud instance here we are using civo as cloud hosting provider.After the machince has started up we need to connect to it using ssh.<br>

*Ref 1: Cloud-machine*
![ssh connect to cloud instance](https://github.com/user-attachments/assets/100d29d6-83d7-4d2f-8d9c-7329fd3c64c7)
<br>
Navigate to the /opt directory in the machince here we will download and install splunk-enterprise <br>
## Step-2
After downloading Splunk Enterprise from there official website<br>
We can install the package using the following command:<br>
`` apt install ./splun-9.3.1-0b8d769cd912-linux-2.6-amd64.deb``<br>
*Ref 2: splunk-package-install-cloud-machine*
![Screenshot 2024-09-18 194331](https://github.com/user-attachments/assets/6a91ae89-0c4f-434b-a9f4-6ca29adde97e)<br>
After the installation we navigate in to the splunk directory using the cd command.<br>
After that we go into the bin directory<br>
## Step-3
For the initial start up of Splunk-Enterprise we use the following command :<br>
`` ./splunk start --accept-license ``<br>
After creating the username and password <br>
using the following command to allow tcp connection <br>
``sudo ufw allow 8000/tcp``

*Ref 3: splunk-cloud-machine*
![initial start of cloud splunk](https://github.com/user-attachments/assets/d83ff489-27f4-4d27-80bd-360db7100fd4)
We can now go the web-browser to login-in to the splunk-dashboard<br>
As this application is hosted on the port 8000<br>
we can connect by the following command using the web-browser:<br>
`` ip-address-of-cloud-machine:8000``<br>
*Ref 4: splunk-cloud-*
![Screenshot 2024-09-18 195026](https://github.com/user-attachments/assets/76012a4b-4276-4bc2-90b3-ba0374e0d59a)
Login with the username and password created in the initial installation of splunk<br>
## Step-4
Here we now need to configure the recieving data port where the splunk-forwarder will forward the alert<br>
by opening a port at 9997 :<br>
*Ref 5: splunk-portforward-*
![Screenshot 2024-09-18 195207](https://github.com/user-attachments/assets/e4cbce8d-5c01-4390-86e0-c9b116e43a85)
## Step-5
As now we can configure Splunk forwarder on our ubuntu virtual machine to send the alerts the cloud-splunk.<br>
In the ubunut machine we need to add the forwarder server with the command :<br>
`` ./splunk add forward-server "ipaddres":9997``<br>
Port 9997 is used by default <br>
To check the list of the server in splunk-Forwarder us the command :<br>
`` ./splunk list forward-server``<br>

*Ref 6: splunk-list-*
![list server on cloud](https://github.com/user-attachments/assets/7a692f52-d03e-415c-a908-7869aa98ef7e)
Reboot with the command:<br>
``./splunk restart``
After this we go into Splunk-enterprise dashboard<br>
## Step-6:
In the splunk cloud dashboard we go to SEARCHING AND REPORTING on the left side <br>
In the data summary we can see the machine <br>
*Ref 7: splunk-data-*


