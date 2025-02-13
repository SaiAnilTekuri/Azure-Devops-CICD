# Voting App Deployment with Azure DevOps and GitOps

## Overview
This project demonstrates how to establish a CI/CD workflow using Azure DevOps with a GitOps approach, leveraging ArgoCD to automate deployments. The application deployed is the **dockersamples/example-voting-app**, developed by the Docker community.

**Repo:** https://github.com/dockersamples/example-voting-app/tree/main

## Application Components
The application consists of multiple microservices written in different languages:
- **Vote (Python)** – A frontend web app for voting between two options.
- **Redis** – Collects new votes.
- **Worker (.NET)** – Consumes votes and stores them in the database.
- **PostgreSQL** – Stores the votes, backed by a Docker volume.
- **Result (Node.js)** – A web app that displays real-time voting results.

This project provided a great opportunity to explore Dockerfile creation for different languages and services and to work with Azure DevOps services.

## Project Workflow
### 1. Setup Azure DevOps
- Created an **Azure DevOps Organization**.
- Created a **project** within the organization.
- Added the application code to an **Azure Repos repository**.

<img width="959" alt="Screenshot 2025-02-12 210744" src="https://github.com/user-attachments/assets/eb0c0fcf-452a-4950-8e58-faaf3b5329d6" />


### 2. CI Pipeline Configuration
- Built **three CI pipelines** (for `vote`, `result`, and `worker`).
- Created a **self-hosted VM runner** for executing the pipelines.

<img width="959" alt="Screenshot 2025-02-12 210702" src="https://github.com/user-attachments/assets/df992155-6e05-4d43-ac12-5c1921307ccd" />


### 3. Kubernetes and ArgoCD Setup
- Created a secret within the namespace for pulling the Docker images, as the images are stored in ACR inside a private repository.
```sh
kubectl create secret docker-registry <secret-name> \
    --namespace <namespace> \
    --docker-server=<container-registry-name>.azurecr.io \
    --docker-username=<service-principal-ID> \
    --docker-password=<service-principal-password>
```
- Provisioned an **Azure Kubernetes Service (AKS) cluster**.
- Installed **ArgoCD** to manage Kubernetes deployments.
- Configured ArgoCD to watch the repository for changes and apply the latest **Kubernetes Deployment and Service** manifests.

<img width="960" alt="Screenshot 2025-02-12 211108" src="https://github.com/user-attachments/assets/d6f6435c-f1e4-4d63-944e-8007adec2dd1" />

<img width="960" alt="Screenshot 2025-02-12 210901" src="https://github.com/user-attachments/assets/22a7fd1e-32a3-447a-b2ed-1c07de9fef81" />



## Key Technologies Used
- **Azure DevOps** – For managing repositories, pipelines, and deployments.
- **Docker** – For containerizing microservices.
- **Kubernetes (AKS)** – For orchestrating the application deployment.
- **ArgoCD** – For implementing GitOps and automating Kubernetes deployments.
- **Redis, PostgreSQL** – Backend data storage.
- **CI/CD Pipelines** – Automating build and deployment processes.

## Conclusion
By integrating Azure DevOps with GitOps using ArgoCD, this project successfully established a fully automated CI/CD workflow. The deployment process ensures that any changes pushed to the repository are automatically detected and deployed to the Kubernetes cluster, enhancing efficiency and reliability.

