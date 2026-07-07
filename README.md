# Multi-OS Apache Web Server Provisioning

An Ansible playbook that automates the installation and configuration of an 
Apache web server with PHP support across mixed Linux environments — 
specifically Ubuntu (apt) and Rocky Linux (dnf).

## What it does

- Updates the package repository cache on the target host
- Installs Apache (`apache2` on Ubuntu, `httpd` on Rocky)
- Installs PHP support for Apache (`libapache2-mod-php` on Ubuntu, `php` on Rocky)
- Automatically detects the target OS and runs the correct tasks using 
  Ansible's `when` conditionals on `ansible_distribution`

## Why I built this

Most real infrastructure isn't single-OS. This playbook demonstrates 
writing idempotent, OS-aware automation — a single playbook that safely 
targets heterogeneous fleets instead of maintaining separate scripts per 
distro. It's part of my home lab, where I provision and manage services 
across a mixed Ubuntu/Rocky environment running on Proxmox.

## Requirements

- Ansible 2.9+
- Target hosts running Ubuntu or Rocky Linux
- SSH access and sudo privileges on target hosts
- Inventory file defining your target hosts

## Usage

1. Update your inventory file with target hosts:
```ini
   [webservers]
   192.168.1.10
   192.168.1.11
```

2. Run the playbook:
```bash
   ansible-playbook -i inventory.ini apache-playbook.yml
