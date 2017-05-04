
# 资料
官网： https://www.docker.com/  
Docker镜像： https://hub.docker.com/explore/  

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

# 列出镜像
docker images




```