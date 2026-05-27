# 🚀 AnsibleLab Infrastructure

A Docker + Ansible based DevOps lab to simulate real-world multi-node infrastructure setup (controller, web servers, database, monitoring).

---

## 🧱 Architecture

- 🧠 **controller** → Ansible control node (runs playbooks)
- 🌐 **web1 / web2 / web3** → Application servers (Node.js + Nginx)
- 🗄️ **db1** → PostgreSQL database server
- 📊 **mon1** → Monitoring node

All services communicate over a private Docker network:  
 `ansible-net (100.64.10.0/24)`

---

## ⚙️ Services Breakdown

### 🧠 Controller
- Ubuntu 24.04
- Ansible installed
- SSH enabled (`devops/devops123`)
- Central node for automation

### 🌐 Web Nodes (web1, web2, web3)
- Node.js 22 + Nginx
- SSH enabled for Ansible management
- Exposed ports:
  - web1 → `8083`
  - web2 → `8084`
  - web3 → `8086`

### 🗄️ Database (db1)
- PostgreSQL 16
- Database: `bankingdb`
- Auto schema init from `schema.sql`
- Port: `5432`

### 📊 Monitoring (mon1)
- Node-based container
- Reserved for monitoring tools/services
- SSH enabled

---

## 🔐 Default Credentials

### 👤 Linux Users (All Nodes)
- Username: `devops`
- Password: `devops123`

### 🗄️ PostgreSQL
- User: `postgres`
- Password: `postgres`

---

## ▶️ Run Project

```bash
docker compose up --build

🌍 Access Points
    • 🧠 Controller → ssh devops@localhost -p 3220
    • 🌐 Web1 → http://localhost:8083
    • 🌐 Web2 → http://localhost:8084
    • 🌐 Web3 → http://localhost:8086
    • 🗄️ DB → localhost:5432

🎯 Purpose
This lab is built for hands-on DevOps practice:
    • ⚙️ Ansible automation
    • 🧩 Multi-node orchestration
    • 🚀 Infrastructure as Code (IaC)
    • 🐳 Docker-based environments
    • 🔁 Real-world deployment simulation

⚠️ Notes
    • ❗ SSH password auth enabled only for learning
    • ❗ Not production secure
    • ❗ Designed strictly for lab/testing use

