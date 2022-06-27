# DevOps CICD pipeline with GitOps, docker, helm, argocd, kubernetes
## Install kubectl:
3 nodes(servers) with Ubuntu 18.04 Bionic Beaver LTS.

One server being “Kube Master” and remaining 2 servers as “Kube Node 1” and “Kube Node 2”.

The first step in setting up a new cluster is to install a container runtime such as Docker.

We will be installing Docker on our three servers in preparation for standing up a Kubernetes cluster.

**Commands:**

```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -sudo add-apt-repository \”deb [arch=amd64] https://download.docker.com/linux/ubuntu \$(lsb_release -cs) \stable”

sudo apt-get update

sudo apt-get install -y docker-ce=18.06.1~ce~3–0~ubuntu

sudo apt-mark hold docker-ce

sudo docker version

```
