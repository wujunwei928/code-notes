
### 安装 pip
wget https://bootstrap.pypa.io/get-pip.py -O - | python

### 设置pip的pypi镜像地址
因为大天朝墙的原因, 官方默认的pypi源速度比较慢, 可以设置国内的pypi源地址, 提高安装python包时的速度。

下面以设置清华大学的pypi源地址为例说明: 
1. 临时使用
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
# 注意，simple 不能少, 是 https 而不是 http
```
2. 设为默认
修改 ~/.pip/pip.conf (没有就创建一个)
如果镜像地址是https的, 例如: 修改index-url至清华大学镜像
```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```
如果你想添加的pypi镜像地址不是https的, 需要多添加一行 trusted-host
```bash
[global]
trusted-host=pypi.douban.com        #防止安装的时候报域名不是https的错误
index-url = http://pypi.douban.com/simple
```
