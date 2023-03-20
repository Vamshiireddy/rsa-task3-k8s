# Solution

## Create AKS cluster using terraform

```bash
# Login into az account using cli
$ az login
# Get appid and password
$ az ad sp create-for-rbac --skip-assignment
# Update variables.tf file in terraform folder with appid and password.
# Run terraform
$ terraform init
$ terraform apply --auto-approve
# update kubeconfig
$ az aks get-credentials --resource-group $(terraform output -raw resource_group_name) --name $(terraform output -raw kubernetes_cluster_name)
```

## Deploy 3 tier application using k8s in AKS

```bash
$ cd k8s-manifests
$ kubectl apply -f deploy-data.yaml
$ kubectl apply -f deploy-server.yaml
# Get loadbalancer IP of backend 
$ kubectl get svc
# Update backend loadbalancer IP in deploy-app.yaml REACT_APP_API_BASE_URL value
$ kubectl apply -f deploy-app.yaml
# Get loadbalancer IP of frontend
$ kubectl get svc
# Access the IP from browser and view the application
```
