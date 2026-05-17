# 01 - Structured Role-Based Ansible Setup

This approach uses a proper Ansible **roles** structure to set up a Python development environment on a Debian server.

## Source
[Original conversation](https://claude.ai/share/4ae28ee3-ee35-4e75-b340-5dd190741109)

## Structure
```
01-structured-roles/
├── inventory.ini
├── site.yml
├── vars/
│   └── python.yml
└── roles/
    └── python-dev/
        ├── tasks/
        │   └── main.yml
        └── handlers/
            └── main.yml
```

## Usage
```bash
# Test connectivity
ansible -i inventory.ini dev_servers -m ping

# Dry run
ansible-playbook -i inventory.ini site.yml --check

# Full run
ansible-playbook -i inventory.ini site.yml --ask-become-pass
```

## What it installs
- Python 3.11 + dev tools
- pip, virtualenv, black, flake8, mypy, pytest, ipython
- Auto-update cron job (3 AM daily)
- Unattended-upgrades for security patches
