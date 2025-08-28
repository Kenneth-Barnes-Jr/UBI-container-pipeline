# A Secure UBI-based Container Pipeline with GitLab & AWS
---

## 🏗️**Techinal Architecture**


1. **Code Commit & Push**
    - Developer pushes code to GitLab.
    - This triggers the GitLab CI/CD pipeline.

2. **Build Stage**
    - GitLab Runner builds a UBI-based container image.
    - The Docker image is tagged with version/commit ID.

3. **Push to Amazon ECR**
    - The image is authenticated using IAM credentials.
    - Built image is pushed and stored in Amazon Elastic Container Registry (ECR).

4. **Deploy to Amazon ECS**
    - ECS pulls the container image from ECR.
    - Service updates the running tasks with the new image.

5. **ECS ensures the application is available across the cluster.**
    - Monitoring with CloudWatch
    - ECS task/service logs are shipped to Amazon CloudWatch.
    - Metrics and alerts help track health, failures, and scaling.

---

## 📜**Project Overview**
I started this project with a simple goal in mind and that was to gain hands-on experience with UBI (Universal Base Image) while building something that feels production-ready. Instead of just containerizing a Flask app, I decided to go further and design a CI/CD pipeline around it.

Why? Because in real-world DevOps, the value isn't just in building a container. It's in creating repeatable, secure, and automated processes that can be scaled across teams and organizations.

---

## 🛠️**Technologies**

- Amazon ECR — Stores and manages container images

- Amazon ECS (Fargate/EC2) — Orchestrates and runs containerized applications

- Docker — Containerization platform for building and packaging applications

- GitLab CI/CD — Pipeline automation for build, test, and deployment

- Amazon IAM — Role-based access and secure permissions for ECS/ECR

- Amazon CloudWatch — Monitoring, logging, and debugging of ECS tasks and services

- Red Hat UBI Images — Lightweight, secure base images for container builds
---
## **🌟Resources**

- AWS ECS & ECR Basics - AWS ECS Documentation | ECR Documentation
- GitLab CI/CD - GitLab CI/CD Pipelines with YAML configuration examples.
- Docker + UBI - Red Hat UBI Images for building secure, lightweight containers.
- Terraform with AWS - Terraform AWS Provider Docs to automate ECS/ECR/IAM.
- Troubleshooting Pipelines - Double-check authentication (AWS credentials in GitLab variables), YAML syntax, and keep stages small and testable.
- Cost Management - Use AWS Pricing Calculator to estimate ECS/ECR costs and avoid surprises.
- Security Tip - Avoid hardcoding secrets in your pipeline; prefer GitLab CI/CD variables or AWS Secrets Manager.

---
## **Future Enhancements**

- Infrastructure as Code (Terraform) – Automate ECS, ECR, and IAM setup for repeatability.

- Monitoring & Logging – Add CloudWatch dashboards or Prometheus/Grafana for deeper visibility.

- Scaling & Load Balancing – Configure auto-scaling policies and integrate an Application Load Balancer.

- Secrets Management – Use AWS Secrets Manager or SSM Parameter Store instead of hardcoding credentials.

- Enhanced CI/CD – Expand GitLab pipeline stages to include security scans, automated testing, and blue/green deployments.