# Ansible Playbooks for Host-Based Installation

This repository contains Ansible playbooks that are used to install various tools and services on target hosts. The installation process is **host-based**, meaning each playbook will run according to the configuration and roles defined for each host in the inventory.

---

## 🔧 What These Playbooks Do

- Install required software (e.g. Docker, Docker Compose, CLI tools)
- Set up configuration files or environment variables
- Deploy services using Docker Compose.

---

## 📂 Playbooks Included

- `docker.yml` – Installs Docker and Docker Compose on the target host
- `deploy-compose.yml` – Clone and runs a docker-compose deployment the application.
- `setup-native-env.yml` – System configuration like updates, users, etc.

---

## 🖥️ How It Works

1. You define your target hosts in `inventory.ini`
2. Each playbook will run only on the hosts specified
3. The tasks are executed based on host-specific variables (found in `host_vars/`)

Example:
```bash
ansible-playbook -i inventory.ini install-docker.yml
```

## ✅ Requirements to Run These Playbooks

To run the Ansible playbooks in this repository, you will need the following:

### 1. Ansible Installed Locally
Install Ansible on your machine:
- Using pip:
  ```bash
  pip install ansible
    ```
### 2. SSH Access to Target Hosts
You must be able to SSH into each target server, with SSH passwordless login (recommend)

### 3. How to use example:
1. First test if all hosts are accesible, run:
    ```bash
        ansible -m ping all
    ```
    To test if a group of hosts are accesible, run:
    ```bash
        ansible -m ping all <group-name>
    ```
2. Run a playbook
     ```bash
        ansible-playbook -i host.yaml docker.yml
    ```
### Note:
### 🔐 SSH Authentication Requirement
To successfully run these playbooks, the machine that runs Ansible (control node) **must have passwordless SSH access** (via SSH key) to all target servers (VMs).

This is because Ansible connects to each host over SSH and executes commands remotely. If SSH key authentication is not set up, Ansible will fail to connect unless you use `--ask-pass`.

> ⚠️ Make sure your Ansible control node has its public SSH key added to the `~/.ssh/authorized_keys` file of each target VM.

You can test SSH connectivity like this:

```bash
ssh ubuntu@192.168.1.10
