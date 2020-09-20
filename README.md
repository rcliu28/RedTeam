# RedTeam
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-config.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system of VMs on the network and watch system metrics, such as CPU usage; attempted SSH logins; sudo escalation failures and more. 

The configuration details of each machine may be found below.
| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.6   |       Linux      |
| Web-1    | Web Server | 10.0.0.8   |       Linux      |
| Web-2    | Web Server | 10.0.0.9   |       Linux      |
| ELK      | ELK Server | 10.1.0.5   |       Linux      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 23.116.233.101

Machines within the network can only be accessed by each other. The DVWA 1 and DVWA 2 VMs send traffic to the ELK server.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 52.250.5.177         |
| DVWA 1   | No                  | 10.0.0.1-254         |
| DVWA 2   | No                  | 10.0.0.1-254         |
| ELK      | No                  | 10.1.0.1-254         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it makes it easier to create computer software and processes by streamlines and simplifies cloud provisioning, configuration management, and application deployment, etc.  

The playbook implements the following tasks:
- Install Docker
- Install python3-pip
- Install Docker python module
- Increase virtual memory
- Download and launch Docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA-1 10.0.0.8
- DVWA-2 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat forward and centralize log data by monitors the log files or specific location, collect log events and forward them to Elasticsearch or Logstash for indexing.

- Metricbeat periodically collect metrics from the operating system and from services running on the server and send the data to Elasticsearch or Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbooks to the Ansible Control Node
- Update the hosts file to include 
  [webserers]
  10.0.0.8
  10.0.0.9

  [elk]
  10.1.0.5

After the hosts file is updated, the following commands should be run:

$ cd /etc/ansible
$ ansible-playbook install_elk.yml
$ ansible-playbook install_filebeat.yml
$ ansible-playbook install_metricbeat.yml

To ensure the installation worked as expected, navigate to http://10.1.0.5:5601 with a web browser. 
