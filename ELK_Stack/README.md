## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![NetworkDiagram](https://github.com/PROXYZ3R0/Cybersecurity/blob/master/ELK_Stack/Images/Untitled%20Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. 
Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  1. Installing docker
  2. Installing ELK
  3. INstalling Filebeat

This document contains the following details:

- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting traffic to the network.

-What aspect of security do load balancers protect? 
	
	The perk to load balancers is that they protect the Availibilty section of the triad. It ensures that traffic doesnt overload/overwhelm the severs.


-What is the advantage of a jump box?

	A Jump Box acts as a monitered and security hardened device that allows two unsimular zecurity zones to be able to have access to each other.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Jump Box and system network.

- What does Filebeat watch for?
 - Filebeat moniters log files and locations you specify, it also collects log events, and will forward the data to either Logstash or Elasticsearch.


- What does Metricbeat record? 

It periodically collects metrics from the services currently running on the server and the operating system.
The configuration details of each machine may be found below.

| Name        | Function      | IP Address          | Operating System |
|----------   |----------     |------------         |------------------|
| Jump Box    |Gateway        |10.0.0.10            | Linux            |
| VM-1        |Virtual Machine|10.0.0.11            | Linux            |
| VM-2        |Virtual Machine|10.0.0.12            | Linux            |
| VM-3        |Virtual Machine|10.0.0.13            | Linux            |
| ELK-VM1     |Traffic Moniter|10.1.0.4             | Linux            |
|Load Balancer|Traffic Manager|52.156.114.227       | n/a              | 


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Local Workstation IP 

Machines within the network can only be accessed by the Jump Box.

-Which machine did you allow to access your ELK VM? 

- Jump Box/Ansible container
- PrivateIP: 10.0.0.10
- PublicIP:  52.156.72.193

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses  |
|---------- |---------------------|---------------------- |
|Jump Box   |   No                |Local Machine          |
|Elk        |   No                |10.0.0.10/Local Machine|
|VM-1       |   No                |10.0.0.10              |
|Red-Team-LB|	No                |Local Machine          |
|Web-2	    |	No		  |10.0.0.10 	          |
|Web-3	    |	No		  |10.0.0.10              |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

-What is the main advantage of automating configuration with Ansible?

 - Allows to make changes across multiple machines at once.

The playbook implements the following tasks:
 - Installed docker.io to house the container. 
 - Installed python3-pip which is a package management system to manage software packages.
 - Increased Virtual memory to alllow system to carry out multiple processes at once. 
 - Download and launch the Elk Container 
 - Enable service docker on boot 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK-Container-SC](https://github.com/PROXYZ3R0/Cybersecurity/blob/master/ELK_Stack/Images/ElkVM1-Container-SC.JPG)




### Target Machines & Beats

This ELK server is configured to monitor the following machines:
 - | Web-1 | Web Server | 10.0.0.11 | Linux |
 - | Web-2 | Web Server | 10.0.0.12 | Linux |
 - | Web-3 | Web Server | 10.0.0.13 | Linux |

We have installed the following Beats on these machines:
- Successfully installed and ran filebeats,and metricbeats on all 3 Virtual Machines.

These Beats allow us to collect the following information from each machine:
- Filebeat collects and moniters all log Files.
- Metricbeats will periodically collect metrics of the operating system and services running.



### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/install-elk.yml
- Update the hosts file to include the foling 
 - ansible_python_interpreter=/usr/bin/python3
- Run the playbook, and navigate to http://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.

## If you are successful you should see the following

![NetworkDiagram](https://github.com/PROXYZ3R0/Cybersecurity/blob/master/ELK_Stack/Images/Kibana.JPG)
