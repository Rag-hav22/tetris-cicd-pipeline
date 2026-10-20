# tetris-cicd-pipeline
Automated CI/CD pipeline deploying a containerized Tetris web application to a Minikube Kubernetes cluster on AWS using Jenkins, Docker, and Docker Hub.
# Tetris CI/CD Pipeline & Kubernetes Deployment

## Project Overview
This repository contains a web-based Tetris application along with an automated Continuous Integration and Continuous Deployment (CI/CD) pipeline[cite: 1]. The goal of this project is to demonstrate end-to-end automation—from code commit on GitHub to automated building, containerization, registry publishing, and orchestration on a Kubernetes cluster running on an AWS EC2 instance[cite: 1, 2].

## Tools & Technologies Used
* **Version Control:** GitHub (source code, Dockerfile, Jenkinsfile, and Kubernetes manifests)[cite: 1, 3]
* **Cloud Infrastructure:** AWS EC2 (Ubuntu server hosting Jenkins, Docker, and Minikube)[cite: 1]
* **CI/CD Automation:** Jenkins (Declarative Pipeline)[cite: 1, 2]
* **Containerization:** Docker & Docker Hub (container registry)[cite: 1]
* **Orchestration:** Minikube & `kubectl` (local Kubernetes cluster running Pods and NodePort Services)[cite: 1]

## Repository Structure
```text
.
├── index.html            # Application source code
├── Dockerfile            # Container blueprint (Nginx web server)
├── Jenkinsfile           # Automated CI/CD pipeline definition
└── k8s/
    ├── deployment.yaml   # Kubernetes Deployment manifest
    └── service.yaml      # Kubernetes NodePort Service manifest
```[cite: 3]

## Pipeline Stages
The Jenkins pipeline automatically triggers on code updates and executes the following stages sequentially[cite: 1, 2]:

1. **Checkout Code:** Pulls the latest application source and configuration files from the GitHub repository[cite: 1, 2].
2. **Build & Test:** Verifies the presence and integrity of application source files and dependencies[cite: 1, 2].
3. **Docker Build:** Packages the application into a lightweight Docker image using the `Dockerfile`[cite: 1, 2].
4. **Push Image:** Authenticates with Docker Hub and publishes the newly built image tagged with the build ID and `latest`[cite: 1, 2].
5. **Minikube Deployment:** Applies the Kubernetes `Deployment` and `Service` manifests via `kubectl`, forcing a rolling update to launch the newly pushed image version on the Minikube cluster[cite: 1, 2].
6. **Verification:** Validates running Pods, deployments, and services, serving the application on NodePort `30007`[cite: 2].

## Demonstrating Automated Redeployment
To verify continuous deployment, updating the application code (e.g., updating version header in `index.html`) and pushing to GitHub automatically triggers the Jenkins pipeline to build, push, and redeploy the updated container version without manual intervention[cite: 1, 2].
