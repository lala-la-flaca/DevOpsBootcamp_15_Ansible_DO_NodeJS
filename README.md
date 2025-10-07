# Module 15 – Configuration Management with Ansible
This exercise is part of Module 15 from TWN DevOps Bootcamp:  Configuration Management with Ansible. Module 15 focuses on automating cloud operations with Python. The demos showcase how to interact with AWS services (EC2, EKS, snapshots), perform monitoring tasks, and implement recovery workflows. By the end of this module, you will have practical experience in scripting infrastructure automation, monitoring, and recovery solutions.
T
# 📦Demo 1 – Health Check: EC2 Status Checks
# 📌 Objective
Use Ansible to automate the deployment of a Node.js application on a DigitalOcean server. This demo shows how to provision a server, set up the environment, create a Linux user, and deploy the app automatically.

# 🚀 Technologies Used
* Ansible: Configuration management tool for automation.
* NodeJS: Runtime environment for JavaScript Apps.
* Digital Ocean: Cloud provider.
* Linux: OS.

# 🎯 Features
  ✅ Deploys Node.js application via Ansible playbook.
  
  🔐 Creates a dedicated Linux user for deployment.
  
  ☁️ Automates package installation and permissions.

# Prerequisites
* DO account with SSH key.
* NodeJs app ready from previous module.

# 🏗 Project Architecture

# ⚙️ Project Configuration
1. Download the Node.js application from the [Nana Repo](https://techworld-with-nana.teachable.com/courses/1108792/lectures/31738145#:~:text=https%3A//gitlab.com/twn%2Ddevops%2Dbootcamp/latest/15%2Dansible/nodejs%2Dapp)
2. Create a DigitalOcean droplet.
3. Create a host file in Ansible.
4. Add the droplet’s IP address, SSH key, and Ansible user to the host file.
5. Create a play to install Node.js and npm.
6. Add a task to update the apt package repository and cache.
7. Add a second task to install Node.js and npm.
8. Create a second play to deploy the Node.js application.
9. Add a task to copy the Node.js project folder to the droplet.
10. Add a second task to unpack the .tgz file for the Node.js application.
11. Run the Ansible playbook to complete the deployment.
