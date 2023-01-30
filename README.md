# kong_kuma_setup_with two demo app's

## Getting Started

### pre-requisites

* Ubuntu-OS
* Docker
* Docker-Compose
* (Enterprise only) A license.json file from Kong
* Helm3
* Kubernetes Cluster (K3's)
* Kong Ingress Controller


### Installation

 #### Docker installation
 The following are the commands to install & Execute the  **Docker** and  **Docker-compose**:

```
$ sudo apt-get update
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

$ sudo apt-get update

$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

$ sudo groupadd docker

$ sudo usermod -aG docker $USER

$ sudo apt install docker-compose

```
 #### Here we are using the K3's cluster
 The following are the commands to install **K3's cluster**
```
$ curl -sfL https://get.k3s.io | sh -
$ export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
$ sudo chmod 644 $KUBECONFIG

```

#### Helm  installation
 The following are the commands to install  **Helm** 
```
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh

```

#### kong  installation using helm charts
 The following are the commands to install  **kong** for kubernetes
```
$ helm repo add kong https://charts.konghq.com
$ helm repo update


# Helm 3
$ helm install kong/kong --generate-name --set ingressController.installCRDs=false -n kong --create-namespace

```
