a VM 需要 an OS， containers can share OS.
kernel namespaces, control groups, Docker

简单指令:
`
    docker images 
    docker image pull ubuntu:latest
    docker container run -it ubuntu:latest /bin/bash
`
Ctrl-PQ  detach docker, 退出但不终止container

```
docker container ls
docker container exec -it $NAMES（or$ID) bash #进入
docker container stop/rm $NAMES
```

`
docker image build -t test:latest
docker image ls
`

### Docker Engine
core software that run and manage containers.
- daemon 管理image，网络，处理api（command）,认证等
- containerd  container supervisor,管理container生命周期
- runc  只有一个任务, create container
组件化。daemon解析docker run命令，以docker api调用containerd，
containerd给runc image， runc创建container。
---
### Docker image

#### 6.1
```
docker container run -d --name webserver -p 80:8080 \nigelpoulton/pluralsight-docker-ci
```  
`-d` for daemon  
`-p` maps ports on the Docker host to ports inside the container.

#### 6.2
```docker image inspect $imageName```  
有一个Cmd的部分，可以查看image的启动脚本



---
### Containerizing an App

#### Dockerfile
有两个目的：  
1. 描述应用
2. 告诉docker，怎样将应用打成一个镜像。

`FROM` 描述base layer of image, 应用会加在这层之上。比如 `FROM ubuntu`  
`LABEL` 添加一些自定义的信息，邮箱什么的  
`RUN` run command as a new layer upon lower layer  
`COPY` copy app file as a new layer upon lower layer  
 
### Swarm mode
容器编排，其他的还有Kubernetes。
A swarm(社区不叫他cluster) 包含多个node， node被分为manager 和 worker
先创建一个swarm， 建一个mgr，join worker或者mgr， 然后创建一个service（名字， 端口， 节点数， image）， 同时运行。
可以动态设置replicas的数目。
滚动升级




