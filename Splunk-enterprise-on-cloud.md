# Splunk Enterprise on a cloud VM

This is the cloud-hosted part of my Snort/Splunk lab. The original Snort VM generated alerts, and Splunk Enterprise ran on a Civo-hosted Ubuntu instance for central log review.

The write-up records installing Splunk on the cloud VM, reaching its web interface and connecting the forwarder. It is a test setup rather than a hardened public deployment. Exposed management ports and sample commands should be reviewed before running them on an internet-facing host.

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


![source data on cloud](https://github.com/user-attachments/assets/aab3fd8d-d542-4686-8de0-ef251028f81e)
For more Friendly layout we are going to use the Snort alert for splunk app that can be downloaded.<br>
This will now give us a better layout of the data that is being recieved in splunk.<br>
*Ref 7: splunk-snort-alert-*
![snort alert cloud dashboard](https://github.com/user-attachments/assets/94f91093-4fa3-47ae-b304-373ea8a8e5a7)
<br>
<br>
## Conclusion:
By following these steps,we have successfully installed Splunk Enterprise on our Ubuntu cloud instance. Splunk is now ready to collect, index, and analyze snort data, giving us valuable insights through its web interface. Remember to secure your Splunk instance, monitor resource usage, and explore additional features such as data ingestion, alerting, and dashboard creation to fully leverage the power of Splunk for your organization's needs.

