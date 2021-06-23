## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

`Diagrams/Azure Project Network Diagram.png`

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file, such as `filebeat-playbook.yml` or `metricbeat-playbook.yml` may be used to install only certain pieces of it, such as Filebeat or Metricbeat respectively.



This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting ssh connections to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network logs and system metrics.

The configuration details of each machine may be found below:

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux 18.04      |
| Web 1    | Server   | 10.0.0.5   | Linux 18.04      |
| Web 2    | Server   | 10.0.0.6   | Linux 18.04      |
| Web 3    | Server   | 10.0.0.7   | Linux 18.04      |
| Elk 1    | Elk Server | 10.2.0.4 | Linux 18.04      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- `99.238.205.185`

Machines within the network can only be accessed by Jump Box VM, with its private IP of 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 99.238.205.185       |
| Web 1    | No                  | 10.0.0.4             |
| Web 2    | No                  | 10.0.0.4             |
| Web 3    | No                  | 10.0.0.4             |
| Elk 1    | Yes                 | 99.238.205.185, 10.0.0.4 |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it limits the potential for human error when manually configuring multiple machines (on larger projects), it saves time as all specified machines are updated at the same time, as well as protecting against any vulnerabilities to a machine that has not been updated. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
-  Install Docker.io on the machine
-  Install python3-pip for package management
-  Install the Docker Module using pip.
-  Increasing the virtual memory of the machine.
-  Donwload and Launch the elk docker web container & enable docker service. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

`Images/Docker_Ps_Output.png`

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6 
- 10.0.0.7 

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to collect log information on the host servers, and sends it over to the Elk stack (Elasticsearch and logstash) to be indexed.
- Metricbeats takes information from the operating system and services on the server, and sends that information to the Elk stack (Elasticsearch and Logstash) to be reviewed. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the `install-elk.yml` file to the `/etc/ansible` directory.
- Update the `hosts` file found in the `/etc/ansible` directory to include private IP of the vm you wish to implement the Elkstack on, followed with the following command: 
  `ansible_python_interpreter=/usr/bin/python3`

This VM should be added to the elk group within the hosts file, so when the install-elk.yml file is run, the script will configure the new vm like any others already found under the elk group. 
- Run the playbook by using the following command:
  - `ansible-playbook install-elk.yml`

- navigate to the new public IP for the elk vm just created, using port 5601 with the following path:
  - http://[your.ELK-VM.External.IP]:5601/app/kibana

to check that the installation worked as expected. If Kibana shows when navigating to this url, then elk has succesfully been deployed on the new VM.
Images/Elk VM Succesful Implementation
