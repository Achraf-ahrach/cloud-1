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

## 🚀 Deployment Instructions

### ✅ Prerequisites

- A cloud server (Ubuntu 20.04 LTS) with:
  - SSH access
  - Python installed
- [Ansible]() installed locally
- Docker and Docker Compose installed on the target machine

### 🔐 Set Up

1. **Clone this repository:**

Clone this repository:

```bash
git clone github.com:Achraf-ahrach/cloud-1.git
cd cloud-1
```

2. Configure inventory:

Edit `inventory.ini` and replace with your server's IP:

```ini
[web]
cloud-1-vm1 ansible_host=YOUR.SERVER.IP ansible_user=root ansible_ssh_private_key_file=~/.ssh/id_ed25519
```

3. Create and configure `.env`:

```
cp .env.example .env
vim .env
```

Fill in required variables like database password, domain, etc.

### 🔐 Encrypting your `.env` file with Ansible Vault

To keep your sensitive environment variables secure, encrypt your `.env` file before deploying:

```bash
ansible-vault encrypt .env --output rules/templates/data.j2
```

- This command will:

  - Encrypt the `.env` file using Ansible Vault
  - Output the encrypted file as `rules/templates/data.j2`
  - Allow the Ansible playbook to decrypt and use it securely

  > **Important:**
  >
  > - You will be prompted to enter a Vault password during encryption and when running the playbook.
  > - Keep your Vault password safe and **never commit it to any public repository** .

  5. Run the playbook:

     Execute the Ansible playbook to deploy the entire stack:
