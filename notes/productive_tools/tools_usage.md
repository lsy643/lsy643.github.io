---
layout: page
mathjax: true
permalink: /notes/productive_tools/tools_usage/
---

Usage of Common Tools
- [Anaconda](#Anaconda)
- [Docker](#Docker)
- [Gitlab](#Gitlab)

## Anaconda

[Anaconda](https://www.continuum.io/) is a Python package management tool.

Common commands:
1. List current environments: `conda info --envs`
1. Create an environment: `conda create --name {env_name} python={python_version}`
1. Clone an environment: `conda create --name {tgt_env_name} --clone {org_env_name}`
1. Remove an environment: `conda remove --name {env_name}`
1. Change an environment: `source activate/deactivate {env_name}`

## Docker


*Portus* maybe deserve consideration for registry UI

#### Common Commands:

1. Pull from local Registry: `docker pull {registry ip}:{registry port}/*`
2. Run with specific GPU: `NV_GPU={i} nvidia-docker run`

#### Private Registry

##### Create Registry
- serving registry
```
docker run -d -p {out port}:5000 --restart=always \
--name {container name} \
-v {path to store images}:/var/lib/registry \
registry:2
```

##### Web UI
```
docker run \
-d \
-e ENV_DOCKER_REGISTRY_HOST={registry ip} \
-e ENV_DOCKER_REGISTRY_PORT={registry port} \
-p 5080:80 \
konradkleine/docker-registry-frontend:v2
```


##### Push and Pull image

take `192.168.116.9:5000` as an example

- push image
1. tag image: `docker tag busybox 192.168.116.9:5000/test/busybox:1.0`
1. push image: `docker push 192.168.116.9:5000/test/busybox:1.0`

- pull image:
    `docker pull 192.168.116.9:5000/test/busybox:1.0`


##### Close Registry
```
docker stop serving && docker rm -v serving
```


##### Config to Use Registry
- Edit '/etc/docker/daemon.json' from server hosts and client hosts to enable regular docker usage
```
{
"insecure-registries" : ["{registry ip}:{registry port}"]
}
```

- restart docker service:
```
sudo service docker restart
```


