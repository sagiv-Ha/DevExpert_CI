# DevExpert CI Pipeline

![CI Pipeline](https://github.com/sagiv-Ha/DevExpert_CI/actions/workflows/ci.yaml/badge.svg)

## Overview

This project demonstrates a complete Continuous Integration (CI) pipeline using GitHub Actions.

The pipeline automatically:

- Builds the project
- Runs automated tests
- Builds a Docker image
- Pushes the image to Docker Hub

The Docker image is tagged using the **Git commit SHA** to ensure traceability and reproducibility.

This repository was created as part of a DevOps CI pipeline assignment.

---

# CI Pipeline Architecture

Developer Push → GitHub Repository → GitHub Actions CI Pipeline  
→ Install Dependencies  
→ Run Tests  
→ Build Docker Image  
→ Push Image to Docker Hub

---

# Project Structure

DevExpert_CI

app.py  
test_app.py  
requirements.txt  
Dockerfile  
README.md  

.github/  
workflows/  
ci.yaml  

---

# Application Description

This project includes a simple **Python Flask application** used to demonstrate a CI pipeline.

The application exposes a basic HTTP endpoint and includes automated tests.

---

# Running the Application Locally

## 1. Clone the repository

git clone https://github.com/sagiv-Ha/DevExpert_CI.git

cd DevExpert_CI

---

## 2. Install dependencies

pip install -r requirements.txt

---

## 3. Run the application

python app.py

---

## 4. Run tests

pytest

---

# Docker Image

The CI pipeline builds and pushes a Docker image to Docker Hub.

Docker image format:

harirs/devexpert_ci:<commit-sha>

Example:

harirs/devexpert_ci:c145cc1cca141f57c102d869f143cf38c7ab9c03

Each image tag corresponds to a unique commit in the repository.

---

# CI Pipeline Workflow

The CI pipeline is implemented using **GitHub Actions**.

Workflow location:

.github/workflows/ci.yaml

Pipeline steps:

1. Checkout repository
2. Setup Python environment
3. Install dependencies
4. Run automated tests
5. Login to Docker Hub
6. Build Docker image
7. Push Docker image to registry

The pipeline runs automatically on every push to the repository.

---

# Secrets Management

Docker Hub credentials are stored securely using **GitHub Secrets**.

Secrets used:

DOCKER_USERNAME  
DOCKER_PASSWORD

These credentials are referenced in the workflow file.

Example:

username: ${{ secrets.DOCKER_USERNAME }}

password: ${{ secrets.DOCKER_PASSWORD }}

GitHub automatically masks secret values in logs.

---

# Best Practices Questions

## 1. Why should kubectl apply not be used in CI?

CI pipelines should focus on building and testing artifacts.

Deployments should not happen inside CI because it mixes responsibilities and reduces deployment control.

Instead:

CI → builds artifacts  
CD → deploys artifacts

This separation improves traceability and system reliability.

---

## 2. Why is "latest" a bad Docker tag?

The "latest" tag is not versioned and can change at any time.

Problems with using latest:

- Difficult debugging
- No reproducibility
- Unclear which version is running

Using commit SHA ensures every image version is unique.

---

## 3. What is the difference between CI and CD?

CI (Continuous Integration)

- Automatically builds and tests code changes
- Ensures new code does not break the system

CD (Continuous Delivery / Deployment)

- Automatically releases or deploys the application after CI succeeds

CI validates code.  
CD delivers code to environments.

---

## 4. How does this pipeline support GitOps?

GitOps uses Git as the single source of truth for infrastructure and deployments.

This pipeline supports GitOps because:

- Every Docker image is tagged with the Git commit SHA
- Deployments can reference exact image versions
- Git history provides traceability

This ensures deterministic and reproducible deployments.

---

# Summary

This project demonstrates a modern CI pipeline that:

- Automates testing
- Builds container images
- Publishes artifacts to a container registry
- Uses secure secret management
- Follows DevOps best practices