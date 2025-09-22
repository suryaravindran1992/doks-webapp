# DOKS Web Application Deployment

## Overview
This repository contains Kubernetes manifests and configuration files for deploying a scalable web application on DigitalOcean Kubernetes Service (DOKS).

    

## Prerequisites
- Docker Hub account
- Digital Ocean account
- kubectl installed
- doctl (DigitalOcean CLI)

## Quick Start


1. Clone the repository:

    git clone https://github.com/suryaravindran1992/doks-webapp.git
    cd doks-webapp

    

2. Build and push Docker image:

    docker build -t <your-dockerhub-username>/do-web-app:latest .
    docker push <your-dockerhub-username>/do-web-app:latest

    

3. Create DOKS cluster:
 

    doctl kubernetes cluster create my-k8s-cluster --region blr1 --version 1.33.1-do.3 --count 2 --size s-2vcpu-2gb --enable-autoscaling --min-nodes 2 --max-nodes 3

    
4. Connect to the cluster

After cluster creation,

    doctl kubernetes cluster kubeconfig save web-app-cluster
    kubectl get nodes # Verify connection

    
5. Deploy the application:

    
    kubectl apply -f deployment.yaml
    kubectl apply -f service.yaml
    kubectl apply -f hpa.yaml

    

Features

- Automated scaling based on CPU utilization (70% threshold)
- Load balancing across pods
- Resource limits and requests configured
- Node auto-scaling enabled


Monitoring

    
    Check deployment status
    - kubectl get deployments

    Monitor pods
    - kubectl get pods

    Check HPA status
    - kubectl get hpa

    View service details
    - kubectl get services

    

6. Cleanup (Optional)

    
    kubectl delete -f service.yaml
    kubectl delete -f deployment.yaml
    kubectl delete -f hpa.yaml
    doctl kubernetes cluster delete my-k8s-cluster

    

## Architecture
[View Architecture Diagram](DOKS_architecture.pdf)
