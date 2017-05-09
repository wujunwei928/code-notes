
# 资料
官网： https://www.docker.com/  
Docker镜像： https://hub.docker.com/explore/  

# 文档
官网文档： https://docs.docker.com/  
Docker — 从入门到实践: https://github.com/yeasy/docker_practice  


# 安装
## Ubuntu
Ubuntu自带的docker.io版本太旧，安装官网最新版本
```bash
# 添加Docker官方软件源地址 （下面两种方法都可以， 针对 Ubuntu 16.04）
sudo apt-add-repository -y "deb https://apt.dockerproject.org/repo ubuntu-xenial main"
# 或
echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" | sudo tee /etc/apt/sources.list.d/docker.list


#  Docker 官方软件源的 GPG 密钥
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
```


# 常用命令
```bash
# 获取镜像： docker pull [选项] [Docker Registry地址]<仓库名>:<标签>
docker pull ubuntu:14.04

# 运行镜像
docker run -it --rm ubuntu:14.04 bash
docker run -it ubuntu:16.04 /bin/bash

# 列出镜像
docker images
docker images -a

# 删除镜像
docker rmi

# 列出容器
docker ps
docker ps -a
docker ps -a -q

# 删除容器
docker rm

# 从新启动容器
docker start -ai 容器ID（一般前3个字母以上即可）



```

# Dockerfile 构建模板
```bash
# Version: 0.0.1

# 基于某个镜像构建
FROM ubuntu:16.04

# 镜像的基本信息
MAINTAINER Wu Junwei "1399952803@qq.com"

# 运行命令
RUN apt-get -y update
RUN apt-get -y install nginx
RUN echo 'Hi, I am docker container' \
    > /var/www/html/index.html

# 绑定端口
# EXPOSE 80

# 设置容器启动时要运行的命令
# ENTRYPOINT ["/usr/sbin/nginx"]
# ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]

# 设置文件挂载点
VOLUME ["/mnt/nginx/media"]

# 复制本地文件到镜像中, 会对压缩文件进行自解压
ADD all_data.tar.gz /root/add_test/

# 复制本地文件到镜像中, 只复制, 不会去做文件提取和解压
# ADD和COPY时, 源路径必须是相对路径, 目标路径必须是绝对路径
# ADD和COPY时, 如果目标路径不存在, docker会自动帮我们创建
COPY all_data.tar.gz /root/copy_test/

# ONBUILD命令为镜像添加触发器, 当一个镜像作为其他镜像的基础镜像时, 该镜像的触发器会被执行
ONBUILD add . /var/www/html/
```
