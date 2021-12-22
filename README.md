# Learn Terraform - Provision an EKS Cluster

This repo is a companion repo to the [Provision an EKS Cluster learn guide](https://learn.hashicorp.com/terraform/kubernetes/provision-eks-cluster), containing
Terraform configuration files to provision an EKS cluster on AWS.

 1. `brew install awscli`
 2. `aws configure`
 3. `git clone https://github.com/hashicorp/learn-terraform-provision-eks-cluster`
 4. `cd learn-terraform-provision-eks-cluster`
 5. `terraform init`
 6. `terraform apply`
 7. `aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)`

## Deploy and access Kubernetes Dashboard

1. `»Deploy and access Kubernetes `
2. `kubectl apply -f metrics-server-0.3.6/deploy/1.8+/`
3. `kubectl proxy`
4. 
