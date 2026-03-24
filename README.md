# 🚀 Azure DevOps → AWS EC2 CI/CD Setup (Step-by-Step)

## 📌 Overview

This project demonstrates how to integrate Azure DevOps with an AWS EC2 instance using a self-hosted agent to achieve automated deployment.

---

# 🎯 Objective

* Automate deployment from Azure DevOps to EC2
* Use SSH for secure Git operations
* Run pipelines on EC2 using a self-hosted agent

---

# 🛠️ Complete Step-by-Step Setup (with Commands)

---

## 🔐 STEP 1: Connect to EC2

```bash
ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
```

---

## 📦 STEP 2: Install Required Packages

```bash
sudo apt update
sudo apt install git -y
sudo apt install nodejs npm -y
```

---

## 🔑 STEP 3: Generate SSH Key on EC2 (for Azure DevOps)

```bash
ssh-keygen -t rsa -b 4096 -C "ec2-azure-devops"
```

Press Enter for all prompts.

---

## 📋 STEP 4: Copy Public Key

```bash
cat ~/.ssh/id_rsa.pub
```

👉 Copy output and add to Azure DevOps:

* User Settings → SSH Public Keys → New Key

---

## 🔗 STEP 5: Clone Repo using SSH

```bash
git clone git@ssh.dev.azure.com:v3/shansk2700/K8s-project/K8s-project app
cd app
```

---

## 🔧 STEP 6: Fix Git Identity

```bash
git config --global user.name "Shahnawaz Sheikh"
git config --global user.email "shansk2700@gmail.com"
```

---

## 🔄 STEP 7: Test Git Pull

```bash
git pull origin main
```

---

## ⚙️ STEP 8: Setup Azure DevOps Self-Hosted Agent

```bash
mkdir ~/az-agent && cd ~/az-agent
```

Download agent (from Azure DevOps UI):

```bash
wget https://vstsagentpackage.azureedge.net/agent/3.xxx/vsts-agent-linux-x64-3.xxx.tar.gz
tar zxvf vsts-agent-linux-x64-*.tar.gz
```

---

## ⚙️ STEP 9: Configure Agent (IMPORTANT)

```bash
./config.sh
```

Provide:

* Server URL: https://dev.azure.com/shansk2700
* Auth: PAT
* Pool: ec2-agent
* Agent Name: ec2-runner

---

## ▶️ STEP 10: Start Agent

```bash
./run.sh
```

OR run as service:

```bash
sudo ./svc.sh install
sudo ./svc.sh start
```

---

## 🧪 STEP 11: Verify Agent Running

```bash
ps -ef | grep Agent
```

---

## 📜 STEP 12: Create Pipeline YAML

```yaml
trigger:
- main

pool:
  name: ec2-agent

steps:
- script: |
    echo "Deploying application..."
    cd /home/ubuntu/app || exit
    git pull origin main
  displayName: "Deploy Code"
```

---

## 🚀 STEP 13: Push Code to Trigger Pipeline

```bash
git add .
git commit -m "update from ec2"
git push origin main
```

---

# 🔄 CI/CD Workflow

```text
Code Push → Azure DevOps Repo
              ↓
Pipeline Trigger
              ↓
EC2 Self-Hosted Agent
              ↓
git pull
              ↓
Application Updated 🚀
```

---

# ⚠️ Troubleshooting Commands

### Check Git Remote

```bash
git remote -v
```

### Change Remote to SSH

```bash
git remote set-url origin git@ssh.dev.azure.com:v3/shansk2700/K8s-project/K8s-project
```

### Test SSH

```bash
ssh -T git@ssh.dev.azure.com
```

### Fix Branch Tracking

```bash
git branch --set-upstream-to=origin/main
```

---

# ✅ Outcome

* Fully working CI/CD pipeline
* Automatic deployment on code push
* Secure SSH-based Git integration
* Self-hosted agent running on EC2

---

# 🚀 Future Improvements

* Dockerize application
* Deploy on Kubernetes (EKS)
* Add CI stages (build/test)
* Integrate monitoring

---

# 💡 Key Takeaway

This project demonstrates real-world DevOps practices:

* Automation of deployments
* Secure authentication using SSH
* Efficient pipeline execution using self-hosted agents

---

## 🙌 Author

**Shahnawaz Sheikh**
DevOps & Cloud Enthusiast
