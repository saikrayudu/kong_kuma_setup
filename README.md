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
* kuma


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

#### kuma installation using helm charts
 The following are the commands to install  **kuma** for kubernetes
```
$ helm repo add kuma https://kumahq.github.io/charts
$ helm install --create-namespace --namespace kuma-system kuma kuma/kuma

```

Kuma ships with a read-only GUI that you can use to retrieve Kuma resources. By default the GUI listens on the API port and defaults to :5681/gui.

To access Kuma we need to first port-forward the API service with:

```
$ kubectl port-forward svc/kuma-control-plane -n kuma-system 5681:5681

```
####  Explore Kuma with the Kubernetes demo app

To start learning how Kuma works, you can download and run a simple demo application that consists of two services:

demo-app: web application that lets you increment a numeric counter
redis: data store for the counter

### pre-requisites

* Kuma installed on your Kubernetes cluster
* Demo app downloaded from GitHub (https://github.com/kumahq/kuma-counter-demo)

Two different YAML files are available:

demo.yaml installs the basic resources
demo-v2.yaml installs the frontend service with different colors. This lets you more clearly view routing across multiple versions, for example.
gateway.yaml installs a builtin gateway

Install resources in a kuma-demo namespace:
```
$ kubectl apply -f demo.yaml

```
Port forward the service to the namespace on port 5000:
```
$ kubectl port-forward svc/demo-app -n kuma-demo 5000:5000

```

####  Explore the mesh

The demo app includes the kuma.io/sidecar-injection label enabled on the kuma-demo namespace. This means that Kuma already knows that it needs to automatically inject a sidecar proxy to every Kubernetes deployment in the default Mesh resource:

```
apiVersion: v1
kind: Namespace
metadata:
  name: kuma-demo
  namespace: kuma-demo
  labels:
    kuma.io/sidecar-injection: enabled

```
Run:

```
kubectl get namespace kuma-demo -oyaml

```
