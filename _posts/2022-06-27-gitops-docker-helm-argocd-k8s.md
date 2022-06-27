# DevOps CICD pipeline with GitOps, docker, helm, argocd, kubernetes
## Install Docker:

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

## Install kubectl:

**Commands:**

```sh
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

kubectl version --client --output=yaml
```
## Install minikube and initialize cluster:

**Commands:**

```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo install minikube-linux-amd64 /usr/local/bin/minikube

minikube start

kubectl get po -A
```

**Commands for info purpose:**

```sh
minikube stop

minikube delete -all
```
https://medium.com/geekculture/gitops-with-argo-cd-managing-kubernetes-application-using-git-and-argo-cd-42ed6879ab1e
```sh
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl get all -n argocd

kubectl port-forward svc/argocd-server -n argocd 8080:443


```
