Overview

This project demonstrates a complete end-to-end DevOps CI/CD pipeline using:

* GitHub Actions
* Maven
* SonarCloud
* Docker
* Amazon ECR
* Amazon EKS
* Helm
* Kubernetes Ingress
* Terraform

The application is automatically tested, scanned, containerized, pushed to Amazon ECR, and deployed to an Amazon EKS cluster using Helm.

Architecture

Developer Push
      ↓
GitHub Actions CI/CD
      ↓
Maven Testing
      ↓
Checkstyle Analysis
      ↓
SonarCloud Scan
      ↓
Docker Build
      ↓
Push Image to Amazon ECR
      ↓
Helm Deployment
      ↓
Amazon EKS Cluster
      ↓
NGINX Ingress Controller
      ↓
Live Application


Technologies Used
Technology	      Purpose
GitHub Actions	CI/CD Automation
Terraform	      Infrastructure as Code
Amazon EKS	      Kubernetes Cluster
Amazon ECR	      Container Registry
Docker	      Containerization
Helm	            Kubernetes Package Management
Kubernetes	      Container Orchestration
SonarCloud	      Code Quality Analysis
Maven	Java        Build Tool
NGINX Ingress	External Access to Application
Route53	      DNS Management
Project Structure
EKS_CI-CD-github-actions/
│
├── .github/workflows/
│   └── main.yml
│
├── helm/
│   └── vprofilecharts/
│       ├── templates/
│       ├── Chart.yaml
│       └── values.yaml
│
├── kubernetes/
├── src/
├── Dockerfile
├── pom.xml
├── sonar-project.properties
└── README.md

Features
* CI Pipeline
* Maven testing
* Checkstyle validation
* SonarCloud code analysis
* Maven packaging
* CD Pipeline
* Docker image build
* Push image to Amazon ECR
* Connect to EKS cluster
* Deploy application using Helm
* Kubernetes rollout verification
* 
GitHub Actions Workflow

The GitHub Actions workflow automatically triggers on:

Push to main
Push to stage
Pull requests to main
Manual workflow dispatch
Amazon EKS Deployment

The application is deployed to:

Amazon EKS Cluster
Kubernetes namespace: vprofile

The deployment includes:

* Application Pod
* MySQL Database Pod
* RabbitMQ Pod
* Memcached Pod
* Kubernetes Services
* Kubernetes Ingress
* Helm Deployment

Deployment is handled using Helm:

helm upgrade --install vprofile-stack ./helm/vprofilecharts \
--namespace vprofile \
--create-namespace
Docker Image Deployment

Docker images are pushed to Amazon ECR using:

docker build -t vprofileapp:${GITHUB_RUN_NUMBER} .
docker push <ECR-REPOSITORY>
SonarCloud Integration

Code quality scanning is performed using SonarCloud.

The following checks are included:

Code smells
Bugs
Vulnerabilities
Security hotspots
Code coverage
Maintainability analysis
Kubernetes Verification Commands

Verify pods:

kubectl get pods -n vprofile

Verify services:

kubectl get svc -n vprofile

Verify ingress:

kubectl get ingress -n vprofile
Live Application

Application URL:

http://vproappgitops.tcapp.xyz/


GitHub Repository

Repository:

https://github.com/tcollins520/EKS_CI-CD-github-actions


Future Improvements

Potential enhancements:

* ArgoCD GitOps
* Blue/Green Deployments
* AWS Load Balancer Controller
* HTTPS with cert-manager
* ExternalDNS Automation
