---
layout: page
mathjax: true
permalink: /notes/productive_tools/git/
---

Git and Gitlab

## Git

### Common commands
- ignore change: `git checkout .`


## Gitlab
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