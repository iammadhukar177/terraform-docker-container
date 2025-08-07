# 🧱 Task 3: Infrastructure as Code (IaC) with Terraform - Provision Docker Container

## 📌 Objective
Provision a **local Docker container (NGINX)** using **Terraform**, applying Infrastructure as Code (IaC) principles.

## 📚 Table of Contents
- Tools Used
- Project Structure
- Prerequisites
- Step-by-Step Workflow
- Output
- Cleanup
- Outcome
- Useful References
- Author

## 🧰 Tools Used
| Tool        | Description                             |
|-------------|-----------------------------------------|
| Terraform   | IaC tool to provision infrastructure     |
| Docker      | Containerization platform                |
| Provider    | kreuzwerker/docker for Docker control    |

## 📁 Project Structure
terraform-docker-container/
├── main.tf
├── terraform.tfstate
├── README.md
└── logs/
    ├── terraform-init.log
    ├── terraform-plan.log
    ├── terraform-apply.log
    ├── terraform-state.log
    └── terraform-destroy.log

## ⚙️ Prerequisites
Install the following:
- Terraform: https://developer.hashicorp.com/terraform/downloads
- Docker: https://docs.docker.com/get-docker/

Verify installations:
terraform -version
docker --version
docker info

## 🚀 Step-by-Step Workflow

### 1️⃣ Create Terraform Configuration (main.tf)
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx_image" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx_container" {
  name  = "my-nginx"
  image = docker_image.nginx_image.name
  ports {
    internal = 80
    external = 8080
  }
}

### 2️⃣ Initialize Terraform
terraform init | tee logs/terraform-init.log

### 3️⃣ Preview Plan
terraform plan | tee logs/terraform-plan.log

### 4️⃣ Apply Configuration
terraform apply -auto-approve | tee logs/terraform-apply.log

### 5️⃣ Verify Container
docker ps
Visit: http://localhost:8080

### 6️⃣ Check Terraform State
terraform state list | tee logs/terraform-state.log

## 📸 Output
Container: nginx:latest
Port Mapping: 8080:80
Browser: http://localhost:8080 (NGINX welcome page)

## 🧹 Cleanup
terraform destroy -auto-approve | tee logs/terraform-destroy.log

## ✅ Outcome
- Used Terraform as IaC
- Pulled and deployed Docker image
- Managed infrastructure lifecycle using Terraform

## 🔗 Useful References
- Terraform Docker Provider: https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs
- Terraform Docs: https://developer.hashicorp.com/terraform
- Docker Docs: https://docs.docker.com/

## 👨‍💻 Author
Madhukar Sammeta  
DevOps Engineer  
GitHub: https://github.com/iammadhukar177 
LinkedIn: https://linkedin.com/in/Madhukar-Sammeta
