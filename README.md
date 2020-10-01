## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![github-small](https://github.com/TonyChinh/ElkProject/blob/master/RedTeamDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. 
Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting DDOS attacks to the network.

- Load Balancers protect the accessiblilty aspect of our security network. The advantage of having a jump box is that it is the only 
point of attack to the network and is protected through our rules in the security network. The jump can be taken offline without it effecting the WebVM's.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat plays the role of a logging agent that ships different types of data into an ELK stack for analysis.
- Metricbeat is a shipping agent used to collect and ship operating system and service metrics.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.7   | Linux            |
| Web-1    | DVWA     | 10.1.0.8   | Linux            |
| Web-2    | DVWA     | 10.1.0.9   | Linux            |
| Web-3    | DVWA     | 10.1.0.10  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 40.78.15.8
- Personal IP

Machines within the network can only be accessed by Jump Box Provisioner.
- We allowed our Jump Box provisioner to connect to our Elk server through connection of our containers. The IP address of the ELK server is 40.122.108.167.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|Jump Box  | Yes                 | Personal Host IP     |
|Elk Server| Yes                 | Personal Host IP     |
|WebVM's   | No                  | 40.78.15.8           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- These tasks were able to be performed all at once or are able to be staggered depending on the needs of the network.
 Most of all when all of configurations are correct it is a very consistant way of keeping and maintaining of all systems.

The playbook implements the following tasks:
- Install Docker.io
- Install PYTHON-PIP3
- Install Docker module via PIP3
- Command to increase Virtual Memory
- Download and Launch ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![github-small](https://github.com/TonyChinh/ElkProject/blob/master/docker%20ps%20-a.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.8
- 10.1.0.9
- 10.1.0.10

We have installed the following Beats on these machines:
- Filebeat
- MetricBeat

These Beats allow us to collect the following information from each machine:
- Filebeat logs files or locations, collects log events and forwards them to Elasticsearch or Logstash for indexing.
- Metricbeat collects process and system CPU and memory statistics and sends that data to Elasticsearch for indexing.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the host file to include your Elk server private IP.
- Run the playbook, and navigate to http://168.61.168.163:5601/app/kibana to check that the installation worked as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
- ansible-playbook install-elk.yml
- nano hosts
