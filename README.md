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

HTTPS / TLS Implementation
Secure Ingress with cert-manager and Let’s Encrypt
Implemented automated HTTPS for the Kubernetes application running on Amazon EKS using:
•	cert-manager 
•	Let’s Encrypt 
•	Route53 DNS01 challenge 
•	NGINX Ingress Controller 
Features
•	Automated TLS certificate issuance 
•	Automatic certificate renewal 
•	Secure HTTPS ingress routing 
•	DNS-based domain validation 
•	Production-ready Kubernetes ingress setup 
Technologies Used
•	Kubernetes Ingress 
•	cert-manager 
•	Let’s Encrypt ACME 
•	AWS Route53 
•	NGINX Ingress Controller 
•	Helm 
DNS Architecture
GoDaddy → Route53 → EKS NGINX Ingress → Application
TLS Workflow
1.	cert-manager monitors ingress resources 
2.	Let’s Encrypt DNS01 challenge is generated 
3.	cert-manager creates TXT validation records in Route53 
4.	Let’s Encrypt validates domain ownership 
5.	TLS certificate is automatically issued 
6.	HTTPS traffic is terminated at the NGINX ingress controller 
Kubernetes Resources Configured
•	ClusterIssuer 
•	Certificate 
•	Ingress 
•	Route53 DNS records 
•	Kubernetes TLS secrets 
Security Improvements
•	Encrypted HTTPS traffic 
•	Trusted public certificate authority 
•	Automated certificate lifecycle management 
•	Elimination of self-signed certificates 
HTTPS Endpoint
https://vproappgitops.tcapp.xyz
