# terraform-vpc-architecture-on-aws

This repository contains a **modular, reusable Terraform configuration** that builds a **production-grade AWS VPC** with:
- 🧩 **1 VPC** (`10.0.0.0/16`)
- 🌐 **2 Subnets** (Public + Private)
- 🚀 **Internet Gateway**
- ⚙️ **NAT Gateway + Elastic IP**
- 🛣️ **Route Tables and Associations**

Designed with **best practices** for scalability, security, and modularization — perfect for use in **real AWS environments**.

---

## 🌐 Flow Summary

- **Public EC2** → **Internet Gateway** → **Internet**  
- **Private EC2** → **NAT Gateway (Public Subnet)** → **Internet Gateway** → **Internet**

---

## 🗂️ Project Structure

terraform-aws-vpc/
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── modules/
│ └── vpc/
│ ├── main.tf
│ ├── variables.tf
│ └── outputs.tf
└── assets/
└── aws-vpc-diagram.png

yaml
Copy code

---

## ⚙️ Features

| Feature | Description |
|----------|-------------|
| 🏗️ **VPC** | Creates an isolated network (`10.0.0.0/16`) |
| 🌐 **Subnets** | One Public (`10.0.1.0/24`), One Private (`10.0.2.0/24`) |
| 🌉 **Internet Gateway** | Provides Internet access for Public Subnet |
| 🔄 **NAT Gateway** | Enables outbound access for Private Subnet |
| 📦 **Route Tables** | Configured per-subnet for proper traffic flow |
| 🔒 **Private Access** | EC2s in Private Subnet have no direct public IPs |
| ⚙️ **Modular Design** | Reusable `vpc` module for multi-environment setups |

---

## 🚀 Deployment Guide

### 1️⃣ Prerequisites
- AWS CLI configured with credentials (`aws configure`)
- Terraform ≥ **v1.3**
- Proper IAM permissions (EC2, VPC, IGW, EIP, NAT, RouteTables)

### 2️⃣ Initialize and Deploy
```bash
terraform init
terraform plan
terraform apply -auto-approve
💡 Tip: To destroy the environment when done:

bash
Copy code
terraform destroy -auto-approve