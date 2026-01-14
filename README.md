🚀 End-to-End DevOps CI/CD Pipeline on AWS

🔥 Final DevOps Capstone Project — Day 50

This project demonstrates a complete real-world DevOps pipeline built using modern DevOps tools and AWS cloud services.

> Outcome:
Design, automate, and deploy an application using Terraform, Ansible, Jenkins, Docker, GitHub, and AWS EC2 — exactly how production DevOps teams work.



---

🧠 Project Architecture (High Level)

    GitHub (Source Code)
            ↓
    Jenkins (CI/CD Pipeline)
            ↓
    Terraform (Provision EC2 + Security Group)
            ↓
    Ansible (Install & Configure Docker)
            ↓
    Docker (Build & Run Application)
            ↓
    AWS EC2 (Live Production Server)




🧱 Tools & Responsibilities

Tool       	Purpose

GitHub	    Source code management
Jenkins	    CI/CD automation
Terraform   Infrastructure provisioning (EC2, Security Group)
Ansible     Configuration management (Docker installation)
Docker      Application containerization
AWS EC2	    Application hosting




📁 Project Structure

    .
    ├── terraform/
    │   └── main.tf
    ├── ansible/
    │   ├── hosts
    │   ├── site.yml
    │   └── roles/
    │       └── docker/
    │           └── tasks/
    │               └── main.yml
    ├── Dockerfile
    ├── index.html
    ├── Jenkinsfile
    └── README.md




🛠 Phase 1 — Infrastructure Provisioning (Terraform)

📂 Folder: terraform/
Terraform is used to:

Create an EC2 instance
Configure Security Groups (SSH & Application Port)
Output the EC2 public IP


Run Terraform

    terraform init
    terraform apply

✔ Save the EC2 Public IP — it is used in Ansible and Jenkins.



🛠 Phase 2 — Configuration Management (Ansible)

📂 Folder: ansible/
Ansible automatically:

Updates the server
Installs Docker
Starts & enables Docker service
Adds ubuntu user to Docker group


Run Ansible:

     ansible-playbook -i hosts site.yml -u ubuntu
     
✔ Docker is installed without manual SSH work.



🛠 Phase 3 — Application Containerization (Docker)

Dockerfile

    FROM nginx:alpine
    COPY . /usr/share/nginx/html

Application

    <h1>🎉 DevOps Final Project Deployed Successfully!</h1>
    
✔ Lightweight, production-ready container using Nginx Alpine.



🛠 Phase 4 — CI/CD Automation (Jenkins)

Jenkins Pipeline (Jenkinsfile)

Pipeline stages:

1. Checkout code from GitHub

2. Build Docker image

3. Deploy container to EC2 via SSH



✔ Any push to GitHub triggers automatic deployment.



✅ Final Verification

Open in browser:

    http://<EC2_PUBLIC_IP>:8080

🎉 Application successfully deployed using a complete DevOps pipeline.



🧠 Key Learnings & Skills Demonstrated

  ● Infrastructure as Code using Terraform
  ● Server configuration using Ansible
  ● CI/CD automation using Jenkins
  ● Containerization using Docker
  ● Cloud deployment on AWS EC2
  ● End-to-end DevOps workflow understanding



🏁 Final Note

This project reflects real production-style DevOps work, not just theory.

> From “everything is new” → Full DevOps pipeline implemented


👤 Author

    Mahendra Boopathi R
    Aspiring DevOps Engineer | Cloud & Automation Enthusiast ☁️🚀
