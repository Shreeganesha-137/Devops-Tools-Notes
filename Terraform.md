# Terraform on AWS EC2 (Ubuntu) - Complete Guide

---

## What is Terraform?

Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp. It allows you to define, provision, and manage cloud infrastructure using a declarative language called HCL (HashiCorp Configuration Language).

---

## Why Use Terraform?

- Automates infrastructure deployment
- Supports multi-cloud (AWS, Azure, GCP)
- Infrastructure as Code (IaC) - version controlled
- Enables modular, reusable configurations
- Manages resource dependencies and lifecycle
- Safe plan/apply/destroy workflows

---

## How to Install Terraform on Ubuntu (EC2)

### Step 1: SSH into your EC2 instance
```bash
ssh -i "your-key.pem" ubuntu@your-ec2-public-ip
# Installing Terraform and AWS CLI on Ubuntu EC2

---

## 🚀 Install Terraform on Ubuntu

### Step 1: Update packages and install dependencies

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
```

### Step 2: Add HashiCorp GPG key

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

### Step 3: Add official HashiCorp repository

```bash
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
```

### Step 4: Install Terraform

```bash
sudo apt-get update && sudo apt-get install terraform -y
```

### Step 5: Verify installation

```bash
terraform -version
```

---

## ☁️ Install and Configure AWS CLI (v2) on Ubuntu EC2

### Step 1: Install unzip

```bash
sudo apt install unzip -y
```

### Step 2: Download AWS CLI v2 installer

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

### Step 3: Unzip and install

```bash
unzip awscliv2.zip
sudo ./aws/install
```

### Step 4: Verify installation

```bash
aws --version
```

### Step 5: Configure AWS CLI

```bash
aws configure
```

Enter the following:

- AWS Access Key ID
- AWS Secret Access Key
- Default region (e.g. `ap-south-1`)
- Output format (e.g. `json`)

---

## ✅ Confirm AWS is Configured

Run the following:

```bash
aws sts get-caller-identity
```

**Expected output:**

```json
{
  "UserId": "AIDAEXAMPLE",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/your-username"
}
```

---

## 🛠 Other Helpful AWS CLI Commands

```bash
aws s3 ls
aws configure get region
cat ~/.aws/credentials
cat ~/.aws/config
```
# 🛠 Main Terraform Commands with Examples and Use Cases

---

## 1. `terraform init`

Initializes a new or existing Terraform project. It downloads all necessary provider plugins.

```bash
terraform init
```

---

## 2. `terraform plan`

Creates an execution plan showing what Terraform will do. No resources are changed.

```bash
terraform plan
```

**Use Case:** Review infrastructure changes before applying them.

---

## 3. `terraform apply`

Executes the actions proposed in the plan and creates/updates infrastructure.

```bash
terraform apply
```

**Use Case:** Deploy or update resources as per your Terraform configuration.

---

## 4. `terraform destroy`

Removes all resources defined in your Terraform configuration.

```bash
terraform destroy
```

**Use Case:** Clean up resources to avoid costs or reset environments.

---

## 5. `terraform validate`

Checks whether configuration files are syntactically valid.

```bash
terraform validate
```

**Use Case:** Ensure configuration correctness before planning or applying.

---

## 6. `terraform fmt`

Formats Terraform configuration files to a canonical style.

```bash
terraform fmt
```

**Use Case:** Maintain consistent formatting and readability in `.tf` files.

---

# ☁️ Terraform Remote Backend - In Detail

---

## 🔍 What is a Remote Backend?

A remote backend allows you to store Terraform's **state file** in a remote location like **S3**, enabling team collaboration, locking, and better disaster recovery.

---

## ✅ Why Use Remote Backend?

- Share state across teams for collaborative deployments  
- Lock state files using services like DynamoDB to avoid conflicts  
- Secure and reliable disaster recovery  
- Prevent local file loss or corruption

---

## 📦 Example: S3 as Remote Backend

Add the following `terraform` block in your main configuration (`main.tf`):

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "prod/terraform.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-lock-table"
    encrypt        = true
  }
}
```

---

## 🧱 Steps to Set Up S3 Backend with DynamoDB Locking

### Step 1: Create the S3 bucket

```bash
aws s3 mb s3://my-terraform-state-bucket
```

### Step 2: Enable versioning on the S3 bucket

```bash
aws s3api put-bucket-versioning --bucket my-terraform-state-bucket --versioning-configuration Status=Enabled
```

### Step 3: Create DynamoDB table for state locking

```bash
aws dynamodb create-table \
  --table-name terraform-lock-table \
  --attribute-definitions AttributeName=LockID,AttributeType=S \
  --key-schema AttributeName=LockID,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST
```

### Step 4: Run terraform init to use the remote backend

```bash
terraform init
```

Terraform will prompt you to migrate local state to remote.

---

## 📝 Final Notes

- ✅ Always commit your `.tf` files  
- 🚫 Never commit `.tfstate` or `.tfstate.backup` files  
- 📁 Use `.gitignore` to exclude sensitive files  
- 🔐 Use IAM roles or profiles to securely access AWS credentials in production
