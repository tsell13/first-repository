# first-repository
Ansible YAML and network diagrams

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/ELKStack.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
Load balancers help secure a network from DDoS attacks. An advantage of a jump box is that you can access and manage devices in a separate security zone on your network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and system metrics.
Filebeat forwards and gathers log data into Elasticsearch or Logstash (in this network).
Metricbeat collects metrics from the OS and services on the server, which then gets shipped to Elasticsearch or Logstash (in this network).

The configuration details of each machine may be found below.


| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.1   | Linux            |
| DVWA 1   | Web Server | 10.0.0.5   | Linux            |
| DVWA 2   | Web Server | 10.0.0.6   | Linux            |
| ELK      | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: Home IP

Machines within the network can only be accessed by each other.
I allowed the Jump Box VM to access the ELK VM, it’s public IP is 40.78.27.95 while it’s private is 10.0.0.4

A summary of the access policies in place can be found in the table below.


| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Home IP              |
| ELK      | No                  | 10.0.0.4             |
| DVWA 1   | No                  | 10.0.0.6             |
| DVWA 2   | No                  | 10.0.0.6             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because that allows us to deploy and configure machines quickly without taking out time to manually configure one at a time.

The playbook implements the following tasks:
- Install ELK and allocate memory for ELK
- Install Docker python module
- Download and launch Docker web container
- Enable Docker service


### Target Machines & Beats
This ELK server is configured to monitor DVWA 1 and DVWA 2, at 10.0.0.5 and 10.0.0.6, respectively.

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat: Filebeat detects changes to the file system. Specifically, we use it to collect Apache logs.
- Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed sudo escalations, and CPU/RAM statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. We use the jump box for this purpose.

SSH into the control node and follow the steps below:
- Copy the playbook files to /etc/ansible.
- Update the playbook file to include the proper YAML format
- Run the playbook, and navigate to /etc/ansible to check that the installation worked as expected.

 - FAQ
Which file is the playbook? Where do you copy it?
 - The YAML files are the playbook files, copy it into your ansible folder (/etc/ansible)
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
 - Go into your hosts file and include the IPs of the DVWA VMs under [webservers] and then add an [elk] one and put the IP for that VM under it. 
Which URL do you navigate to in order to check that the ELK server is running?
 - curl http://[IP for Kibana]:5601
