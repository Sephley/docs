# Traefik
How our [Traefik](https://doc.traefik.io/traefik/) Proxy is set up.

Like pretty much everything in ClusterStack at this point, Traefik runs in a Docker container.
The Dashboard is only reachable from our internal network (so via VPN or GUI VM).

## Dependencies

> APT-Packages required on the OS (Ubuntu 24.04)
{.is-info}

|Name |Version |
|-|-|
|`docker-ce`| - |
|`docker-ce-cli`| - |
|`containerd.io`| - |
|`docker-buildx-plugin`| - |
|`docker-compose-plugin`| - |

Follow the [official installation guide of docker](https://docs.docker.com/engine/install/ubuntu/)

[I also recommend running docker in a rootless environment](https://docs.docker.com/engine/install/linux-postinstall/)
## Build
>This is just a basic example! The active `docker-compose.yml` file [can be found here!](https://github.com/ClusterStack-Project/docker)
{.is-warning}

`/home/stack/traefik/docker-compose.yml`
```
version: '3'

services:
  reverse-proxy:
    # The official v3 Traefik docker image
    image: traefik:v3.0
    # Enables the web UI and tells Traefik to listen to docker
    command: --api.insecure=true --providers.docker
    ports:
      # The HTTP port
      - "80:80"
      # The Web UI (enabled by --api.insecure=true)
      - "8080:8080"
    volumes:
      # So that Traefik can listen to the Docker events
      - /var/run/docker.sock:/var/run/docker.sock
	whoami:
    # A container that exposes an API to show its IP address
    image: traefik/whoami
    labels:
      - "traefik.http.routers.whoami.rule=Host(`whoami.docker.localhost`)"
```

## Config
`/home/stack/traefik/traefik.yml`
```
providers:
  docker:
    tls:
      cert: ./certs/cert.pem
      key: ./certs/key.pem
```
<https://doc.traefik.io/traefik/routing/routers/#tls>  
<https://doc.traefik.io/traefik/providers/docker/#tls>

## TLS in Traefik
<https://doc.traefik.io/traefik/https/tls/>