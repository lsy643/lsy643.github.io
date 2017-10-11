## Development Tools
Tools like Git, Docker, Notebook, Bazel and so on are very helpful

### 1. Acceleration in China

#### Pip
Use mirror in China by appending the line blow after normal pip command:
```
-i http://pypi.douban.com/simple --trusted-host pypi.douban.com
```

#### Docker
Use mirror from [Daocloud](http://www.daocloud.io/mirror)


#### Ubuntu

1. Find PID with user: `ps -aux | grep {PID}`


### 2. Git
#### Common Git Commands
##### Commit
1. `git add .`
2. `git commit -m "msg"`


##### Syn with remote branch
1. `git fetch origin master`
2. `git merge origin/master`


##### Notices
- When creates something new, create in a new branch
- Do not ues *git rebase*
- Do not use *git pull*

#### Gitlab
Gitlab works like Github.

Create it with command below:

    ```
    docker run --detach \
    --hostname 192.168.149.84 \
    --publish 4443:443 --publish 4080:80 --publish 4022:22 \
    --name gitlab \
    --restart always \
    --volume /home/dell/gitlab/config:/etc/gitlab \
    --volume /home/dell/gitlab/logs:/var/log/gitlab \
    --volume /home/dell/gitlab/data:/var/opt/gitlab \
    gitlab/gitlab-ce:latest
    ```

### 3. Docker
*Portus* maybe deserve consideration

#### Common Commands:

1. Pull from local Registry: `docker pull {registry ip}:{registry port}/*`
2. Run with specific GPU: `NV_GPU={i} nvidia-docker run`

#### Private Registry

##### Create Registry
- serving registry
```
docker run -d -p 5000:5000 --restart=always \
--name apd_registry \
-v /home/dell/apd_registry:/var/lib/registry \
registry:2
```

##### Web UI
```
docker run \
-d \
-e ENV_DOCKER_REGISTRY_HOST=192.168.149.84 \
-e ENV_DOCKER_REGISTRY_PORT=5000 \
-p 5080:80 \
konradkleine/docker-registry-frontend:v2
```



##### Push and Pull image
- push image
1. tag image: `docker tag busybox 192.168.116.9:5000/test/busybox:1.0`

2. push image: `docker push 192.168.116.9:5000/test/busybox:1.0`

- pull image: `docker pull 192.168.116.9:5000/test/busybox:1.0`


##### Close Registry
```
docker stop serving && docker rm -v serving
```


##### Config to Use Registry
- Edit '/etc/docker/daemon.json' from server hosts and client hosts to enable regular docker usage
```
{
"insecure-registries" : ["192.168.149.84:5000"]
}
```

- restart docker service:
```
sudo service docker restart
```


### 4. Notebook

A very good tool to run simple Python programs and run it with docker image is the recommended way.

### 5. Bazel

Bazel is a very good tool to build multi-language programs.

#### build for debug
`bazel build -c opt --config cuda -c dbg --strip=never`

### 6. Anaconda
[Anaconda](https://www.continuum.io/) is a Python package management tool.

Common commands:

1. List current environments: `conda info --envs`
2. Create an environment: `conda create --name {env_name} python={python_version}`
3. Clone an environment: `conda create --name {tgt_env_name} --clone {org_env_name}`
4. Remove an environment: `conda remove --name {env_name}`
5. Change an environment: `source activate/deactivate {env_name}`

### 7. Visual Studio Code

A very good editor to code Python, C++ and many other languages

### 8. Pycharm

An excellent IDE for Python