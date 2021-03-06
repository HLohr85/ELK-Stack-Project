## Automated ELK Stack Deployment

### Overview:

The following project was created and deployed using Microsoft Azure Cloud Services. For this project we worked with different cloud computing service models such as: cloud networking, firewalls, and virtual computing. 

The project covers four different aspects of cloud computing and services:
- **Introduction To Cloud Computing**
  - Distinguish and identify between cloud services
  - Set up a virtual private cloud network
  - Protect the cloud network with a firewall
  - Deploy a virtual computer to the cloud network
- **Cloud Systems Management**
  - Access the entire VNet from a jump box
  - Install and run containers using Docker
  - Set up Ansible connections to VMs inside the VNet
- **Load Balancing and Redundancy**
  - Write Ansible playbooks to configure VMs
  - Create a load balancer on the Azure platform
  - Create firewall and load balancer rules to allow traffic to the correct VMs
- **Testing Redundant Systems**
  - Verify redundancy by turning off one virtual machines used in the infrastructure
  
The files in this repository were used to configure the network depicted below. 

![Azure Cloud diagram](https://github.com/HLohr85/Cybersecurity_Project_1/blob/main/Diagrams/Azure%20Cloud%20diagram%20with%20ELK%20VM.PNG)

These files have been tested, and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

  - [Ansible template configuration files](https://github.com/HLohr85/Cybersecurity_Project_1/tree/main/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA (D*mn Vulnerable Web Application).

The load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- The load balancer protects online security, through the front-end configuration, the load balancer can re-direct traffic to the virtual machines in the backend pool using a different port than the one clients use to communicate with the load balancer. The network can have multiple machines and the tasks are distributed among the virtual machines provding higher availability.
  - Using a jump box adds a layer of security to any network administrator. This is, in most cases to access a jump box one must use an SSH key efore launching a task to any attached virtual machines in the network.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- Filebeat serves to monitors log files and changes configured by the administrator, and notify of those changes. 
- Metricbeat monitors the servers collecting information from the monitored system.  

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web 1    | Webserver| 10.0.0.5   | Linux            |
| Web 2    | Webserver| 10.0.0.6   | Linux            |
| ELK      | ELK Stack| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _23.237.26.67_

Machines within the network can only be accessed by the Jump Box or Host desktop.
- _Jump Box_
  - Public IP 13.64.98.240
  - Private IP 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Port Accessible   | Allowed IP Addresses |
|----------|---------------------|-------------------|----------------------|
| Jump Box | Yes                 | SSH Port 22       | 23.237.26.67         |
| Load Balancer   | Yes                 | HTTP Port 80      | 23.237.26.67         |
| Web 1    | No                  | SSH Port 22       | 10.0.0.4             |
| Web 2    | No                  | SSH Port 22       | 10.0.0.4             |
| ELK      | Yes                 | SSH Port 22, TCP port 5601, HTTP Port 80     | 23.237.26.67         |

### Elk Configuration

We used Ansible to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible allows for Continous Integration/Continous Deployment (CI/CD) and automatically updates a machine in the network when there is a change, thus reducing configuration errors.

The playbook implements the following tasks:
- Install Docker in the remote computer, docker packages applications inside a container.
- Install pip, Python3-pip allow the server to manage software packages easily.
- Increase memory usage, to allow us map the system and use more memory.
- Download and launch the Docker ELK container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![ELK - sudo docker ps -a](https://github.com/HLohr85/Cybersecurity_Project_1/blob/main/ELK/ELK%20docker%20ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- ELK - IP address 10.1.0.4
- Web 1 - IP address 10.0.0.5
- Web 2 - IP address 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat was installed in:
  - Web 1 - IP address 10.0.0.5
  - Web 2 - IP address 10.0.0.6

These Beats allow us to collect the following information from each machine:
- Filebeat is used to collect log files generated by the webserver from the machine that it was installed (click the link below) 
  - [ELK - Filebeat](https://github.com/HLohr85/Cybersecurity_Project_1/blob/main/ELK/ELK%20-%20Filebeat.PNG)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_Answer the following questions to fill in the blanks:_
- Which file is the playbook? Copy the elk.yml file 
- Where do you copy it? Copy the file to: /etc/ansible/install-elk.yml
- Which file do you update to make Ansible run the playbook on a specific machine? Go to nano /etc/ansible/hosts, add a group called (ELK), and specify the ELK IP address.

- The following screenshot checks that the installation worked as expected.
  - [ELK nano host (2)](https://github.com/HLohr85/Cybersecurity_Project_1/blob/main/ELK/ELK%20nano%20host%20(2).PNG)

- How do I specify which machine to install the ELK server on versus which to install Filebeat on? The ELK server 
- Which URL do you navigate to in order to check that the ELK server is running? 
  - http://<ELK.VM.External.IP>:5601/app/kibana

- If the site loads, then you have successfully configured the ELK server (click the link below) 
  - [ELK - Kibana](https://github.com/HLohr85/Cybersecurity_Project_1/blob/main/ELK/ELK%20-%20Kibana.PNG)

  As a **Bonus**, below are some specific commands the user will need to download and install an Ansible tool: 
- Open a terminal and SSH into your jump box run: (ssh username@Public-IP-address-from-JumpBox)
- Start the Ansible container by running: sudo docker ps -a (to get the container name)
- To get root access run: sudo docker start container_ID
- To operate as root run: sudo docker atttach container_ID
- Create your configuration file using nano, run: nano -l filename.yml
- Run the playbook: ansible-playbook filename.yml
- This will download and install the playbook according to the instrutions given
- Before you run the playbook, you can run: ansible-playbook filename.yml --syntax-check

  - The file below has samples of some of the playbooks that we created and ran in our virtual machines (click the link below to view the files):
   - [Ansible template configuration files](https://github.com/HLohr85/Cybersecurity_Project_1/tree/main/Ansible)
   - [ELK files (screenshots)](https://github.com/HLohr85/Cybersecurity_Project_1/tree/main/ELK) 
