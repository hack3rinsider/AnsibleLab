
# 🚀 AnsibleLab Infrastructure

A production-style Infrastructure as Code (IaC) laboratory built using **Ansible**, **Docker**, **Jenkins**, **NGINX**, **PostgreSQL**, and **Linux** to demonstrate enterprise infrastructure automation, configuration management, Blue-Green deployments, traffic switching, and CI/CD workflows.

---

# 🎯 Project Overview

AnsibleLab was designed to simulate a real-world enterprise environment where infrastructure provisioning, configuration management, deployment automation, and operational tasks are managed through Ansible.

The lab follows Infrastructure as Code principles and provides a fully containerized multi-node environment for learning and demonstrating modern DevOps practices.

### Core Objectives

* Infrastructure Automation
* Configuration Management
* Infrastructure as Code (IaC)
* Blue-Green Deployments
* NGINX Traffic Management
* CI/CD Integration
* Service Validation
* Infrastructure Orchestration
* Environment Management

---

# 🏗️ Infrastructure Architecture

```text
                           Jenkins
                              │
                              ▼
                     Ansible Controller
                              │
      ┌───────────────┬───────┴────────┬───────────────┐
      ▼               ▼                ▼               ▼

    web1            web2             web3            db1
   (BLUE)          (GREEN)         (NGINX)      (PostgreSQL)

                                              │
                                              ▼

                                            mon1
                                       (Monitoring)
```

All nodes communicate through a dedicated Docker bridge network.

---

# 🧱 Infrastructure Components

## 🎯 Controller Node

Central automation server responsible for infrastructure management.

### Responsibilities

* Inventory Management
* Playbook Execution
* Role Management
* Template Management
* Variable Management
* Infrastructure Automation
* Environment Tracking
* Traffic Switching

### Features

* Ubuntu Based
* SSH Enabled
* Ansible Control Node
* Agentless Automation

---

## 🔵 Blue Environment

Primary deployment environment.

### Purpose

* Application Hosting
* Deployment Target
* Environment Validation
* Production Candidate

---

## 🟢 Green Environment

Secondary deployment environment.

### Purpose

* Application Hosting
* Blue-Green Deployments
* Testing Environment
* Production Candidate

---

## 🌐 NGINX Load Balancer

Dedicated traffic management node.

### Responsibilities

* Reverse Proxy
* SSL/TLS Termination
* HTTPS Access
* Traffic Switching
* Environment Routing
* Error Handling

### Features

* HTTP Support
* HTTPS Support
* Blue-Green Routing
* Dynamic Backend Switching

---

## 🗄️ Database Server

PostgreSQL infrastructure node.

### Responsibilities

* Database Services
* Data Persistence
* Schema Initialization
* Backend Connectivity

---

## 📊 Monitoring Node

Dedicated monitoring and validation server.

### Purpose

* Monitoring Experiments
* Infrastructure Validation
* Service Verification
* Future Observability Integrations

---

# 📂 Inventory Design

Infrastructure resources are logically grouped.

```ini
[blue]
web1

[green]
web2

[lb]
web3

[databases]
db1

[monitoring]
mon1
```

### Benefits

* Logical Segmentation
* Targeted Automation
* Easier Scaling
* Simplified Management

---

# 🤖 Ansible Features

The platform demonstrates multiple Ansible concepts.

### Configuration Management

* Server Configuration
* Service Configuration
* Environment Standardization
* Infrastructure Consistency

### Automation

* Package Installation
* Service Management
* File Deployment
* Infrastructure Provisioning

### Orchestration

* Multi-Node Management
* Environment Coordination
* Traffic Switching
* Validation Workflows

### Infrastructure as Code

Infrastructure definitions are stored as code using:

* Playbooks
* Roles
* Variables
* Templates
* Inventory Files

---

# 🧩 Role-Based Architecture

The project follows Ansible best practices through reusable roles.

```text
roles/
├── backend/
└── nginx/
```

Each role contains:

* Tasks
* Handlers
* Variables
* Defaults
* Metadata
* Tests

### Advantages

* Reusability
* Maintainability
* Scalability
* Modularity

---

# 📝 Jinja2 Template Management

Dynamic configuration generation is performed using templates.

### Templates

```text
nginx.conf.j2
nginx-site.conf.j2
index.html.j2
```

### Benefits

* Dynamic Configurations
* Environment-Specific Settings
* Reduced Duplication
* Easier Maintenance

---

# 🔄 Blue-Green Deployment Architecture

The infrastructure supports Blue-Green deployment workflows.

```text
Current Production
        │
        ▼
Deploy Inactive Environment
        │
        ▼
Health Validation
        │
        ▼
Approval
        │
        ▼
Traffic Switching
        │
        ▼
Production Verification
```

### Benefits

* Near Zero Downtime
* Safer Releases
* Easy Rollback
* Reduced Risk

---

# 🌐 NGINX Traffic Management

Traffic management is automated using Ansible.

### Capabilities

* Backend Routing
* Reverse Proxying
* SSL Termination
* Traffic Switching
* Environment Selection
* Health Verification

### Supported Workflows

* Blue → Green
* Green → Blue
* Manual Switching
* Automated Switching

---

# 🔐 Security Features

### Access Control

* SSH Authentication
* Controlled Node Access
* Centralized Management

### Network Security

* Isolated Docker Network
* Internal Node Communication
* Infrastructure Segmentation

### Secure Traffic

* HTTPS Support
* SSL/TLS Certificates
* Encrypted Communication

---

# 🐳 Dockerized Infrastructure

The entire lab is containerized.

### Infrastructure Nodes

```text
controller
web1
web2
web3
db1
mon1
```

### Benefits

* Portable Infrastructure
* Consistent Environments
* Easy Rebuilds
* Simplified Testing

---

# 📊 Jenkins Integration

Jenkins acts as the CI/CD orchestrator.

### Pipeline Capabilities

* Infrastructure Validation
* Environment Deployment
* Health Checks
* Traffic Switching
* Production Verification

### Benefits

* Automated Workflows
* Repeatable Deployments
* Reduced Manual Effort

---

# 🏥 Infrastructure Validation

Validation mechanisms ensure infrastructure reliability.

### Checks Performed

* Host Reachability
* Service Availability
* Environment Validation
* Traffic Verification
* Health Checks

---

# 📈 Learning Outcomes

This project demonstrates:

* Ansible Automation
* Configuration Management
* Infrastructure as Code
* Docker Networking
* Blue-Green Deployments
* NGINX Administration
* SSL/TLS Configuration
* Jenkins CI/CD
* Multi-Node Infrastructure Design
* Infrastructure Orchestration
* Environment Management
* Production-Style DevOps Practices

---

# 🎯 Project Highlights

✅ Infrastructure as Code

✅ Agentless Automation

✅ Multi-Node Architecture

✅ Blue-Green Deployments

✅ SSL Enabled NGINX

✅ Traffic Switching Automation

✅ Jenkins Integration

✅ Role-Based Architecture

✅ Jinja2 Templates

✅ Infrastructure Validation

✅ Production-Style Workflows

---

# 📜 License

Educational and portfolio project intended for learning Infrastructure Automation, DevOps Engineering, and Configuration Management using Ansible.
