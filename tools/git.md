## Gitlab

### Setup Gitlab

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



### Usage
- Add port Number `4080` after every IP address when pull or push
- add remote: `git remote add origin_gitlab http://lisiyuan@192.168.116.9:4080/dl_cv/test.git`
- delete remote branch: `git push origin_gitlab --delete <branch_name>`
- push to remote: `git push -u origin_gitlab --all`
- sync fork:


### Cooperation
1. Others can be developers
2. Everyone should develop in one's own branch