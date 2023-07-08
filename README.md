# Ansible-Orchestrated-Apache-Web-Hosting-on-AWS-EC2

This project demonstrates the setup and configuration of a multi-server environment using Ansible on AWS EC2. The goal of this project is to host an Apache server on multiple Ubuntu servers.

## Prerequisites

- AWS account with appropriate permissions to launch EC2 instances.
- Ansible installed on the master server.

## Setup

1. Launch Ubuntu EC2 instances on AWS:
   - Launch four instances with the following names: master, server-1, server-2, server-3, server-4.
   - Ensure that all instances are launched with the same configuration, key pair, and security group.

2. Access the master server:
   - Connect to the master server using SSH.
   - Install Ansible on the master server.

3. Configure SSH access:
   - In the path `./ssh`, create a file named `ansible-key`.
   - Copy and paste the key pair that you used while launching the servers into this file.
   - Run the following command:
     ```
     $ cd ./ssh
     $ vi ansible-key
     # Copy and paste the key pair into the file, save, and exit.
     ```

4. Configure inventory file:
   - By default, the inventory file is stored in `/etc/ansible/hosts`. If it doesn't exist, create a new folder named `ansible` and inside that folder, create the inventory file named `hosts`.
   - Run the following commands:
     ```
     $ sudo mkdir /etc/ansible
     $ sudo vi /etc/ansible/hosts
     ```
   - Add the details of the nodes in the following format:
     ```
     [nodes]
     server-1 ansible_host=<server-1 IP address>
     server-2 ansible_host=<server-2 IP address>
     server-3 ansible_host=<server-3 IP address>
     server-4 ansible_host=<server-3 IP address>
     ```
5. Check inventory information:
   - Run the following command to display the inventory information:
     ```
     $ ansible-inventory --list -y -i /etc/ansible/hosts
     ```
     
6. Ping all nodes:
   - Run the following command to ping all nodes:
     ```
     $ ansible all -m ping -i /etc/ansible/hosts --private-key=~/.ssh/ansible-key
     ```     
     
6. Configure playbook:
   - Create a file named `test.yaml` in the Ansible project directory.
   - Write the necessary Ansible playbook code to install and configure Apache on the target nodes.
   - Run the following command:
     ```
     $ vi test.yaml
     # Add the playbook code, save, and exit.
     ```
7. Execute the playbook:
   - Run the following command from the Ansible project directory:
     ```
     $ ansible-playbook test.yaml -i /etc/ansible/hosts --private-key=~/.ssh/ansible-key
     ```

8. Verify the setup:
   - Access the IP addresses of `server-1`, `server-2`, `server-3`and `server-4` in a web browser.
   - You should see the default Apache page indicating a successful deployment.
  


![Screenshot_20230708_153618](https://github.com/harshartz/Ansible-Orchestrated-Apache-Web-Hosting-on-AWS-EC2/assets/129828021/f62bbf06-4e75-43af-8ac5-e8b4e3a6d2c9)

