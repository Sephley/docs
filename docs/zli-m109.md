# ZLI Module 109
"Dienste in der Public Cloud betreiben und überwachen"
*Course:* <https://moodle.zli.ch/course/view.php?id=1610>

### Auftrag 1.1: Einfache HTML Seite erstellen und mit FTP «deployen»

### Auftrag 2.2: Git zur Sourcecode- und Konfigurationsverwaltung
<https://moodle.zli.ch/mod/h5pactivity/view.php?id=116428>  
<https://github.com/Sephley/Zli-m109>




Configure git username & email
```
git config --global user.name "user"

git config --global user.email "mail@mail.com"
```

### Auftrag 2.3: GitHub Einführung
<https://github.com/Sephley/Zli-m109>

### Auftrag 3.2:
```
sudo apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```
### Intallation minikube
Minikube can create a cluster containing only one node.

```
sudo apt install curl wget apt-transport-https -y  
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64  
sudo cp minikube-linux-amd64 /usr/local/bin/minikube  
sudo chmod +x /usr/local/bin/minikube  
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl  
sudo mv kubectl /usr/local/bin/  
chmod +x kubectl  
minikube start --driver=docker  
minikube addons enable ingress  
minikube addons enable dashboard  
minikube addons enable metrics-server  
sudo reboot  
```

### Auftrag 4.2: Container Orchestration mit Docker Compose

see <https://docs.docker.com/compose/gettingstarted/> for how to set up a generic docker-compose application

see <https://github.com/Sephley/m109-site> for all the files

Docker-compose requires a docker-compose.yml file that can set up multiple Containers.  
Using ```docker compose up``` you start the containers

## Kubernetes
### Pod 
The Pod is the smallest unit in Kubernetes, usually only runs 1 Application.  
Each Pod gets its own IP address, not the container. They are rather ephemeral, which means they are prone to crash.

#### Service 
is used to attach an IP address to a pod, so that if it dies, the new one just uses the service to retain the IP address.  
It is possible to specify, whether the service is internal or external.

#### Ingress
Forwards IP-address of pod to domain name of application.

#### ConfigMap
Is the external Configuration of your application. Is only for non-confidential data! Unless you use secret to encrypt it.

### Volumes / Storage
Attaches a physical storage to a Pod, can be locally connected or also via Cloud.  
Think of it as an external drive plugged in to the kubernetes cluster.

### Deployment
A deployment is a template for creating pods.

### Kubernetes Configuration
deployments get sent to the API server.  
Each config file (written in yml) has 3 parts. The metadata, the specification and the third part defines the type of configuration (like service or deployment).  
Kubernetes always compares the desired state with the actual state and then does anything it can to reach the desired state if that is not the case.

### Minikube - Kubernetes ganz einfach