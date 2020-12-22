# CyberX
CyberSecurity Repository
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![README/Images/cloud-infrastructure.png](Images/cloud-infrastructure.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

![README/Images/installelk.yml](Images/install-elk.yml)
  - 
  
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- _Load balancers provide availiabilty and fault tolerance. The advantage of the jump box is to not have each of the web servers accessible to the network which makes them more secure. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat helps generate and organize log files to send to Logstash and Elastisearch. Specifically, it logs information about the file system, including which files have changed and when. 
- Metricbeat records machine metrics such as uptime or CPU usage and sends them to Logstash and Elastisearch. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    |Web Server| 10.0.0.7   | Linux            |
| Web 2    |Web Server| 10.0.0.6   | Linux            |
| ELK      |Elk Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- TCP Traffic over port 5061 from public IP address

Machines within the network can only be accessed by Jump Box Provisioner.
- Jump Box Provisioner: 10.0.0.4
- TCP Traffic over port 5061 from public IP address

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  |Host Machine Public IP|
| Web 1    | No                  | 10.0.0.4             |
| Web 2    | No                  | 10.0.0.4             |
Elk Server   No                    Public IP 

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- We can ensure our provisioning scripts will run identically everywhere. This will further ensure our automated configurations will do exactly the same thing every time they run, eliminating as much variabiitly between configurations as possible. 

The playbook implements the following tasks:
- Specify a different group of machines as well as a different remote user
- Increase the system memory
- Install the following services: docker.io, python3-pip, and docker. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
No longer have access to Azure so unable to get screenshot of docker ps output

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1: 10.0.0.7
- Web 2: 10.0.0.6

We have installed the following Beats on these machines:
- ELK Server, Web 1 and Web 2

These Beats allow us to collect the following information from each machine:
- Filebeat collects log files from very specific files, such as those generated by Apache, Microsoft Azure, or MySQL databases. Metricbeat collects metrics and system statistics. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the /etc/ansible/files/filebeat-config.yml file to /etc/filebeat/filebeat.yml
- Update the filebeat-playbook.yml file to include the .deb file using a dpkg command
- Run the playbook, and navigate to Step 5: Module Status to check that the installation worked as expected.

- /etc/ansible/files/filebeat-config.yml is the playbook and you copy it to /etc/filebeat/filebeat.yml
- _You update filebeat-playbook.yml. The Elk server is installed on the specific VM you created for ELK and the filebeat playbook is copied to the Web-VM servers only. 
- Kibana > Add Metric Data > Docker Metrics > Module Status to check data (No longer have access to the Azure so can't get the actual URL)

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._ Download the playbook: curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/files/filebeat-config.yml

- Update the files: dpkg -i filebeat-7.4.0-amd64.deb

- Run the playbook: ansible-playbook filebeat-playbook.yml.
