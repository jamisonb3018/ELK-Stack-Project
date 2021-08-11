##### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!<img width="813" alt="Network_Diagram" src="https://user-images.githubusercontent.com/58924211/129057101-4e5d583b-e364-44ce-85d1-638fb02cd4c8.png">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  /etc/ansible/install-elk-playbook.yml

This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

The load balancing ensures that the application will be efficient addition to restricting traffic to the network.

- This protects the servers from becoming overloaded, as well as protecting against Distributed Denial of Service (DDoS) attacks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics and statistics.

- Filebeat watches for any information that has been changed, and when the change took place.

The configuration details of each machine may be found below.


|        Name        | Function | IP Address | Operating System |
|:------------------:|:--------:|:----------:|:----------------:|
| JumpBoxProvisioner |  Gateway |  10.0.0.4  |       Linux      |
|        Web-1       |  Server  |  10.0.0.5  |       Linux      |
|        Web-2       |  Server  |  10.0.0.6  |       Linux      |
|        Web-3       |  Server  |  10.0.0.7  |       Linux      |
|       Elk-VM       |  Server  |  10.1.0.4  |       Linux      |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from my IP Address:

- 100.16.xxx.xx
- Additionally Kibana can be accessed via URL from my home IP address.

Machines within the network can only be accessed by the JumpBoxProvisioner machine.
-Internal IP Address: 10.0.0.4

A summary of the access policies in place can be found in the table below.

|        Name        | Publicly Accessible | Allowed IP Addresses |
|:------------------:|:-------------------:|:--------------------:|
| JumpBoxProvisioner |        Yes          |        Home IP       |
|   Web-1            |         No          |       10.0.0.4       |
|   Web-2            |         No          |       10.0.0.4       |
|   Web-3            |         No          |       10.0.0.4       |
|   Elk-VM           |         No          |   Home IP, 10.0.0.4  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- This allows you to deploy to multiple servers using a single playbook

The playbook implements the following tasks:
- Install docker.io
- Install Python-pip
- Install docker container
- Launch docker container: elk

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="1190" alt="sudo_docker_ps" src="https://user-images.githubusercontent.com/58924211/128806942-e03d2531-6755-4bb4-ac70-06bc80f4044d.png">


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1 (10.0.0.5)  
- Web-2 (10.0.0.6) 
- Web-3 (10.0.0.7)

We have installed the following Beat on these machines:

- Filebeat
- Metricbeat

This Beat allow us to collect the following information from each machine:

- Filebeat will be used to collect log files from very specific files such as Apache, Azure tools and web servers.
- Metericbeat will be used to monitor VM stats, per CPU core stats, per filesystem stats, memory stats and network stats.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- SSH into the ELK Container ssh then ansible@10.0.0.4

- Run docker container list -a to verify that the container is on.

- If it isn't, run docker start sebp/elk.

- Exit the ELK Container

- Navigate to (Your IP Address):5601 from your web browser.

- Open your ELK server homepage

- Click on Add Log Data.

- Click on the DEB tab under Getting Started to view the correct Linux Filebeat installation instructions.

- Choose System Logs.

- Copy the filebeat-playbook.yml file to /etc/ansible/roles

- Filebeat Playbook

- Copy the filebeat-configuration.yml file to /etc/ansible/files.

- Filebeat Configuration

- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.

- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.

- Run the playbook with ansible-playbook filebeat-configuration.yml.

- Confirm that the ELK stack was receiving logs.

- Navigate back to the Filebeat installation page on the ELK server GUI.

- Verify that your playbook is completing Steps 1-4.

- On the same page, scroll to Step 5: Module Status and click Check Data.

- Scroll to the bottom and click on Verify Incoming Data.

- If the ELK stack was successfully receiving logs, you would have seen:

- Copy the metricbeat-configuration.yml file to /etc/ansible/files.

- Copy the metricbeat-configuration.yml file to /etc/ansible/files.

- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.

- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine, 10.1.0.4 for the purposes of my setup.

- Run ansible-playbook metricbeat-configuration.yml

- To verify that your play works as expected, on the Metricbeat installation page in the ELK server GUI, scroll to Step 5: Module Status and click Check Data.

![IMG_5462366A16D5-1](https://user-images.githubusercontent.com/58924211/129099985-a6226891-eb70-40d3-9676-24a80901bf2e.jpeg)

<img width="1168" alt="data_success" src="https://user-images.githubusercontent.com/58924211/129101160-f32dd481-f795-40d8-8cf1-a629b0c914b1.png">


