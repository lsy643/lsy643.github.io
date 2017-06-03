## Docker


### Private Registry

#### Create Registry

```
docker run -d -p 5000:5000 --restart=always \
--name serving \
-v /home/lisiyuan/docker_registry/serving:/var/lib/registry \
registry:2
```

#### Use Registry
```
1. add "insecure-registries" : ["192.168.116.9:5000"] in the /etc/docker/daemon.json

2. restart docker service: docker service docker restart
```

#### Close Registry
```
docker stop registry && docker rm -v registry
```

#### Get Registry Information
```
curl 192.168.116.9:5000/v2/_catalog
```

