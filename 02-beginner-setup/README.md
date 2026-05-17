# 02 - Beginner-Friendly Ansible Setup

A simple, step-by-step Ansible setup for absolute beginners. No prior Ansible knowledge required.

## Source
[Original conversation](https://claude.ai/share/33cd5422-4ae5-4796-a51a-454b7ccf4b47)

## What You Need
- A PC running Linux or macOS (control node)
- A Debian server you can SSH into (managed node)

## Usage
```bash
# 1. Install Ansible on your PC
sudo apt update && sudo apt install ansible

# 2. Set up SSH key auth (one time)
ssh-keygen -t ed25519
ssh-copy-id your_username@your_server_ip

# 3. Test the connection
ansible -i inventory.ini workstation -m ping

# 4. Run the playbook
ansible-playbook -i inventory.ini setup.yml --ask-become-pass
```

## What it installs
- Python 3, pip, venv, and common dev tools
- unattended-upgrades (automatic security updates)
- systemd timer for weekly pip upgrades
