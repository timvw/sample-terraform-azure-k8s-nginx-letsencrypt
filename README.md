# Quickly setup a kubernetes cluster on azure

## Configure the service principal

https://www.terraform.io/docs/providers/azurerm/guides/service_principal_client_secret.html

```bash
export ARM_CLIENT_ID="XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
export ARM_CLIENT_SECRET="XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
export ARM_SUBSCRIPTION_ID="XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
export ARM_TENANT_ID="XXXXX-XXXXX-XXXXX-XXXXX-XXXXX"
```

## Configure terraform environment variables (variables.tf)

```bash
export TF_VAR_client_id=$ARM_CLIENT_ID
export TF_VAR_client_secret=$ARM_CLIENT_SECRET
export TF_VAR_aks_service_principal_app_id=$ARM_CLIENT_ID
export TF_VAR_aks_service_principal_client_secret=$ARM_CLIENT_SECRET
```

## Build the cloud infrastructure

```bash
terraform init
terraform apply -auto-approve
```




az aks get-credentials --resource-group k8s-test --name kaz

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.28.0/deploy/static/mandatory.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.28.0/deploy/static/provider/cloud-generic.yaml
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.13.0/cert-manager.yaml

kubectl create deployment hello-node --image=gcr.io/hello-minikube-zero-install/hello-node
kubectl expose deployment hello-node --port=8080
kubectl apply -f ingress.yml
```

Resources: 
- https://kubernetes.io/docs/tutorials/hello-minikube/
- https://kubernetes.github.io/ingress-nginx/deploy/

```bash
kubectl proxy

curl http://localhost:8001/api/v1/namespaces/kube-system/services/http:kubernetes-dashboard:/proxy


kubectl logs -n ingress-nginx deployment/nginx-ingress-controller -f

kubectl scale deployment -n ingress-nginx --replicas=0 nginx-ingress-controller
kubectl scale deployment -n ingress-nginx --replicas=1 nginx-ingress-controller

```





