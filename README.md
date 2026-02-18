# VProfile GitOps Infrastructure Repository (vprofile-gitops-iac)
## Parent GitOps Project

This repository is part of the GitOps platform:

https://github.com/josephmj0303/vprofile-gitops-eks-platform

## Overview

This repository manages the complete AWS infrastructure required to run the VProfile application using Terraform and GitHub Actions, following GitOps principles.

Infrastructure provisioning is fully automated and version-controlled. Any changes pushed to this repository automatically trigger GitHub Actions workflows to provision or update infrastructure.

---

## Purpose

This repository provisions and manages:

- AWS VPC
- Public and Private Subnets
- Internet Gateway
- Route Tables
- Amazon EKS Cluster
- EKS Node Groups
- Amazon ECR Repository
- IAM Roles and Policies
- Kubernetes Ingress Controller
- Terraform Remote State Backend

---

## GitOps Model

This repository serves as the single source of truth for infrastructure.

Workflow:

Git Push → GitHub Actions → Terraform Plan → Terraform Apply → AWS Infrastructure Updated

Branch strategy:

- stage branch → Terraform Plan
- main branch → Terraform Apply

---

## Architecture Components Created

### Networking

- VPC
- Public Subnets
- Private Subnets
- Internet Gateway
- Route Tables

### Kubernetes

- Amazon EKS Cluster
- Managed Node Groups

### Container Registry

- Amazon ECR Repository

### Kubernetes Add-ons

- NGINX Ingress Controller

---

## Repository Structure

```
vprofile-gitops-iac/
│
├── terraform/
│   ├── eks-cluster.tf
│   ├── main.tf
│   ├── variables.tf
│   ├── vpc.tf
│   ├── terraform.tf
│   └── outputs.tf
│
├── .github/
│   └── workflows/
│       ├── terraform-main.yml
│       └── terraform-stage.yml
│
└── README.md
```

---

## Terraform Remote State

Terraform state is stored remotely in S3.

Benefits:

- State locking
- Version control
- Team collaboration
- Prevents state corruption

---

## GitHub Actions Workflow

Trigger conditions:

Push to stage branch → Terraform Plan
Push to main branch → Terraform Apply

Pipeline stages:

Terraform Init
Terraform Format Check
Terraform Validate
Terraform Plan
Terraform Apply
Configure kubectl
Install Ingress Controller


---

## Deployment Instructions

### Step 1: Clone Repository

git clone https://github.com/josephmj0303/vprofile-gitops-iac.git

cd vprofile-gitops-iac

---

### Step 2: Configure GitHub Secrets

Required secrets:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
BUCKET_TF_STATE
AWS_REGION

---

### Step 3: Deploy Infrastructure

Push changes to stage branch:

git checkout stage
git push origin stage

Push changes to main branch:

git checkout main
git push origin main


GitHub Actions will automatically provision infrastructure.

---

## Infrastructure Created

After deployment, the following will be created:

- VPC
- Subnets
- Internet Gateway
- EKS Cluster
- Node Groups
- ECR Repository
- Load Balancer
- IAM Roles

---

## Verification

Check cluster:

aws eks update-kubeconfig --region us-east-1 --name vprofile-eks
kubectl get nodes

---

## Benefits

- Fully automated infrastructure provisioning
- Version-controlled infrastructure
- Repeatable deployments
- No manual configuration
- Easy rollback
- Production-ready infrastructure

---

## Future Improvements

- Terraform modules
- Multi-environment support
- Terraform Cloud integration
- Automated destroy workflow
- Add monitoring stack provisioning
