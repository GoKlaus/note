## 原理

基于linux 容器化技术



## 镜像

### 镜像源配置

debian / ubuntu

```sh
/etc/default/docker

DOCKER_OPTS="--registry-mirror=https://registry.docker-cn.com"

# 查看docker 信息
docker info 
```

### 查看本地镜像

```shell
docker images
```



### 查询镜像

```shell
docker search httpd
```



### 拉镜像

```shell
docker pull ubuntu
```

拉取之前可以先查看镜像

### 删除镜像

```shell
docker rmi hello-world
```



### 创建镜像

- 1、从已经创建的容器中更新镜像，并且提交这个镜像
- 2、使用 Dockerfile 指令来创建一个新的镜像



### 更新镜像



### 构建镜像

```shell
docker build 
```

使用dockerfile 来构建



### 设置镜像标签

```shell
docker tag 860c279d2fec runoob/centos:dev
```



## 容器

基于镜像，运行后得到容器

### 启动容器

```sh
docker run -i -t ubuntu:15.10 /bin/bash

- i 允许你对容器内的标准输入 (STDIN) 进行交互
- t terminal 在新容器内指定一个伪终端或终端
-d:让容器在后台运行
-P:将容器内部使用的网络端口随机映射到我们使用的主机上
```

启动容器（后台模式）

```shell
docker run -d ubuntu:15.10 /bin/sh -c "while true; do echo hello world; sleep 1; done"
docker run -itd --name ubuntu-test ubuntu /bin/bash
```

### 查看容器信息

```shell
docker ps  /  docker ps -a
- CONTAINER ID        容器 ID
- IMAGE               使用的镜像
- COMMAND             启动容器时运行的命令
- CREATED             容器的创建时间
- STATUS              容器状态
- PORTS               容器的端口信息和使用的连接类型（tcp\udp）
- NAMES               自动分配的容器名称

```



### 查看docker内部日志

```shell
docker logs 2b1b7a428627 -容器id
```



### 进入容器

```shell
docker attach
-- docker attach 1e560fca3906 
docker exec：推荐大家使用 docker exec 命令，因为此退出容器终端，不会导致容器的停止
-- docker exec -it 243c32535da7 /bin/bash

```





### 退出容器

```shell
- 从容器内部退出，容器并没有停止
root@0123ce188bd8:/#  exit 
```



### 停止容器

```shell
docker stop <容器 ID>
docker stop amazing_cori -容器名字
```



### 重启容器

```shell
docker restart <容器 ID>
```



### 导出和导入容器

```shell
docker export 1e560fca3906 > ubuntu.tar  导出容器

cat docker/ubuntu.tar | docker import - test/ubuntu:v1 导入容器
```



### 删除容器

```shell
docker rm -f 1e560fca3906
```



映射端口

```shell
-p 是容器内部端口绑定到指定的主机端口
docker run -d -p 5000:5000 training/webapp python app.py
-P 是容器内部端口随机映射到主机的高端口
```





按照配置文件，运行docker build 之后生成的









## Docker-compose 

作用：定义和运行多容器 Docker 应用程序的工具。通过 Compose，您可以使用 YML 文件来配置应用程序需要的所有服务。然后，使用一个命令，就可以从 YML 文件配置中创建并启动所有服务

例子：



docker命令