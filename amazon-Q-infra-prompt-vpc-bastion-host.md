📌 Amazon Q – Infrastructure Generation Prompt

Use the prompt below with Amazon Q to generate a complete, production-ready Terraform infrastructure.

👉 Copy & Paste Prompt
Create a complete AWS three-tier VPC infrastructure using Terraform with the following requirements:

Project Structure:
- Modular Terraform code with separate modules for VPC, bastion host, and VPC flow logs
- Environment-specific tfvars files (dev, staging, prod)
- Deployment scripts with validation and formatting checks
- Backend configuration for S3 state storage

VPC Module Requirements:
- Configurable CIDR block (default: 10.0.0.0/16)
- Multi-AZ deployment across 2 availability zones
- 3-tier subnet architecture:
  - Public subnets (10.0.1.0/24, 10.0.2.0/24) for web tier
  - Private subnets (10.0.11.0/24, 10.0.12.0/24) for application tier
  - Database subnets (10.0.21.0/24, 10.0.22.0/24) for database tier
- Internet Gateway for public subnets
- NAT Gateways for private subnet internet access (configurable single/multi NAT)
- Route tables with proper associations
- Database subnet group for RDS
- DNS hostnames and resolution enabled

Bastion Host Module Requirements:
- Ubuntu 22.04 LTS AMI (latest)
- Configurable instance type (default: t3a.large)
- Security group allowing SSH from configurable CIDR blocks
- Optional key pair creation with public key input
- Optional Elastic IP association
- Optional SSM Session Manager access with IAM role and AmazonSSMManagedInstanceCore policy
- Encrypted EBS root volume (GP3, configurable size)
- User data script for hostname configuration

VPC Flow Logs Module Requirements:
- Optional flow logs to S3 or CloudWatch
- S3 bucket with unique naming using random suffix
- CloudWatch log group configuration
- IAM role for flow logs service

Configuration Files:
- variables.tf with all configurable parameters
- outputs.tf with VPC IDs, subnet IDs, bastion details, and SSH commands
- terraform.tfvars.example with sample values
- Environment-specific tfvars (dev.tfvars, staging.tfvars, prod.tfvars)
- backend.tf.example for S3 backend configuration
- versions.tf with AWS provider ~> 5.0

Deployment Automation:
- deploy.sh script with environment parameter
- Terraform initialization, validation, formatting checks
- Plan generation with approval prompt
- Apply with error handling and colored output
- Makefile with common commands (init, plan, apply, destroy, clean)

Default Configuration:
- Project: "three-tier-vpc", Environment: "dev"
- Region: us-east-1, AZs: us-east-1a, us-east-1b
- Single NAT Gateway for cost optimization in dev
- Flow logs disabled in dev, enabled in staging/prod
- Bastion with SSM access enabled
- Comprehensive tagging (Environment, Project, Owner, ManagedBy, CostCenter)

Security Features:
- Encrypted EBS volumes
- Restrictive security groups
- Optional SSM access (no SSH keys required)
- VPC Flow Logs for monitoring
- Proper IAM roles with least privilege

File Structure:

├── main.tf
├── variables.tf
├── outputs.tf
├── versions.tf
├── backend.tf.example
├── terraform.tfvars.example
├── Makefile
├── environments/
│   ├── dev.tfvars
│   ├── staging.tfvars
│   └── prod.tfvars
├── modules/
│   ├── vpc/
│   ├── bastion/
│   └── vpc-flow-logs/
└── scripts/
   └── deploy.sh

Create all files with proper Terraform best practices, error handling, and documentation.
Include README.md with setup instructions and usage examples.
