# PXE Boot

# My GitLab Setup
The purpose of this assignment is to set up a GitLab Server as if it were for a large-scale company.

My GitLab Server was setup in a personal PVE (Proxmox Virtual Environment) as a VM using Docker-Compose.

## Installation Procedure
### Setup an Ubuntu Server and install Docker & Docker-Compose
Follow this [guide](<https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository>) (official Docker installation guide)

and this [guide](<https://docs.docker.com/compose/install/linux/#install-using-the-repository>) (official Docker-Compose installation guide)  
Note that after follwing the first guide Docker-Compose may already be installed.

### Setup GitLab using Docker-Compose
Follow this [guide](<https://docs.gitlab.com/ee/install/docker.html#install-gitlab-using-docker-compose>)

I altered the `docker-compose.yaml` a little from the one in the manual.  
Basically, I switched to the Commuity Edition of GitLab and altered the hostname to something I may use.  
My file:  
```
version: '3.6'
services:
  web:
    image: 'gitlab/gitlab-ce:latest'
    restart: always
    hostname: 'git.clusterstack.net'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'https://git.clusterstack.net'
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - '80:80'
      - '433:433'
      - '22:22'
    volumes:
      - '$GITLAB_HOME/config:/etc/gitlab'
      - '$GITLAB_HOME/logs:/var/log/gitlab'
      - '$GITLAB_HOME/data:/var/opt/gitlab'
    shm_size: '256m'
```

## Monitoring Solution

## GitLab Conifguration