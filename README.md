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
### Create a Docker-compose file
```
$ vim docker-compose.yaml
```
