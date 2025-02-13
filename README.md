# Voting App Deployment with Azure DevOps and GitOps

## Overview
This project demonstrates how to establish a CI/CD workflow using Azure DevOps with a GitOps approach, leveraging ArgoCD to automate deployments. The application deployed is the **dockersamples/example-voting-app**, developed by the Docker community.

## Application Components
The application consists of multiple microservices written in different languages:
- **Vote (Python)** – A frontend web app for voting between two options.
- **Redis** – Collects new votes.
- **Worker (.NET)** – Consumes votes and stores them in the database.
- **PostgreSQL** – Stores the votes, backed by a Docker volume.
- **Result (Node.js)** – A web app that displays real-time voting results.

This project provided a great opportunity to explore Dockerfile creation for different languages and services.

## Project Workflow
### 1. Setup Azure DevOps
- Created an **Azure DevOps Organization**.
- Created a **project** within the organization.
- Added the application code to an **Azure Repos repository**.

### 2. CI Pipeline Configuration
- Built **three CI pipelines** (for `vote`, `result`, and `worker`).
- Created a **self-hosted VM runner** for executing the pipelines.

### 3. Kubernetes and ArgoCD Setup
- Provisioned an **Azure Kubernetes Service (AKS) cluster**.
- Installed **ArgoCD** to manage Kubernetes deployments.
- Configured ArgoCD to watch the repository for changes and apply the latest **Kubernetes Deployment and Service** manifests.

## Key Technologies Used
- **Azure DevOps** – For managing repositories, pipelines, and deployments.
- **Docker** – For containerizing microservices.
- **Kubernetes (AKS)** – For orchestrating the application deployment.
- **ArgoCD** – For implementing GitOps and automating Kubernetes deployments.
- **Redis, PostgreSQL** – Backend data storage.
- **CI/CD Pipelines** – Automating build and deployment processes.

## Conclusion
By integrating Azure DevOps with GitOps using ArgoCD, this project successfully established a fully automated CI/CD workflow. The deployment process ensures that any changes pushed to the repository are automatically detected and deployed to the Kubernetes cluster, enhancing efficiency and reliability.

