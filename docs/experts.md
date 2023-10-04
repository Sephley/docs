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

It is recommended to export the `$GITLAB_HOME` variable like this: `export GITLAB_HOME=/srv/gitlab`  
and then adding this to `.bashrc` so you don't have to do it every time.  
However, this didn't work for me, so I ended up hard-coding them in the `docker-compose.yaml` file.

I altered the `docker-compose.yaml` a little from the one in the manual.  
Basically, I switched to the Commuity Edition of GitLab, altered the hostname to something I may use and hard-coded the `$GITLAB_HOME` variable.  
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
      - '/srv/gitlab/config:/etc/gitlab'
      - '/srv/gitlab/logs:/var/log/gitlab'
      - '/srv/gitlab/data:/var/opt/gitlab'
    shm_size: '256m'
```

## Monitoring Solution
I used Prometheus (which comes preinstalled with GitLab) and Grafana as my monitoring solution.

For Grafana, follow this [guide](<https://docs.gitlab.com/ee/administration/monitoring/performance/grafana_configuration.html>)
It used to come shipped with GitLab just like Prometheus, but was deprecated in 16.0 and removed in 16.3.
## GitLab Conifguration
