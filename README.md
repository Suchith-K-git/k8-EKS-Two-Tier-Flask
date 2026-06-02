# What is Amazon EKS?

Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service provided by AWS that allows you to run Kubernetes clusters without managing the Kubernetes control plane.

## AWS Credentials Requirement

Before creating an EKS cluster, create an IAM User with the required permissions. Generate an Access Key and Secret Access Key, then configure AWS credentials using:

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

---

# Install AWS CLI v2

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin --update
```

---

# Install kubectl

```bash
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --short --client
```

---

# Install eksctl

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

---

# Create EKS Cluster

```bash
eksctl create cluster --name three-tier-cluster --region us-west-2 --node-type t2.medium --nodes-min 2 --nodes-max 2
```

---

# Verify Cluster

```bash
kubectl get nodes
kubectl get pods -A
```

---

# Delete EKS Cluster

```bash
eksctl delete cluster --name three-tier-cluster --region us-west-2
```

This command deletes:

* EKS Control Plane
* Worker Nodes
* Node Groups
* Auto Scaling Groups
* Security Groups created by EKS
* Kubernetes Resources
* AWS Load Balancers associated with the cluster

---

# Verify Cluster Deletion

```bash
aws eks list-clusters
```
