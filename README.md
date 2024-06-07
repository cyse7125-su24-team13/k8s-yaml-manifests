# Kubernetes Deployment Repository

This repository contains Kubernetes manifests and configuration files for deploying applications using Kubernetes.

## Table of Contents

- [Kubernetes Deployment Repository](#kubernetes-deployment-repository)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Getting Started](#getting-started)

## Prerequisites

Before you begin, ensure you have the following tools installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Kubernetes Cluster](https://kubernetes.io/docs/setup/) (Minikube, kind, or a cloud provider)
- [Jenkins](https://www.jenkins.io/) (for CI/CD pipeline)
- [yamllint](https://github.com/adrienverge/yamllint) (for linting YAML files)

## Getting Started

1. **Clone the repository:**

   ```bash
   git clone https://github.com/cyse7125-su24-team13/k8s-yaml-manifests.git
   
2. **Commands to Run Kubernetes:**
   Ask the owner for dockerconfigjson and secret.yml to build
   ```bash
   kubectl apply -f secret.yml
   kubectl apply -f server.yml
   kubectl apply -f caddy-service.yml
   kubectl get pods
   kubectl get services
   kubectl port-forward caddy-pod 8080:8080
   kubectl describe pod caddy-pod 
