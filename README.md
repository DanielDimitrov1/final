# SoftServe Academy final project

Deploying an application in docker container on AWS using Terraform.

For reaching this goal, I used the following tools:  

- Terraform
- AWS CLI
- Docker

# Goals:
 - Maximal automation ✅
 - Minimal hard-coding ✅
 - Optimal workflow of the infrastructure ✅


# Description:


I built this project using Terraform and Amazon Web Services - AWS. I chose this path because of the numerous benefits that these platforms provide. According to the best experts in the DevOps field, Infrastructure as a Code is the leading approach to managing data center server, storage, and networking infrastructure. IaC is used to significantly simplify large-scale configuration and management.


My project contains a web application, Terraform modules, root Terraform modules, and configuration files to create an infrastructure.

For the purpose of this project, I used the following tools and technologies:

- Terraform project
- Web application
- Root Terraform module
  - Terraform modules
  - S3 Terraform state - Stores a Terraform state
  - Elastic container registry - Creates an Elastic container registry (ECR) repository to store Docker images
  - Initial build - Builds and pushes initial Docker image to ECR repository
  - ECS cluster - Creates a VPC and a ECS cluster
  - Codebuild - Creates a Codebuild project


# Folders and Files

 - /app - application directory
		- Dockerfile - special file, containing script of instructions, to build Docker image
		- Makefile - special file, containing shell commands, to build and push Docker image to ECR repository
 - /root Terraform module
   - ./config - configuration directory
  	- project.tfvars - Contains variable values for development environment (git branch "main")
  	- secrets.tfvars - Contains secrets (Github token) for Github repository (not presented in the repo)
  	- buildspec.yml - Build SPEC for AWS Codebuild
  - backend.tf - Terraform configuration
  - variables.tf - Terraform variables
  - main.tf - Terraform main file
  - outputs.tf - Terraform outputs
 - /modules - Terraform modules
   - s3 - "S3 Terraform state" module directory
   - ecr - "Elastic container registry" module directory
   - init-build - "Initial build" module directory
   - cluster - "ECS cluster" module directory
   - codebuild - "Codebuild" module directory






# Deploying process


The deployment of such infrastructure is not a simple process. We have to do several steps in order to deploy the project effectively and efficiently.

First:
 - Add AWS AIM user credentials to ~/.aws/credentials
[default]
	- aws_access_key_id = YOUR AWS ACCESS KEY ID
	- aws_secret_access_key = YOUR AWS SECRET ACCESS KEY

Following steps:

- Comment backend "s3" in ./terraform/backend.tf file
	- terraform init
	- terraform apply -target=module.s3_terraform_state --var-file=./config/project.tfvars

- Uncomment backend "s3" in ./terraform/backend.tf file
	- terraform init
	- terraform apply --var-file=./config/project.tfvars --auto-approve

- Check results
	- Go to your AWS account and check created infrastructure resources
	- Go to the DNS name created Application Load Balancer and check an information on a web page

![Screenshot_112](https://user-images.githubusercontent.com/112561988/201911398-bd3a69b0-9d9c-416c-96ac-28bfcb7b5cd9.jpg)

