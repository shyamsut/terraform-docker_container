# 🚀 Terraform + Docker: Provision Local Container

> A simple Infrastructure as Code (IaC) project to provision a local **Docker container** using **Terraform**.

---

## 🎯 Objective

Use **Terraform** to define and deploy a local **Docker container**, showcasing Infrastructure as Code for local development environments.

---

## 🧰 Tools & Technologies

- [Terraform](https://www.terraform.io/)
- [Docker](https://www.docker.com/)
- OS: Ubuntu 22.04 LTS

---

## 📁 Project Structure

terraform-docker-container/
├── main.tf # Terraform configuration
├── init.log # terraform init output
├── plan.log # terraform plan output
├── apply.log # terraform apply output
├── state.log # terraform state list output
└── destroy.log # terraform destroy output


---

## 📝 main.tf

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx" {
  name  = "nginx-container"
  image = docker_image.nginx.name
  ports {
    internal = 80
    external = 8080
  }
}
⚙️ Commands & Execution
🔹 Step 1: Initialize Terraform

terraform init > init.log
Initializes the working directory and downloads the Docker provider.

🔹 Step 2: Review the Plan

terraform plan > plan.log
Generates an execution plan to show what will be created.

🔹 Step 3: Apply the Configuration

terraform apply -auto-approve > apply.log
Provisions the Docker image and container.

✅ Output check:


docker ps
Visit: http://localhost:8080

🔹 Step 4: Check Terraform State

terraform state list > state.log
Example output:


docker_container.nginx
docker_image.nginx
🔹 Step 5: Destroy the Resources

terraform destroy -auto-approve > destroy.log
Cleanly removes all Docker resources created by Terraform.

✅ Deliverables
main.tf – Terraform configuration file

*.log – Execution logs of init, plan, apply, state, and destroy



