## Automated ELK Stack Deployment

[Elk Project  drawio](https://user-images.githubusercontent.com/89983935/148483082-37808a3d-de58-40d4-bd08-84391d582d0e.png)

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.


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

The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks  
A advantage for using a jump box is it can act as an audit for traffic and a single point where we can manage user accounts

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.

Filebeat is a lightweight shipper for forwarding and centralizing log data
Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name                 | Function   | IP Address | Operating System |
|----------------------|------------|------------|------------------|
| Jump-Box-Provisioner | Gateway    | 10.0.0.4   | Linux            |
| Web-1                | Webserver  | 10.0.0.5   | Linux            |
| Web-2                | Webserver  | 10.0.0.6   | Linux            |
| ELK-1                | Monitoring | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox/bastion machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

-20.185.38.203

Machines within the network can only be accessed by Jumpbox or basion host.

-The Jumpbox
PublicIP: 20.185.38.203
PrivateIP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly  Accessible | Allowed IP Address     |
|----------------------|----------------------|------------------------|
| Jump-Box-Provisioner | Yes                  | 40.76.35.254/ 10.0.0.4 |
| Web-1                | No                   | 10.0.0.5               |
| Web-2                | No                   | 10.0.0.6               |
| ELK-1                | No                   | 10.2.0.4               |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it helps considerably with the representation of Infrastructure as Code (IAC). IAC involves provisioning and management of computing infrastructure and related configuration through machine-processable definition files

The playbook implements the following tasks:

Step 1: Install docker.io
Step 2: Install pip3
Step 3: Increase virtual machine memory
Step 4: Download and launch ELK ocntainer and enable associated ports
Step 5: Enable docker on reboots

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

-10.0.0.5
-10.0.0.6

We have installed the following Beats on these machines:

-Filebeat
-Meatbeat

These Beats allow us to collect the following information from each machine:

-File beat can allow Kibana to moniter log data and put it into dashboard. Once the data is collected it can be readable on Elasticsearch 
-Metricbeat can monitor systeam performace, load, cpu usage and analyzing memory. All of this is readable on the dashboard after configureing the machine data 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to Ansible control node.
- Update the hosts file to include webservers and elk

[webservers]

10.0.0.5 ansible_python_interpreter=/usr/bin/python3
10.0.0.6 ansible_python_interpreter=/usr/bin/python3

[elk]

10.2.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_
. install-elk.yml
. /etc/ansible
- Which file do you update to make Ansible run the playbook on a specific machine? 
- hosts
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
. One can specify the "elk" group to install on the ELK server and the "webservers" group to install Filebeat.
- Which URL do you navigate to in order to check that the ELK server is running?
