# Linux Server Setup

Ansible playbooks for setting up a Python development environment on a Debian Linux server.

## Repository Structure

| Folder | Description | Best For |
|--------|-------------|----------|
| [01-structured-roles/](./01-structured-roles/) | Role-based setup with separate vars, tasks, and handlers | Advanced users who want clean, reusable structure |
| [02-beginner-setup/](./02-beginner-setup/) | Simple single-playbook setup with step-by-step guide | Beginners new to Ansible |
| [03-wsl-pull-model/](./03-wsl-pull-model/) | WSL on Windows + server self-updates via cron | Windows users; hands-off automation |

## Quick Start

Pick the approach that fits you:

### New to Ansible? Start here:
```bash
cd 02-beginner-setup/
# Edit inventory.ini with your server IP and username
ansible-playbook -i inventory.ini setup.yml --ask-become-pass
```

### On Windows? Use this:
```bash
cd 03-wsl-pull-model/
# Edit inventory.ini with your server IP and username
ansible-playbook -i inventory.ini playbook.yml --ask-become-pass
```

### Want a clean role-based structure?
```bash
cd 01-structured-roles/
# Edit inventory.ini and vars/python.yml
ansible-playbook -i inventory.ini site.yml --ask-become-pass
```

## Prerequisites

- A Debian Linux server with SSH access
- Ansible installed on your control machine (or WSL for Windows)
- SSH key authentication set up to the server

## What Gets Installed

All three approaches install:
- Python 3 + pip + venv + dev headers
- Common tools: black, flake8, pytest, ipython
- Automatic security updates via `unattended-upgrades`
