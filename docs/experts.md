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

I altered the `docker-compose.yaml` quite a lot from the one in the manual.  
I switched to the Commuity Edition of GitLab, altered the hostname to something I may use, hard-coded the `$GITLAB_HOME` variable (because it wasn't working) and added grafana & prometheus.  
My file:  
```
version: '3.6'
services:
  web:
    image: 'gitlab/gitlab-ce:latest'
    restart: always
    container_name: gitlab
    hostname: 'localhost'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://localhost:8929'
        prometheus_monitoring['enable'] = true
        prometheus['listen_address'] = 'localhost:9090'
        # Add any other gitlab.rb configuration here, each on its own line
    ports:
      - '8929:8929'
      - '9090:9090'
    volumes:
      - '/srv/gitlab/config:/etc/gitlab'
      - '/srv/gitlab/logs:/var/log/gitlab'
      - '/srv/gitlab/data:/var/opt/gitlab'
    shm_size: '1g'
  grafana:
    image: 'grafana/grafana'
    container_name: grafana
    restart: unless-stopped
    ports:
      - '3000:3000'
    volumes:
      - grafana-storage:/var/lib/grafana
volumes:
  grafana-storage: {}
```

## Monitoring Solution
I used Prometheus (which comes preinstalled with GitLab) and Grafana as my monitoring solution.

For Grafana, follow this [guide](<https://docs.gitlab.com/ee/administration/monitoring/performance/grafana_configuration.html>) to set it up.  
It used to come shipped with GitLab just like Prometheus, but was deprecated in 16.0 and removed in 16.3.  
For this reason, I had to add it in as a separate container in the `docker-compose.yml` file.

Once I had my Grafana Container up and running, I imported the Prometheus Metrics by adding a connection to `192.168.1.212:9090` (My Prometheus).  
When it comes to actually adding graphs / dashboards, I found that there are many premade ones here: <https://grafana.com/grafana/dashboards/>  
Just download the JSON and import it into Grafana.

## GitLab Runner Setup
For the GitLab Runner, I made a separate VM for resource management purposes.  
Since nothing else is running on this VM, there is no need to use Docker-Compose.

Just like before, I used this [guide](<https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository>) to install Docker.  
Then I proceeded to create a volume to store persistant data: `docker volume create gitlab-runner-config`

To run the GitLab Runner, use:  
```
docker run -d --name gitlab-runner --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v gitlab-runner-config:/etc/gitlab-runner \
    gitlab/gitlab-runner:alpine
```  
Note that I am using the `alpine` image because it is more lightweight. The other option would be to use the `latest` tag which uses `ubuntu`.

Now we need to [register this Runner](https://docs.gitlab.com/runner/register/index.html?tab=Docker#register-with-a-runner-authentication-token).  
In your GitLab Settings you can add a runner, which will enable you to generate an authentication token.  
I ran this command on my Runner VM (setup in non-interactive mode):  
```
docker run --rm -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner:alpine register \
  --non-interactive \
  --url "192.168.1.212" \
  --token "$RUNNER_TOKEN" \
  --executor "docker" \
  --docker-image alpine:latest \
  --description "docker-runner"
```  
Then create a project with a CI-CD Pipeline and add the runner to the project.
### Why only one Runner?

## GitLab Conifguration
