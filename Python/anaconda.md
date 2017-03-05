# 介绍
Anaconda 是 Python 科学技术包的合集，功能和 Python(x,y) 类似。
包管理使用 conda，包含常用科学计算包都有：numpy，sicpy，pandas，matplotlib，spyder，scikit-learn....。

Anaconda Python 是完全免费的企业级的Python发行大规模数据处理、预测分析和科学计算工具。

Linux系统里面，Anaconda 所有的东西都只安装在一个目录中，例如：/home/wjw/anaconda/， 安装、更新和删除都很方便。
Anaconda的开发和维护中有Python创始人和社区的核心成员。
Anaconda目前提供Python 2.7.X,Python 3.6.X两个系列发行包，这也是其他发行版所望尘莫及的。因此在各种操作系统中，无论是Linux，还是Windows、Mac,都推荐Anaconda！

使用Python的同学, 在安装Package的时候, 应该都遇到过提示安装依赖项的情况, 
如: gcc, zlib-devel, bzip2, bzip2-devel, libxml2(lxml) 等.
但是有时, 我们只是服务器上的一个普通用户, 没有超级用户权限,无法安装相关依赖项, 
这时Anaconda就派上用场了, 它把所有的依赖管理都帮你处理好了, 安装完之后有了一个用户级别的python环境
使用Anaconda时, 推荐使用其自带的conda包管理工具, 会自动解决安装过程中的相关依赖
>本人之前用pip在windows上安装 mysql-python 包的时候, 提示升级C++版本
>但是使用 conda 安装 mysql-python 的时候, 自动解决这这个依赖问题.

# 下载
完整版下载地址：https://www.continuum.io/downloads  
Mini版下载地址：https://conda.io/miniconda.html  
因为包含了大量的科学包，Anaconda 的完整版下载文件比较大（约 500 MB）  
如果只需要某些包，或者需要节省带宽或存储空间，可以使用Mini版（仅包含conda和 Python）。

# Anaconda 的包管理工具 conda
## 设置 Anaconda 镜像地址
将Anaconda的镜像地址设置为国内的清华大学地址, 提高包下载速度。
```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```

运行 *conda install numpy* 测试一下吧。
