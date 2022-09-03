## 镜像

镜像名称一般分两个部分组成：\[repository\]:\[tag\]

* 查看镜像：docker images
* 删除镜像：docker rmi
* 拉取镜像：docker pull
* 构建镜像：docker build
* 推送镜像：docker push
* 保存镜像：docker save
* 加载镜像：docker load

## 容器

* 运行容器：docker run
* 暂停容器：docker pause
* 从暂停运行容器：docker unpause
* 停止容器：docker stop
* 从停止运行容器：docker start
* 容器状态：docker ps
* 容器日志：docker logs
* 进入容器：docker exec
* 删除容器：docker rm

### 运行容器

```shell
docker run --name [containerName] -p 80:80 -d [imageName]
```

* docker run：创建并运行一个容器
* --name：容器名字
* -p：将宿主机与容器端口映射，冒号左侧是宿主机端口，右侧是容器端口
* -d：后台运行容器
* imageName：镜像名称，例如 nginx

### 进入容器

```shell
docker exec -it [containerName] bash
```

* docker exec：进入容器内部
* -it：给当前进入容器创建一个标准输入、输出终端，允许与容器交互
* [containerName]：容器名称
* bash：进入容器后执行的命令，bash 是一个 Linux 终端交互命令，例如 Windows 下面的 CMD