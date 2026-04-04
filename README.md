# AuraScale Infrastructure Core 🚀

A production-grade, automated EKS (Elastic Kubernetes Service) environment built with **AWS CloudFormation** and **GitHub Actions**. This repository manages the foundational "Platform Layer" for AuraScale.

## 🏗️ Architecture Overview

The infrastructure follows a strictly decoupled, layered approach to ensure high availability and security.

```mermaid
graph TD
    subgraph GitHub [CI/CD]
        A[main-pipeline.yml]
    end

    subgraph AWS_Cloud [AWS eu-west-1]
        subgraph Networking
            B[vpc.yaml]
        end

        subgraph IAM_Identity
            C[eks-roles.yaml]
            D[alb-role-stack.yaml]
            E[eks-access.yaml]
        end

        subgraph Compute
            F[eks-cluster.yaml]
            G[eks-nodes.yaml]
        end

        subgraph K8s_Config
            H[ArgoCD / argo-app.yaml]
            I[alb-service-account.yaml]
        end

        A --> B
        B --> C
        C --> F
        F --> G
        G --> H
    end

📂 Project StructureFolderDescriptionKey Files.github/CI/CD Automationmain-pipeline.ymlnetworking/Core Network Layervpc.yaml (Public/Private Subnets, NATGW)iam/Identity & Accesseks-roles.yaml, eks-access.yaml (Access Entries)clusters/Kubernetes Engineeks-cluster.yaml (v1.31), eks-nodes.yamlk8s-config/Cluster Runtimeargo-app.yaml, alb-service-account.yaml
