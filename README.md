## Automated ELK Stack Deployment
 
The files in this repository were used to configure the network depicted below.
 
![Network_diagram](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Diagrams/AMIES%20Network_Diagram.drawio.png)
 
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml files may be used to install only certain pieces of it, such as Filebeat.
 
  - [Ansible Configuration File](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/Anisble_cfg/ansible.cfg)
  - [Filebeat Configuration File](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/Filebeat/filebeat-config.yml)
  - [Filebeat Playbook](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/Filebeat/filebeat-playbook.yml)
  - [Metricbeat Configuration File](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/MetricBeat/metricbeat-config.yml)
  - [Metricbeat Playbook](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/MetricBeat/metricbeat-playbook.yml)
  - [Hosts](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/hosts.yml)
  - [Elk install Playbook](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/install-elk.yml)
 
This Readme contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
 
 
### Description of the Topology
 
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
 
Load balancing ensures that the application will be highly available & secure, in addition to restricting access to the network.
- Load balancers distribute traffic across available machines, preventing Denial of service attacks whilst keeping the network accessible and secure.
-  Having a jump box allows the system to be updated all at once as only a single system requires the update, keeping the service available with little to no downtime.  
 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the systems files and logs.
- filebeat will be watching out for log data for us whilst metricbeat will be keeping an eye on system metrics & stats and directing them out to Kibana for our review.
 
The configuration details of each machine:
 
| Name       | Function     | IP Address | Operating System |
|------------|--------------|------------|------------------|
| Jump Box   | Gateway      | 10.10.0.4  | Linux            |
| Web-1      | Web server   | 10.10.0.5  | Linux            |
| Web-2      | Web server   | 10.10.0.6  | Linux            |
| Web-3      | Web server   | 10.10.0.7  | Linux            |
| Elk Server | Data Monitor | 10.1.0.1   | Linux            |
 
### Access Policies
 
The machines on the internal network are not exposed to the public Internet.
 
Only the Jump Box and the Elk Server can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-124.170.54.169
 
Machines within the network can only be accessed by HTTP & SSH.
- The only machine that has permission to access the Elk Server is the Jump Box, of which its IP address is 10.10.0.4.
 
A summary of the access policies in place:
 
| Name       | Publicly Accessible | Allowed IP Address(es)     |
|------------|---------------------|----------------------------|
| Jump Box   | Yes                 | 124.170.54.169             |
| Web-1      | No                  | 10.10.0.4                  |
| Web-2      | No                  | 10.10.0.4                  |
| Web-3      | No                  | 10.10.0.4                  |
| Elk Server | Yes                 | 124.170.54.169 & 10.10.0.4 |
 
### Elk Configuration
 
Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous as it allows us to efficiently update and deploy new VM's significantly reducing the time required to set up each VM individually and deploy future VMs that may be required.
 
The playbook implements the following tasks:
- Install docker.io
- Install Pip3
- Install docker python module
- Change system control to allow more memory
- Download and launch docker elk container
- Enable service docker on boot
- [The Whole Elk Installation Playbook can be accessed by clicking on this sentence](https://github.com/StaticTV/super-spoon/blob/main/Elk_Stack_Azure_VM_Project/Ansible/install-elk.yml)
 
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.10.0.5
- 10.10.0.6
- 10.10.0.7
 
We have installed both Filebeat and Metricbeat on these machines allowing us to collect the following information from each machine:
Metricbeat: Collects system metrics and statistics from these machines and sends them to be analyzed. Enables us to detect possible attacks.
Filebeat: Detects the changes to the system files.  
 
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
 
SSH into the control node and follow the steps below:
- Copy the .yml files to the ansible directory.
- Update the hosts file to include your web servers and your elk servers IP addresses.
- Run the playbook, and navigate to "http://your_webserver_IP:5601" to check that the installation worked as expected.
 
