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
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed locally
- Docker and Docker Compose installed on the target machine

### 🔐 Set Up

1. **Clone this repository:**

```bash
git clone git@github.com:Achraf-ahrach/cloud-1.git
cd cloud-1
```

2. **Configure inventory:**

Edit `inventory.ini` and replace with your server's IP:

```ini
[web]
cloud-1-vm1 ansible_host=YOUR.SERVER.IP ansible_user=root ansible_ssh_private_key_file=~/.ssh/id_ed25519
```

3. **Create and configure `.env`:**

```bash
cp .env.example .env
vim .env
```

Fill in required variables like database password, domain, etc.

4. **Encrypt your `.env` with Ansible Vault: 🔐**

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
> - Keep your Vault password safe and **never commit it to any public repository**.

5. **Run the playbook:**

Execute the Ansible playbook to deploy the entire stack:

```bash
ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass
```

6. **Access your application:**

- Open your browser and visit your server’s IP or configured domain
- Complete the WordPress setup wizard

## 📦 Services

| Service    | Port | Container Name | Purpose               |
| ---------- | ---- | -------------- | --------------------- |
| WordPress  | 9000 | wordpress      | Blogging platform     |
| PhpMyAdmin | 8080 | phpmyadmin     | DB management         |
| MariaDB    | 3306 | mariadb        | SQL database backend  |
| Nginx      | 443  | nginx          | Reverse proxy + HTTPS |

## 🔄 Features

- Automated provisioning with Ansible
- Fully containerized architecture (1 container = 1 process)
- Persistent data volumes for durability
- Secure access with restricted public exposure
- TLS support (Let's Encrypt or custom certificates)
- Scalable for multi-server deployment

## 🔐 Security Notes

- SSH access via key authentication only
- Database not exposed to public network
- Environment variables encrypted and handled securely
- Keep Vault password confidential and off public repos

## 📝 Notes

- You may use Scaleway, AWS, GCP, or any provider of your choice.
- Free DNS providers like DuckDNS or `.tk` domains are supported.
- Always shut down unused servers and services to avoid costs.
- The deployment persists across server reboots and retains data integrity.

## 📫 Contact

**Achraf Ahrach**  
[achrafahrach44@gmail.com](mailto:achrafahrach44@gmail.com)

## ✅ Evaluation Criteria

- [x] Fully automated deployment with Ansible (or similar)
- [x] Functional WordPress site with all services running in separate containers
- [x] Data persistence after reboot
- [x] Secure, limited public access configuration
- [x] Valid Docker Compose setup
- [x] TLS and domain name handling (optional but appreciated)
