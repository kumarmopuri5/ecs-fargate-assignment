ECS Fargate CI/CD Deployment Pipeline

This project demonstrates an end-to-end DevOps deployment pipeline for a containerized Node.js application deployed on Amazon ECS Fargate using Terraform (Infrastructure as Code) and GitHub Actions (CI/CD automation).

📌 Architecture Overview

This solution follows a modern cloud-native deployment model:

User → Application Load Balancer → ECS Fargate Service → Docker Container → CloudWatch Logs

CI/CD Flow:

Developer Push → GitHub → GitHub Actions → Docker Build → Amazon ECR → ECS Rolling Deployment

🧱 Infrastructure (Terraform)

Infrastructure is provisioned using Terraform and includes:

VPC with public subnets
Internet Gateway & Route Tables
Application Load Balancer
Target Group & Listener
ECS Cluster (Fargate)
ECS Task Definition & Service
IAM Execution Role
Security Groups
CloudWatch Log Group
CloudWatch CPU Alarm
🐳 Application

A simple Node.js web server:

Runs on port 3000
Containerized using Docker
Base image: node:18
Deployed on ECS Fargate
📦 Container Registry

Docker images are stored in Amazon Elastic Container Registry (ECR).

Pipeline automatically:

Builds Docker image
Tags image
Pushes image to ECR
Updates ECS service
⚙️ CI/CD Pipeline (GitHub Actions)

Pipeline stages:

Source checkout
Docker image build
Push image to ECR
Trigger ECS deployment
🔁 Deployment Strategy

This implementation uses Rolling Deployment (ECS default strategy).

Deployment behaviour:

New task revision is created
ALB health checks validate new tasks
Traffic shifts gradually
Old tasks are terminated safely

This ensures:

✔ Zero downtime deployment
✔ Controlled rollout
✔ Automatic failure recovery

Future enhancement:

Blue/Green deployment can be implemented using AWS CodeDeploy integration.

📊 Monitoring & Observability

Monitoring is implemented using Amazon CloudWatch:

Container logs → CloudWatch Logs
ECS CPU utilization alarm configured
ALB health checks ensure availability
🛠 Terraform Usage

Initialize Terraform:

terraform init

Plan infrastructure:

terraform plan

Apply infrastructure:

terraform apply

Destroy infrastructure:

terraform destroy
📜 Runbook
🚀 Deploy Application
Push code to main branch
GitHub Actions pipeline triggers automatically
New container image is deployed via ECS rolling update
🔁 Rollback Strategy

Rollback options include:

Option 1 — ECS Revision Rollback

Update ECS service to previous task definition revision

Option 2 — CI/CD Rollback

Re-run previous successful GitHub Actions workflow

Option 3 — Manual Image Rollback

Deploy previous Docker image tag from ECR
📄 Logs

CloudWatch Log Group:
/ecs/assignment

🧯 Troubleshooting Guide

ALB 504 Gateway Timeout
Verify ECS task is running
Check security group port configuration
Confirm target group health status
ECS Task Not Starting
Verify IAM execution role
Ensure Docker image exists in ECR
Validate container port mapping
Pipeline Failure
Verify GitHub Secrets configuration
Check AWS credentials permissions
Confirm ECR authentication step

🎯 Outcome

This project demonstrates:

✔ Infrastructure as Code (Terraform)
✔ Containerization (Docker)
✔ Serverless container compute (ECS Fargate)
✔ CI/CD automation (GitHub Actions)
✔ Production-grade deployment architecture
✔ Monitoring & rollback readiness

🧭 Architecture Diagram

Refer to:

architecture-diagram.png
