# 🚀 Azure DevOps → AWS EC2 CI/CD Setup

## 📌 Overview

This project demonstrates how to integrate Azure DevOps with an AWS EC2 instance to achieve automated deployment using a self-hosted agent. The goal was to enable real-time code updates from the repository to the EC2 server.

---

## 🎯 Objective

* Set up CI/CD pipeline
* Enable secure communication between Azure DevOps and EC2
* Automate code deployment on every push

---

## 🛠️ What I Learned

### 🔐 1. SSH Authentication

* Generated SSH keys
* Configured `authorized_keys` on EC2
* Switched from HTTPS to SSH for Git operations
* Eliminated password-based authentication

---

### 📦 2. Git Setup on EC2

* Cloned repository using SSH
* Fixed branch tracking issues
* Configured Git username and email
* Used `git pull` for syncing latest code

---

### ⚙️ 3. Azure DevOps Pipeline

* Created YAML-based pipeline
* Understood triggers (`main` branch)
* Learned pipeline structure (steps, scripts)

---

### 🖥️ 4. Self-Hosted Agent Setup

* Installed Azure DevOps agent on EC2
* Configured agent using `config.sh`
* Connected agent to custom pool (`ec2-agent`)
* Ran agent using `run.sh` and as a service

---

### 🚀 5. Deployment Automation

* Pipeline runs directly on EC2 (no SSH needed in pipeline)
* Automatically pulls latest code from repo
* Executes deployment commands

---

### ⚠️ 6. Troubleshooting

* Fixed:

  * SSH permission issues
  * Git remote URL problems
  * Branch tracking errors
  * Pipeline authorization errors
  * Agent queue and concurrency issues

---

## 🔄 CI/CD Workflow

```text
Code Push (Azure Repo)
        ↓
Pipeline Trigger
        ↓
Self-hosted Agent (EC2)
        ↓
git pull
        ↓
Application Updated 🚀
```

---

## 📁 Project Structure

```text
/home/ubuntu/app
    ├── source code
    ├── package.json
    └── deployment files
```

---

## 📜 Sample Pipeline (azure-pipelines.yml)

```yaml
trigger:
- main

pool:
  name: ec2-agent

steps:
- script: |
    cd /home/ubuntu/app || exit
    git pull origin main
  displayName: "Deploy Latest Code"
```

---

## ✅ Outcome

* Successfully integrated Azure DevOps with AWS EC2
* Achieved automated deployment on code push
* Eliminated manual deployment steps
* Built a foundation for advanced CI/CD pipelines

---

## 🚀 Future Improvements

* Dockerize the application
* Deploy using Kubernetes (EKS)
* Implement CI stages (build, test)
* Add monitoring & logging
* Use Infrastructure as Code (Terraform)

---

## 💡 Key Takeaway

This setup demonstrates a real-world DevOps workflow where:

* Automation replaces manual deployment
* Secure authentication ensures safe operations
* CI/CD pipelines improve efficiency and reliability

---

## 🙌 Author

**Shahnawaz Sheikh**
DevOps & Cloud Enthusiast
