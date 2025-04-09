# My K8s Terraform Setup

This repo contains Terraform code to provision a Kubernetes cluster on AWS using:

- VPC with public/private subnets
- Bastion host
- Control plane & node security groups

## Getting Started

1. Clone this repo
2. Copy `terraform.tfvars.example` to `terraform.tfvars`
3. Fill in your own values
4. Run:

```bash
terraform init
terraform plan
terraform apply
