## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![link to diagram](https://github.com/aherron26/ELK-Stack-Project/blob/main/ELK-Visual.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the host file may be used to install only certain pieces of it, such as Filebeat.

[Link to Playbook File](https://github.com/aherron26/ELK-Stack-Project/blob/main/elk-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting traffic to the network.

-What aspect of security do load balancers protect? 
-Protects against DDoS attacks.

-What is the advantage of a jump box? 
-The main advantage of using a JumpBox is having one origination point for administrative tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the web traffic and system logs.

-What does Filebeat watch for?
-Log files

-What does Metricbeat record? 
-Collects metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.4   | Linux            |
| Web-1    |DVWA Server| 10.0.0.5   | Linux            |
| Web-2    |DVWA Server| 10.0.0.6   | Linux            |
| Web-3    |DVWA Server| 10.0.0.8   | Linux            |
| Elk-VM   |ELK Server | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from my local host machine's IP address.


Machines within the network can only be accessed by ssh.
-Which machine did you allow to access your ELK VM? What was its IP address? 
-The only machine allowed to access the ELK VM is the Jump Box machine and its IP address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | My host machine's IP |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |  
| Web-3    | No                  | 10.0.0.4             |
| ELK      | Yes                 | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows IT administrators to automate away the drudgery from their daily tasks. That frees them to focus on efforts that help deliver more value to the business by spending time on more important tasks.

-What is the main advantage of automating configuration with Ansible?
-It aims to provide large productivity gains to a wide variety of automation challenges.
 

The playbook implements the following tasks:
-In 3-5 bullets, explain the steps of the ELK installation play.
- Install docker.io
- Install python3-pip
- Install the docker module 
- Increase the virtual memory, allowing us to run everthing
- Allocate the memory
- Download and launch the elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](https://github.com/aherron26/ELK-Stack-Project/blob/main/Elk-Docker-PS.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.5), Web-2 (10.0.0.6), and Web-3(10.0.0.8)

We have installed the following Beats on these machines:
- Filebeats and Metricbeats

These Beats allow us to collect the following information from each machine:
-In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. 
-Filebeat monitors the log files or locations that you specify, collects log events.
-Metricbeats collects metrics from the operating system and from services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat Configuration and Metricbeat Configuration file to the Ansible Container.
- Update the host file to include the host ip address and the ip addresses of the web servers.

    -Line #1106
    
    output.elasticsearch:
    
    hosts: ["10.1.0.4:9200"]
    
    username: "elastic"
    
    password: "changeme"

    ...
    
    -Line#1806
   
    setup.kibana:
    
    host: "10.1.0.4:5601"
    
    
- Run the playbook, and navigate to 10.1.0.4:5601/app/kibana to check that the installation worked as expected.

