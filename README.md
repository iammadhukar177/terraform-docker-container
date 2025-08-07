# 
## 
 TASK 3: Infrastructure as Code (IaC) - Provision Docker Container using Terraform
 Objective
 Provision a **local Docker container** (Nginx) using **Terraform** to demonstrate Infrastructure as
 Code (IaC).
 ## 
 Tools Used
 | Tool | Description |
 |-----------|-----------------------------------------|
 | Terraform | Infrastructure as Code (IaC) tool |
 | Docker | Containerization platform |
 | Provider | `kreuzwerker/docker` for Docker control |
 ## 
 Project Structure
 ```
 terraform-docker-container/
 main.tf # Terraform config file
 README.md # Project documentation
 logs/ # Terraform command logs
 terraform-init.log
 terraform-plan.log
 terraform-apply.log
 terraform-state.log
 terraform-destroy.log
 terraform.tfstate # Terraform-managed state (after apply)
 ```
 ## 
### 
 Setup Instructions
 Prerequisites
 Ensure the following tools are installed:- Terraform: https://developer.hashicorp.com/terraform/downloads- Docker: https://www.docker.com/products/docker-desktop
 Verify installations:
 ```
 terraform -version
 docker --version
 ```
 Make sure Docker is **running**:
 ```
 docker info
 ```
 ## 
### 
 Step-by-Step Execution
 Step 1: Create the Terraform Configuration
 **main.tf**
 ```hcl
 terraform {
 required_providers {
 docker = {
 source = "kreuzwerker/docker"
 version = "~> 3.0.2"
 }
 }
 }
 provider "docker" {}
 resource "docker_image" "nginx_image" {
 name = "nginx:latest"
 keep_locally = true
 }
 resource "docker_container" "nginx_container" {
 name = "my-nginx"
 image = docker_image.nginx_image.name
ports {
 internal = 80
 external = 8080
 }
 }
 ```
 ### 
```
 Step 2: Initialize Terraform
 terraform init | tee logs/terraform-init.log
 ```
 ### 
```
 Step 3: Review Plan
 terraform plan | tee logs/terraform-plan.log
 ```
 ### 
```
 Step 4: Apply the Terraform Configuration
 terraform apply -auto-approve | tee logs/terraform-apply.log
 ```
 ### 
```
 Step 5: Verify the Container is Running
 docker ps
 ```
 Visit in browser: http://localhost:8080
 ### 
 Step 6: Check Terraform State
 ```
 terraform state list | tee logs/terraform-state.log
 ```
 ### 
```
 Step 7: Destroy the Infrastructure
 terraform destroy -auto-approve | tee logs/terraform-destroy.log
 ```
 ## 
 Outcome
 You now understand how to use **Terraform** to:- Pull Docker images- Create and manage Docker containers- Manage infrastructure as code
 References- Use Terraform commands and state files effectively
 ## - [Terraform Docker Provider
 Docs](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs)- [Terraform Official Docs](https://developer.hashicorp.com/terraform)
 ## 
 Author
 **Madhukar Sammeta**
 _Full Stack Developer & DevOps Engineer_
 [GitHub](https://github.com/) | [LinkedIn](https://linkedin.com/
