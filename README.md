## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Image](Images/Elk_Stack_Instance_and_VNet.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the /etc/ansible file may be used to install only certain pieces of it, such as Filebeat.

  - _etc/ansible/install-elk.yml_

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized access to the network.
- _Load balancers protect the availbility of services on a server. Open web servers can experience Dos (denial of service) attacks. This type of attack floods servers with requests, which in turn renders them unavailable to other users. A load balancer can drop requests packets from an IP which is exhibiting a Dos attack.  A jump box acts a gateway router between VMs on a network and the internet. Securing and monitoring this single node is call fanning in and is much easier than monitoring each individual VM._

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- _Filebeat collects data about the file system_
- _Metricbeat collects machine metrics, such as uptime_

The configuration details of each machine may be found below.

| Name        |  Function    | IP Address  | Operating System |
|-------------|---------------|--------------|----------------------|
| Jump Box |  Gateway     |  10.1.0.4    |         Linux             |
| Elk-Server |  Elk Stack    |  10.0.0.4    |         Linux             |
| Web-1       | Web Server |   10.1.0.5    |         Linux             |
| Web-2       | Web Server |   10.1.0.6    |         Linux            |
| Web-3       | Web Server |   10.1.0.7    |         Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _Personal workstation_

Machines within the network can only be accessed by the Jump Box.
- _The Jump box private IP is 10.1.0.4_

A summary of the access policies in place can be found in the table below.

|     Name       | Publicly Accessible | Allowed IP Addresses |
|---------------|------------------------|---------------------------|
| Jump Box   |            Yes                | Personal Workstation   |
|  Elk-Server  |            No                 |         10.1.0.4                |
|   Web-1       |            No                 |       10.1.0.4/10.0.0.4    |
|   Web-2       |            No                 |       10.1.0.4/10.0.0.4    |
|   Web-3       |            No                 |       10.1.0.4/10.0.0.4    |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it increases the efficiency of having to set up the configuration of each machine individually.


The playbook implements the following tasks:
- Install Docker
- Install pip3
- Install Python Docker Module
- Download and Launch a docker Web Container
- Ensure Docker is Started on Boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

 [image](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.5
- 10.1.0.6
- 10.1.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files, some of which can be system, wifi or even error logs.
- Metricbeat monitors metrics from the system and services running on the server. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the /install-elk.yml file to the ~/etc/ansible directory.
- Update the etc/ansible/hosts file to include the Elk Server IP by adding it under the [elk] group to specify which machine to run playbooks on.
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.
