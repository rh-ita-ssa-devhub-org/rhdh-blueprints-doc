# Blueprints Overview

RHDH Blueprints are software templates that automate project creation and configuration.

## What is a Blueprint?

A blueprint is a reusable template that defines:

- **Project structure**: Files, directories, and configurations
- **Parameters**: User inputs to customize the output
- **Actions**: Steps to execute during scaffolding
- **Outputs**: Links and resources created

## Available Blueprints

### Application Blueprints

| Blueprint | Description | Language/Framework |
|-----------|-------------|-------------------|
| Spring Boot Service | REST API with Spring Boot | Java |
| Quarkus Application | Cloud-native Quarkus app | Java |
| Node.js Service | Express.js microservice | Node.js |
| Python FastAPI | FastAPI application | Python |

### Infrastructure Blueprints

| Blueprint | Description | Technology |
|-----------|-------------|------------|
| Kubernetes Deployment | K8s manifests and Helm charts | Kubernetes |
| ArgoCD Application | GitOps deployment setup | ArgoCD |
| Tekton Pipeline | CI/CD pipeline definition | Tekton |

## Blueprint Categories

!!! info "Categories"
    Blueprints are organized into categories for easier discovery:
    
    - **Backend Services**: APIs, microservices, batch jobs
    - **Frontend Applications**: Web apps, SPAs, mobile backends
    - **Infrastructure**: Deployments, pipelines, configurations
    - **Documentation**: Tech docs, ADRs, runbooks

## Choosing a Blueprint

Consider these factors when selecting a blueprint:

1. **Technology stack**: Match your team's expertise
2. **Requirements**: Align with project needs
3. **Integrations**: Consider existing tooling
4. **Maintenance**: Evaluate long-term support


