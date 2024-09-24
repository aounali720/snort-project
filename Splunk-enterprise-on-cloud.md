
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


## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*
