# 🚀 AnsibleLab Infrastructure

A production-style DevOps lab built using Docker, Ansible, Jenkins, PostgreSQL, Nginx, and Node.js to simulate real-world multi-node infrastructure, deployment automation, and CI/CD workflows.

---

# 🏗️ Infrastructure Architecture

```text
                    Jenkins
                       │
                       ▼
                 Controller Node
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
        web1         web2         web3
          │            │            │
          └────────────┼────────────┘
                       │
                       ▼
                      db1
                       │
                       ▼
                     mon1
```

All containers communicate over a private Docker network.

---

# 🧱 Services

## 🧠 Controller

* Ubuntu 24.04
* Ansible Control Node
* SSH Enabled
* Executes Playbooks
* Manages Infrastructure Automation

---

## 🌐 Web Nodes (web1, web2, web3)

* Ubuntu + Node.js 22
* Nginx Reverse Proxy
* PM2 Process Manager
* Banking Application Deployment Target
* SSH Enabled

### Access

* web1 → http://localhost:8083
* web2 → http://localhost:8084
* web3 → http://localhost:8086

---

## 🗄️ Database Server (db1)

* PostgreSQL 16
* SSH Enabled
* Auto Database Initialization
* Auto Schema Import
* Banking Application Database

### Database

* Database Name: bankingdb
* Port: 5432

### Auto Startup Tasks

Container startup automatically:

* Enables PostgreSQL network access
* Creates bankingdb
* Imports schema.sql
* Creates seed users

---

## 📊 Monitoring Node (mon1)

* Ubuntu-based Monitoring Container
* Reserved for monitoring stack experiments
* SSH Enabled

---

# 🔐 Default Credentials

## Linux User

Username:

devops

Password:

devops123

---

## PostgreSQL

Username:

postgres

Password:

postgres

---

# 🏦 Banking Application Deployment

Banking application is deployed using Ansible.

Features:

* User Registration
* Login Authentication
* Deposit Money
* Transfer Funds
* Transaction History
* Profile Management
* Admin User Management

---

# 🤖 Ansible Automation

Playbooks automate:

* Package Installation
* Application Deployment
* Nginx Configuration
* Backend Startup
* PM2 Process Management
* Multi-Node Deployment

Example:

```bash
ansible-playbook -i inventory.ini deploy-banking.yml
```

---

# 🔄 Jenkins CI/CD

Pipeline automatically:

1. Pulls latest code
2. Builds infrastructure
3. Recreates containers
4. Deploys application
5. Starts backend services
6. Verifies deployment

This provides a complete CI/CD workflow for learning DevOps practices.

---

# 🐳 Docker Infrastructure

Managed using Docker Compose.

Start:

```bash
docker compose up -d --build
```

Stop:

```bash
docker compose down
```

---

# 🎯 Learning Objectives

This lab demonstrates:

* Docker Containerization
* Multi-Node Infrastructure
* Ansible Automation
* PostgreSQL Administration
* Nginx Reverse Proxy
* PM2 Process Management
* CI/CD with Jenkins
* Infrastructure as Code
* Full Stack Application Deployment
* Production-Style DevOps Workflows

---

# ⚠️ Notes

* Designed for learning and portfolio projects.
* SSH password authentication is enabled for lab convenience.
* Not intended for production use without additional hardening.

---

# 📜 License

Educational and portfolio project.
