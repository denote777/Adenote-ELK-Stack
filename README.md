## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img width="411" alt="image" src="https://user-images.githubusercontent.com/94246930/168835767-c3001a3f-ead7-4eb0-a766-5dae64008b42.png">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml config file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

• The load balancer protects the network's availability by spreading traffic equally so that no one server is overburdened, preventing DoS attacks

• The Jump Box Provisioner automates computer configuration changes and limits access to the virtual network in Infrastructure as a Code (IaC) configurations

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

• Filebeat keeps an eye on the log files or locations you designate, collects log events, and sends them to Elasticsearch or Logstash to be indexed

• Metricbeat is a server monitoring tool that collects metrics from the system and services operating on the server, such as Apache, MySQL, HAProxy, MongoDB, and so on

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|        Name        |        Function       | IP Address | Operating System |
|--------------------|-----------------------|------------|------------------|
| JumpBox-Provisioner| Gateway               | 10.0.0.5   | Linux            |
| Web-2              | Host DVWA 2           | 10.0.0.4   | Linux            |
| Web-3              | Host DVWA 3           | 10.0.0.6   | Linux            |
| Web-4              | Host DVWA 4           | 10.0.0.7   | Linux            |
| ELK                | Metric/Log Collection | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

• SSH port 22 on my Workstation with my Public IP.
Only 10.0.0.5 has access to the network's machines (ELK Server).

Machines within the network can only be accessed by 10.1.0.4 (ELK Server)

• Which machine did you allow to access your ELK VM? My Public IP address via TCP port 5601.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses                        |
|----------|---------------------|---------------------------------------------|
| Jump Box | No                  | My Workstation Public IP via SSH on Port 22 |
| Web-2    | No                  | 10.0.0.4 via SSH on Port 22                 |
| Web-3    | No                  | 10.0.0.6 via SSH on Port 22                 |
| Web-4    | No                  | 10.0.0.7 via SSH on Port 22                 |
| ELK      | Yes                 | My Workstaion Public IP via HHTP on Port 80 |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

•What are the primary benefits of using Ansible to automate configuration? It's adaptable, making it simple to reuse changes on other associated VMs.

The playbook implements the following tasks:

• Set up Docker 
• Set up Python3-pip
• Enable Docker on Boot 
• Increase and Use Virtual Memory 
• Install and Launch Docker Elk Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(<img width="468" alt="image" src="https://user-images.githubusercontent.com/94246930/162865431-78b6f5be-eb85-4cb6-bea9-8f987d1685b1.png">)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
•	Web-2: 10.0.0.4
•	Web-3: 10.0.0.6
•	Web-4: 10.0.0.7

We have installed the following Beats on these machines:
•	Filebeat
•	Metricbeat

These Beats allow us to collect the following information from each machine:
•	Filebeat monitors data logs such as Unique vistors, operating systems, heatmap etc.
•	Metricbeats collects metrics and system statistics such as CPU usage, RAM etc


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to /etc/ansible.
- Update the /etc/ansible/hosts file to include virtual elk server as seen below.
- Run the playbook, and navigate to *ansible-playbook <yml_file>.yml and navigate to <public_ip_of_elk>:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
The. yml are playbook files which can be placed in the ansible container to be deployed.

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

The host file can be updated to make Ansible run on a specific machine.

The file where the ELk server can be installed can be seen on the elk.yml and the (filebeat.yml)[Ansible/filebeat-playbook.yml] contains the file that installs the filebeat.

- _Which URL do you navigate to in order to check that the ELK server is running?

http://(elk-server-public-ip-address):5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

As a Bonus, provide the specific commands the user will need to run to download the playbook, update the files, etc.
Commands to install ansible, write and run playbook:
•	First ssh into Jumpbox-Provisioner: ssh admin@jump-box-ip

•	Then update Jumpbox: sudo apt-get update

•	Install Docker.io: sudo apt install docker.io

•	Verify the status of docker: sudo systemctl status docker

•	Start Docker if it is not running: sudo systemctl start docker

•	Pull Ansible Docker Container : sudo docker pull cyberxsecurity/ansible

•	Launch Ansible Container: docker run -ti cyberxsecurity/ansible:latest bash

•	To View docker container list created: sudo docker ps

•	Start the Docker container created: sudo docker start container_name

•	Activate shell on container: sudo docker attach container_name

•	To view ansible created: cd /etc/ansible

•	Create yml file by using the extenton: my_yml_file.yml

•	Run yml file: ansible-playbook my_yml_file.yml
   
