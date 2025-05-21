# ☁️ Cloud-1 – Automated Deployment of Inception

> An automated deployment of a WordPress-based website infrastructure using Docker and Ansible on a remote cloud server.

## 📜 Project Overview

This project is an extension of the **Inception** subject at 42, focusing on **automating** the deployment of a containerized WordPress setup. Each component of the infrastructure is containerized and orchestrated via Docker Compose, while Ansible handles remote provisioning and setup.

The infrastructure includes:

- 🔧 WordPress
- 🐬 MariaDB (MySQL-compatible database)
- 🛠️ PhpMyAdmin
- 🌐 Nginx (as reverse proxy)
- 🔐 TLS (HTTPS) support (optional)
- 🔁 Persistent volumes
- 🔐 Hardened public access

## 🗂️ Project Structure

```bash
.
├── .env.example               # Example environment variables
├── .gitignore                 # Ignored files and folders
├── inventory.ini              # Ansible inventory with target host(s)
├── playbook.yml               # Main Ansible playbook
├── README.md                  # This file
└── rules                      # All configuration and deployment logic
    ├── files
    │   ├── docker-compose.yml       # Core service composition
    │   ├── mariadb
    │   │   ├── Dockerfile           # Custom MariaDB image
    │   │   └── tools
    │   │       └── db.sh            # DB initialization script
    │   ├── nginx
    │   │   ├── conf
    │   │   │   └── default          # Nginx config
    │   │   └── Dockerfile           # Nginx Docker image
    │   └── wordpress
    │       ├── Dockerfile           # Custom WordPress image
    │       └── tools
    │           └── script.sh        # WordPress setup script
    ├── handlers
    │   └── main.yml                 # Ansible handlers
    ├── tasks
    │   └── main.yml                 # Main task automation
    └── templates
        └── data.j2                  # Jinja2 template (e.g., environment files)
```
