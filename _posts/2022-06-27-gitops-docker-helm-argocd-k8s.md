# DevOps CICD pipeline with GitOps, docker, helm, argocd, kubernetes

![alt text](https://github.com/imsandeepreddy/imsandeepreddy.github.io/blob/main/_images/CICD.png?raw=true)

## Prerequisites:
### Install Docker:

**Commands:**

```sh
sudo apt-get remove docker docker-engine docker.io containerd runc

sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

sudo usermod -aG docker $USER && newgrp docker
```

### Install kubectl:

**Commands:**

```sh
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

kubectl version --client --output=yaml
```
### Install minikube and initialize cluster:

**Commands:**

***Note: tunnel command is to access the load balancer external IP through host. 
This command should be kept running. Run remaining commands in other terminal***

```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start
minikube tunnel
```
**Commands for info purpose:**

```sh
kubectl get po -A
minikube stop
minikube delete --all
```
### Install Helm:

**Commands**

```sh
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```
### Install ArgoCD inside minikube cluster:

**Commands**

```sh
helm repo add argo https://argoproj.github.io/argo-helm
helm install argocd argo/argo-cd --set server.service.type=LoadBalancer
```
**Commands to access ArgoCD UI**

```sh
kubectl port-forward service/argocd-server -n default 8080:443
kubectl -n default get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
## Instructions to add repository in ArgoCD:
1. Settings > Create repo using HTTPS
2. Provide details as:
    a. Type = git
    b. project = default
    c. Repository URL = 
    d. Username
    e. Password = Personal Authentication Token
3. Click Connect
4. Application > New App
5. Provide details as:
    a. Application name
    b. project = default
    c. Sync Policy = Automatic
    d. Prune Resources checked
    e. Auto-Create Namespace checked
    f. Apply out of sycn only checked
    g. Repository URL
    h. Revision = HEAD
    i. Path = path to helm chart
    j. Destination = default value
    k. Namespace
6. Click Create
7. Verify that app health is "Healthy".

## Access app deployed on minikube cluster:

1. Run below command:
```sh
$ kubectl get svc
```
2. Open browser and access
http://REPLACE_WITH_EXTERNAL_IP

## Reference material:

https://medium.com/geekculture/gitops-with-argo-cd-managing-kubernetes-application-using-git-and-argo-cd-42ed6879ab1e

https://levelup.gitconnected.com/gitops-ci-cd-using-github-actions-and-argocd-on-kubernetes-909d85d37746
