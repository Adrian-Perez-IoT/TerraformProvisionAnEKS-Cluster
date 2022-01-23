# Learn Terraform - Provision an EKS Cluster

This repo is a companion repo to the [Provision an EKS Cluster learn guide](https://learn.hashicorp.com/terraform/kubernetes/provision-eks-cluster), containing
Terraform configuration files to provision an EKS cluster on AWS.

 1. `brew install awscli` //Install the package AWS CLI
 2. `aws configure` // Enter your AWS Access Key ID, Secret Access Key, region and output format (JSON)
 3. `git clone https://github.com/hashicorp/learn-terraform-provision-eks-cluster` // It contains the example configuration used in this tutorial.
 4. `cd learn-terraform-provision-eks-cluster`
 5. `terraform init` // Omotoañoze Terrafpr, wprlsáce
 6. `terraform apply` // Provision the EKS cluster
 7. `aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)` //Configure Kubectl


## Deploy and access Kubernetes Dashboard

### Deploy Kubernetes Metrics Server

1. `wget -O v0.3.6.tar.gz https://codeload.github.com/kubernetes-sigs/metrics-server/tar.gz/v0.3.6 && tar -xzf v0.3.6.tar.gz` // Dowload and unzip the metrics server
2. `kubectl apply -f metrics-server-0.3.6/deploy/1.8+/` // Deploy the metrics server to the cluster
3. `kubectl get deployment metrics-server -n kube-system` // Verify that the metrics server has been deployed
4. `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml` // Will schedule the resources necessary for the dashboard.
5. `kubectl proxy` // Create a proxy server that will allow you to navigate to the dashboard from the browser on your local machine.
6. `kubectl apply -f https://raw.githubusercontent.com/hashicorp/learn-terraform-provision-eks-cluster/main/kubernetes-dashboard-admin.rbac.yaml` // In another terminal (do not close the kubectl proxy process), create the ClusterRoleBinding resource.
5. `kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep service-controller-token | awk '{print $1}')` // Then, generate the authorization token.
6. `terraform destroy` // Clean up your workspace
