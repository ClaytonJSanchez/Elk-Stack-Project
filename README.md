# Elk-Stack-Project
A project working with cloud secruity, Ansible and Bash cripts, inlcuding a network diagram of my Azure workspace.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Cloud security network diagram draw.io Clayton.S](https://github.com/ClaytonJSanchez/Elk-Stack-Project/blob/main/Diagrams/Cloud%20security%20network%20diagram%20draw.io%20Clayton.S.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

[install-elk.yml](ClaytonJSanchez/Elk-Stack-Project/Ansible/roles/install-elk.yml.md)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting in-bound access to the network.

- The availabilty of servers in a network is defended from traffic irregularities by rerouting traffic of user requests across multiple servers through load balacncing. In response to traffic being rerouted, if needed, it minimizes the likelehood of downtime. Ensuring the reliability of a server.

What is the advantage of a jump box?_
- The advantage of using jumpbox is its strict use for adminstrative purposes only and the ability to controll access points of the virtual machine.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing
- Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the serve

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Web Server | 10.0.0.5 | Linux            |
| Web-2    | Web Server | 10.0.0.6 | Linux            |
| elk-stack-vm | Elk Server | 10.1.0.5 | Linux        |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisoner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Workstation public IP: 97.81.124.188

Machines within the network can only be accessed by Jump-Box-Provisioner.
- My workstations front-end IP (97.81.124.188) provided access to my elk-stack-vm through port 5601.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes (ssh)           | 97.**.***.***        |
| Web-1    | No                  | ssh from 10.0.0.4    |
| Web-2    | No                  | ssh from 10.0.0.4    |
| elk-stack-vm | Yes (http)      | 97.81.124.188        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because of it's continuity and reliability. IAC(Infrastructure as Code) is directly improved due to it only containing infrastructure specifications which lends itself to be easily configured and managed later down the road.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![sudo docker ps screenshot](https://github.com/ClaytonJSanchez/Elk-Stack-Project/blob/main/Ansible/sudo-docker-ps-screenshot.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat and Metricbeat on the web servers.

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._: 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Elk-Stack-Project.
- Update the host file to include web server and elk
  -[webservers]
  10.0.0.5 ansible_python_interpreter=/usr/bin/python3
  10.0.0.6 ansible_python_interpreter=/usr/bin/python3
  - [elk]
  10.1.0.5 ansible_python_interpreter=/usr/bin/python3
- Run the playbook, and navigate to http://104.43.212.30:5601/app/kibana to check that the installation worked as expected.


