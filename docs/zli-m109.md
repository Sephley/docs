# ZLI Module 109
"Dienste in der Public Cloud betreiben und überwachen"
*Course:* <https://moodle.zli.ch/course/view.php?id=1610>
## Day 1

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
### Auftrag 4.2: Intallation minikube

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