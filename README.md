# Module 15 – Configuration Management with Ansible
This exercise is part of Module 15 from the TWN DevOps Bootcamp. In Module 15, we focus on automating server setup and application deployment using Ansible. You learn how to configure servers, deploy Node.js and Nexus, integrate with Terraform and Jenkins, manage Docker containers, and organize playbooks with roles. Each demo builds practical automation skills for real-world DevOps environments.

# 📦Demo 1 – Automate NodeJS application Deployment
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
* NodeJS app ready from the previous module.

# 🏗 Project Architecture

# ⚙️ Project Configuration
1. Download the Node.js application from the [Nana Repo](https://techworld-with-nana.teachable.com/courses/1108792/lectures/31738145#:~:text=https%3A//gitlab.com/twn%2Ddevops%2Dbootcamp/latest/15%2Dansible/nodejs%2Dapp)
2. Create a DigitalOcean droplet.
   
   <img src="" width=800 />
  
3. Create a host file in Ansible.
   
   <img src="" width=800 />
  
4. Add the droplet’s IP address, SSH key, and Ansible user to the host file.
   
   ```bash
   174.138.55.43 ansible_ssh_private_key_file=~/.ssh/id_rsa ansible_user=root
   ```
   <img src="" width=800 />
   
5. Create a play to install Node.js and npm.
   
   ```bash
   ---
    - name: Install nodeJS and npm
      hosts: 174.138.55.43
      tasks:
      - name: Update repo & cache
        apt: 
          update_cache : yes
          force_apt_get: yes
          cache_valid_time: 3600
      - name: Install npm and nodeJS
        apt:
          pkg:
            - nodejs
            - npm
   ```
 
8. Create a second play to add a new Linux user
   ```bash
       - name: create a new linux user
      hosts: 174.138.55.43
      vars_files:
        project-vars.yaml
      tasks:
        - name: create linux user
          user:
            name: "{{user_name}}"
            comment:  "{{user_name}} admin"
            group: admin
          register: user_creation_result
        
        - debug: msg={{user_creation_result.name}}
   ```
10. Create a third play to deploy the Node.js application.
    
   ```bash
      - name: Deploy nodejs app
  hosts: 174.138.55.43
  become: True
  become_user: "{{user_name}}"
  vars_files:
    project-vars.yaml
  vars:
    user_home_directory: /home/{{user_name}}
  tasks:   
  - name: unpack the nodejs tar file
    unarchive:
      src: "{{location}}/nodejs-app-{{version}}.tgz"
      dest: "{{user_home_directory}}"
  
  - name: install dependencies
    community.general.npm:
      path: "{{user_home_directory}}/package"
  
  - name: start the application
    command: 
      chdir: "{{user_home_directory}}/package/app"
      cmd: node server
    async: 1000
    poll: 0

  - name: ensure app is running
    shell: ps aux | grep node
    register: app_status
  
  - name: print output from command
    debug:
      var: app_status.stdout_lines
   ```
   <img src="" width=800 />
   

13. Run the Ansible playbook to complete the deployment.
    
    ```bash
    ```
    <img src="" width=800 />
