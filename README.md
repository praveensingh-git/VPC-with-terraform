# AWS VPC + EC2 with Terraform

This project provisions a **VPC** with public and private subnets, an **Internet Gateway**, a **Route Table**, and an **EC2 instance** running inside the public subnet using **Terraform**.

---

## 📌 Architecture

The infrastructure created looks like this:

- **VPC** (`10.0.0.0/16`)
  - **Public Subnet** (`10.0.1.0/24`)
    - Connected to the Internet Gateway via Route Table  
    - Hosts an **EC2 instance**
  - **Private Subnet** (`10.0.2.0/24`)  
- **Internet Gateway** attached to the VPC
- **Route Table** that routes `0.0.0.0/0` to the Internet Gateway
- **EC2 Instance**
  - AMI: `ami-0955d1e82085ce3e8` (Ubuntu for `eu-north-1`)
  - Type: `t3.micro`

---

## 🛠️ Prerequisites

Before deploying, make sure you have:

- [Terraform](https://developer.hashicorp.com/terraform/downloads) installed (>= v1.5.0 recommended)
- An AWS account
- AWS credentials configured via:
  ```bash
  aws configure
  ```
- Proper IAM permissions to create VPC, subnets, EC2, and related networking resources

## 🚀 Usage

Clone this repository
```
git clone https://github.com/your-username/VPC-with-terraform.git
cd VPC-with-terraform
```

Initialize Terraform
```
terraform init
```

Preview the plan
```
terraform plan
```

Apply the configuration
```
terraform apply
```

Destroy resources (when done)
```
terraform destroy
```

## 📂 Files

`main.tf`→ Contains all resources (VPC, subnets, IGW, route table, EC2)

(Optional) `variables.tf` → Can be created for reusability

(Optional) `outputs.tf` → Can be added to output instance IP, VPC ID, etc.

## 🔒 Security Notes

The EC2 instance is created without a Security Group definition here. By default, it will not allow inbound access.

For SSH/HTTP/HTTPS access, you should define and attach a security group with proper ingress/egress rules.

Never hardcode AWS credentials in `.tf` files.
