# 03 - WSL + Pull Model Setup

A comprehensive guide for **Windows users** using WSL (Windows Subsystem for Linux). Uses a **pull model** — the server runs Ansible on itself daily to stay updated.

## Source
[Original conversation](https://claude.ai/share/beeff980-4725-44e4-abda-eeb995b0a206)

## Architecture

```
Windows PC (WSL/Ubuntu)          Debian Server
┌─────────────────────┐          ┌──────────────────────────┐
│  You write playbooks │──SSH──▶ │  Runs Ansible on itself  │
│  Run once to deploy  │          │  Every day at 3:00 AM    │
└─────────────────────┘          │  via cron                │
                                  └──────────────────────────┘
```

## Prerequisites

### 1. Install WSL on Windows
Open PowerShell as Administrator:
```powershell
wsl --install -d Ubuntu
```
Restart your computer after installation.

### 2. Set up Ansible in WSL
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y ansible
```

### 3. Set up SSH key authentication
```bash
ssh-keygen -t ed25519 -C "ansible-control"
ssh-copy-id youruser@192.168.1.100
```

## Usage

```bash
# Test connection
ansible -i inventory.ini devservers -m ping

# First run (deploys everything + sets up self-running cron)
ansible-playbook -i inventory.ini playbook.yml --ask-become-pass

# Re-run anytime to push updates
ansible-playbook -i inventory.ini playbook.yml --ask-become-pass
```

## What it does
- Installs Python 3, pip, venv, build tools on the Debian server
- Creates a Python virtualenv at `~/venvs/dev` with ipython, requests, black, flake8, pytest
- Installs Ansible on the server itself
- Sets up a cron job (3 AM daily) to self-run the playbook
- Configures unattended-upgrades for security patches
- Logs all auto-runs to `/var/log/ansible-self/run.log`

## Verifying it works
```bash
# SSH into the server, then:
sudo crontab -l                          # Check cron job exists
ls /opt/ansible-self/                    # Check playbook is deployed
sudo systemctl status unattended-upgrades

# Manual test of the self-run:
sudo ansible-playbook -i /opt/ansible-self/inventory.ini /opt/ansible-self/playbook.yml
```
