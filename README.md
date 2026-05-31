# Local IaC & CI/CD Pipeline with Terraform, Ansible & Jenkins

[![Jenkins Pipeline](https://img.shields.io/badge/Jenkins-CI%2FCD-blue)](https://www.jenkins.io/)
[![Terraform](https://img.shields.io/badge/Terraform-IaC-purple)](https://www.terraform.io/)
[![Ansible](https://img.shields.io/badge/Ansible-Automation-red)](https://www.ansible.com/)

## 📌 Project Overview
This project demonstrates an **end-to-end Infrastructure as Code (IaC) and CI/CD pipeline** using:
- **Terraform** – provisions a Docker container (Nginx) locally.
- **Ansible** – configures the container by injecting a custom `index.html` and reloads Nginx.
- **Jenkins** – orchestrates the entire pipeline (checkout → Terraform apply → Ansible provision → verify → destroy).

The pipeline runs completely **on your local machine** with zero cloud cost, making it perfect for learning and portfolio.

## 🏗️ Architecture

```mermaid
graph LR
    A[GitHub] -->|poll/push| B[Jenkins]
    B -->|terraform_apply| C[Docker_Container_Nginx]
    C -->|ansible_playbook| D[Custom_index.html]
    D -->|verify| E[docker_ps]
    E -->|post_always| F[terraform_destroy]
