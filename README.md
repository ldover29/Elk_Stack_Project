# Elk_Stack_Project
UofT Cybersecurity Project 1: A brief look into automating ELK Stack - By LaJuan Dover

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![name-of-you-image](https://github.com/ldover29/Elk_Stack_Project/blob/main/Diagrams/Elk_Diagram.png?raw=true)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

![Alt text](https://github.com/ldover29/Elk_Stack_Project/blob/main/Ansible/Filebeat/filebeat.yml)

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

- Load balancers are used to protect from attacks like denial of service (Dos) by lightening the traffic load to other servers. An advantage to using a jump box is that they are typically used as a jumping off point to ssh into another virtual machine. This can help restrict access from attacks and the internet.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat watches log files
- Metricbeat records metrics

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    |    VM    | 10.0.0.5   | Linux            |
| Web-2    |    VM    | 10.0.0.6   | Linux            |
| Web-3    |    VM    | 10.0.0.8   | Linux            |
| Elk      | ElkStack | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- personal IP
- 10.0.0.4

Machines within the network can only be accessed by SSH.
- The Jump Box (10.0.0.4)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- There is less room for human error and is more efficent. Also, automation saves time when it comes to repition.

The playbook implements the following tasks:
- Install docker
- Install python
- Download and launch docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![name-of-you-image](https://github.com/ldover29/Elk_Stack_Project/blob/main/Diagrams/Images/docker_ps_output.png?raw=true)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: collects webserver logs and any changes to system files 
- Metricbeat: collects metrics of the operating system

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration and playbook file that is provided to "etc/ansible" directory in the ansible container
- Update the "hosts" file to include the private IP address of the machine that will be installing and configure ELK. Example below:
 
  [webservers]
  - [your.private.IP] ansible_python_interpreter=/usr/bin/python3	
  - [your.private.IP] ansible_python_interpreter=/usr/bin/python3

  [elk]
  - [your_VM_IP] ansible_python_interpreter=/usr/bin/python3
- Run the playbook using the command "ansible-playbook (name-of-playbook)", and navigate to Kibana (http://[Public IP]:5601/app/kibana) to check that the installation worked as expected.
