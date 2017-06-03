## Docker


### Private Registry

#### 1. Create Registry
- serving registry
```
docker run -d -p 5000:5000 --restart=always \
--name deep_learning_registry \
-v /home/lisiyuan/docker_registry/deep_learning_registry:/var/lib/registry \
registry:2
```


#### 2. Use Registry
- Edit '/etc/docker/daemon.json' from server hosts and client hosts to enable regular docker usage
```
{
"insecure-registries" : ["192.168.116.9:5000"]
}
```
- restart docker service:
```
docker service docker restart
```



#### 3. Push and Pull image
- push image
1. tag image: `docker tag busybox 192.168.116.9:5000/test/busybox:1.0`

2. push image: `docker push 192.168.116.9:5000/test/busybox:1.0`

- pull image: `docker pull 192.168.116.9:5000/test/busybox:1.0`


#### 4. Close Registry
```
docker stop serving && docker rm -v serving
```

#### 5. WebUI for docker registry
- WebUI for serving registry
```
docker run -d \
--name serving_webui \
-e ENV_DOCKER_REGISTRY_HOST=192.168.116.9 \
-e ENV_DOCKER_REGISTRY_PORT=5000 \
-p 5200:80 \
konradkleine/docker-registry-frontend:v2
```



#### 6. Get Registry Information
```
curl 192.168.116.9:5000/v2/_catalog
```

