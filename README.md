# Amazon EKS Cluster Setup on AWS

## 🚀 What is Amazon EKS?

**Amazon Elastic Kubernetes Service (EKS)** is a managed Kubernetes service provided by AWS that makes it easy to deploy, manage, and scale containerized applications using Kubernetes.

With EKS, AWS manages the Kubernetes control plane (Master Nodes), while you manage the worker nodes and applications.

### Benefits of EKS

* Fully managed Kubernetes control plane
* High availability across multiple Availability Zones
* Integrated with AWS IAM for security
* Automatic Kubernetes updates and patching
* Seamless integration with AWS services
* Scalable and production-ready

---

# Prerequisites

Before creating an EKS cluster, you need:

## 1. AWS Account

Create an AWS account if you do not already have one.

## 2. IAM User / Role

Create an IAM User or IAM Role with administrative permissions.

### Required Permissions

For learning purposes, you can attach:

* AdministratorAccess

OR create a custom policy with permissions for:

* EKS
* EC2
* VPC
* CloudFormation
* IAM
* Auto Scaling

### Verify IAM Access

```bash
aws sts get-caller-identity
```

---

# Step 1: Install AWS CLI v2

Download AWS CLI:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

Install unzip package:

```bash
sudo apt update
sudo apt install unzip -y
```

Extract AWS CLI package:

```bash
unzip awscliv2.zip
```

Install AWS CLI:

```bash
sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin --update
```

Verify installation:

```bash
aws --version
```

---

# Step 2: Configure AWS CLI

Configure AWS credentials:

```bash
aws configure
```

Provide:

```text
AWS Access Key ID
AWS Secret Access Key
Default Region Name
Default Output Format
```

Verify:

```bash
aws sts get-caller-identity
```

---

# Step 3: Install kubectl

Download kubectl:

```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
```

Make it executable:

```bash
chmod +x ./kubectl
```

Move to system path:

```bash
sudo mv ./kubectl /usr/local/bin
```

Verify installation:

```bash
kubectl version --short --client
```

---

# Step 4: Install eksctl

Download eksctl:

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
```

Move binary to system path:

```bash
sudo mv /tmp/eksctl /usr/local/bin
```

Verify installation:

```bash
eksctl version
```

---

# Step 5: Create an EKS Cluster

Example:

```bash
eksctl create cluster \
--name demo-cluster \
--region ap-south-1 \
--nodegroup-name workers \
--node-type t3.medium \
--nodes 2
```

This process may take 15–20 minutes.

---

# Step 6: Verify Cluster

Check cluster information:

```bash
kubectl cluster-info
```

View nodes:

```bash
kubectl get nodes
```

View system pods:

```bash
kubectl get pods -A
```

---

# Useful EKS Commands

### List Clusters

```bash
eksctl get cluster
```

### Get Nodes

```bash
kubectl get nodes
```

### Get Pods

```bash
kubectl get pods -A
```

### Get Services

```bash
kubectl get svc -A
```

### Get Namespaces

```bash
kubectl get ns
```

### Delete Cluster

```bash
eksctl delete cluster --name demo-cluster --region ap-south-1
```

---

# Architecture

```text
AWS Account
     │
     ▼
 IAM User / Role
     │
     ▼
 AWS CLI
     │
     ▼
 eksctl
     │
     ▼
 Amazon EKS Cluster
     │
     ├── Control Plane (Managed by AWS)
     │
     └── Worker Nodes (EC2 Instances)
               │
               ▼
             Pods
```

---

# Learning Outcome

After completing this setup, you will be able to:

* Install AWS CLI
* Configure AWS credentials
* Install kubectl
* Install eksctl
* Create an EKS Cluster
* Manage Kubernetes workloads on AWS
* Delete EKS clusters when no longer needed

Happy Kubernetes Learning! 🚀☸️
